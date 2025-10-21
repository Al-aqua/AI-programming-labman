# Lab 1: Python Fundamentals & Data Types

## Objectives

- Master basic Python programming concepts
  - Variable declaration and data types (int, float, string, bool)
  - Control structures (if/else statements, loops)
  - Functions and basic syntax
- Write scripts demonstrating loops and conditional logic
- Build foundational skills for AI programming in Python

## Tools and Resources

- **Tools**
  - [Python](https://www.python.org/)
  - [Jupyter Notebook](https://jupyter.org/) or [Visual Studio Code](https://code.visualstudio.com/)

- **Resources**
  - [Python Documentation](https://docs.python.org/3/)
  - [Python Tutor](https://pythontutor.com/)
  - [Python Crash Course](https://ehmatthes.github.io/pcc_3e/)
  - [Real Python Tutorials](https://realpython.com/)

## Content

### 1. Variables and Data Types

Variables store information that your program can use and modify. Python supports several fundamental data types that are essential for AI programming.

#### 1.1 Code Example

```python
# Integer data type
age = 25
count = 100

# Float data type
temperature = 37.5
price = 99.99

# String data type
name = "Ahmed"
message = "Welcome to AI Programming"

# Boolean data type
is_active = True
has_error = False

# Printing variables
print(f"Name: {name}, Age: {age}")
print(f"Temperature: {temperature}°C")
print(f"Is Active: {is_active}")
```

**Explanation:**

- `int`: Whole numbers (positive, negative, or zero)
- `float`: Decimal numbers for precise calculations
- `str`: Text data enclosed in quotes
- `bool`: True or False values used in conditions

#### 1.2 Exercise

Create a script that:

1. Declares variables for a person's name, age, height (in meters), and whether they are a student
2. Print all variables using f-strings
3. Calculate and print the person's age in months
4. Check if the person is old enough to vote (18+ years)

---

### 2. Conditional Statements (if/elif/else)

Conditional statements allow your program to make decisions and execute different code based on conditions.

#### 2.1 Code Example

```python
# Simple if statement
score = 85

if score >= 90:
    print("Grade: A")
elif score >= 80:
    print("Grade: B")
elif score >= 70:
    print("Grade: C")
else:
    print("Grade: F")

# Using logical operators
age = 20
has_license = True

if age >= 18 and has_license:
    print("You can drive")
elif age >= 18:
    print("You need a license")
else:
    print("You must be 18 to drive")

# Nested conditions
temperature = 35

if temperature > 30:
    print("It's hot")
    if temperature > 40:
        print("It's extremely hot!")
else:
    print("It's cool")
```

**Explanation:**

- `if`: Executes code if condition is True
- `elif`: Checks another condition if previous is False
- `else`: Executes if all conditions are False
- `and`, `or`, `not`: Logical operators to combine conditions

#### 2.2 Exercise

Write a program that:

1. Takes a student's score (0-100) as input
2. Assigns and prints the corresponding grade (A: 90+, B: 80-89, C: 70-79, D: 60-69, F: <60)
3. Prints motivational messages based on performance:
   - If A or B: "Excellent work!"
   - If C: "Good effort, keep improving"
   - If D or F: "Please see your instructor"

---

### 3. Loops (for and while)

Loops allow you to repeat code multiple times, essential for processing datasets in AI.

#### 3.1 Code Example

```python
# For loop with range
print("Counting from 1 to 5:")
for i in range(1, 6):
    print(i)

# For loop with list
fruits = ["apple", "banana", "orange", "mango"]
for fruit in fruits:
    print(f"I like {fruit}")

# While loop
count = 0
while count < 5:
    print(f"Count: {count}")
    count += 1

# Loop with break and continue
for i in range(1, 11):
    if i == 5:
        continue  # Skip 5
    if i == 8:
        break  # Stop at 8
    print(i)

# Nested loops (multiplication table)
for i in range(1, 4):
    for j in range(1, 4):
        print(f"{i} × {j} = {i*j}", end="  ")
    print()
```

**Explanation:**

- `for`: Iterates over a sequence (range, list, string)
- `while`: Repeats while condition is True
- `break`: Exits the loop immediately
- `continue`: Skips current iteration
- `range(start, end)`: Generates numbers from start to end-1

#### 3.2 Exercise

Write a program that:

1. Reads 5 numbers from the user using a loop
2. Calculates and prints the sum, average, maximum, and minimum
3. Uses nested loops to create a pattern (e.g., pyramid of asterisks)
4. Implements loop control (break/continue) appropriately

---

### 4. Functions

Functions are reusable blocks of code that perform specific tasks, crucial for organizing AI code.

#### 4.1 Code Example

```python
# Simple function
def greet(name):
    return f"Hello, {name}!"

result = greet("Alice")
print(result)

# Function with multiple parameters
def add(a, b):
    return a + b

sum_result = add(10, 20)
print(f"Sum: {sum_result}")

# Function with default parameters
def power(base, exponent=2):
    return base ** exponent

print(power(5))       # Uses default exponent=2
print(power(5, 3))    # Uses exponent=3

# Function with multiple return values
def get_min_max(numbers):
    return min(numbers), max(numbers)

min_val, max_val = get_min_max([5, 2, 8, 1, 9])
print(f"Min: {min_val}, Max: {max_val}")

# Function with no return (performs action)
def print_separator():
    print("-" * 30)

print_separator()

# Function with *args (variable arguments)
def calculate_average(*numbers):
    if len(numbers) == 0:
        return 0
    return sum(numbers) / len(numbers)

avg = calculate_average(10, 20, 30, 40)
print(f"Average: {avg}")
```

**Explanation:**

- `def`: Defines a function
- `return`: Sends value back to caller
- Parameters can have default values
- `*args`: Allows function to accept variable number of arguments
- Functions improve code reusability and organization

#### 4.2 Exercise

Create a program with functions that:

1. `calculate_grade(score)`: Takes a score and returns letter grade
2. `is_prime(number)`: Returns True if number is prime
3. `find_average(*scores)`: Calculates average of any number of scores
4. `validate_input(value, min_val, max_val)`: Checks if value is within range
5. Call each function multiple times with different inputs

---

### 5. Working with Lists

Lists store collections of data, fundamental for handling datasets in AI.

#### 5.1 Code Example

```python
# Creating lists
numbers = [1, 2, 3, 4, 5]
mixed = [1, "hello", 3.14, True]
empty = []

# Accessing elements
print(numbers[0])      # First element: 1
print(numbers[-1])     # Last element: 5
print(numbers[1:3])    # Slice: [2, 3]

# Modifying lists
numbers.append(6)      # Add to end
numbers.insert(0, 0)   # Insert at position
numbers.remove(3)      # Remove specific value
popped = numbers.pop() # Remove and return last

# List operations
print(len(numbers))         # Length
print(10 in numbers)        # Check membership
numbers_copy = numbers.copy()  # Copy list

# List comprehension
squares = [x**2 for x in range(1, 6)]
print(squares)  # [1, 4, 9, 16, 25]

# Sorting
unsorted = [5, 2, 8, 1, 9]
sorted_asc = sorted(unsorted)
print(sorted_asc)  # [1, 2, 5, 8, 9]
```

**Explanation:**

- Lists are ordered and mutable (can be changed)
- Indexing starts at 0; negative indexing counts from end
- Slicing creates sub-lists without modifying original
- List comprehensions provide concise syntax for creation

#### 5.2 Exercise

Write a program that:

1. Creates a list of 10 student scores
2. Finds and prints the highest and lowest scores
3. Calculates average using a loop
4. Uses list comprehension to create a list of passing scores (≥60)
5. Sorts scores and prints them in ascending order

---

## Summary

You now understand:

- Variable declaration and Python data types
- Conditional logic with if/elif/else
- Loop structures (for and while)
- Function definition and reusability
- List operations and manipulation

These fundamentals are essential for all AI programming tasks ahead!

## Up Next

In the next lab, you'll learn about DataFrames and Pandas, two powerful tools for working with datasets in Python.
