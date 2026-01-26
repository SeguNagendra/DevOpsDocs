---
sidebar_position: 6
---

<!-- ## File Handling -->

### 1. File Handling in Python

Python allows you to create, read, write, and delete files using built-in functions.

#### Opening a File

```python
file = open("example.txt", "r")  # modes: 'r', 'w', 'a', 'x'
print(file.read())
file.close()
```

#### Reading a File

```python
file = open("example.txt", "r")
print(file.readline())  # Read first line
for line in file:
    print(line)
file.close()
```

#### Writing to a File

```python
file = open("example.txt", "w")
file.write("Hello, World!\n")
file.write("Welcome to Python.")
file.close()
```

#### Using `with` Statement (Best Practice)

```python
with open("example.txt", "r") as file:
    content = file.read()
    print(content)

# File is automatically closed
```

#### Appending to a File

```python
with open("example.txt", "a") as file:
    file.write("\nAppended line.")
```
---

### 1. Automating File Operations

Python's built-in `os` and `shutil` modules allow automation of file and directory tasks.

```python
import os, shutil

# Create directory
os.mkdir("new_folder")

# Rename a file
os.rename("old.txt", "new.txt")

# Remove file or directory
os.remove("delete_me.txt")
os.rmdir("empty_folder")

# Copy file
shutil.copy("source.txt", "destination.txt")
```

---

### 2. Reading from a File

```python
with open("data.txt", "r") as file:
    content = file.read()
    print(content)
```

* `"r"` = read mode
* `with` = automatically closes the file

---

### 3. Writing to a File

```python
with open("log.txt", "w") as file:
    file.write("This is a log entry.")
```

* `"w"` = write mode (overwrites if exists)
* `"a"` = append mode (adds to existing content)

---

### 4. Working with Paths

```python
from pathlib import Path

# Create a path object
path = Path("my_folder/my_file.txt")

print(path.exists())       # Check existence
print(path.name)           # File name
print(path.suffix)         # File extension
print(path.parent)         # Parent directory
```

---

### 5. Listing Files in a Directory

```python
from pathlib import Path

folder = Path(".")
for file in folder.iterdir():
    print(file.name)
```

---

### 6. Scheduling Tasks with `schedule` Module

```python
import schedule
import time

def job():
    print("Task is running!")

schedule.every(5).seconds.do(job)

while True:
    schedule.run_pending()
    time.sleep(1)
```

---

### 7. Automating with `subprocess`

Run terminal/command-line scripts from Python.

```python
import subprocess

# Run a shell command
subprocess.run(["echo", "Hello from Python!"])
```

---

### 8. Using `glob` to Search Files

```python
import glob

files = glob.glob("*.txt")
print(files)
```

* You can use wildcards like `*` or `?` to filter file names.

---

### 9. Example: Archiving Logs Automatically

```python
import shutil
import datetime

# Create archive name with timestamp
timestamp = datetime.datetime.now().strftime("%Y%m%d-%H%M%S")
shutil.make_archive(f"logs_{timestamp}", 'zip', "./logs")
```

---

### 10. Summary

| Task            | Module         |
| --------------- | -------------- |
| File read/write | `open()`       |
| Directory ops   | `os`, `shutil` |
| Path management | `pathlib`      |
| File search     | `glob`         |
| Scheduling      | `schedule`     |
| Run commands    | `subprocess`   |

---