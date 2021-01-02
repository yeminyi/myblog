---
layout: post
title: Why use Question mark and Exclamation mark in TypeScript 
categories: typeScript 
tags: [typeScript]
---
## Question mark ？
Using TypeScript, 3 places where the question mark operator appears.

### Conditional Operator 
(Ternary Operator)
``` typescript
// Conditional Operator 三元运算符
// 当 isNumber(input) 为 True 是返回 ? : 之间的部分； isNumber(input) 为 False 时
// 返回 : ; 之间的部分
const a = isNumber(input) ? input : String(input);
```
### Optional Parameter
``` typescript
// Optional Parameter
// here ? indicates that the name attribute may not exist
function getUser(user: string, field?: string) {
}

// here ? indicates that the name may not exist
class A {
  name?: string
}

interface B {
  name?: string
}
```

### Check whether undefined
``` typescript
// Check whether undefined
// Here defined by the Error object is an optional parameter. If you write this way, the compiler will prompt
// Error TS2532: Object is possibly'undefined'.
return new Error().stack.split('\n');

// We can add the ? Operator and call stack.split when the attribute exists. If stack does not exist, return empty
return new Error().stack?.split('\n');

// the same as below
const err = new Error();
return err.stack && err.stack.split('\n');

```
``` typescript
// Before
if (foo && foo.bar && foo.bar.baz) {
    // ...
}

// After 
if (foo?.bar?.baz) {
    // ...
}
```

##  Exclamation mark !
Using TypeScript, 3 places where the exclamation mark operator appears.

### Unary Operator
``` typescript
// ! 就是将之后的结果取反，比如：
// 当 isNumber(input) 为 True 时返回 False； isNumber(input) 为 False 时返回True
const a = !isNumber(input);
```

### Optional Parameter
 The language feature is called Non-null assertion operator.  when you add an exclamation mark after variable/property name, you're telling to TypeScript that you're certain that value is not null or undefined.
``` typescript
// 因为接口B里面name被定义为可空的值，但是实际情况是不为空的，那么我们就可以
// 通过在class里面使用！，重新强调了name这个不为空值
class A implemented B {
  name!: string
}

interface B {
  name!: string
}
```
### Emphasize that this field must exist
``` typescript
// 强制链式调用
// Here defined by the Error object is an optional parameter. If you write this way, the compiler will prompt
// Error TS2532: Object is possibly'undefined'.
new Error().stack.split('\n');

// We are sure that this field appears 100%, then we can add it ! , Emphasize that this field must exist
new Error().stack!.split('\n');
```



