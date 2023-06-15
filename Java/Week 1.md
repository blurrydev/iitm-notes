# Lecture 1

### What is the difference between Interpreter and Compiler?

- A compiler translates our high level code into low level code in *one shot*.
- An interpreter translates our code *line by line* into low level code.

### Different types of Programming Language

#### Imperative
- Focuses on explicit instructions and step by step procedures.
- Programs specify how to achieve the result by declaring variables, control flow structure etc.
- Example: Java, C, C++

#### Declarative
- Emphasizes describing the desired outcome or result.
- Programs specify what is to be achieved rather than how to achieve it.
- Examples: SQL, HTML, CSS

# Summary

#### Memory Management:
- Memory management involves allocating and deallocating memory for program execution.
- In low-level languages like C or C++, manual memory management is required, where the programmer explicitly allocates and deallocates memory.
- In higher-level languages like Java and Python, memory management is automated through techniques like garbage collection.
- Java uses automatic garbage collection, where the runtime system frees memory for objects that are no longer referenced.
- Python also uses garbage collection, specifically a technique called reference counting, which tracks the number of references to an object and frees the memory when the count reaches zero.

#### Types:
- Programming languages have different approaches to handling data types.
- Java is a statically typed language, meaning that variables must have a declared type at compile-time, and the type is checked before execution.
- Python, on the other hand, is dynamically typed, allowing variables to hold values of different types during execution without explicit type declarations.

#### Abstraction and Modularity:
- Abstraction and modularity are fundamental principles in software engineering.
- Abstraction involves simplifying complex systems by breaking them down into smaller, more manageable units.
- Modularity refers to organizing code into separate, self-contained modules or components.
- Both Java and Python support abstraction and modularity through classes, interfaces (Java), and modules (Python).
- Java follows a strict object-oriented approach, where everything is an object, and code is organized into classes and interfaces.
- Python supports both object-oriented programming and procedural programming paradigms, providing flexibility in code organization.

#### Object-Oriented Programming (OOP):
- OOP is a programming paradigm that focuses on objects and their interactions.
- Java and Python are both object-oriented languages, but they have some differences in their approach to OOP.
- Java enforces strong encapsulation through access modifiers (public, private, etc.) to control visibility and ensure data integrity.
- Python adopts a more relaxed approach to encapsulation, allowing attributes and methods to be accessed directly.
- Both languages support inheritance, where new classes can be derived from existing classes to inherit properties and behaviors.
- Java employs static typing for method parameters and return values, while Python uses dynamic typing, allowing more flexibility in function signatures.

#### Classes:
- In object-oriented programming, a class is a blueprint or template for creating objects.
- A class defines the properties (attributes) and behaviors (methods) that objects of that class will possess.
- It serves as a reusable structure that encapsulates data and functionality related to a particular concept or entity.
- Classes allow us to create multiple instances (objects) based on the same blueprint, each with its own unique data and behavior.

#### Objects:
- Objects are instances of a class. They represent specific entities or things that exist at runtime.
- An object is created by instantiating a class using the "new" keyword in Java or through direct assignment in Python.
- Each object has its own set of attributes, which represent its state, and methods, which define its behavior.
- Objects interact with each other by invoking methods and accessing each other's attributes.

##### Class and Object Example (Java):
```java
// Class definition
class Car {
    // Attributes
    String brand;
    String color;
    int year;

    // Constructor
    public Car(String brand, String color, int year) {
        this.brand = brand;
        this.color = color;
        this.year = year;
    }

    // Method
    public void startEngine() {
        System.out.println("The " + brand + " car's engine is started.");
    }
}

// Object creation
Car myCar = new Car("Toyota", "Red", 2020);

// Accessing attributes
System.out.println("My car is a " + myCar.brand + " " + myCar.color + " car.");

// Invoking methods
myCar.startEngine();
```

##### Class and Object Example (Python):
```python
# Class definition
class Car:
    # Constructor
    def __init__(self, brand, color, year):
        self.brand = brand
        self.color = color
        self.year = year

    # Method
    def start_engine(self):
        print("The", self.brand, "car's engine is started.")

# Object creation
my_car = Car("Toyota", "Red", 2020)

# Accessing attributes
print("My car is a", my_car.brand, my_car.color, "car.")

# Invoking methods
my_car.start_engine()
```

In both Java and Python, classes and objects provide a way to model real-world entities or abstract concepts and define their properties and behaviors. You can create as many objects as needed based on a single class, each with its own unique data.