---
title: "Promises in JavaScript"
seoTitle: "JavaScript Promise"
datePublished: Tue Feb 13 2024 11:07:13 GMT+0000 (Coordinated Universal Time)
cuid: clsk9drg4000c09l619jaevd9
slug: promises-in-javascript
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1707822187452/b62caf23-9a14-4ee3-9358-44493e194ced.png
tags: javascript, coding, codingnewbies

---

Before getting started with the main focus of this article, let's explore an important concept that lays the foundation for our discussion.

## Asynchronous programming

In JavaScript, operations typically occur synchronously, meaning one operation runs at a time. This implies that a function must finish executing entirely before the next function can commence. However, synchronous operations can pose issues when certain tasks take a considerable amount of time to complete, leading to delays in the overall execution flow. To address this challenge, asynchronous operations were introduced. With asynchronous programming, tasks can commence and run at the same time, allowing new operations to begin even before previous ones have finished. This approach helps prevent operations from waiting on each other, thereby improving efficiency and responsiveness within applications.

### Still confused?

let's imagine a scenario where a mother gives her son a list of chores: washing the plates, making dinner, taking out the trash, and washing his dirty clothes.

The son who is likely feeling frustrated can handle these chores in one of two ways:

In the first scenario, the son diligently completes each task one after the other: first washing the plates, then making dinner, followed by taking out the trash, and finally washing his clothes. This sequential approach mirrors synchronous operation in programming, where tasks are executed in a predetermined order, with each task waiting for the previous one to finish before starting.

Now, in the second scenario, the son decides to multitask: while the washing machine handles his dirty clothes, he takes out the trash, and simultaneously, he washes the plates while cooking dinner. This scenario reflects asynchronous operation in programming. Here, tasks can overlap and occur simultaneously, without strictly sticking to a sequential order. Just as the son efficiently manages multiple chores at once, asynchronous programming allows different operations to proceed independently and concurrently, enhancing overall efficiency and responsiveness.

So just like the frustrated son has more time to play video games in the second scenario unlike the first, asynchronous operation takes a shorter time to execute compared to synchronous operation.

## So why do we need Promises

With the introduction of asynchronous programming, Promises became a vital tool for managing such operations effectively. As the name suggests, Promises are a way for the browser to assure us that it will fulfill a certain operation. When a Promise is created, it returns an object which is a representation of the completion or failure of that operation.

Just like when our uncles promise us money, which they could give us or pull the 'I will give you later' card, the browser could give us the data we asked for or return an error if it is unable to get the data.

Promises have three distinct states:

1. **Pending:** This state indicates that the associated operation has not yet started or is currently running.
    
2. **Fulfilled:** When the operation is successfully completed, the Promise transitions to the fulfilled state. This indicates that the browser has fulfilled its promise and resolved the operation as expected.
    
3. **Rejected:** If the operation encounters an error or fails for any reason, the Promise transitions to the rejected state. In this case, the browser notifies us of the failure by sending an error message which let's us know what went wrong.
    

Promises play a crucial role in asynchronous JavaScript programming, providing a structured way to handle asynchronous operations and manage their outcomes effectively.

## So how do we create this Promise?

A Promise is created using the `Promise` constructor and the constructor accepts a callback function as an argument. This callback function takes in two parameters: `resolve` and `reject`. Let's take a look at the example below to better understand.

```javascript
const newPromise = new Promise((resolve, reject) => {
  setTimeout(() => {
    const success = true;
    if (success === true) {
      resolve("Operation was successful");
    } else {
      const error = new Error("An error occurred");
      reject(error);
    }
  }, 2000);
});
```

* `resolve` : When invoked, this function indicates that the asynchronous operation has successfully completed. It can optionally take in a value, which could be a string, an object, or an array containing data relevant to the successful completion of the operation.
    
* `reject` : Whereas, this function is called to signal that the asynchronous operation has encountered an error or failed for some reason. Like `resolve`, `reject` can also accept a value, typically a string, an object, or an array, providing information about the error or the reason for the failure.
    

Looking at the example above let's assume that the `success` variable indicates the fulfillment or rejection of the promise. Therefore if `success` is true then the promise invokes the resolve function and the reject function if otherwise.

*Note: The setTimeout was added to add a little delay to the operation.*

## Now how do we handle this Promise

Since we understand how to create a Promise, let's explore how to handle it. Promises can be managed using various methods, one of which involves utilizing the `.then()` and `.catch()` functions.

* `.then` : This function is used to handle the fulfillment or rejection of a Promise. It takes two optional callback functions as arguments:
    

```javascript
const onFulfilled = (result) => {
  console.log(result); //Output: Operation was successful
};
const onRejected = (error) => {
  console.log(error); //Output: An error occurred
};
newPromise.then(onFulfilled, onRejected);
```

The `onFulfilled` function is invoked if the Promise is fulfilled, and it receives the resolved value as its argument, which is referred to as `result` in this case. As we can see, the output is the same as the value passed into the `resolve` function when we created the Promise.

On the other hand, the `onRejected` function is invoked if the Promise is rejected, and it receives the reason for the rejection as its argument. Similarly, the output is the same as the value passed into the `reject` function.

Now, let's use our uncles' promises to illustrate this concept. When our uncles promise to give us money or our favorite video game the next day, we can think of it as them creating a promise. When the time comes for them to fulfill the promise by giving us the money, it's like receiving the 'result' we expected. However, if they fail to fulfill their promise and don't give us the money, it's the same as encountering an 'error.'

So, we can tell our siblings that our uncle promised to give us money 'then' actually gave us the money, or our uncle promised to give us money 'then' said he didn't have the money.

Therefore, whenever you encounter a promise in JavaScript, you can simply think of it as having a promise 'then' checking whether you receive the expected result or encounter an error.

Note: The `onRejected` function is rarely added to the .then() method since errors can be handled in a different way, which we will explore next.

* `.catch` : This function works similarly to the `onRejected` function. It is used to handle errors that occur during the execution of a Promise, receiving the error message as an argument.
    

```javascript
newPromise.then(onFulfilled).catch((error)=>{
   console.log(error); //Output: An error occurred
})
```

In this example, the `.catch()` method is chained after the `.then()` method to handle any errors that may occur in the Promise chain. If any error occurs in the preceding `.then()` method, it will be caught and handled by the `.catch()` function.

So if we decide not to add the `onRejected` function to the `.then()` callback, we can use the `.catch()` method to handle any errors we encounter.

Now let's take a look at another concept that we can use when handling promises using `.then()` and `.catch` method

* `.finally()` : This function is used to specify a block of code that should be executed regardless of whether the Promise is resolved or rejected. This can be useful for performing cleanup tasks or finalizing operations.
    

```javascript
const onFulfilled = (result) => {
  console.log(result);
  // Output: Operation was successful
  // Finally block executed
};

newPromise.then(onFulfilled)
  .catch((error) => {
    console.log(error); 
    // Output: An error occurred
    // Finally block executed
  })
  .finally(() => {
    console.log('Finally block executed'); 
    // Output: Finally block executed
  });
```

In this example, the `.finally()` method is utilized to define a block of code that executes after the Promise chain completes, irrespective of whether the Promise is resolved or rejected. This ensures that the specified code is always executed, offering a convenient way to handle cleanup tasks or finalize operations.

So, whether you receive money from your uncle or not, you still have to wash the plates he used for eating.

## Chaining Promises

Promises in JavaScript can be chained together using the `.then()` function. Let's explore this concept through an example:

```javascript
// Step 1: Prepare Soup (Promise)
const promiseOne = new Promise((resolve) => {
  setTimeout(() => {
    console.log("Preparing Soup");
    resolve("Put pot on Fire");
  }, 1000);
});

// Step 2: Add oil (Promise)
const promiseTwo = new Promise((resolve) => {
  setTimeout(() => {
    resolve("Added Oil");
  }, 2000);
});

// Step 3: Add Pepper (Promise)
const promiseThree = new Promise((resolve) => {
  setTimeout(() => {
    resolve("Added Pepper");
  }, 1500);
});

// Step 4: Boiling Soup (Promise)
const promiseFour = new Promise((resolve) => {
  setTimeout(() => {
    resolve("Soup boiling");
  }, 1000);
});

// Chaining Promises to make the sandwich
promiseOne
  .then((result) => {
    console.log(result); // Output: Preparing Soup Put pot on Fire
    return promiseTwo;
  })
  .then((result) => {
    console.log(result); // Output: Added Oil
    return promiseThree;
  })
  .then((result) => {
    console.log(result); // Output: Added Pepper
    return promiseFour;
  })
  .then((result) => {
    console.log(result); //Output: Soup boiling
  })
  .catch((error) => {
    console.error("Error making sandwich:", error);
  });
```

In this example, promises are utilized to represent each step in the process of preparing soup. The `.then()` method is employed to chain these promises sequentially. As each promise resolves, the next step in the process is executed. Any errors that occur during the process are caught and handled using the `.catch()` function.

Essentially, when a promise yields its result, it returns another promise, and this pattern continues. However, it's important to note that the chaining breaks wherever an error occurs. For instance, if `promiseTwo` rejects, the next `.then()` will not be executed.

Feel free to experiment with this code in your code editor to gain a better understanding of its behavior.

## Methods in Promises

In JavaScript, the built-in `Promise` feature is utilized for handling promises, offering a variety of methods to effectively manage them. We will explore several of these methods that are commonly encountered in everyday coding tasks, assuming you code regularly.

* `Promise.all()` : This is a static method on the `Promise` object in JavaScript. It accepts an array of Promises and returns a single Promise that resolves only when each Promise in the array resolves.
    
    Let's examine how it works with an example:
    

```javascript
const promise1 = new Promise((resolve, reject) => {
  setTimeout(() => resolve("Promise 1 resolved"), 1000);
});

const promise2 = new Promise((resolve, reject) => {
  setTimeout(() => resolve("Promise 2 resolved"), 1500);
});

const promise3 = new Promise((resolve, reject) => {
  setTimeout(() => resolve("Promise 3 resolved"), 2000);
});
const allPromises = Promise.all([promise1, promise2, promise3]);
allPromises
  .then((values) => {
    console.log("All promises resolved:", values);
/* Output:
All promises resolved: 
[
    "Promise 1 resolved",
    "Promise 2 resolved",
    "Promise 3 resolved"
]
*/
  })
  .catch((error) => {
    console.error("At least one promise rejected:", error);
  });
```

In this example, `Promise.all()` returns a single Promise which is stored in the `allPromises` variable. This Promise is then handled using the `.then()` function. When the Promise is resolved, the `.then()` function receives an array containing the resolved values of each Promise in the array.

If any of the Promises in the array rejects, the `allPromises` Promise will fail and return an error. You can test this by changing one of the `resolve` functions in any of the Promises to `reject`.

Feel free to try this out in your code editor and share the output in the comments below..

* `Promise.allSettled()` : This function is similar to the `Promise.all()` function, but with a key difference. Unlike `Promise.all()`, which fails immediately if any Promise in the array rejects, `Promise.allSettled()` returns the status of each Promise, whether fulfilled or rejected, in the `.then()` function.
    
    Let's examine how it works with an example:
    

```javascript
const promise1 = new Promise((resolve, reject) => {
  setTimeout(() => resolve("Promise 1 resolved"), 1000);
});

const promise2 = new Promise((resolve, reject) => {
  setTimeout(() => resolve("Promise 2 resolved"), 2000);
});

const promise3 = new Promise((resolve, reject) => {
  setTimeout(() => reject(new Error("Promise 3 rejected")), 1500);
});

const allPromises = Promise.allSettled([promise1, promise2, promise3]);
allPromises.then((values) => {
  console.log(values);
});
 
// Output:
// [
//   {
//        "status": "fulfilled",
//        "value": "Promise 1 resolved"
//    },
//    {
//        "status": "fulfilled",
//        "value": "Promise 2 resolved"
//    },
//    {
//        "status": "rejected",
//        "reason": Error: Promise 3 rejected 
//    }
// ]
```

In this example, even though the third Promise is rejected, `Promise.allSettled()` still returns all the values in the `.then()` function, each with its respective status (`fulfilled` or `rejected`). This behavior is useful when you want to handle the results of all Promises, regardless of whether they succeed or fail.

It's worth noting that `Promise.allSettled()` does not require a `.catch()` function, as it always resolves, providing the status of each Promise in the array.

Feel free to experiment with this code to explore its behavior further.

* `Promise.race()` : This function is a method on the Promise object that accepts an array of Promises and returns a single Promise. The value or error returned by this single Promise is determined by the first Promise in the array to resolve or reject. In other words, the fastest Promise determines the outcome for all Promises in the array.
    
    Let's examine how this works with an example:
    
    ```javascript
    const promise1 = new Promise((resolve, reject) => {
      setTimeout(() => resolve("Promise 1 resolved"), 3000);
    });
    
    const promise2 = new Promise((resolve, reject) => {
      setTimeout(() => resolve("Promise 2 resolved"), 2000);
    });
    
    const promise3 = new Promise((resolve, reject) => {
      setTimeout(() => reject(new Error("Promise 3 rejected")), 2500);
    });
    
    const allPromises = Promise.race([promise1, promise2, promise3]);
    allPromises
      .then((values) => {
        console.log(values); // Output: Promise 2 resolved
      })
      .catch((error) => {
        console.error(error); 
      });
    ```
    
    Note: If `promise2` gives an error the `allPromises` will give an error as well since `promise2` is the fastest promise to run within 2secs(2000 ms).
    
    Feel free to play around with the time and see how this affects the output.
    
* `Promise.any()` : This function is a method on the Promise object that accepts an array of Promises and returns a single Promise. The value returned by the single Promise depends on the first promise in the array to fulfill, i.e. the promise that resolves first.
    
    Unlike `Promise.race()`, which doesn't consider whether the first promise to settle resolves or rejects, `Promise.any()` only deals with the promise that resolves first. If all the promises in the array reject, an AggregateError is returned.
    
    Let's examine this behavior with an example:
    

```javascript
const promise1 = new Promise((resolve, reject) => {
  setTimeout(() => resolve("Promise 1 resolved"), 3000);
});

const promise2 = new Promise((resolve, reject) => {
  setTimeout(() => resolve("Promise 2 resolved"), 2000);
});

const promise3 = new Promise((resolve, reject) => {
  setTimeout(() => reject(new Error("Promise 3 rejected")), 1000);
});

const allPromises = Promise.any([promise1, promise2, promise3]);
allPromises
  .then((values) => {
    console.log(values); //Output: Promise 2 resolved
  })
  .catch((error) => {
    console.error("First Promise rejected:", error);
  });
```

In this example, even though `promise3` settles first, it doesn't determine the output of `allPromises` because it rejects. Among the two promises that resolve, `promise2` resolves first, which is why it determines the output of `allPromises`.

Feel free to experiment with the timing of the promises to observe how it affects the output.

## Async/Await Function

`async/await` is a modern JavaScript feature that simplifies asynchronous programming by enabling you to write asynchronous code in a synchronous style. It offers a cleaner and more readable syntax for working with Promises and asynchronous operations, enhancing code maintainability and readability. We already looked into the `.then()` and `.catch()` method of handling Promises now let's take a look at how to handle Promises using `async/await` method.

* `async` : This keyword is used to define asynchronous functions in JavaScript. An asynchronous function is one that performs operations that may take an unpredictable amount of time to complete. By prefixing a function declaration with `async`, it signals that the function will perform asynchronous operations.
    
* `await` : This keyword is used exclusively within functions defined with the `async` keyword. It allows an asynchronous operation to pause execution until a Promise is settled (either fulfilled or rejected). When `await` is used, the function will wait for the Promise to settle, and it will return the resolved value when the Promise resolves.
    

Here's a basic example illustrating the usage of `async` and `await`:

```javascript
// Step 1: Prepare Soup (Promise)
const promiseOne = new Promise((resolve) => {
  setTimeout(() => {
    console.log("Preparing Soup");
    resolve("Put pot on Fire");
  }, 1000);
});

// Step 2: Add oil (Promise)
const promiseTwo = new Promise((resolve) => {
  setTimeout(() => {
    resolve("Added Oil");
  }, 3000);
});

// Step 3: Add Pepper (Promise)
const promiseThree = new Promise((resolve) => {
  setTimeout(() => {
    resolve("Added Pepper");
  }, 3500);
});

// Step 4: Boiling Soup (Promise)
const promiseFour = new Promise((resolve) => {
  setTimeout(() => {
    resolve("Soup boiling");
  }, 2000);
});

// Chaining Promises to make the sandwich
const asyncFunction = async () => {
  const result1 = await promiseOne;
  console.log(result1); // Output: Preparing Soup  Put pot on Fire
  const result2 = await promiseTwo;
  console.log(result2); // Output: Added Oil
  const result3 = await promiseThree;
  console.log(result3); // Output: Added Pepper
  const result4 = await promiseFour;
  console.log(result4); // Output: Soup boiling
};
asyncFunction();
```

In the code above the `await` keyword in front of each promise tells the asynchronous function that the function should pause until the promise is settled(either resolved or rejected) before moving to the next line. This effectively makes the function behave synchronously, even though it's performing asynchronous operations.

It's important to note that the `await` keyword can only be used inside an asynchronous function, which is why the `async` keyword is needed to define the function as asynchronous

## Handling Error in Async/Await Method

You might have been wondering what happens if any of the Promises reject and how to handle that. Well, that's where the `try...catch` block comes into play.

Let's take a look at how we can deal with that:

```javascript
// Step 1: Prepare Soup (Promise)
const promiseOne = new Promise((resolve, reject) => {
  setTimeout(() => {
    console.log("Preparing Soup");
    resolve("Put pot on Fire");
  }, 1000);
});

// Step 2: Add oil (Promise)
const promiseTwo = new Promise((resolve, reject) => {
  setTimeout(() => {
    reject("An error occurred when adding oil");
  }, 3000);
});

// Step 3: Add Pepper (Promise)
const promiseThree = new Promise((resolve, reject) => {
  setTimeout(() => {
    resolve("Added Pepper");
  }, 3500);
});

// Step 4: Boiling Soup (Promise)
const promiseFour = new Promise((resolve, reject) => {
  setTimeout(() => {
    reject("An error occurred during boiling");
  }, 2000);
});

// Chaining Promises to make the sandwich
const asyncFunction = async () => {
  try {
    const result1 = await promiseOne;
    console.log(result1);
    const result2 = await promiseTwo; // This promise rejects and the function exits
    console.log(result2);
    const result3 = await promiseThree; // This line would not run
    console.log(result3);
    const result4 = await promiseFour; // This line would not run
    console.log(result4);
  } catch (error) {
    console.log(error); // Output: An error occurred when adding oil
  }
};
asyncFunction();
```

In this example, the asynchronous operations are enclosed within a `try` block. If an error occurs within any of these operations, such as the rejection of `promiseTwo`, the function jumps to the `catch` block. Consequently, subsequent asynchronous operations (`promiseThree` and `promiseFour`) are not executed. Instead, the error message from the rejected promise is caught and logged, providing a clear indication of what went wrong.

The `try...catch` block offers a structured approach to handle errors in asynchronous code, enhancing code readability and maintainability.

## Conclusion

Asynchronous programming in JavaScript, facilitated by Promises and modern constructs like `async/await`, has changed the way developers handle tasks that involve time-consuming operations. By allowing operations to run synchronously and asynchronously, JavaScript applications can achieve better responsiveness and efficiency.

Promises serve as a crucial tool for managing asynchronous operations, offering a structured approach to handle the completion or failure of tasks. The various Promise methods, such as `Promise.all()`, `Promise.allSettled()`, `Promise.race()`, and `Promise.any()`, provide developers with flexible ways to coordinate and manage multiple asynchronous tasks effectively.

Furthermore, the introduction of `async/await` simplifies asynchronous code even further by providing a more readable and synchronous-like syntax for handling Promises. This modern approach enhances code readability and maintainability, making asynchronous programming more accessible to developers.

In conclusion, mastering asynchronous programming techniques in JavaScript, including Promises and `async/await`, is essential for building responsive, efficient, and scalable applications in today's web development landscape.

I know coding can be overwhelming but you have got this, Goodluck.

If you found this content helpful, consider connecting with me on [Twitter](https://www.twitter.com/@codeWithFash), [LinkedIn](https://www.linkedin.com/in/ayomikun-fasina), and [GitHub](https://www.github.com/Fasina-ayomikun). Also, don't forget to subscribe to my [YouTube channel](https://www.youtube.com/@webDevIn10) for more insights and tutorials!