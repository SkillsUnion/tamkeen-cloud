# 1.3: React

Learning Objectives

1. React is a frontend framework and library that allows us to create custom, nest-able UI elements with a combination of HTML and JavaScript syntax (JSX)
2. How to write JSX
3. How to write and render Functional based React components
4. How to use props
5. How to use state
6. What are component lifecycles and lifecycle methods
7. How to handle JS events in React
8. How to design component architecture

## Introduction

<a href="https://legacy.reactjs.org/" target="_blank">React</a> is a frontend framework and library that allows us to create custom, nest-able UI elements with a combination of HTML and JavaScript syntax (JSX). React's HTML-like structure makes it easy to visualise, and its integrated JS makes it easy to render dynamic data. Alternative but less popular frontend libraries include <a href="https://vuejs.org" target="_blank">Vue</a> and <a href="https://angularjs.org" target="_blank">Angular</a>.

We will use React's official <a href="https://react.dev/learn" target="_blank">guide</a> and <a href="https://react.dev/learn/tutorial-tic-tac-toe" target="_blank">tutorial</a> to learn React, and the <a href="https://vitejs.dev/guide/" target="_blank">Vitejs</a> environment to scaffold our first React apps. Vite is a build tool that provides a fast and lean development experience for modern web projects. Vite leverages new advancements in the JavaScript ecosystems, the ability of native ES modules within the browser and the rise of JavaScript tools written in compile-to-native languages. This is because browsers do not read React natively; they read HTML, CSS and JS, not JSX.&#x20;

The following sections provide Rocket's annotations to React's official <a href="https://react.dev/learn" target="_blank">guide</a> and <a href="https://react.dev/learn/tutorial-tic-tac-toe" target="_blank">tutorial</a> to explain concepts that the React team assumes readers know.



## Day 5

### 1: <a href="https://react.dev/reference/react-dom/client/createRoot#usage" target="_blank">Hello World</a>

In this section you should begin to understand that React applications are bound to a single root, this code is generated when we start a new React application using <a href="https://vitejs.dev/guide/" target="_blank">Vitejs</a>. Give this a shot yourself and generate a new React application with <a href="https://vitejs.dev/guide/" target="_blank">Vitejs</a>, you should be able to see a similar file structure to the official documentation above.&#x20;

To create a new React application using Vite, open up your CLI tool and run this command in the directory where you want to create your application:

`npm create vite@latest`

You will be prompted to input a name.

Then you will be asked what type of application you want to create, use your arrow keys to navigate to 'React' and press 'enter'.

Then using arrow keys once more navigate down to 'JavaScript', if you don't need standard build tools later in development you can choose 'JavaScript + SWC' and click enter.&#x20;

Now you can follow the instructions within the CLI to first navigate into the newly created directory, then install the required dependancies and finally run the React application using the command `npm run dev`, to view the application you should open the URL that is shown in your CLI, it should be something like <a href="http://localhost:5173/" target="_blank">**http://localhost:5173**</a>, the output on the page should be similar to the image below. &#x20;

<figure><img src="../../.gitbook/assets/Screenshot 2023-10-18 at 2.49.25 PM.png" alt=""><figcaption><p>Vite and React</p></figcaption></figure>

There are some key files that you should be aware of within this starter code. Note that the index.html is in the root of the project directory, it is in the entry point to your application and is required for the React App. Please explore the files within the starter code and consider the points below,

1. Within the src/main.jsx file `document.getElementById('root')` is a DOM (Document Object Model) command that retrieves the HTML element with ID "root". React renders our app inside that element. React removes the need to write DOM code and the above command is the only DOM command we will need.
2. <mark style="color:red;">**Note**</mark> that if you want to add and use images within your Vite React applications please add the images into the `public` directory and import as usual.&#x20;
3. Rocket recommends that you familiarise yourself with as many of the provided examples as you can to understand and digest the relevant concepts
4. Rocket recommends completing most of the "Learn React" guide before attempting the "Tutorial: Tic Tac Toe" so the tutorial's concepts sink in better
5. If there is anything you do not understand in the guide, please let your SL know and we can include it in these notes!

### 2: <a href="https://react.dev/learn/writing-markup-with-jsx" target="_blank">Introducing JSX</a>

JSX or JavaScript and XML affords developers the opportunity to write HTML-like markup within a JavaScript or JSX file. Without using JSX developers would be forced to utilise React <a href="https://react.dev/reference/react/createElement" target="_blank">createElement</a>, this is less readable and intuitive than JSX. By employing JSX we can combine rendering logic alongside markup within what developers name components. While JSX looks like HTML it is stricter and can display dynamic information. It should be noted that JSX has its own rules that should be followed.&#x20;

1. JSX elements may only return a single root element, to display multiple elements just wrap them within a single parent tag.&#x20;
2. Close all HTML tags.
3. DOM stands for "Document Object Model", which is a JavaScript representation of HTML rendered on a web page. Frontend frameworks like React use the DOM to programmatically manipulate UI without manually specifying HTML. Rocket recommends <a href="https://www.w3schools.com/js/js_htmldom.asp" target="_blank">W3School's intro to JavaScript HTML DOM</a> (just the 1st page) for a primer. For Rocket's Bootcamp we can stop at DOM Intro without reading W3School's subsequent pages on DOM.
4. Use camelCase for most if its props,<a href="https://react.dev/learn/writing-markup-with-jsx#3-camelcase-salls-most-of-the-things" target="_blank"> click here for more details</a>. To apply CSS classes to JSX elements we will need to use the `className` keyword instead of `class`, which we used with vanilla HTML. This is because `class` is a reserved keyword in JS used to declare classes (which we will see in 4: Components and Props below).

### 3: <a href="https://react.dev/learn/javascript-in-jsx-with-curly-braces" target="_blank">JavaScript in JSX</a>

Within JSX, "{ }" or "curly braces" allow developers to write and execute JavaScript bound to the HTML-like code. This makes JSX more dynamic than HTML and allows for data binding basically straight out of the box.&#x20;

1. When you want to add JavaScript logic or code into JSX you are able to do so by using curly braces within the JSX. Think of these using these braces { } like a window into the world of JavaScript.&#x20;
2. You can pass string attributes to JSX, do this using single or double quotations.
3. You can only use curly braces as text directly within a JSX tag **OR** as attributes immediately following the `=` sign.
4. You should use double curly braces in some instances when writing JSX. Such as using inline CSS or passing a js object into a JSX element. &#x20;

React follows what we call a "declarative" UI paradigm, where we tell our computers how the UI should look, but not how to achieve that look. The declarative paradigm is a layer on top of the "imperative" paradigm of DOM manipulation more commonly used before React.

## Post-Class Exercises: Codecademy React 101&#x20;

Complete all exercises in the following Codecademy lessons when they are assigned in the Rocket course schedule.

1. JSX
   1. <a href="https://www.codecademy.com/courses/react-101/lessons/react-jsx-intro/exercises/why-react" target="_blank">Intro to JSX</a>
   2. <a href="https://www.codecademy.com/courses/react-101/lessons/react-jsx-advanced/exercises/jsx-classname-class" target="_blank">Advanced JSX</a>



## Day 6

### 4: <a href="https://react.dev/learn/your-first-component" target="_blank">React Components</a>

The concept of Components is core to React, they are the foundation of our React code, we use components to build user interfaces. This makes them ideal starting points once you've understood the basics of React JSX. React allows developers to combine markup, CSS and JavaScript into components that could be reusable UI elements within your application. Similarly to HTML tags we can compose, order and nest components to develop full pages within React applications. When building a Component follow these rules:

1. Export the Component&#x20;
2. Define the Component function
3. Add any markup required, this is what we want to display within the Component
4. Render the Component onto the React Application by nesting it into the App.jsx
5. <a href="https://reactjs.org/docs/jsx-in-depth.html#user-defined-components-must-be-capitalized" target="_blank">User-defined components must be capitalised</a>. Otherwise React will think they are HTML tags.

### 5: <a href="https://react.dev/learn/passing-props-to-a-component" target="_blank">Component Props</a>

React components can communicate with each other via props, a parent may pass information down to child component and this data always flows downwards. There will be some familiar props associated to JSX tags, but you you can actually pass anything from a parent its children.

1. To pass props specify the information that should be passed from the parent to the child.
2. Access the prop information that was passed to the child component and set default values if required.
3. You can pass anything as a prop from a parent component to a child, you can access props by destructuring the individually passed sets of information or by referring to props.
4. Props are immutable, checkout <a href="https://react.dev/learn/passing-props-to-a-component#how-props-change-over-time" target="_blank">this example</a> to see how they can change over time.

## Introduction to React Hooks

React Hooks are a newer and more efficient syntax for React Components. They allow us to write all components as functional components, and use so-called "Hook" functions to replace class component functionality such as state management and lifecycle methods. Components with hooks are functionally the same as class components.

Rocket recommends using Hooks in our exercises and projects from now on because Hooks are a cleaner syntax and the <a href="https://reactjs.org/docs/hooks-faq.html#should-i-use-hooks-classes-or-a-mix-of-both" target="_blank">React team recommends using Hooks for new projects</a>. The React team is <a href="https://beta.reactjs.org/" target="_blank">re-writing the official React tutorials to use Hooks</a>. React Router v6 (the latest and greatest version of React Router) that we are about to learn only supports React Hooks syntax natively, and Rocket recommends using Hooks to enable us to use the latest React Router features.

## Introducing Hooks

<a href="https://reactjs.org/docs/hooks-intro.html" target="_blank">Hooks Intro</a>

1. Many companies will still be using <a href="https://legacy.reactjs.org/docs/react-component.html" target="_blank">Class based React Components</a> in their code. It will be important for us to still understand class Components, but know how to write Components with Hooks for new code to take advantage of latest React functionality. If you want to explore how to use state and lifecycles in React Class based Components you can read <a href="https://legacy.reactjs.org/docs/state-and-lifecycle.html" target="_blank">this documentation</a>.&#x20;

## Hooks at a Glance

This page is an overview of all of the subsequent tutorial pages. The subsequent pages go into more depth on each topic.

<a href="https://reactjs.org/docs/hooks-overview.html"" target="_blank">Hooks Overview</a>

1. React Hooks provide all the functionality we need from React Class based Components that we didn't previously have with Functional Components of the past.
2. `useState` hook replaces `this.state` and `this.setState` with a new pair of variables for getting and setting a specific state value.
3. Note how the React team <a href="https://reactjs.org/docs/hooks-faq.html#should-i-use-one-or-many-state-variables" target="_blank">encourages us to use multiple `useState` Hooks</a> in the same component for each type of state. There is no need to store all of a component's state in a single `this.state` object like we did previously.
4. Returning a cleanup function from `useEffect` is advanced functionality and we will not be using it as often at Rocket
5. We will not be writing custom Hooks at Rocket; feel free to skim through the "Building Your Own Hooks" section
6. We will learn about `useContext` and `useReducer` hooks in a later submodule.

## Using the State Hook

We will use the `useState` Hook most often. Clear explanations of what the `useState` Hook is and how to use it.

<a href="https://reactjs.org/docs/hooks-state.html"" target="_blank">Hooks State</a>

1. Rocket strongly recommends following the naming convention of `X` and `setX` as the de-structured state variable names from `useState`. This makes our code more readable because other engineers will immediately know what each variable is for.

### Sample useState Hook

{% include youtube.html id="eb6HKsxHoas" %}
React Hooks useState

### 6: <a href="https://react.dev/learn/managing-state" target="_blank">React State management, useState</a>

While creating your application and enlarging functionalities you will find that you are developing your components and states into much larger and complex files than you had before. IT is important to manage state effectively and reduce redundant or duplicated states within your application.&#x20;

1. When using useState to manage component state Rocket advises following these steps
   1. Import the useState hook from the react package, at the top of the component file
   2. Within your functional component declare a state variable and the updater function using the useState hook. As shown on <a href="https://react.dev/learn/managing-state#reacting-to-input-with-state" target="_blank">line 4</a>.&#x20;
   3. The initialValue of the state is passed into useState.
   4. You can update this variable using the updater function.
2. We will take a longer look onto useContext and useReducer later in this course.
3. When developing your state, group information if two state variables always change together, therefore unify them into a single state variable. Here are some more rules regarding <a href="https://react.dev/learn/choosing-the-state-structure" target="_blank">state structure</a>.
4. When updating a state variable its possible to use its current value, this is done by invoking a callback function on the updater function. Take a look at <a href="https://react.dev/reference/react/useState#updating-state-based-on-the-previous-state" target="_blank">these examples here</a>.

## Using the useEffect Hook

At Rocket we will use `useEffect` instead of the lifeCycleMethod `componentDidMount` for setting up subscriptions such as Firebase listeners and for data fetching. `useEffect` also allows us to perform functionality that was previously provided by `componentDidUpdate` and `componentWillUnmount`, but we will use that functionality less often.

<a href="https://reactjs.org/docs/hooks-effect.html"" target="_blank">Hooks Effect</a>

1. As the docs mention, we can think of `useEffect` as running after the component renders.
2. A memory leak is when data that we use in parts of our apps is not properly cleaned up after the app stops using those parts. This can cause our apps to run slowly and even crash if the "leaks" cause our computers to run out of memory while running our apps. This will rarely happen to use in practice because JavaScript has automatic memory management and our apps will not be the most complex for now.
3. Returning a cleanup function from `useEffect` is optional and we will not use it often at Rocket.
4. No need to worry too much about "Optimizing Performance by Skipping Effects"; we will rarely need this and we can come back to it once we're more familiar with using `useEffect` and Hooks in general.

## Rules of Hooks

Rocket uses Create React App for our projects that includes the ESLint plugin for Hooks, so ESLint should enforce these rules for us by default.

<a href="https://reactjs.org/docs/hooks-rules.html"" target="_blank">Hooks Rules</a>

### Sample useEffect Hook

{% include youtube.html id="z4eeYjk57aM" %}
React Hooks useEffect

### 7: <a href="https://react.dev/learn/lifecycle-of-reactive-effects" target="_blank">Component LifeCycles</a> & <a href="https://react.dev/learn/synchronizing-with-effects#how-to-write-an-effect" target="_blank">useEffect</a>

While developing React components it is possible to embed executable code within a component that runs on certain conditions. A common and useful pattern developers employ would be to call an API after the Component loads to get some information to display within the application. This can be controlled by the `useEffect` hook that is part of ReactJs.&#x20;

1. Understand a components lifecycle and how they are "mounted", "updated" and "unmounted".
2. In React we use effects to describe how to synchronise  an external system to the current prop and state.&#x20;
3. Understand how useEffect is implemented in components and what are the triggers that will force them to execute code
   1. Import the useEffect hook from the react package, at the top of the component file
   2. Call it at the top level of the component and put in your code, note state updates must be handled using conditional statements
   3. Handle effect with dependencies, inside the dependency array, passed as the second argument to useEffect
   4. Handle any effect clean ups by implemented a cleanup function within the effect.&#x20;
4. <a href="https://react.dev/reference/react/useEffect" target="_blank">React's offical guide and additional reference</a> to the useEffect hook

## Post-Class Exercises: Codecademy React 101

Complete all exercises in the following Codecademy lessons when they are assigned in the Rocket course schedule.

1. React Components
   1. <a href="https://www.codecademy.com/courses/react-101/lessons/your-first-react-component/exercises/hello-world-component" target="_blank">Your First React Component</a>
   2. <a href="https://www.codecademy.com/courses/react-101/lessons/react-components-advanced-jsx/exercises/render-multiline-jsx" target="_blank">Components and Advanced JSX</a>
   3. <a href="https://www.codecademy.com/courses/react-101/lessons/components-render-each-other/exercises/components-interacting-intro" target="_blank">Components Render Other Components</a>
   4. <a href="https://www.codecademy.com/courses/react-101/lessons/this-props/exercises/this-props-intro" target="_blank">this.props</a>
2. Hooks
   1. <a href="https://www.codecademy.com/courses/react-101/lessons/stateless-functional-components/exercises/stateless-functional-component-intro" target="_blank">Function Components</a>
   2. <a href="https://www.codecademy.com/courses/react-101/lessons/the-state-hook" target="_blank">The State Hook</a>
   3. <a href="https://www.codecademy.com/courses/react-101/lessons/the-effect-hook/exercises/function-component-effects" target="_blank">The Effect Hook</a>

## Additional Resources

The following resources are optional and can be used more for reference than upfront reading.

1. <a href="https://reactjs.org/docs/hooks-custom.html" target="_blank">Build Your Own Hooks</a>
2. <a href="https://reactjs.org/docs/hooks-reference.html" target="_blank">Hooks API Reference</a>
3. <a href="https://reactjs.org/docs/hooks-faq.html" target="_blank">Hooks FAQ</a>



## Day 7

### 8: <a href="https://react.dev/learn/responding-to-events" target="_blank">Handling Events</a>

When users click on a button they expect some result, or some change, take the counter example if you click on the button the state increments. To develop these types of functionality within our React applications we will need to handle events, but assigning an event listener to our elements and define some callback functions to handle the event in a meaningful way. In our JSX code we need to follow these steps to handle events.

1. How do you handle events?
   1. Attach the event listener to the element, such as an `onClick` or `onBlur` event.
   2. Define the callback function that will handle said event, accessing the event data if required. Remember to pass this function to the event handler.&#x20;
   3. Update state within this callback function by calling an updater function, run a side effect or execute any code.
2. "Events on DOM elements" are the same as <a href="https://www.w3schools.com/js/js_events.asp" target="_blank">JavaScript events or HTML events</a>. JS events allow us to perform logic on events that happen on our web pages such as mouse clicks. React supports a <a href="https://react.dev/reference/react-dom/components/common#common-props" target="_blank">wide range of events.</a>
3. Remember that functions that are passed to event handlers must be passed and not called, you can wrap the given function in an anonymous function if you need to pass in arguments.
4. You are able to stop event propagation as well as the default action.



### 7: <a href="https://react.dev/learn/conditional-rendering" target="_blank">Conditional Rendering</a>

Components will often need to display different UI's depending on conditions passed down as props, or the information its processing. You are able to conditionally render JSX in React using various patterns within JavaScript including conditonal statements that return JSX, or <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Conditional\_operator" target="_blank">ternary operators</a>.

1. Conditional rendering is one of the most powerful features of React, enabling us to use conditional logic to specify what a component should render.
2. You can use inline code for conditionals, `condition ? true : false` syntax is the <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Conditional\_Operator" target="_blank">JavaScript conditional operator</a>.

### 8: <a href="https://react.dev/learn/rendering-lists" target="_blank">Lists and Keys</a>

Lables on cds and JSX keys in an array serve similar purposes, it helps us to identify unique items from thier siblings. Keys help React to identify different JSX elements throughout thier lifetimes. You can generate key values in whatever way you would like, but if you've pulled data out of a database, they might already have identities, such as an Id property. You could create you're own incrementing counter to set unique keys within an application or implement <a href="https://www.npmjs.com/package/uuid" target="_blank">uuid</a> or another packaged that can assign unique id's within an application.&#x20;

1. Rocket recommends always using keys when rendering JSX elements in a list for performance reasons.
2. Keys should be unique among siblings
3. Keys cannot change as that would defeat the purpose of them

## Day 8

### 9: <a href="https://react.dev/reference/react-dom/components#form-components" target="_blank">Forms</a>, <a href="https://react.dev/reference/react-dom/components/input" target="_blank">input</a>, <a href="https://react.dev/reference/react-dom/components/select" target="_blank">select</a>, <a href="https://react.dev/reference/react-dom/components/textarea" target="_blank">textarea</a>

HTML forms and their elements afford developers the opportunity to capture user information as they interact with our application. Forms can be composed of a combination of inputs, selects and textareas, when wrapped in a form tag the values of these inputs can be extracted as form data. Or they can be maintained purely using state. Employ React element such as input, select and text areas to give users different input capabilities.&#x20;

1. An <a href="https://www.w3schools.com/html/html_forms.asp" target="_blank">HTML form</a> is an HTML element that either refreshes the page or navigates to a new page when the user submits the form. We often do not want this behaviour in React, opting to update UI on submit without refresh. To disable "refresh on submit" behaviour, Rocket recommends the technique in the React docs, to provide the `form` a `handleSubmit` callback function that calls `event.preventDefault`.
2. When handling the submit method from a form you should target the `event.target.value` to get the current value of an input.&#x20;
3. You must control the form elements that you use within a React component, do this by passing the value prop to it and handling the associated event. <a href="https://react.dev/reference/react-dom/components/input#controlling-an-input-with-a-state-variable" target="_blank">Have an in-depth look here</a>.&#x20;
4. Note how you will need to create state to capture form data.

## Post-Class Exercises: Codecademy React 101&#x20;

Complete all exercises in the following Codecademy lessons when they are assigned in the Rocket course schedule.

1. <a href="https://www.codecademy.com/courses/react-101/lessons/react-forms/exercises/react-forms-intro" target="_blank">React Forms</a>



### Day 9

### 10: <a href="https://react.dev/learn/sharing-state-between-components" target="_blank">Lifting State Up</a>

Managing state on components can get challenging and confusing when you need to share data between multiple components.  Especially so while still having to preform live updates and dynamically render content. The process of lifting up state means your children components actually receive data as props. Instead of storing the data on each child, you store the data on a shared parent of both child components. &#x20;

1. It is important that we pass both the temperature value and handle-change function from `Accordian` to `Panel` so the app can maintain only 1 "source of truth" state for the active value in `Panel`. If it helps, Rocket recommends drawing the component hierarchy to visualise how data flows in the application and verifying our understanding with our classmates and section leader.

### Day 10

### 11: <a href="https://react.dev/learn/thinking-in-react" target="_blank">Thinking In React</a>

Developing a user interfaces in React can be challenging. Instead of looking at a webpage as a whole, you should instead split it into sections or components, at this stage we can consider the states required for each component to correctly render as intended. To ensure that data follows correctly you then need to connect your components pass information or functions from parents to children.&#x20;

1. <a href="https://www.w3schools.com/js/js\_json_intro.asp" target="_blank">JSON</a> (JavaScript Object Notation) is a data format similar to JavaScript Objects, except can be used in text or file form. An API (Application Programming Interface) is typically a URL that manipulates and/or returns data. A JSON API is an API that returns data in JSON format, one of the most common formats to send and receive data on the internet.
2. Notice the example and how it passes updater function and state from the parent to the child, such that we can control and alter state.

### Day 11

### <a href="https://react.dev/learn/tutorial-tic-tac-toe" target="_blank">Tutorial: Intro to React</a>

If you finish the React Guide pages above early, feel free to start and finish this tutorial early to have more time for [Project 1](../1.p-frontend-app.md).

1. Rocket recommends starting with Setup Option 1 (Write Code in Browser) to focus on understanding React. If you finish the tutorial and have time, do Setup Option 2 (Local Development Environment) and port your code over to understand how to use Create React App. We will use Create React App to develop all frontend projects at Rocket.
2. Rocket recommends using <a href="https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi?hl=en" target="_blank">React DevTools</a> whenever developing React apps. It can help us debug quicker.
3. Note the tutorial's recommendation to use `on[Event]` naming convention for props that represent events and `handle[Event]` for methods that handle events.



>**New to Rocket Academy?**
>
>If you're not enrolled in Rocket's Bootcamp and visiting this page, <a href="https://www.rocketacademy.co/courses/bootcamp-course" target="_blank">check out our website</a> to learn more about our Bootcamp course!
