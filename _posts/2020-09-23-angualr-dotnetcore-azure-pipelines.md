---
layout: post
title: How to deply the Angular + .Net Core WebAPI using an Azure DevOps CI pipeline?
categories: azure
tags: [azure,pipelines,DevOps]
---

## Instruction

How to create and deply the Angular + .Net Core WebAPI as an Azure App Service using an Azure DevOps CI pipeline?

I found many examples for the same folder for the project.In this case, I separated the front-end and  the back-end in different folder however in the same repo of the github and the same solution.Let's start it.


## Create the Project

I am using the angular template for the illustration. 

you can create your DotnetCore 3.1 Project ,as below
![enter image description here]({{site.baseurl}}/assets/img/2020-09-23-angualr-dotnetcore-azure-pipelines/dotnetcore.jpg)
and use the Angular template. 
![enter image description here]({{site.baseurl}}/assets/img/2020-09-23-angualr-dotnetcore-azure-pipelines/angulartemp.jpg)


You will see the solution as below.

![enter image description here]({{site.baseurl}}/assets/img/2020-09-23-angualr-dotnetcore-azure-pipelines/solution.jpg)

## Move the Folder 

![enter image description here]({{site.baseurl}}/assets/img/2020-09-23-angualr-dotnetcore-azure-pipelines/foldermoveout.jpg)

You can add the folder to the solution like this.

![enter image description here]({{site.baseurl}}/assets/img/2020-09-23-angualr-dotnetcore-azure-pipelines/movefrontend.jpg)

## Update the solution file

In this case, we need to update the ngDotnetCore.csproj which is for the .net core backend code.

Change the SpaRoot because we changed the Angular front-end to the other folder.
 ``` xml
 <SpaRoot>..\ClientApp\</SpaRoot>
```
Remove the setting for the npm install as below . Because you will use the Azure DevOps to run it later.

``` xml
Remove this 
<!-- As part of publishing, ensure the JS resources are freshly built in production mode -->
    <Exec WorkingDirectory="$(SpaRoot)" Command="npm install" />
    <Exec WorkingDirectory="$(SpaRoot)" Command="npm run build -- --prod" />
    <Exec WorkingDirectory="$(SpaRoot)" Command="npm run build:ssr -- --prod" Condition=" '$(BuildServerSideRenderer)' == 'true' " />
    
```
Add this as below. It will copy the front-end files to back-end folder and include the newly-built files in the publish output.
``` xml
  <Target Name="PublishRunWebpack" AfterTargets="ComputeFilesToPublish">
    <!-- Include the newly-built files in the publish output -->
    <!-- Copy the dist from the front end folder -->
    <ItemGroup>
      <_CopyItems Include="$(SpaRoot)dist\**\*.*" />
    </ItemGroup>
    <Copy SourceFiles="@(_CopyItems)" DestinationFolder="dist" />
    <!-- Include the dist from the front end folder,if in the other folder it can't include in the publish output folder  -->
    <ItemGroup>
      <DistFiles Include="dist\**;" />
      <ResolvedFileToPublish Include="@(DistFiles->'%(FullPath)')" Exclude="@(ResolvedFileToPublish)">
        <RelativePath>%(DistFiles.Identity)</RelativePath>
        <CopyToPublishDirectory>PreserveNewest</CopyToPublishDirectory>
        <ExcludeFromSingleFile>true</ExcludeFromSingleFile>
      </ResolvedFileToPublish>
    </ItemGroup>
  </Target>

  ```

## Create Web App

Create the Webapp in Azure.Be care to choose free plan if you wouldn't like to pay anything.
And make sure the .net core version is 3.1
![enter image description here]({{site.baseurl}}/assets/img/2020-09-23-angualr-dotnetcore-azure-pipelines/createWebapp.jpg)


