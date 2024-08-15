### **Comprehensive Assignment: Python Project Covering Modules 1-7**

---

### **Objective:**
Develop a Python application that incorporates concepts from all the modules (1-7). This project will require you to use Python fundamentals, data structures, OOP principles, modules, packages, asynchronous programming, and package management.

### **Project Overview:**
You will create a Python-based **Task Management System** that allows users to manage tasks through a command-line interface (CLI). The system will include features for adding, viewing, updating, and deleting tasks, along with additional features like saving tasks to a file, fetching motivational quotes from an API asynchronously, and organizing the code into modules and packages.

---

### **Requirements:**

1. **Task Class Implementation (Module 4):**
   - Create a `Task` class with the following attributes:
     - `id`: Unique identifier for the task.
     - `title`: Title of the task.
     - `description`: Description of the task.
     - `completed`: Boolean flag indicating whether the task is completed or not (default: `False`).

   - Implement methods for:
     - Marking a task as complete.
     - Updating the title and description.
     - Returning a string representation of the task.

   ```python
   class Task:
       id_counter = 1

       def __init__(self, title, description):
           self.id = Task.id_counter
           Task.id_counter += 1
           self.title = title
           self.description = description
           self.completed = False

       def mark_complete(self):
           self.completed = True

       def update(self, title=None, description=None):
           if title:
               self.title = title
           if description:
               self.description = description

       def __str__(self):
           return f"Task[{self.id}]: {self.title} - {'Completed' if self.completed else 'Pending'}"
   ```

2. **Task Management System (Modules 2, 3, and 5):**
   - Implement a `TaskManager` class to manage a collection of `Task` objects. This class should support adding, viewing, updating, and deleting tasks.
   - Use lists to store tasks and dictionaries to manage task attributes.
   - Use destructuring and the spread operator where applicable.
   - Implement a method to save and load tasks from a file.

   ```python
   import json

   class TaskManager:
       def __init__(self):
           self.tasks = []

       def add_task(self, title, description):
           task = Task(title, description)
           self.tasks.append(task)

       def view_tasks(self):
           for task in self.tasks:
               print(task)

       def update_task(self, task_id, title=None, description=None):
           for task in self.tasks:
               if task.id == task_id:
                   task.update(title, description)

       def delete_task(self, task_id):
           self.tasks = [task for task in self.tasks if task.id != task_id]

       def save_to_file(self, filename="tasks.json"):
           with open(filename, 'w') as f:
               tasks_data = [task.__dict__ for task in self.tasks]
               json.dump(tasks_data, f)

       def load_from_file(self, filename="tasks.json"):
           try:
               with open(filename, 'r') as f:
                   tasks_data = json.load(f)
                   self.tasks = [Task(**task) for task in tasks_data]
           except FileNotFoundError:
               print("File not found. Starting with an empty task list.")
   ```

3. **Asynchronous Features (Module 6):**
   - Implement an asynchronous method in the `TaskManager` class to fetch a motivational quote from an API and display it after adding a new task.
   - Use `asyncio` and `aiohttp` for asynchronous HTTP requests.

   ```python
   import aiohttp
   import asyncio

   class TaskManager:
       # ... (previous code)

       async def fetch_quote(self):
           async with aiohttp.ClientSession() as session:
               async with session.get('https://api.quotable.io/random') as response:
                   data = await response.json()
                   print(f"Motivational Quote: {data['content']} - {data['author']}")

       async def add_task_with_quote(self, title, description):
           self.add_task(title, description)
           await self.fetch_quote()
   ```

4. **Organizing Code into Modules and Packages (Module 7):**
   - Organize your `Task` and `TaskManager` classes into separate modules within a package named `task_manager`.
   - Create an `__init__.py` file within the package to handle the imports.
   - Use relative imports within the package.

   **Directory Structure:**
   ```
   task_manager/
       __init__.py
       task.py
       manager.py
   main.py
   ```

   - Example:
     - **task_manager/task.py:**
       ```python
       class Task:
           # (Task class implementation)
       ```
     - **task_manager/manager.py:**
       ```python
       from .task import Task
       import json

       class TaskManager:
           # (TaskManager class implementation)
       ```

     - **main.py:**
       ```python
       from task_manager.manager import TaskManager
       import asyncio

       async def main():
           manager = TaskManager()
           manager.load_from_file()
           await manager.add_task_with_quote("Finish assignment", "Complete the Python project.")
           manager.view_tasks()
           manager.save_to_file()

       asyncio.run(main())
       ```

5. **Dependency Management (Module 7):**
   - Create a `requirements.txt` file listing all the dependencies for your project.
   - Ensure that your project can be easily set up by installing the necessary packages using `pip`.

   ```bash
   aiohttp==3.7.4
   ```

---

### **Submission Requirements:**

1. **Code:** Submit the complete codebase, including all modules, packages, and the main script.
2. **Screenshots:** Provide screenshots of the terminal showing the application in use, including adding tasks, fetching quotes, and saving/loading tasks.
3. **`requirements.txt`:** Include a `requirements.txt` file with all the dependencies.
4. **Documentation:** Write a brief `README.md` explaining how to set up and run the project, including any dependencies that need to be installed.

---

### **Assessment Criteria:**

- **Correctness:** The application should meet all the functional requirements and correctly implement the features described.
- **Code Quality:** Code should be clean, well-organized, and follow best practices (e.g., proper use of functions, classes, and modules).
- **Use of Modules and Packages:** Code should be modular, with appropriate use of packages and modules to organize the project.
- **Asynchronous Programming:** The application should demonstrate the correct use of asynchronous programming using `asyncio` and `aiohttp`.
- **Documentation:** The project should include clear instructions for setup and usage, as well as a well-documented `requirements.txt` file.

---
