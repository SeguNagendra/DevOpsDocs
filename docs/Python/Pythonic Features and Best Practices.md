---
sidebar_position: 12
---

<!-- ## Pythonic Features and Best Practices -->

### 1. List Comprehensions

A concise way to create lists.

```python
# Traditional way
squares = []
for i in range(5):
    squares.append(i * i)

# Pythonic way
squares = [i * i for i in range(5)]
```

---

### 2. Dictionary Comprehensions

```python
squares = {x: x*x for x in range(5)}
print(squares)  # {0: 0, 1: 1, 2: 4, 3: 9, 4: 16}
```

---

### 3. Unpacking

Extract multiple values at once.

```python
name, age = ("Alice", 25)
print(name, age)
```

Unpacking in loops:

```python
pairs = [(1, 'one'), (2, 'two')]
for num, word in pairs:
    print(num, word)
```

---

### 4. Enumerate

Use `enumerate()` to loop with index and value.

```python
colors = ['red', 'green', 'blue']
for index, color in enumerate(colors):
    print(index, color)
```

---

### 5. Zip

Combine two lists together:

```python
names = ['Alice', 'Bob']
ages = [25, 30]
for name, age in zip(names, ages):
    print(name, age)
```

---

### 6. Using `any()` and `all()`

```python
nums = [1, 2, 3]
print(all(n > 0 for n in nums))  # True
print(any(n > 2 for n in nums))  # True
```

---

### 7. Chaining Comparisons

```python
x = 15
if 10 < x < 20:
    print("x is between 10 and 20")
```

---

### 8. Context Managers (with statement)

Automatically handles file closing.

```python
with open('sample.txt', 'r') as file:
    data = file.read()
```

---

### 9. Using `_` for Ignored Values

```python
for _ in range(3):
    print("Hello")
```

---

### 10. Ternary Conditional Expressions

```python
age = 20
status = "Adult" if age >= 18 else "Minor"
print(status)
```

---

### 11. Using `is` vs `==`

* `is` checks identity (same object in memory)
* `==` checks value equality

```python
x = [1, 2]
y = x
z = [1, 2]

print(x is y)  # True
print(x == z)  # True
print(x is z)  # False
```

---

### 12. Use Docstrings

Document your functions properly.

```python
def greet(name):
    """Return a greeting message."""
    return f"Hello, {name}!"
```

---

### 13. Idiomatic Python Style (PEP 8)

* Use `snake_case` for variables and functions
* Use 4 spaces for indentation
* Add whitespace around operators
* Keep lines under 79 characters

---

### 14. Avoid Unused Imports and Variables

Keep your code clean and readable.

---
