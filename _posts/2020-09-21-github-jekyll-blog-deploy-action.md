---
layout: post
title: Jekyll Deploy Action
categories: github
tags: [jekyll,github,blog,CI/CD]
---

 It's really convenient to build and deploy the Jekyll site to Github Pages.

## ⭐ Usage

At First, you should add a github workflow file (e.g. .github/workflows/build-jekyll.yml) in your repository's master branch as below:

```
{% raw %}
name: Build and Deploy to Github Pages

on:
  push:
    branches:
      - master  # Here source code branch is `master`, it could be other branch

jobs:
  build_and_deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2

      # Use GitHub Actions' cache to cache dependencies on servers
      - uses: actions/cache@v1
        with:
          path: vendor/bundle
          key: ${{ runner.os }}-gems-${{ hashFiles('**/Gemfile.lock') }}
          restore-keys: |
            ${{ runner.os }}-gems-

      # Use GitHub Deploy Action to build and deploy to Github
      - uses: jeffreytse/jekyll-deploy-action@v0.1.3
        with:
          provider: 'github'
          token: ${{ secrets.GH_TOKEN }} # It's your Personal Access Token(PAT)
          repository: ''             # Default is current repository
          branch: 'gh-pages'         # Default is gh-pages for github provider
          jekyll_src: './'           # Default is root directory
          jekyll_cfg: '_config.yml'  # Default is _config.yml
          jekyll_baseurl: ''         # Default is using _config.yml
          bundler_ver: '>=0'         # Default is latest bundler version
          cname: ''                  # Default is to not use a cname
          actor: ''                  # Default is the GITHUB_ACTOR
{% endraw %}
```
To schedule a workflow, you can use the POSIX cron syntax in your workflow file. The shortest interval you can run scheduled workflows is once every 5 minutes. For example, this workflow is triggered every hour.

```
on:
  schedule:
    - cron:  '0 * * * *'
```
After this, we should provide permissions for this action to push to the gh-pages branch:

-   Create a  [Personal Token](https://github.com/settings/tokens)  with repos permissions and copy the value.
-   Go to your repository’s Settings and then switch to the Secrets tab.
-   Create a token named  `GH_TOKEN`  (important) using the value copied.

Additionally, if you don't have the gh-pages branch, you can create it as below:

```
git checkout --orphan gh-pages
git rm -rf .
git commit --allow-empty -m "initial commit"
git push origin gh-pages
```

## 💡 Tips

- The gh-pages branch is only for the site static files and the master branch is for source code.
- It maybe have a error when create workflow file to push. You can create the file on github directly : `create new file` with the path `github/workflows/build-jekyll.yml` under the repo in the master branch.Or please refer [the link](https://github.com/gitextensions/gitextensions/issues/4916#issuecomment-557509451) by Mike-E-wins
  ```
  ! [remote rejected] master -> master (refusing to allow an OAuth App to create or update workflow `.github/workflows/build.yml` without `workflow` scope)error: failed to push 
  ```
- [Github Link Here](https://github.com/marketplace/actions/jekyll-deploy-action) [Jekyll Link](https://jekyllrb.com/docs/continuous-integration/github-actions/)