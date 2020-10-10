---
title: PImpl
layout: default
category:
- Software_Design
tags:
- SOLID
---

# PImpl

PImpl or Pointer to implementation ic C++ technique for extracting  implementation into a separate class and access it through pointer.

**Contents**
* TOC
{:toc}

## Example Use Case

Consider following class:

```cpp
#include "Engine.h"
class Car
{
public:
    Car();
    ~Car();

    void Start();
    void Stop();

private:
    Engine m_engine;
};
```

### Changing Private Members in a class

Private member mean outside code cannot access it. So, why then calling code gets recompiled when private members are changed?

* Change in size of object
* Private functions participate in overload resolution

In above example, we have to include Engine.h in Car.h even if it is private member. So even if calling code is not interested/ using Engine class directly, all those dependencies are now introduced.
If we add another private member to Car.h, then all the calling code gets recompiled.

### Encapsulation

If you listen to talks from Uncle Bob (e.g. [Uncle Bob SOLID principles](https://youtu.be/zHiWqnTWsn4?t=2287) ), then you will come across following:

> OO did not give us encapsulation, it weakened it!

Encapsulation means that users of a class should not have any knowledge about implementation. Private members are exposed in headers, so those are visible (although not usable) to users of a class.

In above example, calling code is interested in Car and it's public method like Start, Stop. Exposing private members gives some clue on how these are implemented.

## Using PImpl

PImpl or *Pointer to implementation* helps in these situations. It removes the implementation details (Encapsulation), reduces recompiles by placing implementation in a separate class and accessing it through an opaque pointer.

```cpp

class Car
{
public:
    Car();
    ~Car();

    void Start();
    void Stop();

private:
    class CarImpl;
    CarImpl* m_impl;
};

#include "Engine.h"
class CarImpl
{
public:
    CarImpl();
    ~CarImpl();

    void Start();
    void Stop();

private:
    Engine m_engine;
};
```

### Advantages of PImpl

* Removes the implementation details (Encapsulation).
* Reduce recompilation due to changes in private members
* Calling code is exposed to types which are required to consume given class and not to type which are needed for implementing given class.

### Performance Costs

* Additional implementation object construction/destruction and memory allocation.
* Extra indirections in case implementation object needs to access info from visible class.

### Ways to implement

Herb Sutter talks about following four common ways:

* Move all private data (not functions) to impl class
* Move all private members to impl class
Issue: Virtual functions need to be available in visible class even if private.
* Move all private, protected members to impl class
Issue: Derived classes need to have access to protected members through visible class.
* Make visible class public interface with all the forwarding directions to impl object.
Issue: Now visible class cannot be used for inheritance.

## References

* [GotW #7b Solution: Minimizing Compile-Time Dependencies, Part 2](https://herbsutter.com/2013/12/31/gotw-7b-solution-minimizing-compile-time-dependencies-part-2/)
* [Compilation Firewalls](http://www.gotw.ca/gotw/024.htm)
* [The Pimpl Pattern - what you should know](https://www.bfilipek.com/2018/01/pimpl.html)
* [How to implement the pimpl idiom by using unique_ptr](https://www.fluentcpp.com/2017/09/22/make-pimpl-using-unique_ptr/)
