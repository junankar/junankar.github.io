---
title: C++11 Move Semantics
---

# C++11 Move and Forward

**Contents**
* TOC
{:toc}

## Use Case: Avoid unnecessary copy operations

[A Brief Introduction to Rvalue References](https://www.artima.com/cppsource/rvalue.html) provides example of  swap where unnecessary temp copy object can be avoided.

```cpp
void SwapVectors(vector<int>& a, vector<int>& b)
{
    auto temp(a);
    a = b;
    b = temp;
}
```

## Move Semantics

Copy constructor and assignment operator can be overloaded for these use cases.

Copy semantics is used for lvalue reference input.
Move semantics is used for rvalue reference input

```cpp
    // copy semantics
    // Argument is an lvalue, the argument should be copied from.
    BigData(const BigData& other);
    BigData& operator=(const BigData& other);

    // move semantics
    // Argument is an rvalue, that means calling code has temporary object or using std::move.
    // So, contents of input can be moved to this object
    BigData(BigData&& other);
    BigData& operator=(BigData&& other);
```

```cpp
    // Copy semantics
    BigData bigDataCopy1;
    bigDataCopy1 = bigData;
		
    // Move semantics
    BigData bigDataMoved1;
    bigDataMoved1 = BigData();
```

## std::move

Now, what if we need to invoke move semantics for an lvalue?
An rvalue reference cannot be bound to an lvalue. That's where std::move helps.

Before going to std::move, let's visit different components involved in it.

### std::remove_reference

Obtains the non-reference type to given type. 

remove_reference< T >::type&& will always given rvalue reference type. That is needed in std::move implementation.

```cpp
    std::remove_reference<int &>::type&& i = 100;
    std::remove_reference<int &&>::type&& j = 200;
```

### Template argument deduction

If a template function takes argument by rvalue reference:

* Input argument is lvalue, then T is resolved to lvalue reference.
* Input argument is rvalue, then T is resolved to non-reference type.

```cpp
template <typename T>
void foo(T&& arg)
{
    if(!std::is_reference<T>::value)
        cout << "Type T is not reference" << endl;
    if(std::is_lvalue_reference<T>::value)
        cout << "Type T is lvalue reference" << endl;
} 

int main()
{
    int i=10;
		
    // Passing lvalue to foo(), T will be resolved to int& (lvalue reference type)
    foo(i);
		
    // Passing rvalue to foo(), T will be resolved to int (non reference type)
    foo(100);

    return 0;
}
```

### Reference collapsing rules

If T represents lvalue reference type (e.g. int&) or rvalue reference type (e.g. int&&):
* T&& will be resolved to T&& only in case of T representing rvalue reference (e.g. int &&)
* In all other case, result is T&.

Going back to earlier example of template argument deduction

```cpp
template <typename T>
void foo(T&& arg)
{
    if(std::is_lvalue_reference<T&&>::value)
        cout << "Type T is lvalue reference" << endl;
    if(std::is_rvalue_reference<T&&>::value)
        cout << "Type T is rvalue reference" << endl;
}

int main()
{
    int i=10;
		
    // Passing lvalue to foo().
    // T results into int& (template argument deduction)
    // T&& is now int& &&
    // This is collapsed into int&
    foo(i);
		
    // Passing rvalue to foo().
    // T results into int (template argument deduction)
    // T&& is now int&&
    foo(100);

    return 0;
}
```

### std::move
std::move accepts an lvalue/ rvalue as argument and returns rvalue.

```cpp
template <class T>
typename remove_reference<T>::type&&
move(T&& a)
{
    return a;
}
```

With std::move we can avoid copy issues.

```cpp
void SwapVectors(vector<int>& a, vector<int>& b)
{
    auto temp(std::move(a));
    a = std::move(b);
    b = std::move(temp);
}
```

## Perfect Forwarding

[A Brief Introduction to Rvalue References](http://thbecker.net/articles/rvalue_references/section_07.html) provides example of factory function.

Let's say we need to write a wrapper function to log some input and then call a processing function.

```cpp
template <class T>
void foo(T& i) {}

template <class T>
void foo(const T& i) {}

template <class T>
void foo(T&& i) {}

template <class T>
void LoggerFoo(T arg)
{
    // Log data and then call function foo
    foo(arg);
}

void main()
{
    int i=10;
    const int j= 200;
    LoggerFoo(i); // lvalue
    LoggerFoo(j); // const lvalue
    LoggerFoo(500); // rvalue
}
 ```
 
Issue here is that LoggerFoo is creating a local copy arg and then only pass by reference version of foo is getting called.

We can have following options:

* Pass arg by reference: LoggerFoo(**T&** arg)
	* Correct overloads of foo are getting called for LoggerFoo(i) and LoggerFoo(iref)
	* LoggerFoo(500) deos not compile, as we cannot bind an rvalue to lvalue reference.
* Pass arg by const reference: LoggerFoo(**const T&** arg)
	* Now only const reference overload is called for foo irrespective of input type to LoggerFoo()
* Overriding LoggerFoo() for each override of Foo()?	This will need a lot of work if Foo() has multiple parameters!

```cpp
template <class T>
void LoggerFoo(T& arg)
{
    foo(arg);
}

template <class T>
void LoggerFoo(const T& arg)
{
    foo(arg);
}

template <class T>
void LoggerFoo(T&& arg)
{
    foo(arg);
}
```

Let's try with rvalue reference.

```cpp
template <class T>
void LoggerFoo(T&& arg)
{
    // Log data and then call function foo
    foo(arg);
}
```

Now LoggerFoo() supports lvalue, const lvalue, rvalue inputs.
Const semantics are preserved, but lvalue/rvalue-ness is lost.
Foo() oveloads only for lvalue references are getting called.

## std::forward
Forward preserves the lvalue/rvalue-ness of the argument.
If an lvalue is passed to LoggerFoo(), then lvalue will be passed to Foo().
If an rvalue is passed to LoggerFoo(), then rvalue will be passed to Foo().

```cpp
template<class U>
U&& forward(typename remove_reference<U>::type& a)
{
  return static_cast<U&&>(a);
}
```

```cpp
template <class T>
void LoggerFoo(T&& arg)
{
    // If input to LoggerFoo() is lvalue, T for LoggerFoo will be resolved to T& (e.g. int&) by template argument deduction
    // forward will receive type U=T& and will try to cast output to U&& => T& &&, which will be collapsed to T&
    // So, LoggerFoo(lvalue) will result into call of Foo(lvalue reference)
	
    // If input is rvalue, T for LoggerFoo will be resolved to T (e.g. int) by template argument deduction
    // So, forward will receive type U=T and will try to cast output to U&& => T &&, which will be collapsed to T&&
    // So, LoggerFoo(rvalue) will result into call of Foo(rvalue reference)
		
    foo(std::forward<T>(arg));
}
```

## References

* [A Brief Introduction to Rvalue References](http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2006/n2027.html)
*  [A Brief Introduction to Rvalue References](https://www.artima.com/cppsource/rvalue.html)
* [C++ Rvalue References Explained](http://thbecker.net/articles/rvalue_references/section_01.html)
