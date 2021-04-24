---
title: C++11 Initializer List
classes: wide
permalink: /cpp/initializer-lists/
excerpt: "C++11 Initializer List."
last_modified_at: 2020-07-27
---

###  initializer_list class

C++11 introduced class called initializer_list.

```cpp
template <class Type>
class initializer_list
```

An initializer_list can be constructed by using brace initialization.
begin(), end(), size() methods are provided to support iteration.

```cpp
initializer_list<int> inputList{1, 2, 3};
for(const auto* iter = inputList.begin(); iter != inputList.end(); ++iter)
	cout << *iter << " ";
```
 
Copy of an initializer_list results into new list referencing to the members of the original list. 
 
```cpp
initializer_list<int> inputList1{1, 2, 3, 4, 5};
initializer_list<int> inputList2(inputList1.begin(), inputList1.begin()+3);
initializer_list<int> inputList3(inputList1);

for(auto* iter = inputList2.begin(); iter != inputList2.end(); ++iter)
	cout << *iter << " ";
cout << endl;

if(inputList2.begin() == inputList3.begin())
	cout << "Members are referenced" << endl;
```	

### STL containers support for initializer lists

```cpp
vector<int> inputVec = {1, 2, 3};
map<string, int> inputMap = { {"One", 1}, {"Two", 2}, {"Three" ,3} };
```

###  Using initializer lists for constructors

#### Class without constructor

```cpp
#include <initializer_list>
#include <string>

using namespace std;

class Person {
public:
    string m_name;
    int m_age;	
};

int main()
{
    Person personA{};           // default brace initialization (with empty braces)
    Person personB{ "XYZ" };    // same order as declaration in class, can skip members
    Person personC{ "XYZ", 99}; // same order as declaration in class 
    return 0;
}
```

#### Class with constructor: Use list elements in order of parameters

```cpp
class Person {
public:
    Person(){}
    Person(int age, string name):m_name(name), m_age(age){}
 
private:
    string m_name;
    int m_age;	
};

int main()
{
    Person personA{};
    Person personC{ 99, "XYZ"}; // same order as parameters, cannot skip parameters
    return 0;
}
```
