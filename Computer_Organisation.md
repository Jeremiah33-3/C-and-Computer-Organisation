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
