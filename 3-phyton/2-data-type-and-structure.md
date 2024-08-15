## **Data Types and Structures**

---

### **1 Primitive Data Types**

**Overview:**
Python provides several built-in data types that are used to represent various types of data. These are known as **primitive data types** because they are the simplest forms of data.

**1. Integers (`int`):**
- **Description:** Represents whole numbers, both positive and negative, without a fractional component.
- **Examples:**
  ```python
  age = 25
  year = 2024
  negative_number = -42
  ```

**2. Floating-Point Numbers (`float`):**
- **Description:** Represents real numbers, i.e., numbers with a fractional component.
- **Examples:**
  ```python
  price = 19.99
  height = 5.9
  negative_float = -3.14
  ```

**3. Strings (`str`):**
- **Description:** Represents a sequence of characters, used to handle text.
- **Examples:**
  ```python
  name = "Alice"
  greeting = 'Hello, World!'
  multi_line_string = """This is a
  multi-line string"""
  ```

**4. Booleans (`bool`):**
- **Description:** Represents one of two values: `True` or `False`.
- **Examples:**
  ```python
  is_raining = True
  is_sunny = False
  ```

---

### **2 Control Structures**

**Overview:**
Control structures are fundamental concepts in programming that allow the flow of a program to change depending on conditions or repetitions.

**1. Conditionals**

**`if`, `else`, `elif`:**
- **Purpose:** Allows the program to make decisions and execute different blocks of code based on conditions.
- **Syntax:**
  ```python
  if condition1:
      # Code to execute if condition1 is true
  elif condition2:
      # Code to execute if condition2 is true
  else:
      # Code to execute if both conditions are false
  ```

**Examples:**
```python
age = 18

if age >= 18:
    print("You are an adult.")
elif age >= 13:
    print("You are a teenager.")
else:
    print("You are a child.")
```

**2. Loops**

**`for` Loop:**
- **Purpose:** Repeats a block of code a fixed number of times.
- **Syntax:**
  ```python
  for variable in iterable:
      # Code to execute for each item in iterable
  ```

**Examples:**
```python
for i in range(5):
    print(f"Iteration {i}")
```

**`while` Loop:**
- **Purpose:** Repeats a block of code as long as a condition is true.
- **Syntax:**
  ```python
  while condition:
      # Code to execute while condition is true
  ```

**Examples:**
```python
count = 0
while count < 5:
    print(f"Count is {count}")
    count += 1
```

**3. Loop Control Statements**

**`break`:**
- **Purpose:** Terminates the loop prematurely when a certain condition is met.
- **Example:**
  ```python
  for i in range(10):
      if i == 5:
          break
      print(i)
  ```

**`continue`:**
- **Purpose:** Skips the current iteration of the loop and proceeds to the next iteration.
- **Example:**
  ```python
  for i in range(10):
      if i % 2 == 0:
          continue
      print(i)
  ```

**`pass`:**
- **Purpose:** A null operation; it is used when a statement is required syntactically but no code needs to be executed.
- **Example:**
  ```python
  for i in range(5):
      if i == 3:
          pass  # No operation, just a placeholder
      print(i)
  ```

---

### **3 Complex Data Types**

**Overview:**
Python provides more complex data types that are capable of storing collections of items or more structured forms of data.

**1. Lists (`list`):**
- **Description:** An ordered, mutable collection of items, which can be of any data type.
- **Syntax:**
  ```python
  my_list = [1, 2, 3, 4, 5]
  ```
  
**Common List Operations:**
- **Indexing and Slicing:**
  ```python
  first_item = my_list[0]   # Access the first item
  sublist = my_list[1:3]    # Get a sublist from index 1 to 2
  ```
- **List Methods:**
  - **`append(item)`**: Adds an item to the end of the list.
    ```python
    my_list.append(6)
    ```
  - **`remove(item)`**: Removes the first occurrence of an item.
    ```python
    my_list.remove(3)
    ```
  - **`sort()`**: Sorts the list in ascending order.
    ```python
    my_list.sort()
    ```

**2. Tuples (`tuple`):**
- **Description:** An ordered, immutable collection of items.
- **Syntax:**
  ```python
  my_tuple = (1, 2, 3, 4, 5)
  ```
  
**Tuple Operations:**
- **Indexing and Slicing:**
  ```python
  first_item = my_tuple[0]   # Access the first item
  subtuple = my_tuple[1:3]   # Get a subtuple from index 1 to 2
  ```
- **Immutability:** Tuples cannot be modified (no append, remove, etc.).

**3. Dictionaries (`dict`):**
- **Description:** A collection of key-value pairs, where each key is unique.
- **Syntax:**
  ```python
  my_dict = {"name": "Alice", "age": 25, "city": "New York"}
  ```
  
**Common Dictionary Operations:**
- **Accessing Values:**
  ```python
  name = my_dict["name"]
  ```
- **Adding/Updating Entries:**
  ```python
  my_dict["email"] = "alice@example.com"  # Add new key-value pair
  my_dict["age"] = 26  # Update value for existing key
  ```
- **Removing Entries:**
  ```python
  del my_dict["city"]  # Remove a key-value pair
  ```

**4. Sets (`set`):**
- **Description:** An unordered collection of unique items.
- **Syntax:**
  ```python
  my_set = {1, 2, 3, 4, 5}
  ```
  
**Common Set Operations:**
- **Adding Items:**
  ```python
  my_set.add(6)
  ```
- **Removing Items:**
  ```python
  my_set.remove(3)
  ```
- **Set Operations:**
  - **Union (`|`)**: Combines two sets.
    ```python
    set1 = {1, 2, 3}
    set2 = {3, 4, 5}
    union_set = set1 | set2  # {1, 2, 3, 4, 5}
    ```
  - **Intersection (`&`)**: Returns items common to both sets.
    ```python
    intersection_set = set1 & set2  # {3}
    ```
  - **Difference (`-`)**: Returns items in the first set but not in the second.
    ```python
    difference_set = set1 - set2  # {1, 2}
    ```

---