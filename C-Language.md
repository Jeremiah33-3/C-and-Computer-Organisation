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
