---
Subject: Java
tags:
  - revision
Last Updated: 2023-09-01T15:29
---
# Interface and Abstract

## Abstract
- This cannot be instantiated on it's own.
- It can be subclassed by non-abstract class.
- It can have *instance variables*, *constructors* & *methods* with access modifiers.
- Abstract classes support constructors.

- Abstract classes can have non abstract methods along with abstract methods.
- If a class is declared abstract and has abstract methods then it is mandatory or all classes to either provide implementation of all abstract methods or declare itself abstract as well.
- Concrete methods can provide default implementation that can be inherited by the subclasses.

## Interface
- An interface is a contract that defines a set of methods that implementing classes must provide.
- It can have only abstract methods (method without a method body).
- It can't have instance variables, constructors or methods with access modifiers.
- Implementing an interface does not involve inheritance. It's more like a contract that a class agrees to fulfil.
- Interfaces are commonly used to achieve loose coupling and provide a common protocol.

- All methods declared within an interface are implicitly abstract. 
- Interfaces can't have concreate methods.
- A class that implements an Interface must provide implementations 

`A class can extend a class and can implement any number of interfaces simultaneously.`

## Connection
- 

# Week 12

- One listener can listen to multiple objects.
	- Three buttons on the windows report to a common listener.
- One component can inform multiple listeners.
	- Exit Browser will report all the tabs that are currently open.
- Must explicitly set up association between components and listener.
- Events are lost if nobody is listening.

- JButton is the swing class for button.
- Corresponding listener classes