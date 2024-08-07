# C Programming Language stuffs 

## [Documentation](https://devdocs.io/c/)
- https://devdocs.io/c/

## Extremely useful video explanation
- https://www.bilibili.com/video/BV1Vm4y1r7jY/?spm_id_from=333.337.search-card.all.click

## edit, compile, exceute 

- for python and JS, there is a REPL in the printer to see the result printed on screen, but not C (not compile and print on the fly)
- in C, program is first comfiled into assembly language then machine language; we run in machine language (directly understood by the processor) -> that's what make C so fast, but is slightly inconvenient
  - cycle: editor to create file, c compiler to compile into machine code, execute the machine code -- if incorrect, cycle repeats
    1. vim file.c -> (produces) source code file.c (editing)
    2. gcc file.c -> (produces) a.out (machine code, compiling)
    3. run a.out -> (produces) output (execute)
  - note while editing, indentation is optional but encouraged (for readability) 

## Structure 

CS2100 says:
- a basic c program has 4 main parts: preprocessor directives (header, definition/macro expansions -> **instructions for compiler**), input (thru stdin's scanf or file input), compute (arithmetic operations and assignment statements), output (thru stdout using printf, or file output)
- input/output
  - [format specifiers](https://www.geeksforgeeks.org/format-specifiers-in-c/), which are placeholders for values to be displayed or read
  - width: with printf(), %5d displays an int in a width of 5, right justified
  - decimal places: %8.3 display a real no (float or double) in a width of 8, with 3 decimal places, right justified.
  - for scanf(), use format specifiers without indicating width. decimal places...
  - \n is an eg of [escape sequence](https://www.geeksforgeeks.org/escape-sequence-in-c/) -> to display certain characters (with special meaning, regex, newlines..) properly.
- computation
  - a function body has two parts
  - declarations statements: tell compiler what type of memory cells needed
    - declare use of var/const (must decalre type in C)
    - user-defined identifier (certain rules to follow)
    - reserved words/[keywords](http://c.ihypress.ca/reserved.html) -> cannot be used as var name (identifier)
    - standard identifiers (names of common functions, avoid naming var/func as such)
  - executable statements: describe the processing on the memory cells
    - I/O statements (prinf..) and computational + assignment statements
    - assignment statements store a value or a computational result in a var (also left side of '=' in assignment is called lvalue)
      - lvalue must be asignable (invalid assignment is when an expr/value is put as the lvalue)
      - assignment can be cascaded with [associativity](https://www.mathsisfun.com/associative-commutative-distributive.html) from [right to left](https://stackoverflow.com/questions/25589257/what-does-left-to-right-associativity-mean) (e.g. a = b = c= 3 + 6 which is equivalent to a = (b = (c = 3+6)) )
  - side effect
    - as assignment statement incur side effect which is returning the value of its right-hand side expr apart from assigning the value to the var
    - useful to double assign (e.g. z = a = 12)
    - but avoid convuluted code (e.g. a = 5 + (b = 10))

- Mainly 6 sections: Documentation, Header, Definition, Global Declaration, Main() function, Sub Program
- Documentation: Description, in comments (optional)
- Header (preprocessor) :
  - inclusion of header files (.h)
  - with extension .h which contains C function declarations and macro definitions
  - lines starting with # will be processed by the [preprocessor](https://www.geeksforgeeks.org/cc-preprocessors/)
  -  e.g., #include<stdio.h>
- Definition (preprocessor)
  - #define preprocessor is used to create a constant throughout the program ([one way](https://www.freecodecamp.org/news/constants-in-c-explained-how-to-use-define-and-const-keyword/) to define constant in c)
  - e.g. #define PI 3.14 (name PI will be places by 3.14 whenever the program encouters the name)
- Global: global variables, function declaration, and static variables; global scope (used anywhere in the program)
-  Main method:
  - entry point of the program
  - decalre of return type at the declaration (int <- convention /void)
  - always return 0 (by convention, returning non-zeros [signals that an error occurred](https://stackoverflow.com/questions/18446686/main-function-in-c))
  - exceution of statements inside the curly braces (definition, body of the main() function)
- Sub-programs: user-declared functions  

Notes on preprocessor directives:
- it provides inclusion of header files, macro expansions, conditional compilation (under circumstances, code that is produced can change, and we can set what the code is compiled for what processor)
- cs2100 focuses on header files and macro expansions
- macro expansions
  - define a macro for a constant value and can even take arguments
  - #define PI 3.142 e.g.
  - C compiler will substitute every code that matches the macro defined with the value specified during compilation.
  - do not put semicolon at the end
 

## [typecasting](https://www.geeksforgeeks.org/c-typecasting/) and [type conversion](https://www.geeksforgeeks.org/type-conversion-c/)
> typecasting is the process of converting one data type to another using the casting operator during program design (different from type conversion)

- type of the destination data type may be smaller than the source data type (narrow typecasting)
- two forms: implicit and explicit

Implicit type casting seems to be type conversion, compiler infers the datatype

Explicit --> using the casting operator.

In assignment: `dest_type a = (dest_type) b`

In expresssion: `dest_type a = (dest_type) b / c`

> type conversion is the process of converting one data type to another, may or may not be using the casting operator, performed by the compiler. (superset of type casting)

- done at compile time, widening conversion
- two forms: implicit and explicit

Implicit type conversion is automatic, done by the compiler on its own. Takes place when there is multiple datatypes present in one expression; all datatype will be upgraded to the largest data type (bool -> char -> short int -> int -> unsigned int -> long -> unsigned -> long long -> float -> double -> long double).

Explicit type conversion is type casting

### [Integer promotion](https://www.geeksforgeeks.org/integer-promotions-in-c/)
> data types being automatically promoted/converted into integer IN AN EXPRESSION involving ARITHMETIC OPERATION. A subset of implicit converion done by the compiler

Either int or unsigned int.

 
## [Static and dynamic library ](https://www.geeksforgeeks.org/static-vs-dynamic-libraries/)
Compilation of code -> linker links library functions to code -> 2 ways to do it 
1. Static linking (static lib)
> make a copy of all used library functions to the executable file

It creates larger binary files -> more space on disk and main memory

2. Dynamic linking (dynamic lib)
> placing name of the library in the binary file. The actual linking happens when the program is run, when both the binary file and the library are in memory.

--> [pragma comment](https://stackoverflow.com/questions/3484434/what-does-pragma-comment-mean)
> compiler directive to leave a comment to the generated object file
- `#pragma comment(lib, libname)` tells the linker to add the 'libname' library to the list of library dependencies

## [internal vs external linkage](https://www.geeksforgeeks.org/internal-linkage-external-linkage-c/) (static and extern) 
Firstly, to understand that linkage is different from scope. Scope of an identifier (var or const) is the part of the program where the ientifier is directly accessible, handled by the compiler. Linkage, on the other hand, is determined at the linking process handled by the linker; it determined how vars are linked by the linker -- whether the var can be used only within the translation unit the var is in or in every translation unit of the project.
1. Internal Linkage

An identifier implementing internal linkage is not accessible outside the translation unit it is declared in. This property is implemented using the `static` keywork on the identifier. 

2. External Linkage

An identifier implementing external linkage is visible to every translation unit. `extern` implements external linkage.
 
## Pointers and functions

1. Pointer
C is high level lang -> but the lower end of the spectrum is due to:
- pointers which allow direct manipulation of memory contents
- has a set of manipulation operators, allowing efficient bitwise operations

All pointer variables have the same size ( either 4 bytes or 8 bytes depending on the OS), yet it is still crucial to declare the pointer var to the correct type it is intended to point to as type declaration is needed in the pointer for dereferencing and pointer arithmetic purposes. This is especially obvious when we perform arithmetic operations on the pointer such as incrementing/decrementing the ptr --> the ptr will point to a new address that is incremented by the type it is declared as (e.g., int *p, p++ will increment the address by 4 bytes)

**address**
- imagine memory like pigeonholes with numbers (use to identity the slot) -> which is formally known as address
- a variable occupies some space in the com mem, and hence it han an address
- need not know the address of the var, refer to it by name, but the system(compiler) keeps track of the var's address
- yet sometimes you have to get the address yourself
  - by making use of address operator & (refer to the var's address e.g. &name)
  - %p\n is for pointers
  - addresses are printed out in hexadecimal (base 16) format
  - the address of a var varies from run to run, as the system allocates any free mem to the var
- pointer variable
  - a var that contains the address of another var is called a pointer variable or simply pointer
  - var a_ptr is said to be pointing to var a
  - if the address of a is immaterial, we simply draw an arrow from the blue box to the var it points to
  - declaration:
    - type *pointer_name
    - type is the data type of the bar this pointer may point to
    - pointer_name is the name (identifier of the pointer)
    - good practise to name pointer sthsth_ptr or _p
  - since a pointer contains an address, only an address may be assigned to a pointer
  - can initialise a pointer during initialisation, alternatively, you can declare the pointer first, then assign the value to the pointer
  - we can access a var directly or indirectly thru pointers by using the indirection operator (or dereferencing operator)*
    - e.g. printf("a= %d\n", *a_ptr); equivalent to printf("a = %d\n", a)
    - *a_ptr is synoynmous with a
  - when we store address of var to a pointer, pointer points to the var, assigning value to the pointer *p will change the value of that var too
  - when pointing the pointing to var, no need star (e.g. b = &a)
  - can decalre double a, b*;
  - if you want to print out the value of a pointer, just printf("%d.., *p1)
  - *p1 refers to the address of the var the pointer is pointing to, hence the value; (*p1)++: bracket needed as dereferencing operator has a lower precedence than the increment operator -> no bracket, pointer will be increment first then do a dereference (increment var vs increment pointer)
  - [pointer to pointer / double pointer]([url](https://www.geeksforgeeks.org/c-pointer-to-pointer-double-pointer/))
```c
...
type ** ppa = &pa // where pa is a pointer var
**ppa = some_value // dereferencing two times to get the var that is pointed to by pa
type* parr[10] = {pa, ppa} // an array of pointers

// make 2-D array by declaring pointer to pointer
int arr1[4] = {0};
int arr2[4] = {0};
int arr3[4] = {0};

int* parr[3] = {arr1, arr2, arr3}; //array name = address of its first element
printf("%d", parr[0][1]); // 0
```

**incrementing pointer**
- recall data types take up a fixed bytes always (e.g. int is ususally 4 bytes)
- increment the address by the size of data type it is pointing to (increment by 1 int, 4 bytes...)

**pointer to multidimensional array**
- *(arr + i) -> incrementing the array index by i elements 
- *( *(arr + i) + j) -> increment by row, then by columns, equivalent to arr[i][j]

**common mistake with pointers**
- int *n; *n = 123; printf("%d\n", *n); ➡️ [segmentation fault](https://stackoverflow.com/questions/2346806/what-is-a-segmentation-fault) (core dumped) -> must remove the file "core" from your directory, takes up a lot of space

**why use pointer**
- when we pass the address of a var into a function:
  1. to pass the addresses of two or more var to a function so that the function can pass back to its caller new values of the var
  2. to pass the address of the first element of an array to a function so that the function can access all elements in the array (then use pointer arithmetic to access the rest; useful when array is very large)

**void pointers**
- `void* e1`
- when you can't confirm the type which the pointer is pointing to, usually when a standard function is receiving a pointer as argument
- can use type casting when initialising the function e.g. `*(int*)e1`

2. Functions
- libraries offering functions for you to use
- function prototype -> what type the func returns, and what arguments it expect (e.g. <stdio.h> has func prototypes)
- calling function
  - note: when using scanf(), must refer &x and &y -> adresses, scanf needs to modify x and f and the only way a function can modify var is through its address
  - need to -lm during compilation (tell c to take the code from math library and compile it with our program)

**User-defined functions**
- we can define and use our own functions
- for a set of operations that are used more than once (computation), good to encapsulate it in a function (code resuability)
- we declare a function prototpye by declaring the type the function is returning and the arg(s) it takes (e.g. double circle_area(double);)
- then we define the function outside of the main() function (e.g. double circle_area(double diameter) {...})
- Note
  - good practise to put func protypes at the top of the program, before the main() function, to inform the compiler of the functions that your program may use and their return types and param types. (like include <studio.h> is putting all of the prototypes at the top of the program)
  - a func prototype includes only the functions's return type, func name, and the data types of the params but names of params no need
  - func definition follow after the main() function (easier to analyse)
  - without func prototypes -> get warning or errors (c assumes the default return type is int)

**pass-by-value and scope rule**
- actual params (actual args) are passed to the formal params by a amechanism known as pass-by-value; scoping (global, local var)
- we pass in the values of the var into the args
- formal params are local to the function they are declared in
- var declared within the func are also local to the func
- local params are var are only accessible in the fun they are declared (**scope rule**)
- when a func is called
  1. activation record created in call stack
  2. mem allocated for the local params and var of the func
  3. once the function is done, activation record is removed and mem allocated for the local params and var is released
- hence local params and var of a function exist in mem only during the execution of the function. they are called automatic var (automatically created and automatically removed)
- in contrast, static var exist in the mem even after the function is executed
- therefore, var in the main function and var in the local scope of the function are different even if a in passed into the function -> different activation records (two different var) -> only the value is passed into the function thru the params

**consequence of pass-by-value**
- func cannot change any var declared outside of its scope

**func with pointer params**
- func may or may not return a value (void or data type)
- all params and vars in the function are local to the function
- args from a caller are passed by value to a func's params
- to allow a func to return more than one value or to modifu values of var defined outside of it -> pointers (access var using its address)
- pointers and functions
  - func prototype: params still have decalre type, but with * to represent pointers
  - in definition, we pass in the pointers to the vars
  - dereference the pointer (go to the var the pointer is pointing to directly)

**pointer to a function**
- [guide](https://www.geeksforgeeks.org/function-pointer-in-c/)
- `return_type (*func_ptr)(param_type) = &func` or `return_type (*func_ptr)(param_type) = func`
  - function names can also get functions' addresses as well like array names
- pass in argument by `(*func_ptr)(arg);` or `func_ptr(arg);` if you used the function's name directly
- `*(void(*)())0` can be a pointer to a function type just like int*, char*... with 0 as the address that could store a function
- rename: `typedef void (* pf_t)(int); // void(*)(int) renamed to pf_t`
- array of function pointers (function pointer of the same type, meaning return value, argument lengths and types should be the same): `return_t (*arr[n])(...arg_type) = {...function_names};`
  - can straightaway call `arr[i](args)`

**common mistake**
- accessing var in main() func in a user-defined func

## arrays, strings, and structures

> data collection and organisaition (for the purpose of more logical representation and ease of manipulation)

1. Arrays
> homogeneous collection of data (of the same data type)
- includes the element type, array name, and size (max no of elements)
- array elements occupy contiguous mem locations and are accessed through indexing (from index 0 onwards) (next to each other)
- decalration:
  - int c[30] -> elem type, array name, and size
  - to initialise it, delcare and assign to {e1, e2, ..., en} (can be initialised at the time of declaration)
  - initialisation at declaration can omit the size of the array
  - initialisation can also: declare less elem than max -> the rest will be 0;
  - int d[5] (null) vs int d[5] = {0} (set to 0 for all)
  - cannot declare then assign (e.g. int f[5]; f[5] = {1...})
- note:
  - to access the individual array elem from within a func -> have to pass in the address of the elem (e.g. &c[i])
  - cannot simply set an array to another:
    - an aray name is fixed (constant) pointer; it points to the first elem of the array and this cannot be altered
    - the code will attempt to alter an arrpointer to make it point elsewhere (illegal)
- array and pointers
  - when the arr name a appears in an expr, it refers to the address of the first element (ie &a[0]) of that array; printf("%p\n", a);)
  -  using memcpy() in <string.h> library function to copy one arr to another (out of syllabus)
  -  array pointers subtraction --> &arr[n - 1] - &arr[0] = n - 1 (the number of elements between the last elements and the first inclusive)
- array params in functions
  - returntype func_name(type [] ...)
  - note the arr name is a pointer to the arr -> passing it into param copies the content of the arr over to a new arr (local function)
  - function prototype
    - name of params optional in prototype
  - function header in the function definition
    - no need to put array size [] insdie, even if array size is present, compiler just ignores it
    - instead, provide the array size through another parameter
    - this is true for prototype too
  - since an arr name is a pointer, using int * vs int [] in prototype is allowed (another alternative syntax, syntatic sugar for array param in function prototype and function header in the function definition)
  - modifying array in a func
    - no need to use address operator since the arr itself is a pointer
    - but func can modify the content of the arr it received whether you intend or not (implication)
    - thats mean when array is passed into it, `sizeof` operation on the array gives 8 bytes because that is the size of the pointer datatype

### [Pointer to array](https://www.geeksforgeeks.org/pointer-array-array-pointer/)
- a nuance between pointer to the 0th element of the array and pointer to the entire array
```c
...
int arr[5] = {0};
int* p = arr; // pointer to the 0th element; p++ increase by the size of the data type
int (*ptr)[5] = $arr; // pointer to the entire array; ptr++ increase by the total size of the array
```
- to declare pointer to array of pointers, note the type is: `datatype** p = arr;`

### multidimensional array
  - [pointer to MD array](https://stackoverflow.com/questions/14808908/pointer-to-2d-arrays-in-c)
    - `int (p*)[5] = &arr` where arr[3][5] is a 2D array will be a pointer to the first element of the array, each increment will increase by the size of the row to the next row. Then to access elements, we can `*( *(p + i) + j)` as deferencing here: `*(p+i)` gives `p[i]` (the 'inner' array)

2. strings
> an array of chars with a null character "\0" at the end of the array (terminated by)
- we can use string functions (include <string.h>) to manipulate strings
- declare a string as an arr of chas then assign char to an elem of an arr of chars
- or initialiser for string
  - char fruit_name[] = "apple" (double quote! automatically null at the end)
  - char fruit_name[] = {'a', 'p',...,'\0'}
- so always one more size for the last null terminator
- functions read string from stdin (keyboard)
  - [fgets](https://www.geeksforgeeks.org/fgets-gets-c-language/)(str, size, stdin); ([standard input](https://stackoverflow.com/questions/44423865/what-exactly-is-stdin); file reader)
  - scanf("%s", str); (read until first white space)
- print string to stout (monitor)
  - puts(str); // terminates with newline
  - printf("%s\n", str)
  - gets(str) read a string interactively, however, due to security reason, we avoid it and use fgets() function instead (stackoverflow attack)
- fgets() also reads in newline character eat\n\0 (reads all the way to the newline character)
- string functions <string.h>
  - strlen(s) : return the number of char in s
  - strcmp(s1, s2) : compare the ascii values of the corresponding chars in string s1 and s2
    - return a negative int if s1 is lexicographically less than s2
    - positive if s1 is greater or
    - 0 is s1 and s2 are equal
  - strncmp(s1, s2, n): compare first n char of s1 and s2
  - strcpy(s1, s2): copy the string pointed to by s2 into arr pointed to by s1.
    - func returns s1
    - but be careful of stackoverflow attack
  - strncpy(s1, s2, n) copy first n char od string pointed to s2 into s1 (recommended)
  - importance of '\0' in a string
    - to be treated as a string, arr of char must be terminated with null char
    - string functions cannot work properly on arr of char
    - may result in illegal access of memory if not properly handled by '\0'
  - cannot assign string value directly -> strcpy or use a pointer:
```c
#include <string.h>

char str[50] = "a string";
strcpy(str, "New Value");
// can't do this: str = "another"; 

// or pointer:
char *str = "Hello, World!";
str = "New Value";
```
  - string literals are immutable in c, but character array is mutable:
```c
#include <stdio.h>
int main() {
    // String literal (immutable)
    char *immutable_string = "hello";
    // Attempting to modify a string literal results in undefined behavior
    // immutable_string[0] = 'H';  // DON'T DO THIS!

    // Character array (mutable)
    char mutable_string[] = "hello";
    mutable_string[0] = 'H';  // Modifies the string
    printf("%s\n", mutable_string);  // Output: "Hello"

    return 0;
}
```

3. [structure](https://www.geeksforgeeks.org/structures-c/)
> structure allow grouping of heterogeneous members of different types, a group canbe a member of another group  (structure type, a new data type)
- typedef struct { data..} struct_name
- note: a type is NOT a variable (data type vs var)
- the following is a definition of a type, not a declaration of a var
`typedef struct {`
    `int name;`
    `float name;`
`} struct_name;`
  - a type needs to be defined before we can declare var of that type
  - no memory is allocated to a type
- declaration syntax is similar to declaring ordinary var
  - before function prototypes but after preprocessor directives
  - data_type data_name (e.g. result_t result_1)
- initialisation
  - syntax is like array initialisation: e.g. result_t result1 = { 123321, 93.5, 'A' } ;
  - or { {...} } if there is another struct within the struct
- accessing members of a structure var by using the dot (.) operator
- a bit like object in OOP languages
- the structure members are read in individually the same way as do for ordinary variables
- assigning structures
  - we use the dot operator to access individual member of a structure var
  - if we use the structure var's name, we are referring to the entire structure
  - we may do assignments with structures e.g. result2 = result1 (unlike arrays)
- return structure from function
  - given a data type struct_type, define a func func() that returns a structure of this type -> struct_name func(...)
  - to call this function: just call and assign the returned value to a struct of that type
- pass structure to function
  - as a parameter in a function is akin to assigning the structure to the parameter
  - the entire structure is copied (i.e. members of the actual param are copied into the corresponding members of the formal parameter)
  - pass-by-value
  - can pass the structure or pointer var to the structure to the function, and the access of members might be slightly different, but pass in by pointer is preferred so to ensure efficiency is not compromised when passing in structs that are very big in size:
```c
void func(struct Name n)
{
  n.attr; // accessing member through dot operator
}
// need to pass in the pointer to the struct!
void func(struct Name* n)
{
  n->attr; // accessing member through arrow operator
}
```
- combine structure and array: give lot of flexibility in organising data
- pass address of structure to function
  - pass structure to function is just copying the value over (pass by value) -> a separate copy of it is made in the called function
  - original structure var will not be modified by the function
  - to allow modification -> pass in adrress (pointer) of the structure var to the function
  - note that passing an arr of structures to a function is a different matter. as the arr name is a pointer, the function is able to modify the array elements
  - but note *struct_pointer.mem -> dereferncing the member, dot operator has higher precedence, so must put (*struct_pointer).mem
- arrow operator ->
  - synatatic sugar 
  - (*struct).mem is equivalent to struct->mem

## Control structures in C

**Selection structures**
-> C provides two control strcutres that allow you to select a group of statements to be executed or skipped when certain conditions are met
1. if-else structures or just if(condition)
2. switch statements
   - switch(var/expr) + case value1... case value2... default
   - if var/expr = value1 it will executes case value1
   - need a break; (if you do not intend the execution to fall into the next case)
  
Condiion and relational operators (in details)
- a condition is an expression eval to true or false
- composed of expressions combined with relational operators
- C does not have boolean values (everything is a number)
  - false is 0, anything that is not 0 is true
  - 1 is the default truthy value

Logical operators:
- complex condition: combining two or more Boolean expr
- && || !
- logical table is helpful

Evaluation of Boolean expr:
- done according to precedence and associativity
  1. primary expr operators (left to right)
  2. unary (right to left)
  3. biary (left to right)
     - * / % more + - more >,<,<=,>= more && more ||
  5. ternary (right to left)
  6. assignment (right to left)
- note: to prevent ambiguity, add parentheses for readability and correct intents

Short Circuit evalutaion (interesing feature in C)
- C will not evaluate the logical expr if it knows it's false for sure (lazy evaluation)
- as soon as it knows the outcome of expr, it can stop evaluating
- || and &&

**Reptition Structures**
- loops
- while ( condition ), do while( condition ), for (initialisation; condition; update)
- do while's body is always going to be executed at least once but while will not execute if the expr is false at first loop
- using break in a loop
 - in a nested loop, break only break out of the inner most loop where it is declared
- continue
  - skip a value but continue to execute
  - same as nested loop, it skipped a value within the nested loop 

## [Tokens](https://www.geeksforgeeks.org/tokens-in-c/?ref=lbp)

> smallest individual element in C that is meaningful to the compiler. 
> keywords, identifiers, constants, strings, special symbols, operators

- **[Keywords](https://devdocs.io/c-c-keywords/)**
> predefined, [reserved](http://c.ihypress.ca/reserved.html![image](https://github.com/Jeremiah33-3/C-and-Computer-Organisation/assets/111181492/4b899888-0ebf-44d9-a27a-dd4492b271ca)
) words (unable to redefine)

"niche" keywords
- auto: default storage class variable (automatic storage duration); declared inside function/block; has garbage values assigned to them (local var)
- enum: user-defined data type holding a list of user-defined integer constants, with value as its index starting from 0 by default
- extern: declare a variable/function that has external linkage outside of the file declaration (getting the definition from another file)
- [static](https://stackoverflow.com/questions/572547/what-does-static-mean-in-c): create static var that is used within the scope of the translation unit
  - preserve states and allow encapsulation
  - static var keeps its value between invocations if it's inside a functin
  - A static global variable or a function is "seen" only in the file it's declared in
- register: var stored in the CPU register instead of memory (for frquently used var and needs faster access)
- struct: used to declare a structure, a collection of variables; user-defined data type
- union: used to declare a union, a collection of var declared under the same memory location; user-defined datatype ([diff between union and struct](https://stackoverflow.com/questions/346536/difference-between-a-structure-and-a-union)

- **identifiers**
> the namespace, var/const names

- **constants**
> vairables with fixed values. cannot be redeclared once defined.
> a symbol whose value never changes (not in python, you can still change the value)
- define using preprocessor directives: cannot simply change the value (disallowed in C) 

- **strings**
> array of characters ending with a null character (‘\0’).

- **special symbols**
> symbols with special meaning such as the {}, [], ()
List:
  - Brackets[]: Opening and closing brackets are used as array element references. These indicate single and multidimensional subscripts.
  - Parentheses(): These special symbols are used to indicate function calls and function parameters.
  - Braces{}: These opening and ending curly braces mark the start and end of a block of code containing more than one executable statement.
  - Comma (, ): It is used to separate more than one statement like for separating parameters in function calls.
  - Colon(:): It is an operator that essentially invokes something called an initialization list.
  - Semicolon(;): It is known as a statement terminator.  It indicates the end of one logical entity. That’s why each individual statement must be ended with a semicolon.
  - Asterisk (*): It is used to create a pointer variable and for the multiplication of variables.
  - Assignment operator(=): It is used to assign values and for logical operation validation.
  - Pre-processor (#): The preprocessor is a macro processor that is used automatically by the compiler to transform your program before actual compilation.
  - Period (.): Used to access members of a structure or union.
  - Tilde(~): Used as a destructor to free some space from memory.
 
- **[operators](https://www.geeksforgeeks.org/operators-in-c-set-2-relational-and-logical-operators/)**
> symbols that trigger an action when applied to C variables and other objects.

Unary, Binary, and Ternary Operators:
  - Unary operators only require a single operand (increment, decrement)
  - binary require two operands (Arithmetic operators, Relational Operators, Logical Operators, Assignment Operators, Bitwise Operator)
  - ternary requires three operands (conditional operator ? : )

Arithmetic operations (in order of precedence):
1. primary expr operators ( (), expr++, expr--) is left associative 
2. unary operators (+, -, ++, --, (_typecast_) is right associate (e.g. x = -23)
3. binary operators (+, -, *, /, %) is left associative
4. assignment operators (+=, *=..)
- generally: execution is left associative, respects parentheses rule, then precedence rule, then associative rule
- truncate result if result can't be stored  (e.g. int n...; n = 9 * 4.5)
- [pre-increment (++expr) vs post increment (expr++) ](https://www.geeksforgeeks.org/pre-increment-and-post-increment-in-c/)
  - pre-increment operator increment the value of a var BEFORE using it in an expression
  - post-increment operator increment the value of a var AFTER using it in an expression
  - they have different precedence and associativity too (precedence of postfix > prefix; postfix is left associative, prefix is right associative)

A more detailed Operator Precedence and Associativity article can he found [here](https://www.geeksforgeeks.org/operator-precedence-and-associativity-in-c/).

Mixed-type arthmetic operators:
- when type casting and arithemetic operations occur in a statement
- which leads to **type casting**
  - use a cast operator to change the type of an expr
  - syntax: (type) expr
  - parenthesus are important -> (type) aa/bb or (type) (aa//bb)

External, internal, and no linkage
_Sources:_
_- https://stackoverflow.com/questions/1358400/what-is-external-linkage-and-internal-linkage_
- External linkage means the variable can be accessible by the whole program, not just within the same translation unit.
- Internal linkage refers to variable only accessible within the scope of translation unit default linkage is external

## Common header files

### Stdio.h
> What is [header files](https://www.geeksforgeeks.org/header-files-in-c-cpp-and-its-uses/)

> utility functions in sum, the header files contain a set of predefined library functions

1. sizeof(data type)
  - gets the size of the data type in bytes (e.g. sizeof(int))
  - note: sizeof is an [operator](https://www.geeksforgeeks.org/sizeof-operator-c/) 
2. scanf()
  - note: scaf(%d, &age) -> need & for address of operator 
3. printf()

### math.h
> for mathematical functions (need to compile with -lm option in sunfire)

### string.h 
> for string functions
