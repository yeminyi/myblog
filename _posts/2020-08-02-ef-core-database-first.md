---
layout: post
title: Entity Framework Core Database First
categories: efcore
tags: [efcore]
---
## Instruction
 It is possible to reverse engineer an existing database into a DbContext and classes, and it is known as Database First approach.
 
Prerequisites
- NuGet Package Microsoft.EntityFrameworkCore.SqlServer
- NuGet Package Microsoft.EntityFrameworkCore.Tools
- Your sql server DB and Tables


### Scaffolding with OutputDir(-O)
The entity classes and a DbContext class are scaffolded into the project's root directory and use the project's default namespace.

in the Package Manager Console:

``` 
PM>Scaffold-DbContext ... -ContextDir Data -OutputDir Models
```
```
PM>Scaffold-DbContext "Server=yourdbserver;Database=yourdb;Trusted_Connection=True;" Microsoft.EntityFrameworkCore.SqlServer -OutputDir Entities
```
```
PM>Scaffold-DbContext "Server=yourdbserver;Database=yourdb;Trusted_Connection=True;" Microsoft.EntityFrameworkCore.SqlServer -O Entities
```
### Scaffolding with Overwriting(-F)

If you already have scaffolding and want to override existing files with new scaffolding (generated using new or updated schema) please use the below command.

``` 
PM>Scaffold-DbContext ....... -Force

PM>Scaffold-DbContext ....... -F
```

## Here are useful links
  <https://entityframeworkcore.com/approach-database-first>

  <https://www.thecodebuzz.com/efcore-scaffold-dbcontext-commands-orm-net-core/>

  <https://www.thecodebuzz.com/getting-started-efcore-entity-framework-core-orm-asp-net-core/>
  
  <https://docs.microsoft.com/en-us/ef/>

