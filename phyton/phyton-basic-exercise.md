
### **Practical Exercise**

**Objective:**
- Write a Python program that prompts the user to enter two numbers and then prints the result of each arithmetic operation (addition, subtraction, multiplication, division, modulus, exponentiation) on these numbers.

**Exercise:**
```python
# Getting input from the user
num1 = float(input("Enter the first number: "))
num2 = float(input("Enter the second number: "))

# Performing arithmetic operations
sum_result = num1 + num2
sub_result = num1 - num2
mul_result = num1 * num2
div_result = num1 / num2
mod_result = num1 % num2
exp_result = num1 ** num2

# Displaying the results
print(f"Sum: {sum_result}")
print(f"Subtraction: {sub_result}")
print(f"Multiplication: {mul_result}")
print(f"Division: {div_result}")
print(f"Modulus: {mod_result}")
print(f"Exponentiation: {exp_result}")
```

**Expected Output:**
```
Enter the first number: 5
Enter the second number: 3
Sum: 8.0
Subtraction: 2.0
Multiplication: 15.0
Division: 1.6666666666666667
Modulus: 2.0
Exponentiation: 125.0
```