---
sidebar_position: 7
---

<!-- ## Error Handling -->

### 1. Why Handle Errors?

Errors (a.k.a. exceptions) can crash your program. Error handling helps:

* Prevent crashes
* Show meaningful error messages
* Handle expected issues (e.g., file not found)

---

### 2. Try-Except Block

```python
try:
    x = 10 / 0
except ZeroDivisionError:
    print("Cannot divide by zero!")
```

* `try`: the block where you expect an error
* `except`: handles the specific error

---

### 3. Catching Multiple Exceptions

```python
try:
    value = int("abc")
except (ValueError, TypeError) as e:
    print("Error:", e)
```

---

### 4. Generic Exception Catch

```python
try:
    # some risky code
except Exception as e:
    print("Something went wrong:", e)
```

> Use this sparingly — it hides all error types!

---

### 5. Else Clause

```python
try:
    print("Hello")
except:
    print("Error occurred")
else:
    print("No error occurred")
```

---

### 6. Finally Clause

```python
try:
    file = open("myfile.txt")
except:
    print("File error")
finally:
    print("Cleanup actions (always runs)")
```

* `finally` always runs — good for cleanup (like closing files).

---

### 7. Raising Exceptions

```python
def divide(a, b):
    if b == 0:
        raise ValueError("b cannot be zero")
    return a / b
```

* Use `raise` to trigger exceptions manually.

---

### 8. Creating Custom Exceptions

```python
class MyError(Exception):
    pass

raise MyError("Something custom went wrong")
```

* Helps define domain-specific problems clearly.

---

### 9. Real-World Example

```python
try:
    with open("data.txt") as file:
        data = file.read()
except FileNotFoundError:
    print("The file was not found!")
```

---

### 10. Summary

| Keyword | Description           |
| ------- | --------------------- |
| try     | Wrap risky code       |
| except  | Handle exceptions     |
| else    | Runs if no error      |
| finally | Always runs           |
| raise   | Manually raise errors |

---