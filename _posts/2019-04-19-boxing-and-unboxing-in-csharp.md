---
layout: post
title: Boxing and Unboxing in C#
categories: C# 
tags: [C#]
---
## Data Types
C# has three kinds of data types, `value types` , `reference types` and pointer types. Value type stores the value itself, whereas the reference type stores the address of the value where it is stored. Some predefined data types such as `int, float, double, decimal, bool, char, etc.` are value types and `object, string, and array` are reference types.

![data types](https://www.c-sharpcorner.com/article/stack-heap-value-type-and-reference-type-in-c-sharp/Images/4.jpg)

## Boxing and Unboxing
While working with these data types, you often need to convert value types to reference types or vice-versa. Because, both have different characteristics and .NET stores them differently in the memory, it must do some work internally to convert them from one type to another. These conversion processes are called boxing and unboxing.

### Boxing
Boxing is the process of converting a value type to the object type or any interface type implemented by this value type. Boxing is implicit.

``` C#
int i = 10;
object o = i; //performs boxing

//practical example
ArrayList list = new ArrayList();
list.Add(10); // boxing
list.Add("Bill");

```
### Unboxing

Unboxing is the reverse of boxing. It is the process of converting a reference type to value type. Unboxing extract the value from the reference type and assign it to a value type.

Unboxing is explicit. It means we have to cast explicitly.

``` C#
object o = 10;
int i = (int)o; //performs unboxing

//A boxing conversion makes a copy of the value.
// So changing the value of one variable will not impact others.
int i = 10;
object o = i; // boxing
o = 20;
Console.WriteLine(i); // output: 10

//The casting of a boxed value is not permitted. 
//The following will throw an exception.
int i = 10;
object o = i; // boxing
double d = (double)o; // runtime exception

//First do unboxing and then do casting
int i = 10;
object o = i; // boxing
double d = (double)(int)o; // valid
```
## Performance
Boxing and unboxing are computationally expensive processes. When a value type is boxed, a new object must be allocated and constructed. To a lesser degree, the cast required for unboxing is also expensive computationally.
So boxing and unboxing degrade the performance. Please avoid using it. Use generics to avoid boxing and unboxing. For example, use List instead of ArrayList.

## Refer the Link
<https://www.c-sharpcorner.com/article/stack-heap-value-type-and-reference-type-in-c-sharp/>

<https://www.tutorialsteacher.com/articles/boxing-unboxing-in-csharp>

<https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/types/boxing-and-unboxing>