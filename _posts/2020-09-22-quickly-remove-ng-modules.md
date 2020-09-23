---
layout: post
title: How to remove the node_modules folder quickly
categories: angular
tags: [angular]
---

## Use rimraf
You could use [rimraf](https://github.com/isaacs/rimraf):
```
 npm install -g rimraf
 rimraf C:\code\yeoman-foo(folder path)
 
 ```

## Error

If there is error like this : cannot be loaded because running scripts is disabled on this system. F or more information, see about_Execution_Policies at https:/go.microsoft.com/fwlink/?LinkID=135170.

This could be due to the current user having an undefined ExecutionPolicy.

You could try the following:

```
Set-ExecutionPolicy -Scope CurrentUser -ExecutionPolicy Unrestricted
```