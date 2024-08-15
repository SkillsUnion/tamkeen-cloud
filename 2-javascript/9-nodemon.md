# 0.5.3: Nodemon

## Learning Objectives

1. Use Nodemon to auto-refresh Node applications on code changes

## Introduction

<a href="https://www.npmjs.com/package/nodemon" target="_blank">Nodemon</a> is an application that restarts our Node app every time we change a file that the app depends on. This is especially useful in development when we make frequent changes to our code. Without Nodemon we would need to manually quit and restart our app on code changes.

## Usage

1.  Install Nodemon globally to run Nodemon from all folders.

    ```
    npm i -g nodemon
    ```
2.  Run `nodemon` on the entry file of our app. When any app files changes, Nodemon will restart the app.

    ```
    nodemon index.js
    ```
