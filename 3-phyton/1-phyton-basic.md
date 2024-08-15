# **Introduction to Python**

### **1 What is Python?**

**Overview:**
- **Python** is a high-level, interpreted programming language that emphasizes code readability with its use of significant indentation. Python's syntax allows programmers to express concepts in fewer lines of code than would be possible in languages such as C++ or Java.
- It was created by **Guido van Rossum** and first released in 1991. Python has a design philosophy that emphasizes code readability, notably using significant whitespace.
- **Python is used for** a variety of purposes, including web development (with frameworks like Django and Flask), data analysis (with libraries like pandas and NumPy), artificial intelligence, machine learning, automation, and more.

**Why Python?**
- **Simple and Easy to Learn:** Python's syntax is straightforward and resembles English, making it easier for beginners to learn.
- **Versatile:** Python can be used for a wide range of applications, from web development to data science, automation, and beyond.
- **Large Community and Ecosystem:** Python has a vast collection of libraries and frameworks, supported by a large community of developers.

### **2 Setting Up Python**

**Installing Python:**
- **Windows:**
  - Download the latest version of Python from the official website: [python.org](https://www.python.org/downloads/).
  - Run the installer and ensure that the option to "Add Python to PATH" is checked.
  
- **macOS:**
  - macOS comes with Python 2.x pre-installed. To install Python 3, you can use Homebrew:
    ```bash
    brew install python
    ```

- **Linux:**
  - On most distributions, Python is already installed. To install the latest version:
    ```bash
    sudo apt-get update
    sudo apt-get install python3
    ```

**Verifying the Installation:**
- Open a terminal or command prompt and type:
  ```bash
  python --version
  ```
  or for Python 3:
  ```bash
  python3 --version
  ```
  This should display the installed version of Python.

**Setting Up a Development Environment:**
- **IDEs and Text Editors:**
  - **VS Code:** A lightweight, powerful source code editor with support for Python through extensions.
  - **PyCharm:** A fully-featured Python IDE that comes in both free (Community) and paid (Professional) versions.
  - **Jupyter Notebook:** An open-source web application that allows you to create and share documents that contain live code, equations, visualizations, and narrative text. It is widely used in data science.

**Running Your First Python Script:**
- Create a new file named `hello.py` and add the following code:
  ```python
  print("Hello, Python!")
  ```
- Save the file and run it from the terminal:
  ```bash
  python hello.py
  ```
  or for Python 3:
  ```bash
  python3 hello.py
  ```
  This should print `Hello, Python!` to the terminal.

### **3 Python Syntax and Basics**

**Python Syntax:**
- **Indentation:** Python uses indentation to define code blocks. Unlike many other languages, Python does not use curly braces `{}` or keywords like `end` to delimit blocks of code.
  ```python
  if 5 > 2:
      print("Five is greater than two!")
  ```
  - The above code uses indentation to define what should be executed if the condition is true.

- **Comments:**
  - Single-line comments start with `#`.
    ```python
    # This is a comment
    print("Hello, World!")
    ```
  - Multi-line comments can be done with triple quotes.
    ```python
    """
    This is a multi-line comment
    in Python.
    """
    ```

**Variables and Data Types:**
- **Variables:** Variables in Python do not require explicit declaration. They are created the moment you first assign a value to them.
  ```python
  x = 5
  y = "Hello"
  print(x)
  print(y)
  ```

- **Data Types:** Python has several built-in data types, including:
  - **Integers (`int`):** Whole numbers, e.g., `5`, `100`, `-20`.
  - **Floats (`float`):** Numbers with a decimal point, e.g., `5.5`, `3.14`.
  - **Strings (`str`):** Text enclosed in quotes, e.g., `"Hello"`, `'World'`.
  - **Booleans (`bool`):** Represents `True` or `False`.

**Basic Input/Output Operations:**
- **Output:** The `print()` function is used to display output in Python.
  ```python
  print("Hello, World!")
  ```
- **Input:** The `input()` function is used to get user input.
  ```python
  name = input("Enter your name: ")
  print("Hello, " + name)
  ```

### **4 Basic Arithmetic Operations**

**Arithmetic Operators:**
- **Addition (`+`):**
  ```python
  result = 5 + 3  # 8
  ```
- **Subtraction (`-`):**
  ```python
  result = 5 - 3  # 2
  ```
- **Multiplication (`*`):**
  ```python
  result = 5 * 3  # 15
  ```
- **Division (`/`):**
  ```python
  result = 5 / 3  # 1.6666666666666667
  ```
- **Floor Division (`//`):** Divides and returns the largest whole number less than or equal to the result.
  ```python
  result = 5 // 3  # 1
  ```
- **Modulus (`%`):** Returns the remainder of the division.
  ```python
  result = 5 % 3  # 2
  ```
- **Exponentiation (`**`):** Raises the number to the power of the exponent.
  ```python
  result = 5 ** 3  # 125
  ```

---