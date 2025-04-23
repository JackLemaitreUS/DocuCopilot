```python
from abc import ABC, abstractmethod
from collections import namedtuple
from dataclasses import dataclass

# 1. Abstract Base Class
class Vehicle(ABC):
    @abstractmethod
    def move(self):
        pass

class Car(Vehicle):
    def move(self):
        return "The car drives on the road"

class Boat(Vehicle):
    def move(self):
        return "The boat sails in the water"

# 2. Metaclass Usage
class MetaSingleton(type):
    _instances = {}
    def __call__(cls, *args, **kwargs):
        if cls not in cls._instances:
            cls._instances[cls] = super().__call__(*args, **kwargs)
        return cls._instances[cls]

class Singleton(metaclass=MetaSingleton):
    def __init__(self, value):
        self.value = value

# 3. Operator Overloading
class Vector:
    def __init__(self, x, y):
        self.x, self.y = x, y

    def __add__(self, other):
        return Vector(self.x + other.x, self.y + other.y)

    def __str__(self):
        return f"Vector({self.x}, {self.y})"

# 4. Descriptor Class
class Celsius:
    def __get__(self, instance, owner):
        return instance._temp

    def __set__(self, instance, value):
        instance._temp = value

class Temperature:
    celsius = Celsius()
    def __init__(self, temp):
        self._temp = temp

# 5. Property Decorator
class Person:
    def __init__(self, name, age):
        self._age = age
        self.name = name

    @property
    def age(self):
        return self._age

    @age.setter
    def age(self, value):
        if value < 0:
            raise ValueError("Age cannot be negative")
        self._age = value

# 6. Context Manager
class FileManager:
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
    def greet(self):
        return "Hello from A"

class B:
    def greet(self):
        return "Hello from B"

class C(A, B):
    pass

# 8. NamedTuple
PersonNT = namedtuple("PersonNT", ["name", "age"])

# 9. Data Classes
@dataclass
class User:
    id: int
    name: str
    active: bool = True

# 10. Slots to Save Memory
class Efficient:
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
