---
layout: post
title: What is JSON Patch
categories: RESTful 
tags: [HTTP,RESTful]
---

## JSON Patch

JSON Patch is a web standard format for describing changes in a JSON document. It is meant to be used together with HTTP Patch which allows for the modification of existing HTTP resources. The JSON Patch media type is application/json-patch+json. 

There is a standard defined in RFC 6902 called “JSON Patch“, which we can use for the HTTP PATCH.
- RFC 6902 (JSOn Patch)
- application/json-patch+json


## Example

The patch

``` json
[
  { "op": "replace", "path": "/baz", "value": "boo" },
  { "op": "add", "path": "/hello", "value": ["world"] },
  { "op": "remove", "path": "/foo" }
]
```

op: Operation.Valid operations are add, remove, replace, move, copy and test. Any other operation is considered an error.

path:The path member is a JSON Pointer that determines a location within the JSON document to modify.

## Operations

### Add

``` json
{ "op": "add", "path": "/biscuits/1", "value": { "name": "Ginger Nut" } }

``` 

Adds a value to an object or inserts it into an array. In the case of an array, the value is inserted before the given index. The - character can be used instead of an index to insert at the end of an array.

### Remove

``` json
{ "op": "remove", "path": "/biscuits" }
``` 
Removes a value from an object or array.
``` json
{ "op": "remove", "path": "/biscuits/0" }
```
Removes the first element of the array at biscuits (or just removes the “0” key if biscuits is an object)

### Replace
``` json
{ "op": "replace", "path": "/biscuits/0/name", "value": "Chocolate Digestive" }
```
Replaces a value. Equivalent to a “remove” followed by an “add”.

### Copy
``` json
{ "op": "copy", "from": "/biscuits/0", "path": "/best_biscuit" }
``` 
Copies a value from one location to another within the JSON document. Both from and path are JSON Pointers.

### Move
``` json
{ "op": "move", "from": "/biscuits", "path": "/cookies" }
``` 
Moves a value from one location to the other. Both from and path are JSON Pointers.

### Test
``` json
{ "op": "test", "path": "/best_biscuit/name", "value": "Choco Leibniz" }
``` 
Tests that the specified value is set in the document. If the test fails, then the patch as a whole should not apply.



## Useful Links

<http://jsonpatch.com/>

<https://gavilan.blog/2019/04/05/asp-net-core-2-2-partial-updates-with-http-patch-json-patch/>

<https://dotnetcoretutorials.com/2017/11/29/json-patch-asp-net-core/>

<https://sookocheff.com/post/api/understanding-json-patch/>