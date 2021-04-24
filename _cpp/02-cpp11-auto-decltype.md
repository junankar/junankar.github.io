---
title: C++11 auto and decltype
permalink: /cpp/auto-decltype/
excerpt: "C++11 auto and decltype."
last_modified_at: 2020-07-27
---

## auto
Allows to declare objects without specifying types.

```cpp
map<string, int> nameToAgeMap { {"XYZ", 50} };
const auto& iter = nameToAgeMap.find("XYZ");
```

## decltype
 
decltype lets  compiler deduce the type of an expression.
 
```cpp
map<string, int> nameToAgeMap { {"XYZ", 50} };
decltype(nameToAgeMap)::value_type entry = {"ABC", 99};
nameToAgeMap.insert(entry);
```

decltype is also useful in template functions where return type can be deduced. Otherwise one more template parameter is needed to be added for specifying return type.

```cpp
template <typename K, typename V>
class KeyValue
{
public:
    K key;
    V value;
};

template <typename T>
auto AddKeys(T keyvalue1, T keyvalue2) -> decltype(keyvalue1.key)
{
    return keyvalue1.key + keyvalue2.key;
}

int main()
{
    KeyValue<int, int> kv1 = {1 , 2};
    KeyValue<int, int> kv2 = {2 , 3};
    std::cout << AddKeys(kv1, kv2) << " ";

    KeyValue<string, int> kv3 = {"ABC", 3};
    KeyValue<string, int> kv4 = {"XYZ", 3};
    std::cout << AddKeys(kv3, kv4).c_str() << " ";

    return 0;
}
```
