---
layout: post
title: How to use Swashbuckle in ASP.NET Core
categories: swashbuckle
tags: [swashbuckle,DotnetCore]
---

## Package installation

-Right-click the project in Solution Explorer > Manage NuGet Packages
-Set the Package source to "nuget.org"
-Ensure the "Include prerelease" option is enabled
-Enter "Swashbuckle.AspNetCore" in the search box
-Select the latest "Swashbuckle.AspNetCore" package from the Browse tab and click Install

## Configuration
In the Startup.ConfigureServices method:
``` C#
public void ConfigureServices(IServiceCollection services)
{
    services.AddDbContext<TodoContext>(opt =>
    opt.UseInMemoryDatabase("TodoList"));
    services.AddControllers();

    // Register the Swagger generator, defining 1 or more Swagger documents
    services.AddSwaggerGen(c =>
    {
      //The configuration action passed to the AddSwaggerGen method adds information 
      //such as the author,license, and description
        c.SwaggerDoc("v1", new OpenApiInfo
        {
              Version = "v1",
              Title = "ToDo API",
              Description = "A simple example ASP.NET Core Web API",
        });
        // Set the comments path for the Swagger JSON and UI.
        var xmlFile = $"{Assembly.GetExecutingAssembly().GetName().Name}.xml";
        var xmlPath = Path.Combine(AppContext.BaseDirectory, xmlFile);
        c.IncludeXmlComments(xmlPath);
    });
}
    
```
In the Startup.Configure method, enable the middleware for serving the generated JSON document and the Swagger UI:
``` C#
public void Configure(IApplicationBuilder app)
{
    // Enable middleware to serve generated Swagger as a JSON endpoint.
    app.UseSwagger();

    // Enable middleware to serve swagger-ui (HTML, JS, CSS, etc.),
    // specifying the Swagger JSON endpoint.
    app.UseSwaggerUI(c =>
    {
        c.SwaggerEndpoint("/swagger/v1/swagger.json", "My API V1");
    });

    app.UseRouting();
    app.UseEndpoints(endpoints =>
    {
        endpoints.MapControllers();
    });
}

    
```
Refer the Link
<https://docs.microsoft.com/en-us/aspnet/core/tutorials/getting-started-with-swashbuckle?view=aspnetcore-3.1&tabs=visual-studio>