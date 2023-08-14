# Computer, number system, ands so on

## [von Neumann Architecture](https://en.wikipedia.org/wiki/Von_Neumann_architecture)

An architecture that describes a computer consisting of 
1. central processing unit (CPU) with registers, control unit (containment of instruction register and program counter) and arithmetic/logic unit (ALU)
2. memory which stores both program and data in random-access memory (RAM)
3. I/O devices

![model to display this architecture](https://upload.wikimedia.org/wikipedia/commons/thumb/e/e5/Von_Neumann_Architecture.svg/600px-Von_Neumann_Architecture.svg.png)

## Variables

> data used in the program

- var has name (identifier), data type, address, and contains a value which could be modified
- var declaration: data type and name (e.g. int count)
- var initialisation + declaration: assignment/initialised during declaration (e.g. int count = 3)
- without initialisation -> var contains an unknown value (may not be zero)
- C language mistakes: no initialisation (immediate assignment next line) and redundant initialisation (int count = 0; count = 123 or scanf("%d", &count))
- every var must be declared with data types; [list](https://www.geeksforgeeks.org/data-types-in-c/) of data types in C
  - int: 4 bytes (-21^31 to 2^31 - 1)
  - float: 4 bytes 
  - double: 8 bytes
  - char: 1 byte (enclosed in a pair of single quotes)
- strongly types vs weakly typed
  - strongly: evrey var needs to be declared with a type vs weakly: type depends on how the var is used
  - other aspects: static/dynamic type checking, safe type checking, type conversions
  - implitcit type conversions [in C](https://www.geeksforgeeks.org/implicit-type-conversion-in-c-with-examples/)
  - C allows pointer values to be explicitly cast
