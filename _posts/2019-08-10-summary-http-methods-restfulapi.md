---
layout: post
title: "Summary of HTTP Methods for RESTful APIs"
categories: RESTful 
tags: [HTTP,RESTful]
---

## POST

Create

201 (Created), ‘Location’ header with link to /users/{id} containing new ID.

Avoid using POST on single resource

## GET

Read

200 (OK), list of users. Use pagination, sorting and filtering to navigate big lists.

200 (OK), single user. 404 (Not Found), if ID not found or invalid.

## PUT

Update/Replace

405 (Method not allowed), unless you want to update every resource in the entire collection of resource.

200 (OK) or 204 (No Content). Use 404 (Not Found), if ID not found or invalid.

## PATCH

Partial Update/Modify

405 (Method not allowed), unless you want to modify the collection itself.

200 (OK) or 204 (No Content). Use 404 (Not Found), if ID not found or invalid.

## DELETE

Delete

405 (Method not allowed), unless you want to delete the whole collection — use with caution.

200 (OK). 404 (Not Found), if ID not found or invalid.

## Safe Methods
As per HTTP specification, the GET and HEAD methods should be used only for retrieval of resource representations – and they do not update/delete the resource on the server. Both methods are said to be considered “safe“.

This allows user agents to represent other methods, such as POST, PUT and DELETE, in a unique way so that the user is made aware of the fact that a possibly unsafe action is being requested – and they can update/delete the resource on server and so should be used carefully.

## Idempotent Methods
The term idempotent is used more comprehensively to describe an operation that will produce the same results if executed once or multiple times. Idempotence is a handy property in many situations, as it means that an operation can be repeated or retried as often as necessary without causing unintended effects. With non-idempotent operations, the algorithm may have to keep track of whether the operation was already performed or not.

In HTTP specification, The methods GET, HEAD, PUT and DELETE are declared idempotent methods. Other methods OPTIONS and TRACE SHOULD NOT have side effects, so both are also inherently idempotent.

## Summary

| HTTP Methods | Safe? | Idempotent? |
| -----------: |----: | ---------: |
|GET | YES | YES   |
|OPTIONS | YES | YES   |
|HEAD | YES | YES   |
|POST | NO | NO   |
|DELETE | NO | YES   |
|PUT | NO | YES   |
|PATCH | NO | NO   |

## Useful Link
<https://restfulapi.net/http-methods/>