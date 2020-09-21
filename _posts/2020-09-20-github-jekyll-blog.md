---
layout: post
title: How to create your blog for free using Jekyll + Github pages
categories: github
tags: [jekyll,github,blog]
---

## Create your blog locally

1.  Install all  [prerequisites](https://jekyllrb.com/docs/installation/).
   
	  1> Open terminal 

	  2> Before installing jekyll, we need to ensure the correct version of ruby . (Ruby version must be 2.5 or higher) .Check your Ruby version using `ruby -v`

	  3> Check your Gems version using `gem -v`
2.  Install the jekyll and bundler  [gems](https://jekyllrb.com/docs/ruby-101/#gems).
    
    ``` Powershell
    gem install jekyll bundler
    ```
    
3.  Create a new Jekyll site at  `./myblog`.
    
    ```Powershell
    jekyll new myblog  
    ```
    
4.  Change into your new directory.
    
    ``` Powershell
    cd myblog  
    ```
    
5.  Build the site and make it available on a local server.
    
    ```Powershell
    bundle exec jekyll serve
    ```
    
6.  Browse to  [http://localhost:4000](http://localhost:4000/)

## Edit your content

To quickly edit the following:

- Title, description and other details in _config.yml

- Content in about.md file

- Content in the blog post within _posts folder. You may also copy paste that file and edit its content to create your second blog post.

- Each time you edit content and want to see how it looks, run `jekyll serve` and see the results on the local host

- To exit from current running process   `Ctrl+C`
  
## Publish to your Github
- If you have a Github account ,then create a new github repo.Otherwise you need to create a new github account firstly.
- Go to VS Code to open the local blog folder, open terminal to initialise your git repo
run 
 ```Powershell
 git init
 ```

- To create the branch gh-pages with the files (Github pages will use this branch for the deployment) , run 
 ```Powershell
 git checkout -b gh-pages
 ```
- To commit all the files, run
 ```Powershell
    git add .
    git commit -m "initial commit"
 ```
- Push to Github
 ```Powershell
    #git remote add origin <git repo link>
    git remote add origin https://github.com/yourgithubname/reponame.git
    git push origin gh-pages
 ```
- You can visit https://yourgithubname.github.io/reponame/.
  Before publish to Github ,make sure you updated the file _config.yml ,set the baseurl as your repo name for the blog.

   > baseurl: "/myblog" # the subpath of your site, e.g. /blog   

- Any update, just commit your changes and push to Github.
  
👉 [Automated Deployment](/myblog/github/2020/09/21/github-jekyll-blog-deploy-action.html)