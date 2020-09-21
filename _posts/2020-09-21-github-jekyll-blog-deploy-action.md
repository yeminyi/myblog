---
layout: post
title: Jekyll Deploy Action
categories: github
tags: [jekyll,github,blog]
---

Usage
At First, you should add a github workflow file (e.g. .github/workflows/build-jekyll.yml) in your repository's master branch as below:

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
To schedule a workflow, you can use the POSIX cron syntax in your workflow file. The shortest interval you can run scheduled workflows is once every 5 minutes. For example, this workflow is triggered every hour.

on:
  schedule:
    - cron:  '0 * * * *'
After this, we should provide permissions for this action to push to the gh-pages branch:

Create a Personal Token with repos permissions and copy the value.
Go to your repository’s Settings and then switch to the Secrets tab.
Create a token named GH_TOKEN (important) using the value copied.
In the end, go to your repository’s Settings and scroll down to the GitHub Pages section, choose the gh-pages branch as your GitHub Pages source.

Additionally, if you don't have the gh-pages branch, you can create it as below:

git checkout --orphan gh-pages
git rm -rf .
git commit --allow-empty -m "initial commit"
git push origin gh-pages
💡 Tip: The gh-pages branch is only for the site static files and the master branch is for source code.