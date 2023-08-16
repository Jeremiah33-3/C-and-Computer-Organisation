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

Q: how are real numbers represented in a computer system? -> finite no of bits, real no are represented in their **approximate** values.
- remember that everything needs to be stored in a real, physical, electronics, which is finite -> finite range and accuracy (cannot be stored in arbitrary accuracy)


