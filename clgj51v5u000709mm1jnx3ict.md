---
title: "Don't Declare Javascript Variable Without Reading This!"
datePublished: Sun Apr 16 2023 08:21:45 GMT+0000 (Coordinated Universal Time)
cuid: clgj51v5u000709mm1jnx3ict
slug: dont-declare-javascript-variable-without-reading-this
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1681554360634/41cbf9b1-bbbe-4004-8750-5e0a0bb837cd.jpeg
tags: variables, hosting, javascript, variable-declaration

---

When using the javascript programming language, one of the most important concepts is declaring variables. As easy as it may sound, this can lead to a five-hour bug fix which is every developer's nightmare. Fully understanding the concept of variable declaration will help a developer's career, especially if you are a beginner. So now that we know how important variables are, we can get into understanding them more.

## **What are variables?**

Variables are used to store data or values (i.e. they act like containers). These values can be a string (e.g. 'this is a variable'), a number, or a boolean (e.g. true or false) and can be declared in three ways which are:

1. Using the **<mark>const</mark>** keyword
    
2. Using the **<mark>let</mark>** keyword
    
3. Using the **<mark>var</mark>** keyword
    

A variable can be expressed or declared using the syntax below.

```javascript
let age = 23
const country = 'Nigeria'
var fake = true
```

## Javascript Scopes

Now that we know how to declare variables, another aspect to understand is scope. A javascript scope is the part or region of your code where a variable is declared or initialised. There are three types of javascript scope, the global scope, the function scope and the block scope.

1. **Global Scope:** When a variable is declared outside a function, an object, or a class, it is said to have a global scope. This variable is also known as a global variable. For Example;
    

```javascript
let x = 2  // This is a global scope or variable
{
   let y = 3 // Not a global scope or variable
}

function getNumber (){
   let z = 4 // Not a global scope or variable
}
```

***Note****: Global variable can be accessed anywhere in the code.*

1. **Local or Function Scope:** When variables are declared inside a function, there are said to have a function scope and are called local variables. An example of a function scope is :
    

```javascript
function getNumber (){
   const z = 4 // Function Scope
   console.log(z) // Output; 4
}
console.log(z) // Reference Error
```

***Note:*** *Variables with function scope cannot be accessed outside the function.*

1. **Block Scope:** This scope was introduced in 2015 when ES6 came along. Variables declared using the const and let keywords are said to have a block scope ( i.e. they are written in curly braces {} ) e.g.
    

```javascript
{
  let x = 3
  const y = 4
  console.log(x)  // Output; 3
  console.log(y)  // Output; 4
} 
console.log(x)  // ReferenceError
console.log(y)  // ReferenceError
```

*Note: Variable with block scope cannot be called outside the block*

## Hoisting in Javascript

Hoisting is another crucial aspect of javascript that occurs when variables, functions or classes in Javascript are moved to the top of the scope they were declared, allowing them to be accessed before they are initialised. For example;

```javascript
console.log(x)  // Output; undefined
var x = 4
```

In the example above, the value gotten in the console is ***undefined*** and not ReferenceError. This shows ***undefined*** because of the use of var, but if let or const were used, a ***reference error*** would be gotten since they cannot be accessed before initialisation. Run the code below in an editor to better understand the concept;

```javascript
console.log(x) // Output; Reference Error
console.log(y) // Output; Reference Error
console.log(z) // Output; undefined
let x = 46
const y = 78
var z = 'Jake'
```

***Note***\*: All methods used for variable declaration are hoisted, but variables declared with var give an undefined value.\*

## Similarities between Const and Let

The const and let keywords were introduced in ES6 ( ECMAScript 2015 or ECMAScript 6). These two keywords have some similar properties, which are listed below:

1. They both have block scope.
    
2. They cannot be redeclared ( i.e. once a variable name has been given, the same name cannot be used again ) e.g.
    

```javascript
let x = 2   // This is allowed
let  x = 3  // This is not allowed

const y = 4  // This is allowed
const y = 5  // This is not allowed 

let z = 'Hello'   // This is allowed
const z = 'World' // This is not allowed
```

1. They are hoisted but cannot be accessed before initialisation.
    

```javascript
console.log(x)  // Reference Error
console.log(y)  // Reference Error

let x = 3
const y = 76
```

Now that we understand the similarities between the two keywords. Let's check out their differences.

## Differences between Const and Let

The main difference between the const and let keywords is that variables declared using the const keyword cannot be reassigned ( *i.e*. their *value cannot be changed*), but when the value is an array or an object, the values in the array or object can be changed. For example;

```javascript
const x = 2 
x = 2 // This is not allowed

const names = ['Ade', 'John', 'Susan']
names[0] = 'Jake' // This is allowed

const person ={
      name: 'John',
      age:36
}
person.age = 45  // This is allowed

person = {} // This is not allowed
names = []  // This is not allowed
```

While variables declared using the let keyword can be reassigned ( *i.e*. *their values can be changed*), for example;

```javascript
let x = 2 
x = 2 // This is allowed

let names = ['Ade', 'John', 'Susan']
names = 'Jake'  // This is allowed

const person ={
      name: 'John',
      age:36
}
person = {} // This is allowed
```

Another difference between the two keywords is that the const keyword must be assigned a value while the let keyword does not need to. An example is given below;

```javascript
const x; // This not allowed
let x;   // This is allowed
```

## The Var Keyword

This is one of the oldest methods of declaring a variable which has been in use since 1995. Even though some developers stopped using it in 2015 after ES6 came along, a few still use it. The variables declared using the var keyword have the following properties;

1. They can be redeclared ( i.e. the variables can be given the same name). An example is shown below;
    

```javascript
var x = 3;
console.log(x); // Output; 3

var x = "Jake"; // This is allowed
console.log(x); // Output; Jake
```

1. They have a function scope but not a block scope. The code below better explains the concept;
    

```javascript
{
  var y = 45
}
console.log(y) // Output; 45

function getNumber (){
   var z = 96
}
getNumber()
console.log(z) // Reference Error
```

1. They can be accessed before the declaration, but the value will be undefined ( i.e. they can be hoisted)
    

```javascript
console.log(x) // Output; undefined
var x = 4
```

## Conclusion

Thanks for reading, and I hope this post has helped you understand variables better. Feel free to contact me on [**Linkedin**](https://www.linkedin.com/in/ayomikun-fasina) or join my [**Discord**](https://discord.gg/GqspVn3T) community to connect with other developers.

* [Subscribe to my Youtube Channel](https://www.youtube.com/@codeWithFash)
    
* [Follow me on Twitter](https://twitter.com/codeWithFash)
    
* [Projects on GitHub](https://github.com/Fasina-ayomikun)