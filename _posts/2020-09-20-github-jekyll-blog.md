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
    
    ```
    gem install jekyll bundler
    ```
    
3.  Create a new Jekyll site at  `./myblog`.
    
    ```
    jekyll new myblog  
    ```
    
4.  Change into your new directory.
    
    ``` 
    cd myblog  
    ```
    
5.  Build the site and make it available on a local server.
    
    ```
    bundle exec jekyll serve
    ```
    
6.  Browse to  [http://localhost:4000](http://localhost:4000/)