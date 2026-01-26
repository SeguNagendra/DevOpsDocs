---
sidebar_position: 8
---

<!-- ## Object-Oriented Programming (OOP) -->

### 1. Introduction to OOP

OOP is a programming paradigm based on the concept of "objects", which can contain data (attributes) and code (methods).

### 2. Classes and Objects

#### Defining a Class

```python
class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age

    def greet(self):
        print(f"Hello, my name is {self.name} and I am {self.age} years old.")
```

#### Creating an Object

```python
p1 = Person("Alice", 25)
p1.greet()  # Output: Hello, my name is Alice and I am 25 years old.
```

---

### 3. `__init__` Method

`__init__` is the constructor method called when an object is created. It initializes the object’s attributes.

---

### 4. Inheritance

Inheritance allows a class to inherit attributes and methods from another class.

```python
class Employee(Person):
    def __init__(self, name, age, job):
        super().__init__(name, age)
        self.job = job

    def show_job(self):
        print(f"I work as a {self.job}.")

emp1 = Employee("Bob", 30, "Engineer")
emp1.greet()
emp1.show_job()
```

---

### 5. Method Overriding

A subclass can override a method from its parent class.

```python
class Dog:
    def sound(self):
        print("Bark")

class Cat(Dog):
    def sound(self):
        print("Meow")

c = Cat()
c.sound()  # Output: Meow
```

---

### 6. Encapsulation

Encapsulation is the bundling of data and methods that operate on that data.

#### Private Variables

```python
class BankAccount:
    def __init__(self, balance):
        self.__balance = balance  # private attribute

    def deposit(self, amount):
        self.__balance += amount

    def get_balance(self):
        return self.__balance

acc = BankAccount(1000)
acc.deposit(500)
print(acc.get_balance())  # Output: 1500
```

---

### 7. Polymorphism

Polymorphism allows functions or methods to behave differently based on the object.

```python
class Bird:
    def fly(self):
        print("Bird can fly")

class Penguin(Bird):
    def fly(self):
        print("Penguins can't fly")

def flying_test(bird):
    bird.fly()

flying_test(Bird())      # Output: Bird can fly
flying_test(Penguin())   # Output: Penguins can't fly
```

---
