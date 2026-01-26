---
sidebar_position: 10
---

<!-- ## Modules and Packages -->

### 1. What is a Module?

A module is a file containing Python code (.py) that can define functions, classes, and variables.

#### Creating a Module

**file: `my_module.py`**

```python
def add(a, b):
    return a + b
```

**Usage:**

```python
import my_module
print(my_module.add(2, 3))  # Output: 5
```

---

### 2. `import`, `from`, `as` Keywords

* `import`: Brings the whole module.
* `from ... import`: Brings specific attributes.
* `as`: Alias a module or function.

```python
import math
print(math.sqrt(16))  # 4.0

from math import pi
print(pi)  # 3.141592...

import math as m
print(m.factorial(5))  # 120
```

---

### 3. Built-in Modules

Python comes with several built-in modules.

Examples:

* `math`
* `datetime`
* `os`
* `random`

```python
import random
print(random.randint(1, 10))
```

---

### 4. Creating Packages

A package is a directory containing multiple modules and a special `__init__.py` file.

**Structure:**

```
my_package/
├── __init__.py
├── math_utils.py
└── string_utils.py
```

#### Accessing a Module from a Package

```python
from my_package import math_utils
math_utils.add(2, 3)
```

---

### 5. Using `__name__ == "__main__"`

This allows a module to be both imported and run as a standalone script.

```python
def greet():
    print("Hello!")

if __name__ == "__main__":
    greet()
```

---

### 6. The `dir()` Function

Lists all attributes and methods of an object or module.

```python
import math
print(dir(math))
```

---

### 7. Installing External Packages

Use `pip` to install external libraries.

```bash
pip install requests
```

Usage:

```python
import requests
response = requests.get("https://api.github.com")
print(response.status_code)
```

---
