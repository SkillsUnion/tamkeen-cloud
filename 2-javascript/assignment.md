# **Comprehensive Assignment: Build a Task Management API**

---

### **Objective:**
Develop a simple Task Management API using Node.js that allows users to manage tasks (create, read, update, delete) using modern JavaScript features such as ES6 syntax, classes, destructuring, async/await, and Node.js modules. The API will be managed using npm and monitored with nodemon.

---

### **Assignment Overview:**
You will create a Node.js application that serves as a backend API for managing tasks. The API will support operations like creating tasks, retrieving a list of tasks, updating tasks, and deleting tasks. You will apply ES6 features in your JavaScript code and leverage Node.js modules, npm for dependency management, and nodemon for running and monitoring your application during development.

---

### **Steps:**

#### **Step 1: Setup the Node.js Project**
1. **Initialize the Project:**
   - Create a new directory for your project.
   - Initialize the project using npm:
     ```bash
     npm init -y
     ```
   - Install the necessary dependencies:
     ```bash
     npm install express
     ```
   - Install nodemon as a development dependency:
     ```bash
     npm install --save-dev nodemon
     ```

2. **Configure nodemon:**
   - Add a `start` script to your `package.json` to run the application with nodemon:
     ```json
     "scripts": {
       "start": "nodemon index.js"
     }
     ```

#### **Step 2: Create a Task Class**
1. **Define a Task Class:**
   - Create a `Task` class in a separate module (`task.js`):
   - The class should have properties for `id`, `title`, `description`, and `completed`.
   - Include methods to update task details and mark the task as complete.
   
   ```javascript
   // task.js
   class Task {
       constructor(id, title, description) {
           this.id = id;
           this.title = title;
           this.description = description;
           this.completed = false;
       }

       updateTask({ title, description }) {
           this.title = title || this.title;
           this.description = description || this.description;
       }

       completeTask() {
           this.completed = true;
       }
   }

   module.exports = Task;
   ```

#### **Step 3: Create the Task Management API**
1. **Set Up Express:**
   - In your `index.js` file, require the necessary modules (`express` and `Task`).
   - Initialize an Express application.

   ```javascript
   const express = require('express');
   const Task = require('./task');
   const app = express();

   app.use(express.json()); // For parsing application/json
   ```

2. **Implement the API Endpoints:**
   - **Create Task** (`POST /tasks`): Accept task data and create a new task.
   - **Get All Tasks** (`GET /tasks`): Return a list of all tasks.
   - **Update Task** (`PUT /tasks/:id`): Update the title or description of an existing task.
   - **Delete Task** (`DELETE /tasks/:id`): Delete a task by ID.

   ```javascript
   let tasks = [];
   let taskIdCounter = 1;

   // Create Task
   app.post('/tasks', (req, res) => {
       const { title, description } = req.body;
       const newTask = new Task(taskIdCounter++, title, description);
       tasks.push(newTask);
       res.status(201).json(newTask);
   });

   // Get All Tasks
   app.get('/tasks', (req, res) => {
       res.json(tasks);
   });

   // Update Task
   app.put('/tasks/:id', (req, res) => {
       const { id } = req.params;
       const task = tasks.find(t => t.id == id);
       if (!task) return res.status(404).json({ message: 'Task not found' });

       task.updateTask(req.body);
       res.json(task);
   });

   // Delete Task
   app.delete('/tasks/:id', (req, res) => {
       tasks = tasks.filter(t => t.id != req.params.id);
       res.status(204).end();
   });

   // Start the server
   app.listen(3000, () => {
       console.log('Task API is running on http://localhost:3000');
   });
   ```

#### **Step 4: Handle Asynchronous Operations**
1. **Simulate Asynchronous Database Operations:**
   - Modify your `Task` class to include asynchronous methods for simulating database save operations.

   ```javascript
   class Task {
       // ... other methods

       async save() {
           return new Promise((resolve) => {
               setTimeout(() => {
                   resolve(this);
               }, 1000); // Simulate 1 second delay
           });
       }
   }
   ```

   - Update your API routes to use `async/await` when creating and updating tasks.

   ```javascript
   // Create Task with async/await
   app.post('/tasks', async (req, res) => {
       const { title, description } = req.body;
       const newTask = new Task(taskIdCounter++, title, description);
       await newTask.save();
       tasks.push(newTask);
       res.status(201).json(newTask);
   });
   ```

#### **Step 5: Test and Run the Application**
1. **Run Your Application:**
   - Start your application using npm:
     ```bash
     npm start
     ```

2. **Test the Endpoints:**
   - Use Postman or curl to test the API endpoints (creating, reading, updating, and deleting tasks).

3. **Document Your API:**
   - Create a simple documentation in a `README.md` file describing how to set up and use your Task Management API.

#### **Submission:**
- **Code**: Submit the entire project code.
- **Screenshots**: Include screenshots of your API responses from Postman or curl, showing successful operations for each endpoint.
- **Documentation**: Provide a `README.md` file explaining the project, setup instructions, and how to use the API.

---

### **Key Concepts Covered:**
- **JavaScript ES6 Features**: Classes, destructuring, async/await, module exports/imports.
- **Node.js Modules**: Creating and importing modules in Node.js.
- **npm**: Managing project dependencies and scripts.
- **nodemon**: Running and monitoring the application during development.

---