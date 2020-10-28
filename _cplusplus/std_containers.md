---
title: C++ Standard Library Containers
---

# C++ Standard Library Containers

> Containers are objects that store other objects.  

Reference: [Working Draft, Standard for Programming
Language C++](https://isocpp.org/files/papers/n4296.pdf#page=759)  

**Contents**
* TOC
{:toc}

## Sequence containers
  
> A sequence container organizes a finite set of objects, all of the same type, into a strictly linear arrangement.

Reference: [Working Draft, Standard for Programming
Language C++](https://isocpp.org/files/papers/n4296.pdf#page=766) 

### array
* Static array with contiguous memory allocation
* Fixed no. of elements
* Random access

```
#include <array>
#include <iostream>
using namespace std;
int main()
{
    array<int, 5> numberArray = {};
    cout << numberArray.size() << endl;
    for(int i=0; i<numberArray.size(); ++i)
        numberArray[i] = i;
    for(auto number : numberArray)
        cout << number << " ";
}
```

References:

* [The array class](https://daveparillo.github.io/intermediate-cpp/containers/sequence-containers.html#the-array-class)
* [array class](https://docs.microsoft.com/en-us/cpp/standard-library/array-class-stl?view=vs-2019)

### vector  

* Dynamic array with contiguous memory allocation
* Random access

```
#include <vector>
#include <iostream>
using namespace std;
int main()
{
    vector<int> numberVec = {1, 2, 3};
    cout << numberVec.size() << endl;
    numberVec.push_back(4);
    numberVec.push_back(5);
    cout << numberVec.size() << endl;
    for(auto number : numberVec)
        cout << number << " ";
}
```

References:

* [An Introduction to std::vector](https://embeddedartistry.com/blog/2017/06/21/an-introduction-to-stdvector/)
* [The vector class](https://daveparillo.github.io/intermediate-cpp/string+vector/vector.html)
* [vector class](https://docs.microsoft.com/en-us/cpp/standard-library/vector-class?view=vs-2019)

### deque

* Double-ended queue which allows fast insertion, deletion at both ends
* No contiguous memory allocation
* Random access

```
#include <deque>
#include <iostream>
using namespace std;
int main()
{
    deque<int> numberDeque = {2, 3, 4};
    numberDeque.push_front(1);
    numberDeque.push_back(5);
    for(auto number : numberDeque)
        cout << number << " ";
}
```

References:

* [The deque class](https://daveparillo.github.io/intermediate-cpp/containers/sequence-containers.html#the-deque-class)
* [deque class](https://docs.microsoft.com/en-us/cpp/standard-library/deque-class?view=vs-2019)
* [Using Vector and Deque](http://www.gotw.ca/gotw/054.htm)

### list

list:
* Doubly linked list providing bidirectional access, faster insertion/ deletion at any position
* No contiguous memory allocation
* Does not provide random access

```
#include <list>
#include <iostream>

using namespace std;

int main()
{
    list<int> numberList = {3, 4};
    numberList.push_front(2);
    numberList.push_front(1);
    numberList.push_back(9);
    numberList.push_back(10);
    for(auto iter = numberList.begin(); iter != numberList.end(); ++iter)
    {
        if(*iter == 9)
        {
            numberList.insert(iter, {5,6,7,8});
            break;
        }
    }

    for(auto number : numberList)
        cout << number << " ";
}
```

References:  

* [The list class](https://daveparillo.github.io/intermediate-cpp/containers/sequence-containers.html#the-list-class)
* [list class](https://docs.microsoft.com/en-us/cpp/standard-library/list-class?view=vs-2019)

### forward_list

* Singly linked list providing forward access, faster insertion/ deletion at any position
* No contiguous memory allocation
* Does not provide random access

Reference:
* [forward_list class](https://docs.microsoft.com/en-us/cpp/standard-library/forward-list-class?view=vs-2019)

## Associative containers
  
* Provide fast retrieval of data based on keys.
* Sorted data structures using tree structures
* set, multiset, map, multimap

> The phrase “equivalence of keys” means the equivalence relation imposed by the comparison and not the operator== on keys. That is, two keys k1 and k2 are considered to be equivalent if for the comparison object comp, comp(k1, k2) == false && comp(k2, k1) == false. For any two keys k1 and k2 in the same container, calling comp(k1, k2) shall always return the same value.
  
Reference:
[Working Draft, Standard for Programming
Language C++](https://isocpp.org/files/papers/n4296.pdf#page=771)

```
#include <set>
#include <string>
#include <iostream>

using namespace std;

class Student
{
public:
    string Name;
    string LastName;   
};

struct StudentCompare {
    bool operator() (const Student& a, const Student& b) const 
    {
        if(a.LastName != b.LastName)
            return a.LastName < b.LastName;
        else
            return a.Name < b.Name;
    }   
};

int main()
{
    set<Student, StudentCompare> studentData;
    studentData.insert(Student{"Name5", "LastName1"});
    studentData.insert(Student{"Name1", "LastName1"});
    studentData.insert(Student{"Name6", "LastName2"});
    studentData.insert(Student{"Name2", "LastName2"});

    // “equivalence of keys" will be used here
    studentData.insert(Student{"Name5", "LastName1"});

    for(auto student : studentData)
        cout << student.Name << " " << student.LastName << endl;
}
```

References:  

* [Tree ADT concepts](https://daveparillo.github.io/intermediate-cpp/containers/trees.html)  
* [The set class](https://daveparillo.github.io/intermediate-cpp/containers/set.html)  
* [The map class](https://daveparillo.github.io/intermediate-cpp/containers/map.html)

## Unordered associative containers
  
* Provide fast retrieval of data based on keys.
* Unsorted data structures using hash tables
* unordered_set, unordered_multiset, unordered_map, unordered_multimap

> Each unordered associative container is parameterized by Key, by a function object type Hash that meets the Hash requirements (17.6.3.4) and acts as a hash function for argument values of type Key, and by a binary
predicate Pred that induces an equivalence relation on values of type Key. 

Another important condition to confirm for hash and predicate

> Two values k1 and k2 of type Key are considered equivalent if the container’s key equality predicate returns true when passed those values. If k1 and k2 are equivalent, the container’s hash function shall return the same value for both.

```
#include <unordered_set>
#include <string>
#include <iostream>

using namespace std;

class Student
{
public:
    string m_name;
    string m_lastName;
};

struct HashFunct {
    size_t operator() (const Student& student) const 
    {
        auto hash1 = std::hash<string>()(student.m_name);
        auto hash2 = std::hash<string>()(student.m_lastName);
        return std::hash<size_t>()(hash1 + hash2);
    }
};

struct PredicateFunct {
    bool operator() (const Student& a, const Student& b) const 
    {
        return (a.m_name == b.m_name) && (a.m_lastName == b.m_lastName);
    }
};

int main()
{
    unordered_set<Student, HashFunct, PredicateFunct> studentData;
    studentData.insert(Student{"Name5", "LastName1"});
    studentData.insert(Student{"Name1", "LastName1"});
    studentData.insert(Student{"Name6", "LastName2"});
    studentData.insert(Student{"Name2", "LastName2"});

    // Hash function will return same value as already existing entry
    // Predicate function will return true as this entry already exists
    studentData.insert(Student{"Name5", "LastName1"});

    for(auto student : studentData)
        cout << student.m_name << " " << student.m_lastName << endl;
}
```

References:

* [Working Draft, Standard for Programming
Language C++](https://isocpp.org/files/papers/n4296.pdf#page=778) 
* [Hashing concepts](https://daveparillo.github.io/intermediate-cpp/containers/unordered_map.html)
* [Hash Table In C++: Programs To Implement Hash Table And Hash Maps](https://www.softwaretestinghelp.com/hash-table-cpp-programs/)

## Container Adapters

* Provide restricted interface for simplicity
* Do not support iterators
* queue, priority_queue, stack

References:

* [The stack class](https://daveparillo.github.io/intermediate-cpp/containers/sequence-containers.html#the-stack-class)
* [The queue class](https://daveparillo.github.io/intermediate-cpp/containers/sequence-containers.html#the-queue-class)
* [priority_queue Class](https://docs.microsoft.com/en-us/cpp/standard-library/priority-queue-class?view=vs-2019)

## Iterator Categories

> Iterators are a generalization of pointers that allow a C++ program to work with different data structures (containers) in a uniform manner.

[Apache C++ Standard Library User's Guide](https://stdcxx.apache.org/doc/stdlibug/2-2.html) provides a nice summary of iterator categories.

| Iterator Category     | Description                                |
|:----------------------|:-------------------------------------------|
|Input Iterator         |Read only, forward moving                   |
|Output Iterator        |Write only, forward moving                  |
|Forward Iterator       |Both read and write, forward moving         |
|Bidirectional Iterator |Read and write, forward and backward moving |
|Random Access Iterator |Read and write, random access               |