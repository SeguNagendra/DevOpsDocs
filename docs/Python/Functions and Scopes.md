---
sidebar_position: 5
---

## Functions and Scope

### 1. Defining Functions

Functions are blocks of reusable code. Use the `def` keyword to define them.

```python
def greet():
    print("Hello, World!")

greet()  # Calling the function
```

---

### 2. Function Parameters and Arguments

Functions can accept parameters (inputs).

```python
def greet(name):
    print(f"Hello, {name}!")

greet("Alice")
```

**Types of Arguments:**

* Positional arguments
* Keyword arguments
* Default arguments
* Variable-length arguments

```python
def add(a, b=5):
    return a + b

print(add(3))         # Uses default b = 5
print(add(3, 2))      # Overrides default

# Variable-length

def print_all(*args):
    for val in args:
        print(val)

print_all(1, 2, 3, 4)
```

---

### 3. Return Statement

Functions can return values using `return`.

```python
def add(x, y):
    return x + y

result = add(3, 5)
print(result)
```

---

### 4. Scope of Variables

Scope determines where a variable can be accessed.

**Types of Scope:**

* **Local:** Defined inside a function
* **Global:** Defined outside any function

```python
global_var = "I am global"

def my_function():
    local_var = "I am local"
    print(global_var)  # Accessible
    print(local_var)   # Accessible only inside

my_function()
# print(local_var)  # Error: not defined outside
```

To modify a global variable inside a function, use `global`:

```python
count = 0

def increment():
    global count
    count += 1

increment()
print(count)
```

---

### 5. Lambda Functions

Short anonymous functions created with `lambda`.

```python
square = lambda x: x * x
print(square(5))  # 25

add = lambda a, b: a + b
print(add(3, 4))   # 7
```

Often used in functions like `map()`, `filter()`, and `sorted()`.

```python
nums = [1, 2, 3, 4, 5]
evens = list(filter(lambda x: x % 2 == 0, nums))
print(evens)  # [2, 4]
```

---

### 6. Recursion

A function calling itself is recursion.

```python
def factorial(n):
    if n == 1:
        return 1
    else:
        return n * factorial(n-1)

print(factorial(5))  # 120
```

Be careful of infinite recursion. Always include a base case.

---

### 7. `*args` and `**kwargs`

Used to pass variable number of arguments.

```python
def show_args(*args):
    for arg in args:
        print(arg)

show_args(1, 2, 3)

# kwargs: keyword arguments as dictionary

def show_kwargs(**kwargs):
    for key, value in kwargs.items():
        print(f"{key} = {value}")

show_kwargs(name="Alice", age=30)
```

---