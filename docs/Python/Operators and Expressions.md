---
sidebar_position: 2
---

<!-- ## Operators and Expressions -->

### 1. Arithmetic Operators

Arithmetic operators allow you to perform mathematical calculations on numerical values. They work on integers, floats, and (to some extent) complex numbers. These operators can be used in equations, assignments, and expressions.

### Operators

| Operator | Meaning              | Usage                  |
|----------|----------------------|------------------------|
| +        | Addition             | Adds two operands      |
| -        | Subtraction          | Subtracts right from left operand |
| *        | Multiplication       | Multiplies operands    |
| /        | Division             | Divides left by right, returns float |
| %        | Modulus              | Divides, returns remainder |
| //       | Floor Division       | Divides, returns integer part |
| **       | Exponentiation       | Raises left to power of right |

### Practical Examples
``` python
a = 15
b = 4
print(a + b) # Output: 19
print(a - b) # Output: 11
print(a * b) # Output: 60
print(a / b) # Output: 3.75
print(a % b) # Output: 3
print(a // b) # Output: 3 (15 divided by 4 is 3.75, floor is 3)
print(a ** b) # Output: 50625 (15 to the power of 4)
```
**Note:** Division `/` always returns a float. Use `//` for integer division (flooring).

---

### 2. Comparison Operators

Comparison operators are used to compare two values. They return a boolean value: `True` or `False`. Such operators are vital in decision-making (if-else, loops).

### Operators


```python
---------------------------------------------------
| Operator | Usage     | Meaning                  |
|----------|-----------|--------------------------|
| ==       | a == b    | True if a equals b       |
| !=       | a != b    | True if a not equal b    |
| >        | a > b     | True if a greater than b |
| <        | a < b     | True if a less than b    |
| >=       | a >= b    | True if a greater/equal b|
| <=       | a <= b    | True if a less/equal b   |

a = 5
b = 10

print(a == b)  # False # True if a equals b 
print(a != b)  # True 
print(a > b)   # False
print(a < b)   # True
print(a >= b)  # False
print(a <= b)  # True
```

**Use Case - Conditional Statement:**

```python
age = int(input("Enter your age: "))
if age >= 18:
print("Adult")
else:
print("Minor")
```
---

### 3. Logical Operators

Logical operators allow combining multiple boolean conditions. They help create advanced conditional logic.

```python

| Operator | Usage        | Meaning                               |
|----------|-------------|----------------------------------------|
| and      | a and b     | True if both a and b are True          |
| or       | a or b      | True if at least one is True           |
| not      | not a       | True if a is False, False if a is True |


x = True
y = False

print(x and y)  # False
print(x or y)   # True
print(not x)    # False
```

### Practical Examples
```python
x, y = 5, 10
print(x > 3 and y < 20) # True
print(x < 3 or y < 20) # True
print(not (x == 5)) # False
```

**Chained Use:**
```python
user, pwd = "admin", "1234"
if user == "admin" and pwd == "1234":
print("Access Granted")
else:
print("Access Denied")
```
---

### 4. Assignment Operators

Used to assign values to variables.

```python

| Operator | Usage     | Equivalent Statement |
|----------|-----------|---------------------|
| =        | x = y     | x = y               |
| +=       | x += y    | x = x + y           |
| -=       | x -= y    | x = x - y           |
| *=       | x *= y    | x = x * y           |
| /=       | x /= y    | x = x / y           |
| %=       | x %= y    | x = x % y           |
| //=      | x //= y   | x = x // y          |
| **=      | x **= y   | x = x ** y          |


a = 10

# Compound assignments
a += 5  # a = a + 5
print(a)  # 15

a -= 3
print(a)  # 12

a *= 2
print(a)  # 24

a /= 4
print(a)  # 6.0
```
### Practical Examples
```python
score = 50
score += 10 # score now 60
score -= 20 # score now 40
score *= 2 # score now 80
score /= 4 # score now 20.0
score %= 7 # score now 6.0
```

**Compound Use:**
```python
counter = 1
for i in range(4):
counter *= 2
print(counter) # 16
```
---

### 5. Bitwise Operators

Operate on binary representations.
Bitwise operators operate on the **binary representations** of integers. Common in low-level programming, optimization, and some mathematical tasks.

```python

| Operator | Symbol | Example | Effect             |
|----------|--------|---------|--------------------|
| AND      | &      | a & b   | 1 if bits in both  |
| OR       | \|     | a \| b  | 1 if in either     |
| XOR      | ^      | a ^ b   | 1 if in only one   |
| NOT      | ~      | ~a      | invert bits        |
| Left shift | <<   | a << n  | shift bits left n  |
| Right shift| >>   | a >> n  | shift bits right n |

a = 5    # 0b0101
b = 3    # 0b0011

print(a & b)  # AND -> 1
print(a | b)  # OR  -> 7
print(a ^ b)  # XOR -> 6
print(~a)     # NOT -> -6
print(a << 1) # Left shift -> 10
print(a >> 1) # Right shift -> 2
```

### Practical Examples
```python
a = 5 # 0b0101
b = 3 # 0b0011
print(a & b) # 1 (0b0001)
print(a | b) # 7 (0b0111)
print(a ^ b) # 6 (0b0110)
print(~a) # -6 (inverts: -(a+1))
print(a << 2) # 20 (shift left 2 bits: 0b010100)
print(b >> 1) # 1 (0b0001)
```
**Use Case - Masking:**
```python
pixel = 0b11100101
mask = 0b00001111
result = pixel & mask # Extract lower 4 bits
print(bin(result)) # 0b00000101
```

---

### 6. Identity and Membership Operators

**Identity:**

```python
Check if two variables reference the **same object** in memory (not just equal content).

| Operator | Usage    | Meaning           |
|----------|----------|-------------------|
| is       | a is b   | True if same obj  |
| is not   | a is not b| True if not same obj |

a = [1, 2, 3]
b = a
c = [1, 2, 3]

print(a is b)   # True
print(a is c)   # False
```

**Membership:**

```python
fruits = ["apple", "banana"]

print("apple" in fruits)     # True
print("cherry" not in fruits) # True
```

---

## 7. Type Casting

### Theory
Type casting allows you to convert a variable from one data type to another. Essential for working with mixed data types (e.g., getting numbers from user input, which is always string).

| Function | Converts to | Example           |
|----------|-------------|------------------|
| int()    | integer     | int("42")        |
| float()  | float       | float("3.14")    |
| str()    | string      | str(3.14)        |
| bool()   | boolean     | bool(1), bool("")|
| list()   | list        | list("abc")      |
| tuple()  | tuple       | tuple([1,2,3])   |
| set()    | set         | set("apple")     |

### Practical Examples
```python
String to int and float
num1 = "100"
print(int(num1) + 1) # 101

num2 = "3.14159"
print(float(num2) * 2) # 6.28318

Int/float to string
price = 45.99
print("Price: " + str(price)) # "Price: 45.99"

List to tuple
colors = ["red", "green", "blue"]
tup = tuple(colors)
print(tup) # ('red', 'green', 'blue')

Sequence to set (removes duplicates)
letters = "banana"
print(set(letters)) # {'b', 'a', 'n'}

Boolean conversion
print(bool(0)) # False
print(bool("abc")) # True
print(bool("")) # False

Input conversion
age = int(input("Enter your age: ")) # Converts input to integer
```

**Note:** Invalid type conversion (e.g., `int("abc")`) raises a `ValueError`.

---