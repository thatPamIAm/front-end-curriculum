---
title: Functions in JavaScript
length: 120
tags: javascript, introduction, foundation, variables
---

## Learning Goals

In this lesson we'll cover:

* How to declare functions with and without parameters
* How to call functions with and without parameters
* Write our own functions

## Vocab

- `Function` A predefined and reusable group of behavior
- `Call/Invoke` Running a function
- `Parameters` The variables declared in a function definition
- `Arguments` The variables passed to a function when it's called/invoked

## Functions
Functions are a way to group statements together to perform a specific task. Functions are reusable blocks of code. To create a function, you must give it a name and then write the statements required for the function to achieve its task inside the function's curly braces. Let's work through the pieces and parts of a function.

### Anatomy of a Function:
```javascript
function makeStatements() {
  var firstStatement = 'Pizza is AMAZING!';
  console.log('Burritos taste delicious!');
  console.log(firstStatement);
}
```

- You declare a function using the keyword `function`.
- Since functions perform an action, it is generally encouraged to use an action verb in the function name. i.e. `getSize`, `saveNote`, `generateRandomNumber`.
- You can name the function anything you want, but it must include a set of parentheses after the name, which can be empty or accept parameters. (we'll go over parameters shortly, but for now let's keep it empty)
- You must follow the parentheses with a set of curly braces, which act as bookends to hold the set of statements you want the function to run when it is called.
- In order to call a function, type the function name with it's parentheses and any associated arguments (Take a look below)

### Invoke a Function:
```javascript
// Invoke a function
makeStatements();
```

When this code is read, `makeStatements()` is "invoked", all three statements within the function's body (those curly braces) get run, one line at a time.  What do you think will happen if we swap the 2nd and 3rd statements?

<section class="call-to-action">
### Your Turn
With the person across from you, create your own functions in the console:
* Write a function that logs to the console a message of "YO!", and then logs a sum of five different integers.
* Write a function that assigns three different math equations to three different variables, then logs the sum of the values of all three variables.
* Write a function that declares a `firstName` variable and a `lastName` variable, then logs a message that incorporates the full name, and then logs a [random number](http://frontend.turing.io/independent-study/random-numbers.html) to the console.
</section>

### Passing Information to a Function:
Sometimes you need to give a function some information in order for it to do its job. You can give that function the information it needs by providing _parameters_ in the function declaration. These are place holders that you identify with appropriately named labels inside the parentheses of your named function. The words you use for your parameters act like variables INSIDE the function, which means they serve as a means to pass values.

### Parameters vs. Arguments
Its a subtle difference. Basically, when you declare a function, and you stipulate the function will accept some bits of information, those are parameters. Then, when you pass the values of the parameters, those are called arguments. Like this:

```javascript
// parameters named on declaration of function
function createDreamCar(make, model) {
  return "My dream car is a " + make + " " + model;
}

// arguments "Audi" and "R8" passed into a called function
createDreamCar("Audi", "R8");
```

### Getting A Value from Functions:
Some functions return information to the code that called them. Wait - what? When a function performs a calculation, like 2 + 2, it will return the "answer" of 4, right?I still need the keyword _return_ in order to return that value back from a function. Let's work with some return statements in functions with parameters in the console:

```javascript
function addTwoNumbers(num1, num2) {
  num1 + num2;
}

function addTwoNumbers(num1, num2) {
  return num1 + num2;
}

function addTwoNumbers(num1, num2) {
  console.log('Boom');
  return num1 + num2;
}

function addTwoNumbers(num1, num2) {
  return num1 + num2;
  console.log('Boom');
}
```

Notice in the last example that when the `return` statement is called in a function, it ends function execution (the following lines do not run), and it specifies a value to be returned to the function caller. Here is the basic structure:

```javascript
// This is the formula:
return [expression];
// The expression to return. If the return is omitted, undefined is returned instead. The [] are meant to show that the expression is dynamic.
```
<section class="note">
### Note
If the expression is omitted/there is no return statement, `undefined` is returned instead.
</section>

The following return statements are all examples that would break function execution:

```javascript
return;
return true;
return false;
return x;
return x + y / 3;
```

<section class="call-to-action">
### You Do
* Create a function called `saySomething` that requires no parameters. This function should return a message of your choice.
* Create a function called `showFavorites` that requires three parameters - a food, a movie, and an animal. Your function should return a string that uses either concatenation or interpolation to return the three favorite things in a string.</
* Create a function called `calculateAge` that takes a single parameter - a year. Your function should return the difference in years from the birth year from our current year, 2019.

If you finish early, try writing tackling [these functions](https://www.teaching-materials.org/javascript/exercises/functions)!
</section>

### Additional Resources & Practice

* [JS Style Guide](https://github.com/turingschool-examples/javascript)
* [JavaScript Playground](http://frontend.turing.io/lessons/module-1/javascript-playground.html) let's you experiment more with these concepts.

