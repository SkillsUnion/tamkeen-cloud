# **Comprehensive JavaScript Exercise**

#### **Objective:**
Build a simple application using modern JavaScript (ES6) features, where you will apply your understanding of classes, destructuring, the spread operator, async/await, and the concept of reference vs. value.

---

### **Scenario:**
You are tasked with creating a small application that manages a list of tasks. Each task has a title, description, and status (completed or not). You will use ES6 classes to create the task structure, destructuring to handle data, the spread operator to manage the task list, and async/await to simulate saving tasks to a server.

---

### **Step 1: Create a Task Class**

1. Define a class `Task` that has the following properties:
   - `title` (string)
   - `description` (string)
   - `completed` (boolean, default to `false`)

2. The class should have methods to:
   - Mark the task as complete.
   - Update the task details (title and description).
   - Display the task details.

```javascript
class Task {
    constructor(title, description) {
        this.title = title;
        this.description = description;
        this.completed = false;
    }

    completeTask() {
        this.completed = true;
    }

    updateTask({ title, description }) {
        this.title = title || this.title;
        this.description = description || this.description;
    }

    displayTask() {
        console.log(`Title: ${this.title}, Description: ${this.description}, Completed: ${this.completed}`);
    }
}
```

---

### **Step 2: Manage the Task List**

1. Create an array `taskList` to store instances of `Task`.

2. Add three tasks to `taskList` using the spread operator.

3. Display all tasks using the `displayTask` method.

```javascript
let task1 = new Task('Buy groceries', 'Milk, Bread, Eggs');
let task2 = new Task('Clean the house', 'Living room, Kitchen, Bathroom');
let task3 = new Task('Study ES6', 'Complete JavaScript module exercises');

let taskList = [...[task1, task2, task3]];

taskList.forEach(task => task.displayTask());
```

---

### **Step 3: Update and Complete Tasks**

1. Update the description of one of the tasks using the `updateTask` method and destructuring.

2. Mark another task as complete using the `completeTask` method.

3. Display the updated task list.

```javascript
task1.updateTask({ description: 'Milk, Bread, Eggs, Cheese' });
task2.completeTask();

taskList.forEach(task => task.displayTask());
```

---

### **Step 4: Save Tasks to a Server (Simulated with Async/Await)**

1. Create an async function `saveTasks` that simulates saving tasks to a server by using `setTimeout` to mimic an asynchronous operation.

2. After "saving" the tasks, log a message indicating success.

```javascript
async function saveTasks(tasks) {
    console.log('Saving tasks to the server...');
    
    return new Promise((resolve) => {
        setTimeout(() => {
            resolve('Tasks saved successfully!');
        }, 2000);
    });
}

saveTasks(taskList).then(message => console.log(message));
```

---

### **Step 5: Demonstrate Reference vs. Value**

1. Create a new task and add it to the task list. Then, create a copy of that task (try both shallow copy and deep copy) and modify the copy.

2. Show how changes to the original task or its copy affect the other (or not), depending on how the copy was made.

```javascript
let task4 = new Task('Go for a run', 'Run 5km in the park');
taskList.push(task4);

// Shallow copy
let task4Copy = task4;
task4Copy.completeTask();

console.log('Original Task 4:', task4);
console.log('Copied Task 4:', task4Copy);

// Deep copy using destructuring
let task4DeepCopy = { ...task4 };
task4DeepCopy.updateTask({ title: 'Go for a walk' });

console.log('Original Task 4 after deep copy update:', task4);
console.log('Deep Copied Task 4:', task4DeepCopy);
```

---

### **Submission:**
- **Code**: Provide the complete code you wrote for this exercise.
- **Screenshots**: Include screenshots of your terminal or console output showing the successful execution of each step.
- **Reflection**: Write a brief reflection on how using ES6 features like classes, destructuring, and async/await improved your development experience.

---

This exercise integrates multiple JavaScript concepts and challenges you to apply them in a practical project. Let me know if there’s anything else you need!