[![General Assembly Logo](https://camo.githubusercontent.com/1a91b05b8f4d44b5bbfb83abac2b0996d8e26c92/687474703a2f2f692e696d6775722e636f6d2f6b6538555354712e706e67)](https://generalassemb.ly/education/web-development-immersive)

# JS Higher-Order Functions

## Learning Objectives

- Review functions in JavaScript
- Define higher-order functions
- Practice working with functions and reference types

### Review JavaScript Functions

What is a function?

- Defined block of code that can be called by other code
- Functions are defined with zero or more **parameters**
  - **Parameters** are the variables for the function inputs upon definition
  - **Arguments** are the values passed in to the function when it is called

<details>
  <summary> What is a method? </summary>
  A method is a function that is defined on an object or class. Methods begin with a <code>.</code>, since they are object-properties. For example, <code>.push()</code> and <code>.reverse()</code> are methods, specifically <code>Array</code> methods.
</details>

### Function Syntax

Remember that functions can be written in several different ways. Get comfortable writing one way first, but don't let the other ways trip you up!

#### Function Declaration

```js
function sum(a, b) {
	// function "sum" defined with parameters a and b
	return a + b;
}
```

#### Function Expression

```js
// ES5 Style
var sum = function (a, b) {
	return a + b;
};

// ES6 Style, with Arrow Functions
// We won't write functions in class in this style just yet, but good to know it exists!
const sum = (a, b) => a + b;
```

#### Function Invocation (calling a function)

When we invoke a function, we use clappers `()` along with any arguments to execute or run the function's code.

```js
sum(3, 4); // function "sum" called with arguments a and b
// => 7
```

Functions always return a value, either...

1. whatever follows a function's **return** statement
2. or if there is no return statement, the function returns the value
   `undefined`.

```js
// in a repl, like the chrome console
console.log('hello!');
// 'hello!'
// => undefined
//// console.log() returns `undefined`, which appears below the console-logged message because the console.log() method is not given a RETURN VALUE
```

#### Function Reference (passing a function as an argument)

Sometimes, we just need to reference the name of a function to execute, especially when passing a callback function to a higher-order function as we'll see later. In that instance, we don't need clappers as the higher-order function will run the function when it's called upon.

```js
function sayHello() {
	console.log('hello world!');
}

btn.addEventListener('click', sayHello);
```

<!-- #### How to Convert to Arrow Syntax

We can convert an existing JavaScript function to use the arrow syntax with the
following steps.

1. Remove the `function` keyword
2. Add an arrow (`=>`) between the function parameters `()` and the opening
   brace `{`

```js
// Without arrow syntax
const helloWorld = function () {
	console.log('Hello World!');
};

// Using arrow syntax
const helloWorld = () => {
	console.log('Hello World!');
};
```

##### Single Expression Implicit Return

Arrow functions bodies that are a single expression have an added benefit, an
implicit return. This means that arrow function bodies without `{}` return the
value of the expression without needing to use `return`.

```js
// Without arrow syntax
const add = function (x, y) {
	return x + y;
};

// Using arrow syntax with an explicit return
const add = (x, y) => {
	return x + y;
};

// Using arrow syntax with an implicit return
const add = (x, y) => x + y;
```

### Arrow Function Caveats

Arrow Functions have a few caveats.

Arrow functions:

- **cannot** be used as a Constructor (`new` does not bind `this`, no
  `prototype` property). This might not mean a lot now, but when we learn about Object-Oriented Programming, this will be handy to remember!
- always have a lexically bound `this` (check out this [article](https://www.freecodecamp.org/news/learn-es6-the-dope-way-part-ii-arrow-functions-and-the-this-keyword-381ac7a32881/#:~:text=While%20in%20ES5%20'this'%20referred,method%20or%20the%20object%20itself.) to learn more about what that means).
- cannot use `arguments` key word ([learn more about `arguments`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/arguments))

### You Try Exercise: Converting To Arrow Syntax

Now it's your turn. Convert the function below to use arrow syntax. The exercises are linked in [lib/script.js](./lib/script.js).

```javascript
// Starting function
const isEven = function (num) {
	return num % 2 === 0;
};

console.log('Is 1 even?', isEven(1));
console.log('Is 2 even?', isEven(2));

// Rewrite the isEven function using arrow syntax in the space below.

//Starting function
function add(num1, num2) {
	return num1 + num2;
}

console.log('What is 3 + 4?', add(3, 4));
console.log('What is 7 + 5?', add(7, 5));

// Rewrite the add function using arrow syntax in the space below. Try to write an implicit return! :)
```
 -->

### Functions as Values

One of the things that makes JavaScript so powerful is that we can reference
functions and treat them like values stored in a variable. You might hear this behavior referred to as [first-class functions](https://developer.mozilla.org/en-US/docs/Glossary/First-class_Function), and it's a feature shared among other scripting languages like Python and PHP as well.

The impact of this is we can:

- add functions to arrays and objects, just like any other value
- pass functions as arguments to another function
- return a function from a function
<!-- 
> 1. Create an array and add a function to it in the first index. How do you
>    invoke it?

<details>
<summary>Example</summary>
<code>
let arr = [
  1,
  function() {
    return 'Hello World';
  },
  2,
  3
];

console.log(arr[1]());
</code>

</details>

> 2. Create a function that takes a function as an argument. How do you invoke
>    it?

<details>
<summary>Example</summary>
<code> function whatShouldISay(func) {
  return func();
}

function sayHello() {
return 'Hello!!!!';
}

console.log(whatShouldISay(sayHello));
</code>

</details>

> 3. Create a function that returns another function. How do you invoke them?

<details>
<summary>Example</summary>
<code>
function sayHello() {
  return 'Hello World';
}

function higherOrderFunction(callback) {
return callBack();
}

console.log(higherOrderFunction(sayHello));
</code>

</details>

<br> -->

A function that takes a function as an argument is called a _higher-order function._ The function that it takes as an argument is called a _callback function_.

## Higher-Order Functions

![morpheus](https://media.git.generalassemb.ly/user/21811/files/0896a280-6997-11eb-8a87-4d41c3783550)

Functions that take other functions as arguments or return them as output are
called **higher-order functions**. The array methods that we're going to learn later
today all fit this definition: they are functions (methods of the Array object)
that take a function as an argument and use it to transform an array of data.

> The function taken as an argument of the higher-order function is called a CALLBACK FUNCTION.

![Higher order functions and callbacks](https://media.git.generalassemb.ly/user/21811/files/c79e8e00-6996-11eb-98dd-3768c8c02827)

The purpose is to provide a level of abstraction (e.g., going through each element in an array and performing some operation for each element).

In the next part of class, we'll learn about array methods that take OTHER FUNCTIONS, i.e., callback functions, as arguments!

## Two Ways of Passing Functions as Arguments

### Passing Named Functions

Perhaps we will often need to print "Hello world" to the console. We can modularize that code into a function called sayHello:

```js
function sayHello() {
	console.log('Hello world ????');
}
```

A higher-order function that takes other functions and returns them can accept the named function as a parameter, A.K.A, a callback function:

```js
// a higher-order function that takes another function as a parameter
function myHigherOrderFunction(callback) {
	return callback();
}

// when passed the named sayHello function as an argument, it returns the callback function
myHigherOrderFunction(sayHello); //prints "Hello world ????" to the console
```

Notice that when we pass the `sayHello` function to the higher-order function, we are just _referencing_ it, not invoking it.

```js
// don't do this!! ????
myHigherOrderFunction(sayHello());

//do this ????
myHigherOrderFunction(sayHello);
```

The higher-order function does the invoking itself -- we just need to tell it the name of the function to run.

### Passing Anonymous Functions

Callback functions can also be defined **anonymously** from WITHIN the higher-order function when it's called.

Revisiting the higher-order function from the previous example, let's say we wanted the HOF to return "Hello galaxy" instead of "Hello world". We don't want to bother with writing an externally-defined named function because we won't need this functionality again elsewhere in our code.

We could write an anonymous (unnamed) function inside of `myHigherOrderFunction` when we invoke it:

```js
myHigherOrderFunction(function () {
	console.log('Hello galaxy ???');
});
```

<!-- This looks even cleaner with ES6 arrow function syntax:

```js
myHigherOrderFunction(() => console.log('Hello galaxy ???'));
``` -->

Notice again that we are not invoking the callback -- we are just referencing it for the higher-order function to run!

### HOF Example

The above examples are a bit contrived and abstract! Two great examples of a practical use case for higher-order functions are built right into JavaScript.

#### [setTimeout()](https://developer.mozilla.org/en-US/docs/Web/API/setTimeout)

This is a very handy higher-order function that executes a callback after a given delay (in milliseconds).

```javascript
function greetMe() {
	console.log('hello world!');
}

setTimeout(greetMe, 2000); // => invokes the greetMe function after a delay of 2 seconds
```

Note that in the example above, we don't invoke the `greetMe` function ourselves, i.e., we don't write `setTimeout(greetMe(), 2000)`. The higher-order function, `setTimeout`, is responsible for invoking its callback function after the given delay.

This could be re-written by passing in an anonymous (unnamed) callback function to the setTimeout:

```js
setTimeout(function () {
	console.log('hello world!');
}, 2000);
```

Note how we are simply defining the callback function inside of the higher-order function. It is unnamed and cannot be referenced in other code.

#### [setInterval()](https://developer.mozilla.org/en-US/docs/Web/API/setInterval)

`setInterval` is very similar to `setTimeout`, but instead of executing the callback function just once after a delay, `setInterval` executes the callback function once every x milliseconds. It's very useful when you need to create a countdown or timer in your application.

```javascript
function greetFriend() {
	console.log('hello friend');
}

setInterval(greetFriend, 1000); // => invokes the greetFriend function once every second (forever!)
```

> How would you rewrite the above code using an anonymous (instead of named) callback function?

### You Try: More Function Exercises

Work on the exercises linked [here](./lib/exercises.js) to get more comfortable working with functions.
