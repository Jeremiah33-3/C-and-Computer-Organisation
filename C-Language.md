# C Programming Language stuffs 

## [Documentation](https://devdocs.io/c/)
- https://devdocs.io/c/

## Structure 
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
