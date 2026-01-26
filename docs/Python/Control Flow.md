---
sidebar_position: 3
---

<!-- ## Control Flow -->

### 1. if, elif, else Statements

These are used to perform different actions based on different conditions.

```python
x = 10
if x > 0:
    print("Positive")
elif x == 0:
    print("Zero")
else:
    print("Negative")
```

---

### 2. Nested Conditions

Conditions can be nested inside other conditions.

```python
x = 5
y = 10

if x < 10:
    if y > 5:
        print("x is less than 10 and y is greater than 5")
```

---

### 3. for Loops

Used to iterate over a sequence (like a list, tuple, or string).

```python
for i in range(5):
    print(i)

fruits = ["apple", "banana"]
for fruit in fruits:
    print(fruit)
```

---

### 4. while Loops

Repeatedly executes as long as the condition is true.

```python
count = 0
while count < 3:
    print("Count:", count)
    count += 1
```

---

### 5. break and continue

* `break`: Exit the loop early
* `continue`: Skip to the next iteration

```python
for i in range(5):
    if i == 3:
        break
    print(i)

for i in range(5):
    if i == 3:
        continue
    print(i)
```

---

### 6. else with Loops

`else` can be used with `for` or `while` to run a block when loop completes normally.

```python
for i in range(3):
    print(i)
else:
    print("Loop finished")
```

---

### 7. pass Statement

A placeholder for future code. Does nothing when executed.

```python
for i in range(5):
    if i == 2:
        pass  # Placeholder
    print(i)
```

---
