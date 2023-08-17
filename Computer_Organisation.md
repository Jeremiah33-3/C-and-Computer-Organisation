# Computer, number system, ands so on

## Programming languages and computer organisation
> a __formal__ language that speicifies a set of __instructions__ for a computer to implement specific algorithms to __solve problems__.

Level of abstraction in descending order: 
- high-level language: level of abstraction closer to problem domain, which prodvides productivity and portability (C, JS)
- assembly lang: textual and symbolic representation of instructions (for the machine to understand), and is translated by a compiler. (for MIPS)
- Machine code: a squence of 0s and 1s, binary bits of instrustions and data for the processor to understand, change by assembler, low-level langugae (for MIPS)

Abstraction layers, hardware/software stack in the computer:
- Software stack
  - application software (cannot run directly on the computer -> needs additional software)
  - additional software is provided through the *operating system.*
    - loader, scheduler (run concurrency), device drivers
  - compiler, aseembler, linker in the computer runs to produce the application software to run on the computer -- the bridge between application software and operating system
- Hardware stack 
  - processor, memory, I/O system (CS2100)
    - underlining these 3 major parts are two important concepts of datapath & control design which apply in particular to processor (control unit)
  - digital logic design (CS2100)
  - circuit design 
  - transistors
- bridge bwtween software and hardware: instruction set architecture (ISA), 0s and 1s (CS2100)

Parts of computer in more details (hardware):
- PC Motherboard
- Intel i7 processor
  - inside the core (CPU): control unit and ALU
 
Computer organisation:
> the study of internal working, structuring and implementaion of a computer system
- refers to the level of abstraction **above the digital logic level, but below the system level.**
- why study:
  - understand optimisation better
  - make better purchasing decisions
  - build better softwares

## [von Neumann Architecture](https://en.wikipedia.org/wiki/Von_Neumann_architecture)

An architecture that describes a computer consisting of 
1. central processing unit (CPU) with registers, control unit (containment of instruction register and program counter) and arithmetic/logic unit (ALU)
2. memory which stores both program and data in random-access memory (RAM)
   - 3 types of mem: RAM, ROM, Flash (kind of RAM but retains mem when power is switched off)
4. I/O devices (keyboard, screen...)

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
  - char: 1 byte (enclosed in a pair of single quotes) -> char is just a 8-bit integrer in C
- note: [signed: take both positive and negative values](https://stackoverflow.com/questions/621290/what-is-the-difference-between-signed-and-unsigned-variables) 
- strongly types vs weakly typed
  - strongly: evrey var needs to be declared with a type vs weakly: type depends on how the var is used
  - other aspects: static/dynamic type checking, safe type checking, type conversions
  - implitcit type conversions [in C](https://www.geeksforgeeks.org/implicit-type-conversion-in-c-with-examples/)
  - C allows pointer values to be explicitly cast

## Data representation and Number Sytem 

Everthing is a number in C... But how are they representated as numbers? -> 0s (<1.15V) and 1s (>3.75V)

**Data Representation**
- C has basic data types: float, int,  double, char
- how data representated depends on the type (context, that's why needs to declare data type) -> the identical strings/same combination of 0s and 1s may give different meaning depending on the type
- **Data are internally represented as sequences of bits (binary digits). A bit is either 0 or 1.**
 - other units: byte, nibble (4 bits), word (multiple of bytes depending on the computer architecture; a single unit of transfer to the CPU)
- N bits can represent up to 2^N values 
- to represent M values, math.ceiling(log2M) bits required -> have to be whole number and even number (math floor will be short of one bit)

**Decimal (base 10) Number System**
- a weighted-positional number system
- base (radix) is 10
- symbols.digits = {0,1,2...9}
- each position has a weight of power of 10
- e.g. decimal is represented by negative powers of 10, thousands has a power of 10^3

**other number system**
- binary (base 2)
  - weights in powers of 2
  - binary digits
- octal (base 8)
  - weights in powers of 8
  - octal digits: 0,1,2...,7
- hexadecimal (base 16)
  - weights in powers of 16
  - hexadecimal digits: 0,1,2...,9,A,B,..,F
- base/radix R
  - weights in powers of R
- **NOTE**: in some programming languages/softwares, speicial notations are used to represent numbers in certain bases
  - C:
    - prefix 0 for octal
    - prefix 0x for hexadecimal
  - QTSpim (MIPS simulator)
    - predix 0x for hexadecimal
  - Verilog:
    - prefix 8"b, h"h, h"d
    
**Base-R to Decimal Conversion**
- subfix is important -> indicates base -> multiple each number according to the powers of R -> demical number

**Decimal to Binary Conversion**
- for whole numbers: repeated division by 2 method
  - division, divides quotient, reminded remainders
  - the remainders forn the ans, with the first remainder as the least significant bit LSB (rightmost) and last as the most significant bit MSB (leftmost)
- for fractions: repeated multiplication by 2 method
  - until fractional product is 0
  - need to substract away the carries
  - the carried digits are the answer, the first carry is the MSB, the last as the LSB
  - answer got to have a dot in front (fractions)
- **note**: for decimal to base-R we use the same technique as decimal to binary except the base changes

__in general, conversion between bases can be done via decimal(interconnection, bridge)__

**Convert binary to octal/hexadecimal**
- binary to octal: partition in groups of 3 (by binary number system)
- octal to binary: reverse
- binary to hexadecimal: partition in groups of 4
- hexadecimal to binary: reverse

**ASCII Code**
> used to represent characters (and Unicode)
- 7 bits plus 1 parity bit (odd or even parity)
- character representation of numbers is different from integer reprensatation
- if want to convert from char number to int number, subtract away 0 in character
- [ASCII](https://www.geeksforgeeks.org/ascii-table/) Table
- characters are represented by numbers

**Negative numbers**
- unsigned no: only non-negative values
- signed no: include all values (positive and negative)
- 3 common representations for signed binary numbers: sign-and-magnitude. 1s complement, 0s complement
- Sign and maginitude
  - the sign is represented by a sign bit -> 0 for + and 1 for -
  - one bit sign and 7 bits magnitude
  - largest value: +127 (10)
  - smalled value: -127 (10)
  - positive and negative 0s -> sign bit
  - to negate a number -> invert the sign
  - subscript sm
  - **Limitations**: not good for doing arithmetic operations
- 1s complement
  - can do arithmetic
  - given a number x which can be expressed as an n-bit binary number, its negated value can be obtained in 1s-complement representation using: -x = 2^n -x -1
  - the negation of the bits (invert)
  - largest value: +127, smallest: -127
  - 2 zeros (all 0s or all 1s)
  - definition of complements: the sum of the two numbers produce 0
  - subscript: 1s
  - the MSB still represents the sign: 0 for positive, 1 for negative
  - **Limitation**: lost 1 value on the negative side
  - **Advantage**: trivial to implement in the computer hardware 
- 2s complement
  - given a number x which can be expressed as an n-bit binary number, its negated value can be obtained in 2s-complement representation using -x= 2^n -x
  - to negate the binary no, invert all the bits then add 1 _(done in hardware too)_ OR right to left, store first 3 numbers at it is, then invert the rest of the bits
  - "2s complement of __"
  - largest value: +127, smallest value = -128
  - 1 zero only (the entire 0s)
  - the MSB still represents the sign: 0 for positive, 1 for negative
  - subscript: 2s
- comparison in 4-bit system
  - positive values remain the same for all 3 representations
  - negative values: different
    1. sign and magnitude: negate the sign bit at MSB 
    2. 1s complement: invert all bits
    3. 2s complement: 1s complement plus 1
- note: overflow positive number becomes negative number (add the bit together and see)
- we can extend the idea od complement on fractions

_Note: the weight of sign bit in 2s complement is -2^(n-1), in 1s is -2^(n-1) -1 )_

**2s complement on addition/substraction**
- Algorithm for addition of integers A + B
   1. perform binary addition on the two numbers
   2. ignore the carry out of the MSB
   3. check the overflow, overflow occurs if the carry in and carry out of the MSB are different, or is result is opposite sign of A and B
- Algo on substraction (A + (-B))
  1. take 2s complement of B
  2. add the 2s complement of B to A
- overflow ❗
  - signed no are of a fixed range
  - if the result of addition/subtraction goes beyond the range, an overflow occurs
  - can be detected if positive add positive becomes negative or negative add negative becomes positive
 
**1s complement on addition/subtraction**
- algo for addition
  1. perform binary addition on the two numbers
  2. if there is a carry out of the MSB, add 1 to the result
  3. check for the overflow, overflow occurs if result is opposite sign of A and B
- algo for subtraction
  1. take 1s complement of B
  2. add the 1s complement of B to A

**excess representation**
> another way of representing negative values
- allows a range of values to be distributed evenly between the positive and negative values, by a simple translation (addition/substraction)
- usually we will do excess- 2^(n-1) where n is the number of bits

Q: how are real numbers represented in a computer system? -> finite no of bits, real no are represented in their **approximate** values.
- remember that everything needs to be stored in a real, physical, electronics, which is finite -> finite range and accuracy (cannot be stored in arbitrary accuracy)
**representation**
- fixed point representation
  - no of bits allocated for the whole no part and fractional part are fixed
  - implemented in the hardware so cannot be changed
  - **problem**: limited range
- floatin point representation
  - represent very small or very large no
  - 3 components: sign, exponent, mantissa (fraction)
**IEEE 754 FLoating point rep**
- have 3 components: sign, exponent, mantissa (fraction)
  - sign: the positive or negative (0 for positive, 1 for negative)
  - exponent: represented in a different sign number system.
    - gives the power of the representation
    - exponential power + 127 
  - mantissa: fraction part, sign applies only to mantissa (normalised with n implicit leading bit 1)
    - scienctific representation? 1.101 * 2^2
    - so that there is standard format and we can save bits (we know for sure first bit is 1) -> one additional bit of accuracy, hidden bit
- base (radix) assumed to be 2
  - two formats
    - single precision (32 bit): 1 bit sign, 8-bit exponent with bias 127 (excess-127), 23-bit mantissa 
    - double precision (64 bit): 1 bit sign, 11-bit exponent with bias 1023 (excess-1023), and 52 bit mantissa
  - we will focus on the single-precision format
- note: need to represent the number in binary
- hexadecimal representation -> binary number is more readable 



