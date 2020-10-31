---
title: Recursion and Backtracking
---

**Contents**
* TOC
{:toc}

## Recursion

Recursion problem can be represented as follows:

```
void Recursion(T input)
{
	// Base case
	if(input == BaseCaseValue)
	{
		// Perform operation if needed
		return;
	}
	else
	{
		// Recursive case:
		// Perform operation
		// Modify input to reach base case
		Recursion(modifiedInput);
	}
}
```

## Backtracking

Backtracking problem can be represented as follows:

```
bool Recursion(T input)
{
	// Base case
	if(Condition_Satisfied(input))
	{
		// Perform operation if needed
		return true;
	}
	else
	{
		// Select  
		  
		// Explore all the remaining choices
		for(auto nextChoice : nextChoices)
		{
			if(Recursion(nextChoice))
				return true;
		}
		
		// Backtrack		
	}
}
```

### N-Queens Problem

<script src="http://gist-it.appspot.com/https://github.com/junankar/CPP/blob/main/Backtracking_8_Queens.cxx"></script>


### Cindy's Puzzle

<details><summary>Click to expand C++ Code</summary>
<p>
<script src="http://gist-it.appspot.com/https://github.com/junankar/CPP/blob/main/Backtracking_Cindys_Puzzle.cxx"></script>
</p>
</details>

### Solving a maze

<details><summary>Click to expand C++ Code</summary>
<p>
<script src="http://gist-it.appspot.com/https://github.com/junankar/CPP/blob/main/Backtracking_Maze.cxx"></script>
</p>
</details>

## References:

* [What is Recursion?](https://daveparillo.github.io/intermediate-cpp/recursion/intro.html)
* [09 CS 106B Lecture Recursion 1 introduction (YouTube)](https://youtu.be/tq0nmIivqCA)
* [Recursion](https://introcs.cs.princeton.edu/java/23recursion/)
* [Recursion and Backtracking](https://www.hackerearth.com/practice/basic-programming/recursion/recursion-and-backtracking/tutorial/)
