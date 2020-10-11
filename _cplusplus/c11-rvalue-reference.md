---
title: C++11 rvalue Reference
---

## lvalue and rvalue References

### The lvalue

An lvalue represents an object that occupies identifiable location in memory and allows us to take address of that memory location by & operator. 

```cpp
int i=100; // i is lvalue
int* iaddress=&i; // Address of i can be obtained by using &

auto foo = [&i]() -> int& {return i;}; // foo() is lvalue
int* address = &foo(); // Address of foo() can be obtained by using &
```

### The rvalue
An rvalue is an expression that is not lvalue i.e. does not represent object with identifiable location in memory.
An expression is an rvalue if it creates a temporary object or literals.

```cpp
int i=100,j=100; // 100 is rvalue
int product = i * j; // i * j is rvalue
auto foo = [](){return 100;}; // foo() is rvalue
	 
// Following statements fail to get address of expression
// Compile error: expression must be an lvalue or a function designator
auto address = &(i*j);
auto returnValAddress = &foo();
```

[Lvalues and Rvalues](https://accu.org/index.php/journals/227) mentions following:

> In the modern C++, lvalue can be considered more as a locator value. An lvalue refers to a defined region of storage. Although, this is not true with the function lvalues since functions are not objects. Similarly, an rvalue can be considered as a value of an expression.

> An intuitive approach would be to think of expressions as functions and then an lvalue can be thought as the result of a function returning a reference.

### The lvalue Reference

Reference is an alias for an object. It is represented using '&' after type.

```cpp
int i=10, j=20;
int& iref=i;
int& jref=j;

++iref; // Equivalent to ++i, changes i to 11
iref = j; // Equivalent to i=j, changes i to 20
iref = jref; // Equivalent to i=j, changes i to 20
		
auto foo_lvalue = [&i]() -> int& {return i;};
int& foo_lvalue_result = foo_lvalue();
		
// In C++0x, we can bind rvalue to a const lvalue reference
const int& reference = 100;
auto foo_rvalue = [](){return 100;}; // foo() is rvalue
const int& foo_rvalue_result = foo_rvalue();
```

A reference must be initialized.
Once a reference has been initialized, it cannot be modified to refer to another object.

```cpp
int& ref;  // Error: 'ref': references must be initialized (C2530)
```

A reference to pointer must be initialized using a pointer.

```cpp
int i=10, j=20;
int* iptr = &i; // Pointer to i (address of i)
int*& iptrRef = iptr; // Reference to pointer to i
*iptrRef = 100; // Equivalent to *iptr = 100, changes i to 100
		
iptrRef = &j; // Equivalent to *iptr = &j, so now iptrRef is reference to pointer to j
*iptrRef = 200; // Equivalent to *(&j) = 100, changes j to 100
```

[R-value references](https://www.learncpp.com/cpp-tutorial/15-2-rvalue-references/) provides a nice table with summary of lvalue references and const  lvalue references.

### The rvalue Reference

An rvalue reference is declared by && after some type.

```cpp
auto foo = [](){return 100;}; // foo() is rvalue
int&& rvalueRef=foo();
```

#### Function Overload

We can now have three different function overloads as follows: 

```cpp
void foo(int& i) {cout << "lvalue reference parameter" << endl;}
void foo(const int& i) {cout << "const lvalue reference parameter" << endl;}
void foo(int&& i) {cout << "rvalue reference parameter" << endl;}
```

[Rvalue References](http://thbecker.net/articles/rvalue_references/section_03.html) mentions following

> Rvalue references allow a function to branch at compile time (via overload resolution) on the condition "Am I being called on an lvalue or an rvalue?"

```cpp
void foo(int& i) {cout << "lvalue reference parameter" << endl;}
void foo(const int& i) {cout << "const lvalue reference parameter" << endl;}
void foo(int&& i) {cout << "rvalue reference parameter" << endl;}
```


* **Case 1:**

```cpp
void foo(int& i) {cout << "lvalue reference parameter" << endl;}

void main()
{
    int i=100;
    const int& const_lval_ref = i;

    foo(i);
    foo(const_lval_ref); // Compiler error: qualifiers dropped in binding reference of type "int &" to initializer of type "const int"
    foo(100); // Compiler error: initial value of reference to non-const must be an lvalue
}
```

* **Case 2:**

```cpp
void foo(int& i) {cout << "lvalue reference parameter" << endl;}
void foo(const int& i) {cout << "const lvalue reference parameter" << endl;}

void main()
{
    int i=100;
    const int& const_lval_ref = i;

    foo(i);              // prints "lvalue reference parameter"
    foo(const_lval_ref); // prints "const lvalue reference parameter"
    foo(100);            // prints "const lvalue reference parameter"
}
```

* **Case 3:**

```cpp
void foo(int& i) {cout << "lvalue reference parameter" << endl;}
void foo(const int& i) {cout << "const lvalue reference parameter" << endl;}
void foo(int&& i) {cout << "rvalue reference parameter" << endl;}

void main()
{
    int i=100;
    const int& const_lval_ref = i;

    foo(i);              // prints "lvalue reference parameter"
    foo(const_lval_ref); // prints "const lvalue reference parameter"
    foo(100);            // prints "rvalue reference parameter"
}
```

## References

* [Lvalues and Rvalues](https://accu.org/index.php/journals/227)
* [A Brief Introduction to Rvalue References](https://www.artima.com/cppsource/rvalue.html)
* [C++ Rvalue References Explained](http://thbecker.net/articles/rvalue_references/section_01.html)
* [boost Move Introduction](https://www.boost.org/doc/libs/1_74_0/doc/html/move/introduction.html)
