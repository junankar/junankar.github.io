---
title: C++11 Range Based For Loop
permalink: /cpp/range-based-for-loop/
excerpt: "C++11 Range Based For Loop."
last_modified_at: 2020-07-27
---

Range based for loops do not need to explicitly use begin() and end() functions or use a counter to keep track of index, providing more readability.

```cpp
vector<int> nos {1, 2, 3, 4};    
for(const auto& no : nos)
    cout << no << " ";

map<string, int> nameToIdMap { {"ABC", 2}, {"XYZ" , 1}};
for(const auto& kv : nameToIdMap)
    cout << kv.first.c_str() << ":" << kv.second  << " ";
```

###  Range Based For Loop for custom types

```cpp

template <typename T, size_t S>
class CustomContainer
{
    T m_data[S] = {};

public:
    const T* GetData() const { return m_data;}
    size_t GetSize() const { return S;} 

    void SetValueAt(size_t index, T value)
    {
        if(index < S)
            *(m_data + index) = value;
        else
            throw std::out_of_range("Out of range"); 
    }
};

template <typename T, size_t S>
const T* begin(const CustomContainer<T, S>& container)
{
    return container.GetData();
}

template <typename T, size_t S>
const T* end(const CustomContainer<T, S>& container)
{
    return container.GetData() + S;
}

int main()
{
    CustomContainer<int, 4> container;
    container.SetValueAt(0, 4);
    container.SetValueAt(1, 6);
    container.SetValueAt(2, 5);
    container.SetValueAt(3, 8);

    for(const auto& iter : container)
        cout << iter << " ";

    return 0;
}

```
