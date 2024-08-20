## **Reference vs Value and Mutable vs Immutable Objects**

---

### **1 Understanding Reference vs Value**

**Overview:**
In Python, variables store references to the values in memory rather than the actual data itself. Understanding the difference between how Python handles variables that store mutable objects versus immutable objects is crucial for writing efficient and bug-free code.

**1. Value vs Reference:**
- **Value:** When you assign a value to a variable, Python creates a reference to that value in memory. The variable does not directly hold the value but rather points to the location in memory where the value is stored.
- **Example:**
  ```python
  x = 10  # x is a reference to the value 10
  y = x   # y now references the same value as x
  print(x, y)  # Output: 10 10
  ```
  - If you modify `x` by assigning it a new value, `y` remains unchanged because the reference is broken:
  ```python
  x = 20
  print(x, y)  # Output: 20 10
  ```

**2. Mutable vs Immutable Objects:**
- **Immutable Objects:** These are objects whose state cannot be modified after they are created. Examples include integers, floats, strings, and tuples.
  - **Example:**
    ```python
    a = "hello"
    b = a
    a = a.upper()  # Modifies 'a', but 'b' remains unchanged
    print(a, b)  # Output: HELLO hello
    ```

- **Mutable Objects:** These are objects that can be modified after they are created. Examples include lists, dictionaries, and sets.
  - **Example:**
    ```python
    list1 = [1, 2, 3]
    list2 = list1
    list1.append(4)  # Modifies 'list1', and 'list2' is also affected
    print(list1, list2)  # Output: [1, 2, 3, 4] [1, 2, 3, 4]
    ```

### **2 Immutable Types in Python**

**Overview:**
Immutable objects cannot be changed after their creation. Any operation that modifies an immutable object will instead create a new object.

**1. Strings:**
- **Explanation:** Strings in Python are immutable. Any operation that alters a string, such as concatenation or replacement, creates a new string.
- **Example:**
  ```python
  s1 = "hello"
  s2 = s1
  s1 = s1 + " world"  # Creates a new string "hello world"
  print(s1, s2)  # Output: "hello world" "hello"
  ```

**2. Tuples:**
- **Explanation:** Tuples are immutable sequences of items. Once a tuple is created, it cannot be modified.
- **Example:**
  ```python
  t1 = (1, 2, 3)
  t2 = t1
  t1 = t1 + (4,)  # Creates a new tuple (1, 2, 3, 4)
  print(t1, t2)  # Output: (1, 2, 3, 4) (1, 2, 3)
  ```

**3. Numbers:**
- **Explanation:** Integers and floating-point numbers are immutable. Any arithmetic operation on a number creates a new object.
- **Example:**
  ```python
  num1 = 100
  num2 = num1
  num1 += 50  # Creates a new number 150
  print(num1, num2)  # Output: 150 100
  ```

### **3 Mutable Types in Python**

**Overview:**
Mutable objects can be changed in place, meaning their state or content can be modified without creating a new object.

**1. Lists:**
- **Explanation:** Lists are mutable, allowing you to change their content by adding, removing, or modifying elements.
- **Example:**
  ```python
  list1 = [1, 2, 3]
  list2 = list1
  list1.append(4)  # Modifies the original list
  print(list1, list2)  # Output: [1, 2, 3, 4] [1, 2, 3, 4]
  ```

**2. Dictionaries:**
- **Explanation:** Dictionaries are mutable collections of key-value pairs. You can add, remove, or update entries.
- **Example:**
  ```python
  dict1 = {"name": "Alice", "age": 25}
  dict2 = dict1
  dict1["age"] = 26  # Modifies the original dictionary
  print(dict1, dict2)  # Output: {"name": "Alice", "age": 26} {"name": "Alice", "age": 26}
  ```

**3. Sets:**
- **Explanation:** Sets are mutable collections of unique elements. You can add or remove items, but duplicate items are not allowed.
- **Example:**
  ```python
  set1 = {1, 2, 3}
  set2 = set1
  set1.add(4)  # Modifies the original set
  print(set1, set2)  # Output: {1, 2, 3, 4} {1, 2, 3, 4}
  ```

### **4 Shared References in Mutable Objects**

**Overview:**
When two variables reference the same mutable object, changes made to the object through one variable are reflected in the other. This is because both variables point to the same memory location.

**Example:**
```python
a = [1, 2, 3]
b = a  # 'b' references the same list as 'a'
a.append(4)  # Modifies the original list
print(a, b)  # Output: [1, 2, 3, 4] [1, 2, 3, 4]
```

**Copying Mutable Objects:**
- **Shallow Copy:** Creates a new object but does not create copies of nested objects; instead, it copies references to them.
  ```python
  import copy
  list1 = [[1, 2], [3, 4]]
  list2 = copy.copy(list1)
  list1[0][0] = 'a'
  print(list1, list2)  # Output: [['a', 2], [3, 4]] [['a', 2], [3, 4]]
  ```

- **Deep Copy:** Creates a new object and recursively copies all objects nested within it.
  ```python
  import copy
  list1 = [[1, 2], [3, 4]]
  list2 = copy.deepcopy(list1)
  list1[0][0] = 'a'
  print(list1, list2)  # Output: [['a', 2], [3, 4]] [[1, 2], [3, 4]]
  ```
