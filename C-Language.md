# C Programming Language stuffs 

## [Documentation](https://devdocs.io/c/)
- https://devdocs.io/c/

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
 
## Pointers and functions

1. Pointer
C is high level lang -> but the lower end of the spectrum is due to:
- pointers which allow direct manipulation of memory contents
- has a set of manipulation operators, allowing efficient bitwise operations

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

**incrementing pointer**
- recall data types take up a fixed bytes always (e.g. int is ususally 4 bytes)
- increment the address by the size of data type it is pointing to (increment by 1 int, 4 bytes...)

**common mistake with pointers**
- int *n; *n = 123; printf("%d\n", *n); ➡️ segmentation fault (core dumped) -> must remove the file "core" from your directory, takes up a lot of space

**why use pointer**
- when we pass the address of a var into a function:
  1. to pass the addresses of two or more var to a function so that the function can pass back to its caller new values of the var
  2. to pass the address of the first element of an array to a function so that the function can access all elements in the array (then use pointer arithmetic to access the rest; useful when array is very large)

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

2. strings
> an array of chars with a null character "\0" at the end of the array (terminated by)
- we can use string functions (include <string.h>) to manipulate strings
- declare a string as an arr of chas then assign char to an elem of an arr of chars
- or initialiser for string
  - char fruit_name[] = "apple" (double quote! automatically null at the end)
  - char fruit_name[] = {'a', 'p',...,'\0'}
- so always one more size for the last null terminator
- functions read string from stdin (keyboard)
  - fgets(str, size, stdin); (standard in; file reader)
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
- ❗ note: in python, % is modulo, but in C, % is remainder 

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
> utility functions

1. sizeof(data type)
  - gets the size of the data type in bytes (e.g. sizeof(int))
2. scanf()
  - note: scaf(%d, &age) -> need & for address of operator 
3. printf()

### math.h
> for mathematical functions (need to compile with -lm option in sunfire)

### string.h 
> for string functions
