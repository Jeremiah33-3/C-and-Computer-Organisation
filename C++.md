# C++ learning notes 

## Difference between C and C++
- [GFG Article](https://www.geeksforgeeks.org/difference-between-c-and-c/)
  - C++ supports OOP, hence polymorphism, encapsulation, inheritance and other relevant concepts of OOP
  - C++ is (mostly) a superset of C (more keywords..)
## Classic mistakes and to-note
1. for loop incremental variables\

Doing this:
```c
int i = 0;
int j = 0;
for(; i < 3; i++)
{
  for (; j < 3; j++)
  {
    ...
  }
}
```
Might not get you the desired number of loops as after the first iteration of the outer loop, the inner loop had increased var j to 3, and for subsequent loops, j is always 3 within the current scope. Versus if there is a 'redeclaration' of var j. 
