---
title: Testing with Chai Spies
tags: TDD, unit testing, mocha, chai, webpack, spies
mod: 2
---

<section class="call-to-action">
We'll continue working with the [our-first-tests repo](https://github.com/turingschool-examples/our-first-tests). Commit any changes you may have made, then checkout the `spies-begin` branch by running the following commands:

 ```bash
 git fetch --all
 git checkout -b spies-begin origin/spies-begin
 ```
 
</section>

## Why Spy with Our Little Eyes?

One of the biggest hurdles with front-end testing, and why it can be so complex, is that your tests are running in a different environment than your app. Your app runs in the **browser**, and your tests run in the **terminal**.

<!-- I've mentioned in our first testing lesson, that TDD was pretty much always a process on the back-end, and it made sense there because when you're writing server-side/back-end code, you're pretty much living in your terminal. One reason testing didn't come around to the front-end side of things was because we have this environmental difference. We couldn't figure out how to run our tests in an environment that behaved like a browser. -->

This environmental difference means that we can't test functionality that's dependent on the browser. The terminal does not have access to all of the objects and web APIs that we have in the browser, and will therefore not understand things like:

`document.getElementById()`

because it doesn't know what a `document` is. If we look at our `window` object in the console, pretty much anything that exists here that we want to use in our code, the terminal will not know about or understand. So we can run into some problems testing our code when we want to do things like:

* manipulate the DOM
* perform network requests
* manage localStorage data

## Practice

Let's look at what would happen if we tried to test a method that leverages `localStorage`.

Let's add a method to our `Box.js` class called `saveDetails` that persists our box information to localStorage:

```js
saveDetails() {
  localStorage.setItem('box', { 
    height: this.height,
    width: this.width
  });
}
```

and now let's try to test this method:

```js
describe('saveDetails', function() {
  it('should save details to localStorage', function() {
    var box = new Box(100, 100);
    box.saveDetails();
    expect(localStorage.getItem('box').to.equal({ 
      width: 100,
      height: 100
    })
});
```

We'll see in our terminal `ReferenceError: localStorage is not defined`. This would be the case even if we changed our expectation to `expect(true).to.equal(true)`, because the test is actually failing during the **execution phase** when our **application code** is trying to do `localStorage.setItem()`.


## What are our Options?

### Mocking LocalStorage

One option is to recreate our own version of `localStorage`. This might sound daunting at first, but it's actually not all that much code:

```js
global.localStorage = {
  store: {},
  setItem(keyName, value) {
    this.store[keyName] = value;
  },
  
  getItem(keyName) {
    return this.store[keyName]
  }
}
```

This is a common and totally reasonable practice in front-end testing. Just like we mock out data to work with, we also sometimes mock out web APIs to bring some of that functionality to the terminal. The only problem with this now, is that if anything is wrong with our implementation of `localStorage`, our tests might fail even if our application code isn't actually broken. 

So our other option is to leverage spies.


### Spies

Spies are useful for when you want to check that something happened - but you don't necessarily care exactly what it did. **Spies will help you verify calls to methods without actually calling them.**

So in our example, we would want to verify that `localStorage.setItem()` was called, but we don't actually care to test the result of that method running. (We can assume the browser has already tested their implementation of `localStorage`, which means that we don't have to!) We are trusting that as long as we're invoking `localStorage.setItem()`, our browser is going to do it.

So all we really want to test is that something was called. We want to **spy** on localStorage, and make sure that its `setItem` method was called. 

A spy will listen for a specific function, `localStorage.setItem`, to be called in a test. When it is called, the spy takes over control of `localStorage.setItem`. The spy runs a “fake” function instead, as if `localStorage.setItem` had actually run.

To do this, we're going to add another `devDependency` to our `package.json` file:

```bash
npm install chai-spies --save-dev
```

To our test file, we'll require in our new dependency and configure `chai` to use it, by adding:

```js
const spies = require('chai-spies');
chai.use(spies);
```

Now instead of mocking out all the functionality of `localStorage`, we can simply assign it to an empty object that we will spy on:

```js
global.localStorage = {};
```


```js
chai.spy.on(localStorage, ['setItem', 'getItem'], () => {});
```

<section class="call-to-action">
Checkout the following documentation on [chai.spy.on](https://github.com/chaijs/chai-spies#spyon) -- what are the three arguments it takes in?
</section>


1. `chai.spy.on()` is a method that let's us define what we want to spy on
2. the **first** argument is the object we want to spy on
3. the **second** argument is an array of any methods we want to override with a spy (or a single string if we're only spying on one method)
4. the **third** argument is an optional replacement for how those methods should behave/what they should do

So what we're doing with this code is saying: "I know that `localStorage` works as it should, because the browser engineers have already tested it. All I want to verify is that I'm actually invoking `localStorage.setItem()`. I am going to replace the default behavior of `localStorage.setItem()` with a spy so that I can assert it was called without having to worry about what's happening under the hood."

Let's see how this changes the assertion logic of our test:

```js
describe('saveDetails', function() {
  it('should save details to localStorage', function() {
    var box = new Box(100, 100);
    box.saveDetails();
    expect(localStorage.setItem).to.have.been.called(1); 
    expect(localStorage.setItem).to.have.been.called.with('box', { width: 100, height: 100 });
});
```

We have two assertions here: 
1. verifies that `localStorage.setItem` was called one time
2. verifies that it was called with accurate arguments


<section class="call-to-action">
Think about the other web APIs and libraries you'll be using in your projects. Where might spies help you? What will be your strategy?
</section>
