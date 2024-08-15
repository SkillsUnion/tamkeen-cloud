## **Working with Python Modules and Packages**

---

### **1 Introduction to Python Modules**

**Overview:**
Modules in Python are files containing Python code (functions, classes, variables) that can be reused in other Python programs. This allows for better organization, code reusability, and maintainability.

**Key Concepts:**
- **Module:** A file containing Python definitions and statements. The file name is the module name with the suffix `.py` added.
- **Package:** A collection of modules organized in directories that provide a hierarchical structure.

**1. Importing Modules:**
- **`import` statement:** Used to import an entire module.
  - **Example:**
    ```python
    import math
    print(math.sqrt(16))  # Output: 4.0
    ```

- **`from ... import ...` statement:** Used to import specific attributes or functions from a module.
  - **Example:**
    ```python
    from math import sqrt
    print(sqrt(25))  # Output: 5.0
    ```

- **`as` keyword:** Used to give a module or function an alias.
  - **Example:**
    ```python
    import math as m
    print(m.sqrt(36))  # Output: 6.0
    ```

**2. Creating Your Own Modules:**
- **Explanation:** You can create your own modules by writing Python code in a `.py` file and then importing it into another Python script.
- **Example:**
  - **my_module.py:**
    ```python
    def greet(name):
        return f"Hello, {name}!"
    ```
  - **main.py:**
    ```python
    import my_module

    print(my_module.greet("Alice"))  # Output: Hello, Alice!
    ```

---

### **2 Python Standard Library**

**Overview:**
Python's standard library is a collection of modules and packages that come with Python, providing a wide range of functionalities, such as file handling, mathematics, networking, and more.

**1. Commonly Used Standard Library Modules:**

- **`math` module:** Provides mathematical functions.
  - **Example:**
    ```python
    import math
    print(math.factorial(5))  # Output: 120
    ```

- **`datetime` module:** Provides classes for manipulating dates and times.
  - **Example:**
    ```python
    from datetime import datetime
    now = datetime.now()
    print(now.strftime("%Y-%m-%d %H:%M:%S"))  # Output: Current date and time
    ```

- **`os` module:** Provides functions for interacting with the operating system.
  - **Example:**
    ```python
    import os
    print(os.getcwd())  # Output: Current working directory
    os.mkdir('new_folder')  # Creates a new directory
    ```

- **`sys` module:** Provides access to system-specific parameters and functions.
  - **Example:**
    ```python
    import sys
    print(sys.version)  # Output: Python version information
    ```

- **`random` module:** Provides functions for generating random numbers.
  - **Example:**
    ```python
    import random
    print(random.randint(1, 100))  # Output: Random integer between 1 and 100
    ```

**2. Exploring the `collections` Module:**
- **`collections` module:** Provides specialized container datatypes like namedtuple, deque, Counter, and more.
  - **Example:**
    ```python
    from collections import Counter

    my_list = [1, 2, 2, 3, 4, 4, 4]
    count = Counter(my_list)
    print(count)  # Output: Counter({4: 3, 2: 2, 1: 1, 3: 1})
    ```

---

### **3 Python Packages**

**Overview:**
Packages are a way of structuring Python’s module namespace by using “dotted module names”. A package is a directory that contains a special file `__init__.py` and can contain multiple modules.

**1. Creating a Package:**
- **Structure:**
  - Create a directory (this will be your package).
  - Inside the directory, create an `__init__.py` file (can be empty or contain initialization code).
  - Add your module files inside this directory.

- **Example:**
  - **my_package/__init__.py:**
    ```python
    # This file can be empty or contain package initialization code
    ```

  - **my_package/module1.py:**
    ```python
    def function1():
        return "Function 1 from module 1"
    ```

  - **my_package/module2.py:**
    ```python
    def function2():
        return "Function 2 from module 2"
    ```

  - **main.py:**
    ```python
    from my_package import module1, module2

    print(module1.function1())  # Output: Function 1 from module 1
    print(module2.function2())  # Output: Function 2 from module 2
    ```

**2. Importing from a Package:**
- **Importing individual modules:**
  - **Example:**
    ```python
    from my_package.module1 import function1
    print(function1())  # Output: Function 1 from module 1
    ```

- **Importing all modules (not recommended for large packages):**
  - **Example:**
    ```python
    from my_package.module1 import *
    from my_package.module2 import *
    print(function1())  # Output: Function 1 from module 1
    print(function2())  # Output: Function 2 from module 2
    ```

**3. Using Relative Imports in Packages:**
- **Relative Imports:** Allows you to import a module relative to the position of the current module.
  - **Example:**
    ```python
    # In my_package/module2.py
    from .module1 import function1

    def function2():
        return function1() + " and function 2 from module 2"
    ```

---

### **4 Managing Dependencies with `pip`**

**Overview:**
`pip` is the package installer for Python. It allows you to install, upgrade, and manage Python packages that are not part of the standard library.

**1. Installing Packages:**
- **Installing a Package:**
  - **Example:**
    ```bash
    pip install requests
    ```

- **Installing a Specific Version:**
  - **Example:**
    ```bash
    pip install requests==2.25.1
    ```

- **Upgrading a Package:**
  - **Example:**
    ```bash
    pip install --upgrade requests
    ```

**2. Uninstalling Packages:**
- **Uninstalling a Package:**
  - **Example:**
    ```bash
    pip uninstall requests
    ```

**3. Listing Installed Packages:**
- **Listing All Installed Packages:**
  - **Example:**
    ```bash
    pip list
    ```

**4. Using `requirements.txt`:**
- **Overview:** `requirements.txt` is a file that lists all the dependencies of a project, making it easy to install them in one go.

- **Creating `requirements.txt`:**
  - **Example:**
    ```bash
    pip freeze > requirements.txt
    ```

- **Installing Dependencies from `requirements.txt`:**
  - **Example:**
    ```bash
    pip install -r requirements.txt
    ```

---