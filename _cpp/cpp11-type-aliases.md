---
title: Type Aliases
permalink: /cpp/type-aliases/
last_modified_at: 2020-07-27
---

# Alias

From C++11, using statement can be used similar to typedef to define type synonyms.

```cpp
    using counter = long;
```

## Function Pointers

Alias make function pointers more readable compared to typedef.

```cpp
# Function Pointer alias
using functPtrAlias = int(*)(int, int);

# Function Pointer typedef
typedef int(*functPtrTypedef)(int, int);

int ProcessNos(functPtrAlias foo, int a, int b) { return foo(a, b); }

static int Add(int a, int b) { return (a+b); }
static int Multiply(int a, int b) { return (a*b); }

int main()
{
    int a=10, b=20;
    cout << ProcessNos(&Add, a, b) << endl;
    cout << ProcessNos(&Multiply, a, b) << endl;
}
```

# References:

* [Aliases and typedefs (C++)](https://docs.microsoft.com/en-us/cpp/cpp/aliases-and-typedefs-cpp?view=msvc-160)
* [How C++ ‘using’ or alias-declaration is better than typedef](https://www.nextptr.com/tutorial/ta1193988140/how-cplusplus-using-or-aliasdeclaration-is-better-than-typedef)