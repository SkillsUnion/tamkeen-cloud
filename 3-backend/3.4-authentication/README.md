# 3.4: Authentication

## Learning Objectives

1. Understand the flow of typical authentication processes and how they use JWTs and cookies
2. Understand how to implement secure authentication with Auth0

## Introduction

Authentication is both simple and complex. The high-level concept of authenticating a user, then saving that user's authentic "badge" in their browser for subsequent requests is simple. But the lower-level concepts of how to authenticate and how to save that badge in the browser can be complex.

At Rocket Academy we will focus on the higher-level concepts of authentication, and let students dig deeper into the lower-level concepts themselves if time permits and students are interested. We will use <a href="https://auth0.com/" target="_blank">Auth0</a> to implement authentication in our API servers, the industry standard for plug-and-play authentication libraries, comparable to Firebase Auth but with friendlier docs.

{% include youtube.html id="cBLCVjyuUsY" %}
What is auth0?


{% include youtube.html id="KhlqoxD3YBM" %}
auth0 Online


{% include youtube.html id="6btuQC4dSsE" %}
auth0 Documentation


## Basic Authentication Flow

At a fundamental level, all authentication involves 3 steps.

1. User enters auth info such as username and password
2. Backend verifies auth info via cryptographic algorithm, typically involving <a href="https://en.wikipedia.org/wiki/Cryptographic_hash_function" target="_blank">hashing</a> and <a href="https://en.wikipedia.org/wiki/Salt_(cryptography)" target="_blank">salting</a>). Verification involves comparing the hashed version of the provided password with the hashed password stored in the database. We never store plain-text passwords for security reasons.
3. If auth info verified, backend sends user's browser a <a href="https://en.wikipedia.org/wiki/HTTP_cookie" target="_blank">cookie</a> that contains proof of authentication, typically either a <a href="https://en.wikipedia.org/wiki/JSON_Web_Token" target="_blank">JSON web token</a> (JWT) or a <a href="https://en.wikipedia.org/wiki/Session_ID" target="_blank">session ID</a> that cannot be forged. Browsers store cookies and send them to relevant websites, thereby proving authentication.

Authentication can be challenging because it involves many moving parts. Our server application must store auth info such as passwords and secret keys securely. Our cryptographic algorithm and proof of authentication must be industry-standard. Any bugs in logic or implementation can result in costly hacks.

This is why Rocket recommends we use a plug-and-play, industry-standard auth solution such as Auth0, and only write our own lower-level authentication logic when there is a strong business need and we have experts to test the robustness of our implementation.

## Implementing Authentication with Auth0

Luckily for us, companies such as Auth0 and Firebase have developed plug-and-play auth solutions that are both secure and easy to use. We will use Auth0 for backend authentication because Auth0 has clearer documentation for this use case.

### Setup Auth0 account and initial app

1. Create Auth0 account if we haven't already
   1. Yes, we will be the one coding
   2. No, we do not need advanced settings
2. Create Application
   1. Choose Single Page Web Application
   2. Choose React



### Review how to authenticate in React app

We should then be directed to a quickstart page like the following, populated with our app's specific domains and IDs. No need to implement anything for now, but read through to understand the high-level process.

<a href="https://auth0.com/docs/quickstart/spa/react/01-login" target="_blank">Official Auth0 setup guide for React apps</a>


1. Note application domain and client ID in Application Settings in the Auth0 dashboard. We will need to include these in our app to communicate with Auth0.
2. Configure callback and logout URLs to allow redirects back to our apps after logging in or out with Auth0
3. Configure allowed web origins to allow auth tokens (JWTs that serve as proof of authentication) to automatically refresh periodically after users have logged in to prevent auto-logout when auth tokens expire
4. Surround `App` component with `Auth0Provider` component to enable Auth0 in our apps. Note `Auth0Provider` uses React context underneath.
5. Add login to app with `loginWithRedirect` function from `useAuth0` React hook. Login is as simple as calling the function, letting users login in Auth0's interface, then redirecting back to our app.
6. Ditto with the `logout` function also from the `useAuth0` React hook. `returnTo: window.location.origin` tells Auth0 to redirect to the root URL of the current browser window after logging out.
7. Retrieve logged-in user profile information through the `user` property of the `useAuth0` hook. `user` contains properties such as `picture`, `name` and `email`.

That's all there is to logging in and out with Auth0 in our frontend! Let's now learn how to send that auth info to our backends for our users to access our backends securely.

### Review how to pass authentication info to API from React app

Now that we've enabled login in our React apps, we need to learn how to pass an access token from Auth0 to our backends to verify authentication.

<a href="https://auth0.com/docs/quickstart/spa/react/02-calling-an-api" target="_blank">Official Auth0 API-calling guide for React apps</a>


1. Our frontends authenticate with our backends via an access token that we retrieve from Auth0 on our frontends, send to our backends in a request, and verify using an Auth0 library on our backends.
2. To retrieve this access token on our frontends, we need to pass additional `audience` and `scope` props to the `Auth0Provider` component.
   1. `audience` is an identifier for our API server that we set in Auth0. This is typically the URL of our API server.
   2. `scope` is a property we define in Auth0 that allows us to only allow access to specific backend routes from specific frontend apps. In our case we will keep scope simple and allow access to all protected routes from our frontend.
3. Retrieve access token with `getAccessTokenSilently` method from `useAuth0` React hook
4. Use `getAccessTokenSilently` to retrieve access token just before we send an API request via Axios. In Auth0's example they use Fetch to send requests, but the concept is the same.
   1. Pass `audience` and `scope` again to `getAccessTokenSilently` to get a token for the correct domain and scope
   2. We need to include the access token in an "Authorization" request header with the format shown in this guide. Our API server will need the header in this format to process the access token.

Voila! We are now ready to set up authorisation in our backends for protected routes!



#### (Legacy React CRA)&#x20;

{% include youtube.html id="CQpz8rHwONk" %}
auth0 Frontend Setup


{% include youtube.html id="AwM2cA5kZpQ" %}
Access Token & Post Request


### <mark style="color:red;">Auth0 Update:</mark>

When defining the Auth0Provider, there has been a slight alteration!\
Please pass in the property authorizationParams to include the redirectUri, audience and scope. Similar to the code below:

```javascript
<Auth0Provider
    domain='<Your-auth-domain>'
    clientId='<Your-client-id>'
    authorizationParams = {{ 
      redirectUri: window.location.origin,
      audience: "<Your-app-API->",
      scope: "read:current_user update:current_user_metadata openid profile email",
    }} 
>
// Make sure you alter the credentials passed above 
```

### Authorise access to protected routes in Express backend

We will implement authentication in our backend first because there are certain credentials to set up for our API server that we will need to use in our frontends later.

Some routes in our backend will be protected, for example routes to access user data or manipulate data. Based on the logged-in user, backends can decide what data to expose to that user and record changes by that user.

<a href="https://auth0.com/docs/quickstart/backend/nodejs/01-authorization" target="_blank">Official Auth0 route-authorisation guide for Express apps</a>

1. Create an API in the Auth0 dashboard and give it an identifier, typically a URL that identifies our API. We will use this API identifier as an `audience` in our frontends when retrieving an access token to communicate with our backends
2. There is no need to understand RS256 and what a private/public keypair is at the moment, other than knowing they are industry-standard security mechanisms.
3. We can ignore scope for now because our apps will be simple and all users should be able to access all features
4. Install Auth0's `express-oauth2-jwt-bearer` middleware to verify authentication on our routes
5. Initialise the middleware in the root `index.js` file of our Express app with our API's identifier as `audience` and the `issuerBaseURL` provided by Auth0 (login to Auth0 while viewing this guide to see it)
6. Insert `checkJwt` middleware in routes that require authentication, and add `checkScopes` middleware in routes that also require specific scopes.

Great job! We now have authentication and secure access to our APIs!

{% include youtube.html id="s1d298jM61k" %}
auth0 Backend Implementation & Testing

### Roundup

Hopefully this gave us a clear high-level overview of what steps we need to implement Auth0 authentication in our frontends, how to send auth info in requests and protect our backends using Auth0 authorisation. We will get more hands-on practice with Auth0 in the upcoming hands-on auth exercise.

Please checkout the finished frontend code below. Note that you will need to setup a application on Auth0 that you integrate with the application.&#x20;

Frontend code is in this <a href="https://github.com/rocketacademy/3.2_react_repo/tree/auth" target="_blank">repository</a>, ensure that you're on the `auth` branch if you want to test the code on your machine you will need to install the dependencies with the command `npm install` after the installation you can run the application with `npm run dev`. To view the rendered page open a browser and navigate to http://localhost:5173 Note, you will need to create your own .env and create your own Auth0 application online with the appropriate setup. To test it with a backend please checkout this <a href="https://github.com/rocketacademy/m3_sequelize_repo/tree/auth" target="_blank">repository</a>, ensure that you're on the `auth` branch if you want to test the code on your machine you will need to install the dependencies with the command `npm install` after the installation, then implement you `.env` . If you've not setup the database previously, run your migrations and seeders and once this is completed you can run the application with `node index.js`.&#x20;
