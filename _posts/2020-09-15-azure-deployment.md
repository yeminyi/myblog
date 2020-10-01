---
layout: post
title: Deployment for Angular + Asp.net core with Sqlite
categories: azure
tags: [azure,sqlite,angular,deploy]
---

## 1.Build the project
  Run `ng build` to build the client project. The build artifacts will be stored in the `dist/` directory. Use the `--prod` flag for a production build.

## 2.Create the apps on Azure.
  Deploy the dist folder to the web app. **Make sure put the web.config file** under the`wwwroot/` as well. Angular on azure need the web.config for routing or read json file(local run ng serve is different with using IIS,need to add web.config ).By the way, WebApp windows environment need add the node.js version app settings.
  
  If no **web.config** in the foler ,it will show the error.
  >Error : The resource you are looking for has been removed, had its name changed, or is temporarily unavailable

  Make a change to angular.json to bundle the web.config file in the build, you will see in the publish output file.

	
	...
	"assets": [
		/src/favicon.ico",
		/src/assets",
		/src/web.config"
	],
	...
	

## 3.Deploy to Azure

### 1) Create a Release Package

Open your terminal and make sure you're in the right folder.  

Run the following command to create a release package in a sub folder called publish:

```dotnet publish -c Release -o ./publish```

### 2) Copy database to the new folder
Copy-Paste your database, for example 'yourDb.db', into the newly created 'publish' folder.

### 3)Publish to Azure
There are few ways to publish to Azure.Choose anyone if you like.
I always use Visual Studio Code and have the Azure App Service extension. 
     
### 4) Set the Connection String
Once the app has been deployed to Azure, you set your connection string in the Azure App Service.

You can find the setting under  `_Settings -> Configuration -> Connection strings.`	There you create a new connection string
		

		[
			{
			"name": "ConnectionStrings",
			"value": "{ \"DefaultConnection\": \"Data Source=yourDb.db;\" }",
			"type": "Custom",
			"slotSetting": true
			}
		]

### 5) Set the Application settings
	 
You can find the setting under _Settings -> Configuration -> Applications Settings 

1> Adding the settings to web apps for your related API address.	

			[
				 {
					"name": "APIAddress",
					"value":"https://the related app address",
					"slotSetting": true
				 }
			]
							
	
2> Adding `ASPNETCORE_DETAILEDERRORS = true` to show the errors.
 	

			[
				 {
					"name": "ASPNETCORE_DETAILEDERRORS",
					"value": "true",
					"slotSetting": true
				 }
			]

3> Adding the `ASPNETCORE_ENVIRONMENT = Development`. Restart the WebApp and then check to see if that works.