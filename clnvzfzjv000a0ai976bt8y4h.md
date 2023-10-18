---
title: "Mastering 'this' in JavaScript: A Comprehensive Guide"
datePublished: Wed Oct 18 2023 16:43:43 GMT+0000 (Coordinated Universal Time)
cuid: clnvzfzjv000a0ai976bt8y4h
slug: mastering-this-in-javascript-a-comprehensive-guide
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1697644882992/d9dec499-6dca-4ae3-92c2-79854cef5444.jpeg
tags: programming-blogs, javascript, web-development, coding, this-keyword

---

## **Introduction**

The `this` keyword in JavaScript often stands as a challenging concept for beginners. This is mainly because its behaviour changes depending on where it is used in the code. By the end of this read, you'll not only have a firm grasp of the topic but also be confidently applying it in your daily coding tasks.

The `this` keyword is applicable in several scenarios in JavaScript. We will carefully examine each use case to provide a comprehensive understanding of its uses and applications.

## The `this` keyword in the Global Scope

The `this` keyword refers to the `window` when called in the global scope i.e. outside a function, object or class. For a deeper dive into the global scope, check out my article: [Don't Declare JavaScript Variable Without Reading This!](https://hashnode.com/post/clgj51v5u000709mm1jnx3ict)

If you type `console.log(this)` in your JavaScript file and run it in a browser, you'll see an output like `[object Window]` in the console which contains the details of the window. To open the console, press `Ctrl + Shift + I` (or `F12`) in your browser if you're using Windows.

This is a visual representation of the output in the console:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697632161646/06603783-19e2-499a-8867-fba7220bcddb.png align="center")

## The `this` keyword in the Objects

When the `this` keyword is called in an object, it often refers to the object itself. Here is an example of this:

```javascript
 const callPerson = {
  name: "Ayo",
  age: 35,
  getNickname: function () {
    console.log(this.name);
  },
};
callPerson.getNickname();
// Output : Ayo
```

In objects, methods (which are essentially functions defined inside objects) can access other properties of the same object. The `this` keyword acts as a reference to the object itself, granting methods the ability to retrieve or modify other properties within the same object. This is why in our example when the `getNickname` method is called, it can access the `name` property of the `callPerson` object through [`this.name`](http://this.name).

## The `this` keyword in the Function Scope

There are two primary ways of declaring a function in JavaScript which are the regular functions and arrow functions. The behaviour of the `this` keyword differs between them. Let's delve deeper into each scenario to understand these distinctions.

### Regular functions:

In a regular function, the behaviour of the `this` keyword varies based on where it is invoked. It might refer to the `window` object just like in the global scope when in an empty function. However, the reference can change in different situations—especially when a strict mode is involved. Let's dive into examples showcasing each of these scenarios.

* When called in an empty function i.e. in a function that's not a method or not inside another function.
    

```javascript
function callThis(){
   console.log(this)  // Output: [object,Window]
}
callThis()
```

* When in strict mode:
    

```javascript
'use strict'

function callThis(){
   console.log(this)  // Output: undefined
}
callThis()
```

As you can see the output is different depending on when used, we will check other use cases of the regular function as we move forward in this article.

### Arrow Functions

In arrow functions, the behaviour of the `this` keyword is distinct. Arrow functions do not have their own value for `this`. Instead, they use the `this` value from the surrounding scope in which they are written i.e. they have a lexical scope. To better understand this let's check a few examples explaining this concept.

```javascript
const callPerson = {
  name: "Ayo",
  age: 35,
  getNickname: () => {
    console.log(this);
  },
};
callPerson.getNickname();
// Output : [object Window]
```

From the example, we will notice that the output when we used an arrow function is different from regular functions. Instead of getting the object containing the name, age and getNickname function, we got the `window` object instead. This is because the `this` value in the surroundings of the object is the global scope, which is the `window`. Let's check one more example:

```javascript
function getName() {
  this.name = "Ayo";
  const getAge = () => {
    console.log(this.name); 
  };
  getAge();
}
getName();
// Output : Ayo
```

Just like the previous example, the arrow function refers to the scope in its surroundings which in this case is the function scope getName.

## The `this` keyword in Event Listeners

When calling the `this` keyword in event listeners, it refers to the DOM element on which the event listener is called. For example:

```xml
<button id="btn">hello</button>
```

Now let's add the event listener;

```javascript
document.getElementById("btn").addEventListener("click", function () {
  console.log(this);
});

//Output: <button id="btn">hello</button>
```

**Note:** When using event listeners always use the regular function since arrow functions do not have a `this` value.

## Explicitly Controlling the `this` value

What is meant by explicitly controlling the `this` value is overriding the default `this` value if it is not what you need. There are three ways of doing that which are by, using the call, bind and apply methods:

* **Using the call method:** The call method is a predefined JavaScript method that allows you to call or invoke a function with a specified `this` value and arguments. Here is an example of how it works:
    

```javascript
function getName(greeting) {
  console.log(greeting + ", " + this.name);// intial this value is the window
}

const person = { name: "John" };
// Now the this value is the object person
getName.call(person, "Hello"); // Outputs: "Hello, John"
```

From the above example, we see how the `this` value changes from the `window` to the object `person`.

* **Using the bind method:** The `bind` method, like `call`, lets you set the `this` value for a function. However, instead of executing the function immediately, it returns a new function with the provided `this` value. For example:
    

```javascript
function getName(greeting) {
  console.log(greeting + ", my name is " + this.name); //intial this value is [object,Window]
}

const person = { name: "Alice" };

// Create a new function with this bound to the person object
const newName = getName.bind(person);

// invoke the new function with the needed parameters
newName("Hello"); // Outputs: "Hello, my name is Alice"
```

* **Using the apply method:** This is similar to the call method, the only difference between them is that the call method allows you to pass in arguments individually while the apply method allows you to pass the arguments as an array. Here is an example differentiating them:
    

```javascript
function introduce(greeting, punctuation) {
    console.log(greeting + ", my name is " + this.name + punctuation);
}

const person = { name: "Bob" };

// Using apply to invoke the function
introduce.apply(person, ["Hello", "!"]);  // Outputs: "Hello, my name is Bob!"

// Using call to invoke the function
introduce.call(person, 'Hello','!');   // Outputs: "Hello, my name is Bob!"
```

## Conclusion

Understanding the `this` keyword in JavaScript can initially seem like a difficult challenge, given its dynamic nature and varied behaviour across different contexts.

Here is a practical piece of advice for those still struggling with the concept: If ever in doubt about what `this` refers to in a specific context, it's advisable to use `console.log(this)` to inspect its value. This simple debugging step can save hours of troubleshooting and offer immediate clarity.

As with many aspects of programming, the key to truly grasping `this` lies in consistent practice and application. Don't be disheartened by initial confusion; even seasoned developers sometimes find themselves double-checking their understanding of context in JavaScript. Keep experimenting, writing code, and challenging your understanding. With time and experience, you will be able to work with this without any issues. Until then, happy coding!

If you found this content helpful, consider connecting with me on [Twitter](https://www.twitter.com/@codeWithFash), [LinkedIn](https://www.linkedin.com/in/ayomikun-fasina), and [GitHub](https://www.github.com/Fasina-ayomikun). Also, don't forget to subscribe to my [YouTube channel](https://www.youtube.com/@webDevIn10) for more insights and tutorials!