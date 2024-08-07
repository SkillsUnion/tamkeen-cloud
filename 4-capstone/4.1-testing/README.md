# 4.1: Testing

## Learning Objectives

1. Programmatic software testing is a crucial feature of software development that all tech companies practice
2. Programmatic testing allows us to quickly verify we did not break existing features when building new ones
3. Programmatic testing involves writing code to test our code
4. There are 3 general categories of programmatic tests: unit tests, integration tests and end-to-end tests



## Introduction

Every mature software product has software tests to verify intended functionality. Without software tests, every time we write a new feature we might not know whether we broke an existing one. This lack of clarity can cause stress, especially when existing features are crucial to user experiences. Engineers working on early-stage products often omit writing tests because their product requirements change often, but once product requirements start to stabilise and mature, testing is necessary to maintain engineer sanity.

Software tests are code written using 1 or more test frameworks that programatically verify that functions, groups of functions, or entire features produce expected output when provided with specific input. Engineers typically merge these tests to repos at the same time they merge the tested feature, guaranteeing tests for every feature in the product. Some engineers prefer to write tests before writing the feature (aka test-driven development), and others prefer to write tests after or while writing the feature (more common).

There are 3 most common categories of software tests: unit tests, integration tests and end-to-end tests. Unit tests typically test individual functions, especially ones with non-trivial logic such as calculations. Integration tests typically test groups of functions, for example a function that triggers functionality in multiple helper functions. End-to-end tests typically test entire features by using frameworks to simulate user actions, and verifying that those actions cause the desired database and UI changes in the app. Unit tests are the simplest and most common form of testing, and engineers often omit end-to-end testing until their product matures.

There is no such thing as perfect testing, but hopefully with mindful testing we can eliminate bugs that would otherwise have happened unnoticed without tests.

## Unit Testing in JavaScript

### Introduction

For illustration purposes we will demonstrate unit testing in JavaScript. For Bootcamp projects and take-home interview assignments, it should be sufficient to write unit tests on our functions like this one.

<a href="https://mochajs.org/" target="_blank">Mocha</a> and <a href="https://www.chaijs.com/" target="_blank">Chai</a> are common test frameworks used together to test JavaScript backends. Mocha is the framework that enables us to run tests. It provides functions in which we can write tests, and a test runner script we can use to run all of a subset of our tests. Chai is an "assertion framework" that allows us to verify values in our code match what we expect, values such as the return value of the function we are testing. Jest is a more common test framework used for frontends that has the same functionality as Mocha and Chai combined.

### Setup

Fork and clone Rocket's <a href="https://github.com/rocketacademy/unit-test-bootcamp" target="_blank">`unit-test-bootcamp` repo</a> to follow along. We have implemented a simple unit test example using Rocket's Express app template.

Before we wrote tests, we created a module to test. In this case, we have created a basic `utils` module in `utils.js` that exports an `add` function that adds 2 numbers. Trivial, but you can imagine more complex functions such as those we implemented for games like Blackjack.


```javascript
const add = (a, b) => {
  return a + b;
};

module.exports = {
  add,
};
```


Next we set up our test framework.

1.  We installed Mocha and Chai libraries as development dependencies. Development dependencies are only used during development and do not need to be included in the final app package shipped to users, helping make the app package smaller.

    ```
    npm i --save-dev mocha chai
    ```


2.  We added a script in `package.json` that allows us to run tests by running `npm test`.&#x20;

    ```
    "test": "mocha"
    ```


3.  We added the Mocha env setting to `.eslintrc.js` for ESLint to support Mocha syntax.

    ```
    mocha: true,
    ```


4.  We created a folder `test` in the root of the repo to store our test files. By default Mocha looks for a folder called `test` to find tests.

    ```
    mkdir test
    ```

At this point we created our test file and wrote our tests in it. We will dissect the test code below.


```javascript
const { expect } = require("chai");
const { add } = require("../utils.js");

describe("Utils", () => {
  describe("Add", () => {
    it("Adds 2 of the same number", () => {
      const result = add(1, 1);
      expect(result).to.equal(2);
    });

    it("Adds 2 different numbers", () => {
      const result = add(1, 2);
      expect(result).to.equal(3);
    });

    it("Adds a positive and a negative number", () => {
      const result = add(1, -1);
      expect(result).to.equal(0);
    });

    it("Adds 2 negative numbers", () => {
      const result = add(-1, -1);
      expect(result).to.equal(-2);
    });
  });
});
```


Now if we run `npm test` from our repo in the command line we should get the following output.

```
unit-test-bootcamp % npm test

> unit-test-bootcamp@1.0.0 test
> mocha

  Utils
    Add
      ✔ Adds 2 of the same number
      ✔ Adds 2 different numbers
      ✔ Adds a positive and a negative number
      ✔ Adds 2 negative numbers

  4 passing (4ms)

unit-test-bootcamp % 
```

### Syntax

#### `expect`

At the top of our test file `test/utils.js` we imported the `expect` module from Chai. `expect` is an "assertion" syntax that helps us "assert" that our code meets expectations.

Observe in each of the `it` blocks (we explain `it` below) how we use `expect` to verify expected values using a pseudo-English syntax.

<a href="https://www.chaijs.com/api/bdd/" target="_blank">Chai's API reference</a> provides a list of assertions we can perform with `expect`.

#### `describe`

`describe` is a syntax for grouping and categorising tests. Notice each `describe` block accepts a string followed by a function, where the string is the description of the group of tests contained within the function.&#x20;

We can nest `describe` blocks within each other to group different types of tests. For example, each function that we test can be in its own nested `describe` block. In our case, our `add` function has its own nested `describe` block, and we could add another nested `describe` block for `subtract` function tests if we ever added a `subtract` function to `utils`.

Notice Mocha logs the description for each `describe` block in the console when running tests.

#### `it`

`it` declares an individual test. Like `describe`, `it` accepts a string followed by a function, where the string is the test description and the function is the test logic. Mocha engineers chose `it` as the function name so that test descriptions could read more like plain English, e.g. `it("Adds 2 of the same number", () => { ... });`

If you put an x infront of any it or describe your test will be skipped.

## Exercises

1. Run the tests in Rocket's repo and review output
2. Break a test on purpose to see what a failing test looks like, e.g. by changing the expected result
3. Add a `multiply` function to `utils` and write tests for it



### React and ExpressJS testing

If you would like to explore testing in your React frontend or ExpressJs backend please read sections [4.1.1](4.1.1-frontend-react-testing.md) and [4.1.2](4.1.2-backend-expressjs-testing.md).&#x20;

