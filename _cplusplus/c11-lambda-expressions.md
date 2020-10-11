---
title: C++11 Lambda Expressions
---

## C++11 Lambda Expressions

Form of Lambda Expression
```cpp
[capture list](parameter list) mutable noexcept -> return-type {body}
```

Internally, compiler generates a class with function call operator().

### Capture List

Specifies variables in the enclosing scope which need to be captured by value or by reference

* [  ] Empty capture list means that lambda expression accesses no variables in the enclosing scope.
* [=] means all the variables in the enclosing scope are captured by value.
* [&] means all the variables in the enclosing scope are captured by reference.

```cpp
int i=100;
auto lambda = [&i]() mutable -> void { i = i * i; };
lambda();
cout << i << endl; // Prints 10000
```

```cpp
int i=100;
auto lambda = [i]() mutable -> void { i = i * i; };
lambda();
cout << i << endl; // Prints 100
```

### Parameter List  

Specifies input parameters for lambda.

```cpp
    int i=20;
    auto lambda = [](int i) -> int  { return i * i; } ;
    int square = lambda(i);
    cout << square << endl; // Prints 40
```

### Mutable Specification

By default lambda's function call operator() is const-by-value. Mutable specification allows lambda to modify variables which are captured by reference.

### Exception Specification

noexcept exception specification to indicate that the lambda expression does not throw any exceptions.

### Return type

Compiler automatically deduces return type if a trailing-return-type is not explicitly specified.

### Example Usage with STL Algorithms

```cpp
    vector<int> numbers {1, 2, 3};    
    for_each(numbers.begin(), numbers.end(),
        [](int element) { cout << element << " ";}
    );
```
