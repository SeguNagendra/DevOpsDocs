---
sidebar_position: 4
---

<!-- ## Data Structures -->

### 1. Lists

A list is an ordered, mutable collection.

```python
fruits = ["apple", "banana", "cherry"]
print(fruits[0])  # apple

fruits.append("orange")
print(fruits)

fruits.remove("banana")
print(fruits)
```

List slicing:

```python
print(fruits[1:])     # ['cherry', 'orange']
print(fruits[-1])     # 'orange'
```

---

### 2. Tuples

A tuple is an ordered, immutable collection.

```python
coordinates = (10, 20)
print(coordinates[0])
```

Tuples can be used for packing and unpacking:

```python
a, b = coordinates
print(a, b)
```

---

### 3. Sets

Sets are unordered collections of unique elements.

```python
unique_numbers = {1, 2, 3, 2, 1}
print(unique_numbers)  # {1, 2, 3}

unique_numbers.add(4)
unique_numbers.remove(2)
print(unique_numbers)
```

Set operations:

```python
set1 = {1, 2, 3}
set2 = {3, 4, 5}

print(set1.union(set2))       # {1, 2, 3, 4, 5}
print(set1.intersection(set2))  # {3}
```

---

### 4. Dictionaries

Dictionaries store key-value pairs.

```python
person = {
    "name": "Alice",
    "age": 30,
    "city": "New York"
}

print(person["name"])
person["age"] = 31
print(person)
```

Loop through a dictionary:

```python
for key, value in person.items():
    print(f"{key} => {value}")
```

---

### 5. List Comprehensions

A concise way to create lists.

```python
squares = [x*x for x in range(6)]
print(squares)  # [0, 1, 4, 9, 16, 25]

# With condition
evens = [x for x in range(10) if x % 2 == 0]
print(evens)
```

---
