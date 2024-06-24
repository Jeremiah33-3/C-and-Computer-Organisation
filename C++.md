# C++ learning notes 

## Difference between C and C++
- [GFG Article](https://www.geeksforgeeks.org/difference-between-c-and-c/)
  - C++ supports OOP, hence polymorphism, encapsulation, inheritance and other relevant concepts of OOP
  - C++ is (mostly) a superset of C (more keywords..)
## Classic mistakes and to-note
1. for loop incremental variables

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

2. array names
If `arr` is the name of the array declared
- `arr` refers const pointer to the address of the first element in the array (array names converted to pointers)
- `&arr[0]` refers to the address of the first element in the array
- `&arr` is the pointer to the ***entire*** array
Thus the implication is:
- incrementing both `arr` and `&arr[0]` by 1 gives the address of the ***next element***：  `arr+1` and `&arr[0]+1`
- incrementing `&arr` increment the address by the size of the array (e.g if arr size is 40, `&arr+1` will gives an address {address of first element} + 40)
