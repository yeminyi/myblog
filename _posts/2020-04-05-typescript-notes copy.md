---
layout: post
title: TypeScript Notes-Basic Types
categories: typescript
tags: [typescript,angular]
---
TypeScript is a strict syntactical superset of JavaScript and adds optional static typing to the language. It is designed for development of large applications and transcompiles to JavaScript.
## Basic Types
### Boolean
``` typescript
let isDone: boolean = false;
```
### Number
``` typescript
let n: number = 6;
let hex: number = 0xf00d;
let binary: number = 0b1010;
let octal: number = 0o744;
let big: bigint = 100n;
```
### String
Just like JavaScript, TypeScript also uses double quotes (") or single quotes (') to surround string data.
``` typescript
let color: string = "blue";
color = "red";

// you can also use template strings, 
// which can span multiple lines and have embedded expressions
let fullName: string = `Bob Bobbington`;
let age: number = 37;
let sentence: string = `Hello, my name is ${fullName}.

I'll be ${age + 1} years old next month.`;
```
### Array
``` typescript
let list: number[] = [1, 2, 3];
//The second way uses a generic array type, Array<elemType>:
let list: Array<number> = [1, 2, 3];
```
### Tuple
Tuple values are individually called items. Tuples are index based. This means that items in a tuple can be accessed using their corresponding numeric index. Tuple item’s index starts from zero and extends up to n-1(where n is the tuple’s size)
``` typescript
// Declare a tuple type
let x: [string, number];
// Initialize it
x = ["hello", 10]; // OK
// Initialize it incorrectly
x = [10, "hello"]; // Error

// OK
console.log(x[0].substring(1));
//error Property 'substring' does not exist on type 'number'.
console.log(x[1].substring(1));

```
### Enum
``` typescript
enum Color {
  Red,
  Green,
  Blue,
}
let c: Color = Color.Green;
```
### Unknown
``` typescript
let notSure: unknown = 4;
notSure = "maybe a string instead";

// OK, definitely a boolean
notSure = false;
```
### Any
The any data type is the super type of all types in TypeScript. It denotes a dynamic type. Using the any type is equivalent to opting out of type checking for a variable.
``` typescript
declare function getValue(key: string): any;
// OK, return value of 'getValue' is not checked
const str: string = getValue("myString");
```
After all, remember that all the convenience of any comes at the cost of losing type safety. Type safety is one of the main motivations for using TypeScript and you should try to avoid using any when not necessary.
### Void
void is a little like the opposite of any: the absence of having any type at all. You may commonly see this as the return type of functions that do not return a value:
``` typescript
function warnUser(): void {
  console.log("This is my warning message");
}
```
### Null and Undefined
By default null and undefined are subtypes of all other types. That means you can assign null and undefined to something like number.
However, when using the --strictNullChecks flag, null and undefined are only assignable to unknown, any and their respective types (the one exception being that undefined is also assignable to void). This helps avoid many common errors. In cases where you want to pass in either a string or null or undefined, you can use the union type string | null | undefined.
``` typescript
// Not much else we can assign to these variables!
let u: undefined = undefined;
let n: null = null;
```
### Never
``` typescript
// Function returning never must not have a reachable end point
function error(message: string): never {
  throw new Error(message);
}
```
### Object
object is a type that represents the non-primitive type, i.e. anything that is not number, string, boolean, bigint, symbol, null, or undefined.
``` typescript
declare function create(o: object | null): void;

// OK
create({ prop: 0 });
create(null);

create(42);
Argument of type '42' is not assignable to parameter of type 'object | null'.
create("string");
```
## Refer the Link

<https://www.typescriptlang.org/docs/handbook/basic-types.html>

<https://www.tutorialspoint.com/typescript/index.htm>