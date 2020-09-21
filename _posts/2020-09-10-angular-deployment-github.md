---
layout: post
title: Angular Apps Deployment to GitHub Pages 
categories: Angular
tags: [github,angular,deploy]
---


# Deploy Using ng deploy

The simplest way to deploy to Github Pages is to take advantage of the  `ng deploy`  Angular CLI command that automates the deployment process. When you run`ng deploy`, it executes a builder that performs the deployment for you. The builder that we’ll use is  `[angular-cli-ghpages](https://npmjs.org/package/angular-cli-ghpages)`.  `ng deploy`  builds your project and deploys the resultant output to a  `gh-pages`  branch on your remote Github repository.

1.  To begin, add the  `angular-cli-ghpages`  builder.

ng add angular-cli-ghpages

2. Deploy your project. If you’re deploying the project to a Github project page you’ll need to set the  `baseHref`  property as the repository name. The  `baseHref`  will be used for all relative URLs on your site. You could specify the  `baseHref`  as part of the project architect deploy options in the  **_angular.json_**  file. Or just pass it as the`--base-href`  flag to the  `ng deploy`  command. If you’re deploying the project to a Github user page, you do not need to set this option.
```
ng deploy --base-href=/<repository-name>/
```
GitHub will automatically enable Pages when you push a  `gh-pages`  branch. There is no need to enable Pages from the repository settings.