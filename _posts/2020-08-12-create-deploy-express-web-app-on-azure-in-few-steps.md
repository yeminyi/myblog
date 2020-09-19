---
layout: post
title: How to create and deploy express web app on azure in few steps
categories: azure
tags: [azure,express,nodejs]
---

## Steps
You can create a new simple(nodejs + express) app and deploy to azure:

### Step 1
install express
`npm install express-generator -g`

### Step 2

create an express sample application:
`express newappname`

### Step 3

   cd newappname
   change directory:
     `> cd newapp`

   install dependencies:
     `> npm install`

   run the app locally:
     `> SET DEBUG=newapp:* & npm start`
### Step 4
  git init &  Azure deployment center - CI/CD 
   choose local git or github

### Step 5
 in vs code - azure app service
   deploy to related app 


## Here are reference links
  <https://docs.microsoft.com/en-us/azure/app-service/quickstart-nodejs?pivots=platform-windows>
  <https://thewebspark.com/2018/04/18/creating-and-deploying-express-web-app-on-azure-in-few-steps/>
