# Promises

## Learning Objectives

1. Understand what Promises are and what purpose they serve
2. Use Promises as a replacement for callback functions
3. Use the `.catch` statement to run specified logic when our programs encounter errors in promises
4. Use the `Promise.all` statement to wait on multiple promises concurrently instead of sequentially

## Introduction

JavaScript Promises allow us to program logic to run after asynchronous function calls return, for example if we wanted to highlight a like button after we have saved the "like" in our database. The same logic would be possible with callback functions, but promises allow us to achieve the same functionality with at most 1 level of nesting.

The following examples use a common HTTP-request-making library called <a href="https://axios-http.com" target="_blank">Axios</a>. Axios is a promise-based HTTP library that allows us to make arbitrary HTTP requests in code. "Promise-based" means Axios functions return promises, allowing us to run certain logic only when the promises "resolve", i.e. when the requests are completed.

## `.then`

The function `axios.get` sends a GET request and returns a promise, on which we then call the promise's `.then` method to perform certain logic only when the GET request is complete, i.e. when we receive a response. 3rd-party asynchronous functions such as `axios.get` often return promises for this purpose, and when unsure we can check their <a href="https://axios-http.com/docs/api_intro" target="_blank">online documentation</a>.

The following code sends a request, then `console.log`s the response when the response is received.

```javascript
import axios from "axios";

// Make a request
axios.get("http://dog.ceo/api/breeds/image/random").then((response) => {
  // Handle request success
  console.log(response);
});
```

The previous code can be rewritten as follows for a clearer breakdown of how `.then` works.

```javascript
import axios from "axios";

// Perform logic after the request is complete.
const handleResponse = (response) => {
  // Handle request success
  console.log(response);
};

// Make a request and store return value (promise) in getRequestPromise
const getRequestPromise = axios.get("http://dog.ceo/api/breeds/image/random");

// Tell the program to call handleResponse when getRequestPromise resolves.
getRequestPromise.then(handleResponse);
```

Note that `handleResponse` receives a `response` parameter. Because the above promise is for an Axios request, the callback function receives an <a href="https://axios-http.com/docs/res_schema" target="_blank">Axios response object</a> as a parameter.

## Sequential Promises

Sometimes we may wish to perform multiple network calls sequentially. For example, when a user requests to change their password, we may wish to:

1. Send a request to change their password
2. When that request is complete, send an email through an email API
3. Render a success message after the email is sent

```javascript
axios
  .post(`https://myapp.com/change-password`, { password: "rocket123" })
  .then((response) => axios.get(`https://myapp.com/send-email`))
  // Render password change success
  .then((response) => console.log("success!"));
```

`.then` always returns a promise, regardless of whether the callback function passed to `.then` returns nothing, a promise, or anything else. Hence we can always call `.then` on the return value of any `.then` call. See <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/then" target="_blank">`.then` docs</a> for a more detailed description of this behaviour.

## `.catch`

`.catch` allows us to run specified logic when our programs encounter errors in promises. For example, if our above request to change password encountered an error such as invalid password or user had no account, we could program logic to return a graceful error message in the `.catch` block. Without `.catch`, our programs would crash on errors in promises.

`.catch` catches errors for all promises in the promises sequence before it. Notice there is only 1 `.catch` for the string of promises below.

```javascript
axios
  .post(`https://myapp.com/change-password`, { password: "rocket123" })
  .then((response) => axios.get(`https://myapp.com/send-email`))
  // Render password change success
  .then((response) => console.log("success!"))
  .catch((error) => {
    console.error(error);
    // Return the user a graceful error message
  });
```

## `Promise.all`

`Promise.all` allows us to wait on multiple promises concurrently instead of sequentially. For example, if I wanted to retrieve independent data to render on a page such product data and user data, I could use `Promise.all` to wait for multiple database queries to all return before proceeding. Without `Promise.all` we would need to wait for each of these queries sequentially using `.then`.

```javascript
Promise.all([
  axios.get('https://myapp.com/products/1'),
  axios.get('https://myapp.com/users/1'),
  // results is an array of results whose elements correspond
  // to the elements in the Promise.all parameter array
]).then((results) => {
  const [product1, user1] = results;
  // Do something with product1 and user1
});
```

## Additional Resources

1. <a href="https://javascript.info/promise-basics" target="_blank">Intuitive and deeper explanation of JavaScript Promises</a>
