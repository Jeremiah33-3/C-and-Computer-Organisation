# C Programming Language stuffs 

## [Documentation](https://devdocs.io/c/)
- https://devdocs.io/c/

## Structure 

CS2100 says:
- a basic c program has 4 main parts: preprocessor directives (header, definition/macro expansions), input (thru stdin's scanf or file input), compute (arithmetic operations and assignment statements), output (thru stdout using printf, or file output)
- input/output
  - [format specifiers](https://www.geeksforgeeks.org/format-specifiers-in-c/), which are placeholders for values to be displayed or read
  - width: with printf(), %5d displays an int in a width of 5, right justified
  - decimal places: %8.3 display a real no (float or double) in a width of 8, with 3 decimal places, right justified.
  - for scanf(), use format specifiers without indicating width. decimal places...
  - \n is an eg of [escape sequence](https://www.geeksforgeeks.org/escape-sequence-in-c/) -> to display certain characters (with special meaning, regex, newlines..) properly. 

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

## [Tokens](https://www.geeksforgeeks.org/tokens-in-c/?ref=lbp)

> smallest individual element in C that is meaningful to the compiler. 
> keywords, identifiers, constants, strings, special symbols, operators

- **[Keywords](https://devdocs.io/c-c-keywords/)**
> predefined, reserved words (unable to redefine)

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
> vairables with fixed values. cannot be redeclared once defined

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
3. printf()

### math.h
> for mathematical functions (need to compile with -lm option in sunfire)

### string.h 
> for string functions
