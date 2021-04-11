---
title: Single and Double Dispatch
---

# Single Dispatch

> Mechanism where the choice of which version of a method to call is based on the type of a single object.

Reference: [Wiki](https://en.wikipedia.org/wiki/Dynamic_dispatch#Single_and_multiple_dispatch)
 
# Double Dispatch

> Mechanism that dispatches a function call to different concrete functions depending on the runtime types of two objects involved in the call.  

Reference: [Wiki](https://en.wikipedia.org/wiki/Double_dispatch)  

Visitor design pattern is good example of using double dispatch where concrete function is selected on basis of concrete visitor and concrete element types.

References:

* [Double dispatch in C++](https://en.wikipedia.org/wiki/Double_dispatch#Double_dispatch_in_C++)
* [Stop reimplementing the virtual table and start using double dispatch](https://gieseanw.wordpress.com/2018/12/29/stop-reimplementing-the-virtual-table-and-start-using-double-dispatch/)
* [Visitor and Double Dispatch](https://refactoring.guru/design-patterns/visitor-double-dispatch)
* [Add methods retroactively in Python with singledispatch](https://opensource.com/article/19/5/python-singledispatch)

