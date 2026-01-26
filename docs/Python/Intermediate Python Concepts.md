---
sidebar_position: 9
---

<!-- ## Intermediate-Level Concepts -->

### 1. Lambda Functions

Anonymous one-line functions:

```python
square = lambda x: x * x
print(square(5))  # 25
```

Used with `map()`, `filter()`, `reduce()`:

```python
nums = [1, 2, 3, 4]
squares = list(map(lambda x: x*x, nums))
print(squares)
```

---

### 2. `map()` Function

Applies a function to every item in an iterable:

```python
nums = [1, 2, 3]
result = list(map(str, nums))
print(result)  # ['1', '2', '3']
```

---

### 3. `filter()` Function

Filters items based on a function:

```python
nums = [1, 2, 3, 4]
even = list(filter(lambda x: x % 2 == 0, nums))
print(even)  # [2, 4]
```

---

### 4. `reduce()` from `functools`

Reduces iterable into a single value:

```python
from functools import reduce
nums = [1, 2, 3, 4]
sum_all = reduce(lambda x, y: x + y, nums)
print(sum_all)  # 10
```

---

### 5. Decorators (Intro)

Functions that modify behavior of other functions.

```python
def decorator_func(original_func):
    def wrapper():
        print("Wrapper executed")
        return original_func()
    return wrapper

@decorator_func
def say_hello():
    print("Hello!")

say_hello()
```

---

### 6. `*args` and `**kwargs`

Accept variable number of arguments.

```python
def example(*args, **kwargs):
    print("Positional:", args)
    print("Keyword:", kwargs)

example(1, 2, a=3, b=4)
```

---

### 7. Assertions

Used to test assumptions in code:

```python
x = 5
assert x > 0, "x must be positive"
```

---

### 8. Working with JSON

```python
import json

data = {"name": "Alice", "age": 25}

# Convert to JSON string
json_str = json.dumps(data)

# Convert back to dictionary
parsed = json.loads(json_str)
print(parsed["name"])
```

---

### 9. Virtual Environments

Create isolated Python environments:

```bash
python -m venv myenv
source myenv/bin/activate  # Linux/macOS
myenv\Scripts\activate     # Windows
```

---

### 10. Installing Packages with pip

```bash
pip install requests
```

Using installed packages:

```python
import requests
response = requests.get("https://api.github.com")
print(response.status_code)
```

---
