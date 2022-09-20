# Object Oriented Programming

It's an imperative [programming paradigm](https://en.wikipedia.org/wiki/Programming_paradigm).

Common programming paradigms include:

- imperative in which the programmer instructs the machine how to change its state,
  - procedural - which groups instructions into procedures,
  - object-oriented - which groups instructions with the part of the state they operate on,
- declarative in which the programmer merely declares properties of the desired result, but not how to compute it
  - functional - in which the desired result is declared as the value of a series of function applications,
  - logic - in which the desired result is declared as the answer to a question about a system of facts and rules,


Important OOPS concepts:
- Abstraction
- Encapsulation
- Inheritance
- Polymorphism

Noob understanding of these things - [here](https://medium.com/omarelgabrys-blog/the-story-of-object-oriented-programming-12d1901a1825) 

## OOPs Design principles

1. KISS - “Keep It Simple, Stupid”
2. DRY - “Don’t Repeat Yourself”
3. YAGNI - "You Ain't Gonna Need It"
4. SOLID - 
   - Single Responsibility Principle
   - Open/Closed Principle
   - Liskov Substitution Principle
   - Interface Segregation Principle
   - Dependency Inversion Principle
5. GRASP - General Responsibility Assignment Software Patterns
   - Information Expert
   - Creator
   - Low Coupling
   - High Cohesion
   - Controller
   - Pure Fabrication
   - Indirection
   - Polymorphism
   - Protected Variations
   - Code Smell
   - Long Method
   - Identifiers
   - Comments
   - The God Object
   - Feature Envy

Refs:
- [Ref of 1-5](https://medium.com/omarelgabrys-blog/object-oriented-analysis-and-design-design-principles-part-6-b78e2b9da023)
- [10 oops design principles](https://medium.com/javarevisited/10-oop-design-principles-you-can-learn-in-2020-f7370cccdd31)

## Design Patterns

1. Structural
2. Behavioral
3. Creational

Refs:
- [Structural, Behavioral, and Creational](https://medium.com/omarelgabrys-blog/object-oriented-analysis-and-design-design-patterns-part-7-bc9c003a0f29)
- [All design patterns](https://github.com/OmarElGabry/DesignPatterns)

## Python OOPs implimentation

**Underscores in python**
```
_name - internal use variable, does not export when `from file import *`
__name - (name mangling - avoid overriding) make attribute name `_ClassName__name_`
__name__ - (dunder methods)
```
**Private/Protected/Public attributes**
```
Public (objs, children, anyone) - name()
Protected (class and child classes) - _name()
Private (only inside class) - __name()
```
**Class var vs instance var**
```python
class Person:
    id = "" # class var
    def __init__(self, name, age):
        # instance var
        self.name = name
        self.age = age
  
    @classmethod # class method
    def fromBirthYear(cls, name, year):
        # a class method to create Person object by birth year.
        return cls(name, date.today().year - year)
  
    def display(self): # instance method
        print("Name : ", self.name, "Age : ", self.age)

    @staticmethod # static method - does not change state 
    def calc_age(birth_year):
        return birth_year - datetime.year 
  
person = Person('mayank', 21)
person.display()
```

**Setters and getters:**
```
__getarr__ (when obj.a is not defined) 
__getarribute__ (everytime when obj.a is called, regardless if its defined or not)
```
```python
class Name:
    @property  
    def age(self):  
        return self._age
    @age.setter
    def get_age(self, new_age):
        self._age = new_age

```
**Inheritance**

`super()` - access direct parent without explicitly using the parents name 
```python
class Child(Parent):
    def __init__(self, a, b):
        super().__init__(a)
        self.b = b
```
**Interfaces and metclass**
```python
from abc import ABC, abstractmethod

class NetworkInterface(ABC):
    @abstractmethod
    def connect(self):
        pass
    @abstractmethod
    def transfer(self):
        pass
```


- [OOPs in python (by realpython)](https://realpython.com/python3-object-oriented-programming/)
- [Programiz easy tutorial](https://www.programiz.com/python-programming/object-oriented-programming)


## References 

- [[imp] Object-Oriented Analysis And Design](https://medium.com/search?q=Object-Oriented+Analysis+And+Design%E2%80%8A)
- [OOPs 10 design interview problems](https://medium.com/javarevisited/top-10-object-oriented-analysis-and-design-interview-questions-and-problems-for-experienced-6c3a53b7cb26)
