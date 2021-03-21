---
title: Disjoint-set Data Structure
category: [Data_Structures_and_Algorithm]
---

## Disjoint-set Data Structure

This is also called as union-find data structure.

[Disjoint-set data structure - Wiki](https://en.wikipedia.org/wiki/Disjoint-set_data_structure) 

> Data structure that stores a collection of disjoint (non-overlapping) sets.

e.g. There are {2, 3, 4, 5, 6, 7, 8, 9} nodes in a graph. All the even nodes are connected together and all the odd nodes are connected together.
  
Then two disjoint-sets will be formed as below:  
  
{2, 4, 6, 8} and {3, 5, 7, 9}

### Equivalence relation
  
"Is Connected To" relation R between two object x, y is an equivalence relation if:

* Reflexive: x is connected to y
* Symmetric: If x is connected to y, then y is connected to x.
* Transitive: If x is connected to y and y is connected to z, then z is connected to z.

### Supported Operations

* void union(x, y): Add connection between x and y
* bool connected(x, y): Return true if x and y are connected. Basically, this means true if x and y belong to same disjoint-set

### Array Representation
file:///C:/workdir/Personal_Projects/junankar.github.io/_cplusplus/creational-design-pattern.md
### Array Representation

### References
* [Disjoint-set data structure - Wiki](https://en.wikipedia.org/wiki/Disjoint-set_data_structure)
* [Case Study: Union-Find](https://algs4.cs.princeton.edu/15uf/) 
* [UNION–FIND](https://www.cs.princeton.edu/~wayne/kleinberg-tardos/pdf/UnionFind.pdf)
* [Disjoint Set Union (Union Find)](https://www.hackerearth.com/practice/notes/disjoint-set-union-union-find/)