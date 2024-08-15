## **Object-Oriented Programming (OOP) in Python**

---

### **1 Introduction to Object-Oriented Programming (OOP)**

**Overview:**
Object-Oriented Programming (OOP) is a programming paradigm that uses objects and classes to structure software programs. OOP allows for the creation of reusable code, easier maintenance, and better organization of large codebases.

**Key Concepts of OOP:**
- **Class:** A blueprint for creating objects (a particular data structure), with attributes (data) and methods (functions) that define the behavior of the objects.
- **Object:** An instance of a class. Objects can have attributes and methods, which are defined by the class.
- **Encapsulation:** The bundling of data and methods that operate on that data within one unit, such as a class, and restricting access to some of the object's components.
- **Inheritance:** A mechanism for creating a new class that is based on an existing class, inheriting its attributes and methods.
- **Polymorphism:** The ability to present the same interface for different data types, allowing objects of different classes to be treated as objects of a common superclass.
- **Abstraction:** The concept of hiding the complex implementation details and showing only the essential features of an object.

---

### **2 Classes and Objects**

**1. Defining a Class:**
- **Syntax:** The `class` keyword is used to define a new class.
- **Example:**
  ```python
  class Dog:
      def __init__(self, name, breed):
          self.name = name
          self.breed = breed
      
      def bark(self):
          return f"{self.name} says woof!"
  ```
  - **`__init__` method:** The constructor method that initializes the object’s attributes.
  - **`self`:** Refers to the instance of the class itself and is used to access variables that belong to the class.

**2. Creating Objects:**
- **Instantiation:** Creating an object from a class.
- **Example:**
  ```python
  my_dog = Dog("Rex", "German Shepherd")
  print(my_dog.bark())  # Output: Rex says woof!
  ```

**3. Attributes and Methods:**
- **Attributes:** Variables that belong to an object.
  ```python
  print(my_dog.name)  # Output: Rex
  print(my_dog.breed)  # Output: German Shepherd
  ```
- **Methods:** Functions that belong to an object.
  ```python
  print(my_dog.bark())  # Output: Rex says woof!
  ```

---

### **3 Inheritance**

**1. Basic Inheritance:**
- **Purpose:** Allows a new class (child class) to inherit attributes and methods from an existing class (parent class).
- **Example:**
  ```python
  class Animal:
      def __init__(self, name):
          self.name = name
      
      def speak(self):
          return f"{self.name} makes a sound"

  class Dog(Animal):
      def speak(self):
          return f"{self.name} barks"

  my_dog = Dog("Rex")
  print(my_dog.speak())  # Output: Rex barks
  ```

**2. Overriding Methods:**
- **Explanation:** A child class can override a method from the parent class.
- **Example:**
  ```python
  class Cat(Animal):
      def speak(self):
          return f"{self.name} meows"

  my_cat = Cat("Whiskers")
  print(my_cat.speak())  # Output: Whiskers meows
  ```

**3. Using `super()`:**
- **Purpose:** The `super()` function is used to call a method from the parent class.
- **Example:**
  ```python
  class Puppy(Dog):
      def __init__(self, name, breed, age):
          super().__init__(name, breed)
          self.age = age
      
      def speak(self):
          return super().speak() + " in a cute way"
  
  my_puppy = Puppy("Buddy", "Golden Retriever", 1)
  print(my_puppy.speak())  # Output: Buddy barks in a cute way
  ```

---

### **4 Encapsulation**

**1. Public, Protected, and Private Attributes:**
- **Public:** Attributes and methods that are accessible from anywhere (e.g., `self.name`).
- **Protected:** Attributes and methods that should not be accessed directly outside the class but can be accessed in derived classes (e.g., `_name`).
- **Private:** Attributes and methods that cannot be accessed directly outside the class (e.g., `__name`).
- **Example:**
  ```python
  class Person:
      def __init__(self, name, age):
          self.name = name  # Public
          self._age = age   # Protected
          self.__salary = 50000  # Private
      
      def get_salary(self):
          return self.__salary

  john = Person("John", 30)
  print(john.name)  # Output: John
  print(john._age)  # Output: 30
  print(john.get_salary())  # Output: 50000
  ```

**2. Getter and Setter Methods:**
- **Purpose:** Encapsulation can be enforced by using getter and setter methods to control access to private attributes.
- **Example:**
  ```python
  class Employee:
      def __init__(self, name, salary):
          self.name = name
          self.__salary = salary
      
      def get_salary(self):
          return self.__salary
      
      def set_salary(self, salary):
          if salary > 0:
              self.__salary = salary

  emp = Employee("Alice", 60000)
  print(emp.get_salary())  # Output: 60000
  emp.set_salary(70000)
  print(emp.get_salary())  # Output: 70000
  ```

---

### **5 Polymorphism**

**1. Method Overloading (Not natively supported in Python):**
- **Explanation:** Python does not support method overloading (i.e., multiple methods with the same name but different parameters). However, you can use default arguments or `*args` and `**kwargs` to simulate this behavior.
- **Example:**
  ```python
  class MathOperations:
      def add(self, a, b, c=None):
          if c:
              return a + b + c
          else:
              return a + b

  math = MathOperations()
  print(math.add(10, 20))  # Output: 30
  print(math.add(10, 20, 30))  # Output: 60
  ```

**2. Method Overriding:**
- **Explanation:** Method overriding occurs when a child class provides a specific implementation of a method that is already defined in its parent class.
- **Example:**
  ```python
  class Shape:
      def area(self):
          return 0

  class Rectangle(Shape):
      def __init__(self, width, height):
          self.width = width
          self.height = height
      
      def area(self):
          return self.width * self.height

  rect = Rectangle(5, 10)
  print(rect.area())  # Output: 50
  ```

**3. Polymorphism with Functions and Objects:**
- **Explanation:** Polymorphism allows objects of different classes to be treated as objects of a common superclass. The same operation can behave differently on different classes.
- **Example:**
  ```python
  class Cat(Animal):
      def speak(self):
          return f"{self.name} meows"

  class Dog(Animal):
      def speak(self):
          return f"{self.name} barks"

  def animal_sound(animal):
      print(animal.speak())

  cat = Cat("Kitty")
  dog = Dog("Rex")

  animal_sound(cat)  # Output: Kitty meows
  animal_sound(dog)  # Output: Rex barks
  ```

---

### **6 Abstraction**

**1. Abstract Classes and Methods:**
- **Explanation:** Abstraction is used to hide the internal implementation of a function or class and only show the relevant functionality. In Python, abstraction can be achieved using abstract classes and methods with the help of the `abc` module.
- **Example:**
  ```python
  from abc import ABC, abstractmethod

  class Animal(ABC):
      @abstractmethod
      def sound(self):
          pass

  class Dog(Animal):
      def sound(self):
          return "Bark"

  class Cat(Animal):
      def sound(self):
          return "Meow"

  # animal = Animal()  # This will raise an error
  dog = Dog()
  print(dog.sound())  # Output: Bark
  ```

---

### **7 Dunder (Magic) Methods**

**1. Common Dunder Methods:**
- **`__init__(self, ...)`:** The constructor method for initializing objects.
- **`__str__(self)`:** Defines the string representation of an object (used by `print()`).
- **`__repr__(self)`:** Defines the unambiguous representation of an object (used by `repr()`).
- **`__len__(self)`:** Defines the behavior of `len()` when called on an object.
- **`__add__(self, other)`:** Defines the behavior of the `+` operator for the object.
- **Example:**
  ```python
  class Book:
      def __init