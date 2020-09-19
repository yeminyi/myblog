---
layout: post
title: "Angular CLI useful commands"
categories: angular
tags: [angular,cli]
---

## Angular CLI
<https://cli.angular.io/>

Lists available commands and their short descriptions.
`ng -h`

### Installing the CLI

`npm install -g @angular/cli`

`ng -v` check the version

you can create a new Angular project with the following CLI command:

`ng new my-angular-app`

### Serve an Application

With the CLI we can also easily serve our application using a local web-server.

You can then cd into your new project and run your application:

cd my-angular-app 

    ng serve <project> [options]
    ng s <project> [options]

`ng serve` or `ng serve -o` (open browser)

### Generation

`ng generate --help` shorten is  `ng g -h` 

#### Component

`ng generate component my-component`<br>
shorten as below<br>
`ng g c my-component`// Creates MyComponent<br>
By default all generated files go in into `src\app\my-component`, a folder called my-component is created for us.

#### The other Scaffolds

| Features |Command | Shorten|
|--|--|
|directive| ng g directive my-new-directive | ng g d my-new-directive|
|pipe| ng g pipe my-new-pipe     | ng g p my-new-pipe |
|service| ng g service my-new-service |ng g s my-new-service|
|class| ng g class my-new-class |ng g cl my-new-class |
|interface| ng g interface my-new-interface |ng g i my-new-interface |
|enum| ng g enum my-new-enum |ng g e my-new-enum|
|module|ng g module my-module|ng g m my-module|

By default all generated files go in into `src\app`, no folder is created.

####  Routing
When creating a new project, simply add the -- routing flag and the CLI will generate a routing module for your project in `src/app/app-routing.module.ts`:

`ng new my-project --routing`

Later on, when you’re developing modules for your application, you can also generate separate routing modules, which is useful when you want to avoid cluttering the root app routing module. Once again, you use the same -- routing flag when generating modules.

`ng generate module my-module --routing`

#### Styling preprocessors
If you’d like to use a different preprocessor, simply replace scss with less or styl.

`ng new my-project --style=scss`


#### Dry runs
`ng g c my-test-component --dry-run`

If you’re a fan of aliases you can also use the alias for this flag, -d.

`ng g c my-test-component -d`

#### Skip tests
When generating schematics using the generate command, you can do this using the  `--skipTests true` flag:

new version cli change to `--skipTests true`

:  <div style="color: red;">  CAN'T USE `--spec=false` ANYMORE </div> 
`ng g c my-testless-component --spec=false`  

:  <div style="color: green;">  SHOULD BE </div> 
`ng g c my-testless-component --skipTests true`


You can also do this when creating your application with the new command:

`ng new my-testless-application --skip-tests`


`ng new my-testless-application -S`

#### Some more options

    --flat: boolean, default false, generate component files in src/app instead of src/app/site-header
    --inline-template: boolean, default false, use an inline template instead of a separate HTML file
    --inline-style: boolean, default false, use inline styles instead of a separate CSS file

#### Examples

    ng generate module myModule --routing --dry-run

    ng g c mycomponent --flat --skipTests true --dry-run

    ng g c mycomponent --flat --skipTests true

    ng g s shared/open-id-connect --skipTests true --dry-run 

    ng g c foldername/mycomponent --flat --skipTests true --inline-style --inline-template --dry-run

### Documentation
Simply add your search term using the doc command and the CLI will automatically open a new browser window with your search term specified in the documentation.

`ng doc animations`


### Build

`ng build`

`--prod=true|false	`
Shorthand for "--configuration=production". When true, sets the build configuration to the production target. By default, the production target is set up in the workspace configuration such that all builds make use of bundling, limited tree-shaking, and also limited dead code elimination.

Running with`--prod` changes a few things:
 1. The bundles now have random strings appended to them to enable cache
    busting.This ensures that a browser doesn’t try to load up
    previously cached versions of the files and instead load the new
    ones from the server.
 2. The file sizes are much smaller. The files have been processed
      through a minifier and uglifier.
 3. There is a much small .gz file, this is a compressed version of the
        equivalent JavaScript file.Browsers will automatically try to
        download the .gz version of files if they are present.

### Test 
`ng test`

### Update

`ng update`

`ng update @angular/cli @angular/core`

`ng update --all` //Whether to update all packages in package.json.