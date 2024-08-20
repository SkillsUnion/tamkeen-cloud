## **Asynchronous Programming with Async/Await in Python**

---

### **1 Introduction to Asynchronous Programming**

**Overview:**
Asynchronous programming is a programming paradigm that allows for the execution of tasks in a non-blocking manner, meaning that tasks can run independently and concurrently without waiting for each other to complete. This is particularly useful for I/O-bound operations, such as file handling, network requests, and database queries.

**Key Concepts:**
- **Synchronous vs Asynchronous Execution:**
  - **Synchronous:** Tasks are executed one after another, and each task must complete before the next one begins.
  - **Asynchronous:** Tasks are started, and the program continues to execute while waiting for these tasks to complete, allowing other tasks to run in the meantime.

- **Concurrency vs Parallelism:**
  - **Concurrency:** Multiple tasks are making progress at the same time but are not necessarily running simultaneously.
  - **Parallelism:** Multiple tasks are executed simultaneously, usually on multiple processors or cores.

**Use Cases for Asynchronous Programming:**
- Handling I/O-bound tasks such as reading/writing files, network requests, and database operations.
- Improving the performance of programs that perform multiple tasks concurrently.

---

### **2 The `async` and `await` Keywords**

**1. The `async` Keyword:**
- **Purpose:** The `async` keyword is used to define a coroutine, which is a special type of function that can be paused and resumed. Coroutines are the building blocks of asynchronous programming in Python.
- **Syntax:**
  ```python
  async def my_coroutine():
      pass
  ```

**2. The `await` Keyword:**
- **Purpose:** The `await` keyword is used to pause the execution of a coroutine until the result of another coroutine or asynchronous operation is available. It can only be used inside `async` functions.
- **Syntax:**
  ```python
  await some_coroutine()
  ```
- **Example:**
  ```python
  import asyncio

  async def say_hello():
      print("Hello")
      await asyncio.sleep(1)
      print("World")

  asyncio.run(say_hello())
  # Output:
  # Hello
  # (1 second pause)
  # World
  ```

---

### **3 The `asyncio` Module**

**Overview:**
The `asyncio` module is the core of asynchronous programming in Python. It provides tools for managing coroutines, tasks, and event loops.

**1. The Event Loop:**
- **Purpose:** The event loop is responsible for managing the execution of asynchronous tasks. It continuously runs and checks if any tasks are ready to execute.
- **Example:**
  ```python
  import asyncio

  async def say_hello():
      print("Hello")
      await asyncio.sleep(1)
      print("World")

  asyncio.run(say_hello())  # This starts the event loop and runs the coroutine
  ```

**2. Creating and Running Coroutines:**
- **`asyncio.run()`:** A function that runs a given coroutine and returns its result.
- **Example:**
  ```python
  async def main():
      await say_hello()

  asyncio.run(main())
  ```

**3. Creating and Running Tasks:**
- **Tasks:** Tasks are used to schedule coroutines concurrently. They are instances of `asyncio.Task` and allow multiple coroutines to run concurrently.
- **Example:**
  ```python
  async def task1():
      await asyncio.sleep(1)
      print("Task 1 completed")

  async def task2():
      await asyncio.sleep(2)
      print("Task 2 completed")

  async def main():
      task_1 = asyncio.create_task(task1())
      task_2 = asyncio.create_task(task2())
      await task_1
      await task_2

  asyncio.run(main())
  # Output:
  # (1 second pause)
  # Task 1 completed
  # (1 second pause)
  # Task 2 completed
  ```

**4. Waiting for Multiple Tasks:**
- **`asyncio.gather()`:** A function that runs multiple coroutines concurrently and waits for them all to complete.
- **Example:**
  ```python
  async def task1():
      await asyncio.sleep(1)
      print("Task 1 completed")

  async def task2():
      await asyncio.sleep(2)
      print("Task 2 completed")

  async def main():
      await asyncio.gather(task1(), task2())

  asyncio.run(main())
  # Output:
  # (1 second pause)
  # Task 1 completed
  # (1 second pause)
  # Task 2 completed
  ```

---

### **4 Asynchronous I/O Operations**

**1. Performing Asynchronous I/O Operations:**
- **Overview:** Asynchronous I/O operations are non-blocking and allow your program to handle other tasks while waiting for I/O operations to complete.

- **Example: Reading and Writing Files Asynchronously:**
  ```python
  import aiofiles
  import asyncio

  async def read_file(file_path):
      async with aiofiles.open(file_path, mode='r') as file:
          contents = await file.read()
          print(contents)

  async def write_file(file_path, content):
      async with aiofiles.open(file_path, mode='w') as file:
          await file.write(content)

  async def main():
      await write_file('example.txt', 'Hello, asyncio!')
      await read_file('example.txt')

  asyncio.run(main())
  ```

**2. Making Asynchronous HTTP Requests:**
- **Overview:** Asynchronous HTTP requests can be made using libraries like `aiohttp`, which allows for non-blocking requests.

- **Example: Fetching Data from an API:**
  ```python
  import aiohttp
  import asyncio

  async def fetch_data(session, url):
      async with session.get(url) as response:
          data = await response.text()
          print(data)

  async def main():
      async with aiohttp.ClientSession() as session:
          await fetch_data(session, 'https://jsonplaceholder.typicode.com/posts/1')

  asyncio.run(main())
  ```

---

### **5 Handling Exceptions in Async Code**

**1. Exception Handling in Coroutines:**
- **Overview:** Exceptions that occur within a coroutine can be caught and handled using `try` and `except`, just like in synchronous code.

- **Example:**
  ```python
  import asyncio

  async def faulty_coroutine():
      await asyncio.sleep(1)
      raise ValueError("An error occurred!")

  async def main():
      try:
          await faulty_coroutine()
      except ValueError as e:
          print(f"Caught an exception: {e}")

  asyncio.run(main())
  # Output:
  # (1 second pause)
  # Caught an exception: An error occurred!
  ```

**2. Cancelling Tasks:**
- **Overview:** Tasks can be cancelled using the `task.cancel()` method. When a task is cancelled, it raises a `CancelledError` exception.
- **Example:**
  ```python
  import asyncio

  async def long_running_task():
      try:
          await asyncio.sleep(10)
      except asyncio.CancelledError:
          print("Task was cancelled")
          raise

  async def main():
      task = asyncio.create_task(long_running_task())
      await asyncio.sleep(1)
      task.cancel()
      try:
          await task
      except asyncio.CancelledError:
          print("Caught task cancellation")

  asyncio.run(main())
  # Output:
  # (1 second pause)
  # Task was cancelled
  # Caught task cancellation
  ```

---