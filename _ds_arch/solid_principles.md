---
title: SOLID Principles
permalink: /ds_arch/solid_principles/
category: [Software_Design]
tags: [SOLID]
excerpt_separator: <!--more-->
---

# SOLID
SOLID is an acronym for five software design principles promoted by Robert C. Martin (Uncle Bob).
<!--more-->

## Single Responsibility Principle
> A class should have one, and only one, reason to change.

* Easier to understand
* Less recompiles
* Less dependencies and chances of introducing regressions

## Open/Closed Principle

> Software entities (classes, modules, functions, etc.) should be open for extension, but closed for modification.

Introduced by [Bertrand Meyer](https://en.wikipedia.org/wiki/Bertrand_Meyer) in [Object-Oriented Software Construction](https://en.wikipedia.org/wiki/Object-Oriented_Software_Construction)

For new requirements, extend the behavior of existing entities by adding new code and not by changing existing code. This provides flexibility to code.

**Examples:**

* AbstractServer: Client class should be able to communicate with different types of server classes.
* DrawAllShapes: DrawAllShapes should be able to draw any shape which can be added in future.
* Interfaces, Strategy, composition design pattern

## Liskov Substitution Principle

> Functions that use pointers or references to base classes must be able to use objects of derived classes without knowing it.

 Introduced by [Barbara Liskov](https://en.wikipedia.org/wiki/Barbara_Liskov)

When this principle is violated, the functions that operate upon pointers or references to base classes will need to check the type of the actual object to
make sure that they can operate upon it properly.

**Examples:**

* Squares aren't Rectangles: Base class Rectangle can allow setting height and width independently. Derived Square class would restrict them to be equal. Any existing function which takes Rectangle* and sets it's height, width depends on the fact that height and width can be set independently.

## Interface Segregation Principle

> Clients should not be forced to depend upon interfaces/ methods that they do not use.

Classes that have “fat” interfaces are classes can be broken into groups of member functions which are used by different set of clients. e.g. member functions group MFG1 is used by clients CG1 and member functions group MFG2 is used by clients CG2, any change in function of MFG1 would also require recompile of clients CG2.

Clients should know about abstract base classes that have cohesive interfaces.

**Examples:**

* ATM UI: Different types of transaction classes will call different UI methods.
* Multiple Inheritance, Adapter pattern

**Challenges:**

* Same object instance is shared through different interfaces.
* The Polyad vs. the Monad: A client wants to use multiple function groups.

## Dependency Inversion Principle

> A. High-level modules should not depend on low-level modules. Both should depend on abstractions (e.g. interfaces).

> B. Abstractions should not depend on details. Details (concrete implementations) should depend on abstractions.

Higher level modules contain policy decisions and business models of an application. These should be reusable in different contexts.

Dependency Inversion can be applied wherever one class sends a message to another.

In C++, utility functions, private member variables are declared in header. These are part of the implementation and not part of interface. So, in C++, implementation is not automatically separated from interface.

**Examples:**

* Button-Lamp: Button class should be able to work with any device and not just Lamp.

## References

* [Articles from Robert C. Martin (Uncle Bob)](https://sites.google.com/site/unclebobconsultingllc/home/articles)
* [The Single Responsibility Principle](https://drive.google.com/file/d/0ByOwmqah_nuGNHEtcU5OekdDMkk/view)
* [The Open Closed Principle](https://drive.google.com/file/d/0BwhCYaYDn8EgN2M5MTkwM2EtNWFkZC00ZTI3LWFjZTUtNTFhZGZiYmUzODc1/view)
* [The Liskov Substitution Principle](https://drive.google.com/file/d/0BwhCYaYDn8EgNzAzZjA5ZmItNjU3NS00MzQ5LTkwYjMtMDJhNDU5ZTM0MTlh/view)
* [The Interface Segregation Principle](https://drive.google.com/file/d/0BwhCYaYDn8EgOTViYjJhYzMtMzYxMC00MzFjLWJjMzYtOGJiMDc5N2JkYmJi/view)
* [The Dependency Inversion Principle](https://drive.google.com/file/d/0BwhCYaYDn8EgMjdlMWIzNGUtZTQ0NC00ZjQ5LTkwYzQtZjRhMDRlNTQ3ZGMz/view)
* [Robert C Martin - The Single Responsibility Principle (YouTube)](https://www.youtube.com/watch?v=Gt0M_OHKhQE)
* [SOLID Design Patterns (YouTube)](https://www.youtube.com/watch?v=agkWYPUcLpg)