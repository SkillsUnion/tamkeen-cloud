# Node.js

## Learning Objectives

1. Know what Node.js is and what it functionality it provides
2. Run the runtime environment using the `node` command

## Introduction

Node.js (Node for short) is a JavaScript "runtime" that runs JS on our computers (as opposed to a user's browser). Node is popular because it enables SWEs to build both frontends and backends in JS, which has simplified feature development, attracted more developers to JS, and resulted in a large number of JS libraries available for both frontend and backend.

During Coding Bootcamp we will use Node for both frontend and backend applications. We will use it with Create React App on the frontend to generate static HTML, CSS and JS files for browsers through React, and we will use it with Express.js on the backend to create API servers that serve data for our apps.

## Warmup: Node console in command line

To warm up with Node, run the following command on the command line.

```bash
node
```

This should open a JS console on the command line similar to the Chrome DevTools console. We can test JS syntax in this console similar to how we might in Chrome.

```
% node
Welcome to Node.js v16.14.2.
Type ".help" for more information.
> a = [1,2,3]
[ 1, 2, 3 ]
> b = [4,5,6]
[ 4, 5, 6 ]
> a+b
'1,2,34,5,6'
> a.concat(b)
[ 1, 2, 3, 4, 5, 6 ]
```

Type `Ctrl+D` to exit, which sends an "end of file" signal to Node to close the program.

## Run JS files with Node

Node is primarily used to run JS files. Try running the following `index.js` file with Node.


```javascript
console.log("hello world");
```


```bash
node index.js
```

Over Bootcamp we will build increasingly complex programs executed with Node.

## Additional Resources

1. Introduction to runtime environments: <a href="https://www.codecademy.com/articles/introduction-to-javascript-runtime-environments" target="_blank">https://www.codecademy.com/articles/introduction-to-javascript-runtime-environments</a>
