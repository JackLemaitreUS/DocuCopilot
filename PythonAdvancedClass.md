```python

from abc import ABC, abstractmethod
from collections import namedtuple
from dataclasses import dataclass

# 1. Abstract Base Class
class Vehicle(ABC):
    """
    Abstract Base Class representing a Vehicle.
    Forces subclasses to implement the 'move' method.
    """
    @abstractmethod
    def move(self):
        """Abstract method to be implemented by subclasses."""
        pass

class Car(Vehicle):
    """Represents a Car, a type of Vehicle."""
    def move(self):
        return "The car drives on the road"

class Boat(Vehicle):
    """Represents a Boat, a type of Vehicle."""
    def move(self):
        return "The boat sails in the water"

# 2. Metaclass Usage
class MetaSingleton(type):
    """
    Metaclass implementing Singleton Pattern.
    Ensures only one instance of a class exists.
    """
    _instances = {}
    def __call__(cls, *args, **kwargs):
        if cls not in cls._instances:
            cls._instances[cls] = super().__call__(*args, **kwargs)
        return cls._instances[cls]

class Singleton(metaclass=MetaSingleton):
    """Class using Singleton metaclass to restrict multiple instances."""
    def __init__(self, value):
        self.value = value

# 3. Operator Overloading
class Vector:
    """
    A simple 2D Vector class with operator overloading.
    Allows vector addition using '+' operator.
    """
    def __init__(self, x, y):
        self.x, self.y = x, y

    def __add__(self, other):
        return Vector(self.x + other.x, self.y + other.y)

    def __str__(self):
        return f"Vector({self.x}, {self.y})"

# 4. Descriptor Class
class Celsius:
    """
    Descriptor class controlling access to Temperature attributes.
    """
    def __get__(self, instance, owner):
        return instance._temp

    def __set__(self, instance, value):
        instance._temp = value

class Temperature:
    """
    Class using Celsius descriptor to manage temperature attributes.
    """
    celsius = Celsius()
    def __init__(self, temp):
        self._temp = temp

# 5. Property Decorator
class Person:
    """
    Class demonstrating the use of property decorators.
    Prevents invalid age assignment.
    """
    def __init__(self, name, age):
        self._age = age
        self.name = name

    @property
    def age(self):
        """Getter method for age."""
        return self._age

    @age.setter
    def age(self, value):
        """Setter method for age, ensuring non-negative values."""
        if value < 0:
            raise ValueError("Age cannot be negative")
        self._age = value

# 6. Context Manager
class FileManager:
    """
    Custom context manager for handling file operations.
    Ensures proper opening and closing of files.
    """
    def __init__(self, filename, mode):
        self.filename = filename
        self.mode = mode

    def __enter__(self):
        self.file = open(self.filename, self.mode)
        return self.file

    def __exit__(self, exc_type, exc_value, traceback):
        self.file.close()

# 7. Multiple Inheritance
class A:
    """Class A providing a greeting method."""
    def greet(self):
        return "Hello from A"

class B:
    """Class B providing a greeting method."""
    def greet(self):
        return "Hello from B"

class C(A, B):
    """Class C inheriting from A and B, following Method Resolution Order (MRO)."""
    pass

# 8. NamedTuple
PersonNT = namedtuple("PersonNT", ["name", "age"])
"""
NamedTuple representing a lightweight, immutable object.
Provides structured data representation without full class overhead.
"""

# 9. Data Classes
@dataclass
class User:
    """
    Data class to simplify object creation.
    Automatically generates __init__, __repr__, and __eq__ methods.
    """
    id: int
    name: str
    active: bool = True

# 10. Slots to Save Memory
class Efficient:
    """
    Class using __slots__ to reduce memory usage.
    Prevents creation of unnecessary attribute dictionary (__dict__).
    """
    __slots__ = ["name", "age"]
    def __init__(self, name, age):
        self.name = name
        self.age = age

# Example Usage
car = Car()
boat = Boat()
singleton1 = Singleton(42)
singleton2 = Singleton(99)
v1, v2 = Vector(2, 3), Vector(4, 1)
t = Temperature(25)
p = Person("Alice", 30)
c = C()
person_named = PersonNT(name="Bob", age=25)
user1 = User(1, "John")
e = Efficient("Charlie", 40)

# Print results
print(car.move()) # The car drives on the road
print(boat.move()) # The boat sails in the water
print(singleton1.value, singleton2.value) # 42, 42 (Singleton pattern)
print(v1 + v2) # Vector(6, 4) (Operator overloading)
t.celsius = 30
print(t.celsius) # 30 (Descriptor)
print(p.age) # 30 (Property)
print(c.greet()) # Hello from A (MRO)
print(person_named.name, person_named.age) # Bob 25 (NamedTuple)
print(user1) # User(id=1, name='John', active=True) (DataClass)
print(e.name) # Charlie (Slots)

```
