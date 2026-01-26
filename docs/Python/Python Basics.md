---
sidebar_position: 1
---

<!-- ## Python 🐍 Basics -->

### 1. What is Python?

Python is a high-level, interpreted programming language created by Guido van Rossum in 1991. It is known for its simplicity and readability, which makes it ideal for beginners.

### Features
- **Simple syntax** modeled after English, making it easy to learn.
- **Interpreted language**, so code runs line by line.
- **Cross-platform**: Runs on Windows, Mac, Linux.
- **Object-oriented** and supports functional programming.
- **Extensive standard library** and third-party packages.

### Where is Python Used?
- **Web development** (Django, Flask)
- **Data science & machine learning** (NumPy, Pandas, TensorFlow)
- **Scripting & automation**
- **Software development**
- **Game development**
- **Networking, cyber security, IoT**

**Example Code:**

```python
print("Hello, Python!")
```

---

### 2. Installing Python

**Steps to Install Python:**

#### Windows
1. Visit the official Python website ([python.org](https://www.python.org)).
2. Download the latest version for Windows.
3. Run the installer and check 'Add Python to PATH'.
4. Complete setup.

#### macOS
- Use the official installer or install via Homebrew:
brew install python

#### Linux
- Use the package manager:
sudo apt-get install python3

Verify installation:

```bash
python --version
```

### Setting Up the Environment
- **IDLE** comes bundled with Python.
- For enhanced coding experience, install editors like **VS Code**, **PyCharm**, or **Jupyter Notebook**.
- Use **virtual environments** (`venv`, `virtualenv`) to manage project-specific dependencies.

---

### 3. Running Python Code

You can run Python code in multiple ways:

**Using the command line:**

```bash
python script.py
```

**Using an IDE:**

* Open the IDE
* Create a `.py` file
* Write code and run it

**Using Python shell:**

```bash
python
>>> print("Hello")
```

---

### 4. Python Syntax & Indentation

Python uses indentation to define blocks of code.

**Example:**

```python
if True:
    print("This is indented")
```

* Indentation is typically 4 spaces
* No braces `{}` for code blocks

---

### 5. Variables & Constants

- **Variables** store data values. Python is dynamically typed; you don't declare types explicitly.
- **Naming Rules:**
  - Must begin with a letter or underscore (_).
  - Cannot start with a number.
  - Case-sensitive.
  - Should not use reserved keywords (e.g., `if`, `while`).

**Example: Declaring variables**

age = 25

name = "Alice"

pi = 3.14159

**Constants:** Python does not have built-in constant types, but by convention, constants are written in uppercase letters.

##### PI = 3.14159 # treated as a constant by convention
---

### 6. Data Types

**Common Data Types:**

- `int`: Integer values, e.g., `10`
- `float`: Floating-point numbers, e.g., `3.14`
- `str`: Strings (text), e.g., `"hello"`
- `bool`: Boolean, either `True` or `False`
- `NoneType`: Special type representing the absence of value, e.g., `None`

**Example:**

```python
x = 10       # int
y = 3.14     # float
name = "Bob" # str
flag = True  # bool
nothing = None  # NoneType
```

Use `type(x)` to check data type.

---

### 7. Comments

Used to document code.

**Single-line comment:**

```python
# This is a comment
```

**Multi-line comment:**

```python
"""
This is a
multi-line comment
"""
```

---

### 8. Input and Output

**Output using print():**

```python
print("Hello, World")
```

**Input using input():**

```python
name = input("Enter your name: ")
print("Hello, " + name)
```

---

