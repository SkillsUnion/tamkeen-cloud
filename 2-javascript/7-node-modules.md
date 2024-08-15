# Node Modules

## Learning Objectives

1. Understand how Node Modules define code that can be grouped together and imported from other files
2. How to import and export functions from Node Modules
3. Learn how access imported variables and variables defined in the current module
4. Understand the difference between named and default exports

## Introduction

Node Modules (aka ES Modules) define code that can be grouped together and imported from other files. This helps clarify business logic by abstracting implementation details into separate files.

Setting up the environment:

1. Create a new directory named `npm_modules`
2. Change directory to `npm_modules`
3. Run the command `npm init -y` to initialise an npm directory&#x20;
4. You should see a new file has been generated, the package.json
5.  To run the scripts you will need to alter this file as below:



```
{
  "name": "npm_modules",
  "version": "1.0.0",
  "description": "modules",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "",
  "license": "ISC",
  "dependencies": {
  }
}
```

Alter this file by adding in a new key and value pair.

```
{
  "type": "module",
  "name": "npm_modules",
  "version": "1.0.0",
  "description": "modules",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "",
  "license": "ISC",
  "dependencies": {
  }
}
```

Now you can run your scrips with node \<scrip-name>

`operations.js` is a Node Module that exports 2 functions: `add` and `subtract`.

```javascript
export const add = (a, b) => {
  return a + b;
};

export const subtract = (a, b) => {
  return a - b;
};
```

`index.js` imports `add` and `subtract` functions from the `operations` module and uses them.

```javascript
import { add, subtract } from "./operations.js";

console.log(add(2, 2));
console.log(subtract(2, 2));
```

`conversion.js` is a Node Module that exports functions to convert metric to US units of measurement.

```javascript
export const kmToMiles = (numKm) => {
  // Convert KM to miles and return value in miles
};

export const celciusToFahrenheit = (tempInCelsius) => {
  // Convert Celsius to Fahrenheit and return value in Fahrenheit
};

export const kgToPounds = (numKg) => {
  // Convert KG to pounds and return value in pounds
};
```

`index.js` imports functions from `conversion` module and uses them without having to worry about implementation details.

```javascript
import {
  kmToMiles,
  celciusToFahrenheit,
  kgToPounds,
} from "./conversion.js";

console.log(kmToMiles(3));
console.log(celciusToFahrenheit(3));
console.log(kgToPounds(3));
```

## Module Scope

Node Modules can only access variables explicitly imported or defined in their file. For example, the variable `PI` in the following `circleUtils` module is not accessible in `index.js` because `PI` is not explicitly imported or defined in `index.js`.


```javascript
const PI = 3.14;

export const getCircleArea = (r) => {
  return PI * (r * r);
};

export const getCirclePerimeter = (r) => {
  return 2 * PI * r;
};
```



```javascript
import { getCircleArea } from "./circleUtils.js";

// PI is used "inside" this function
console.log(getCircleArea(2));
// But PI is not accessible as a variable unless explicitly exported and imported
console.log(PI); // Error
```


## Named vs Default Exports

There are 2 ways of exporting variables from Node Modules: named and default.

### Named Exports

Named exports allow us to export 0 or more named variables from modules. This is helpful when we want to export more than 1 function from a module.

In the `circleUtils` module, we export `getCircleArea` and `getCirclePerimeter` but not `PI`.


```javascript
const PI = 3.14;

export const getCircleArea = (r) => {
  return PI * (r * r);
};

export const getCirclePerimeter = (r) => {
  return 2 * PI * r;
};
```


In `index.js` we can choose which named exports to import. In this case we only import `getCircleArea`, but we could also import `getCirclePerimeter` if we wanted.


```javascript
import { getCircleArea } from "./circleUtils.js";

console.log(getCircleArea(2));
```


### Default Exports

Use default exports when the module only does 1 operation, and all functions in that module exist to support that operation. In general we prefer named exports for clarity of what is exported and imported. Each module can only have 1 default export.

In the `calcHandScore` module, the only function that needs access externally is `calcHandScore`, which we export as a default export.


```javascript
const checkFullHouse = (hand) => {
  // Verify if card hand has a full house
};

const checkStraight = (hand) => {
  // Verify if card hand has a straight
};

const calcHandScore = (hand) => {
  let handScore = 0;
  if (checkFullHouse(hand)) {
    // Update handScore for full house
  } else if (checkStraight(hand)) {
    // Update hand score for straight
  }
  return handScore;
};

export default calcHandScore;
```


`index.js` imports the `calcHandScore` function, allowing it to calculate the score of a card hand without having to worry about the implementation details of how to calculate it.

Note we do not use curly braces `{}` when importing default exports.


```javascript
// No curly braces around imported default export
import calcHandScore from "./calcHandScore.js";

const hand = ["A", "A", "A", "K", "K"];
const handScore = calcHandScore(hand);
console.log(handScore);
```


## Additional Resources

1. <a href="https://youtu.be/qgRUr-YUk1Q" target="_blank">Summary of Node Module usage in 100 seconds</a>
