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

## MIPS (Microprocessor without Interlocked Pipelined Stages)

How a processor works? (particularly MIPS)

1. Instruction set architecture

High-level -> compiler -> assembler 
> ISA: an abstraction on the interface between the hardware and the low-level interface
- software (translated to the instruction set) and hardware (implementing the instruction set)
- includes everything programmers need to know to make the machine code work correctly
- allows computer designers to talk about functions independently from the hardware that performs them
- this abstraction allows many implementations of varying cost and performance to run identical software

2. Loading large constant (32-bit constant into a register)

First, use "load upper immediate" (lui) to set the upper 16-bit 
  - lui $t0, 0xAAAA
  - t0 register ^
  - lower-order bits filled with zeros
Second, use "or immediate" (ori) to set the lower order bits
  - ori $t0, $t0, 0xF0F0
  - higher-order bits filled with zeros

3. Machine code vs assembly language
- instructions in binary vs human readable
- hard and tedious to code vs easier to write than machine code, symbolic version of machine code
- may also be written in hexadecimal for a more human-readable format vs may provide "pseudo-instructions" as syntatix sugar -> when considering performance only real instructions are counted

4.Components 

Two major components in a computer: processor and memory
processor: perform computations -> bus: bridge between the two components -> memory: storage of code and data 
- code and data reside in memory -> transferred into the processor during execution
- processor is faster than RAM (working) ->To avoid frequent access of memory
- Need instruction to move data into registers
  - Also to move data from registers to memory later
- since memory access is slow, we avoid frequent access of memory by providing temporary storage for values in the processor (known as registers)
  - moving data from memory into a register -- load
  - moving data from a register into memory -- store
  - variable mapping: loading a variable into another var (register), in assembly code when converting from c to assembly code
- reg-to-teg arithmetic
  - arithmetic operations can now work directly on registers only
  - arithmetic operation uses a constant value instead of register value
- to repeat a set of instructions/ make a chice (loop and switch, if-else)
  - control flow instruction: change the control flow based on condition
    - repetition and selection can both be supported
    - execution will repeat from the indicated position is condition succeeded
    - once condition is false, execution will continue sequentially (until we see another control flow instruction)
- Bus: data connector between mem and processor
- mem is typically simply a RAM 

Summary:
- the stored memory concept: both instructions and data are stored in memory
- the load-store model: limit memory operations and relies on registers for storage during execution
- major type of assembly instructions
  - mem: move values between memory and registers
  - calculation: arithmetic and other operations
  - control flow: change the sequential execution

General purpose registers:
- fast memories in the processor
  - data are transferred from memory to registers for faster processing
- limited in number
  - a typical architecture has 16 to 32 registers
  - compiler associates variables in program with registers [done by compiler !]
- registers have no data type
  - unlike progam variables
  - machine/assembly instruction assumes the data stored in the register is of the correct type
    - instruction: add -> store as 32 bit 2s complement; addu -> unsigned binary no.; fadd -> IEEE 754 repre (what registers store as instructed by the instruction
- 32 registers in MIPS assembly language
  - can be referred by a number ($0, $1,..., $31)
  - can be referred by a name (e.g. $a0, $t1)

MIPS Assembly Language
- each instruction executes a simple command
  - usually has a counterpart in high-level programming lang like C/C++, Java
- each line of assembly code contains at most 1 instruction
- \# (hex-sign) is used for comments (ignored by assembler)
- most of the MIPS arithmetic/logic operations have three operands: 2 sources and 1 destination + operation (op)
- arithmetic operation
  - addition
    - assume values of sources and dest are loaded into registers
    - known as variable mapping (done by compiler)
      - var-to-register mapping deals with step (1) (i.e. load) and step (3) (i.e. store). All computations are assumed to be in register for this set of instructions. 
    - actual code to perform the loading will be shown later in mem instruction
    - important: MIPS arithmetic op are mainly register-to-register (operations are register, destination also in register)
  - substraction
    - positions of sources are important for substraction (fixed)
  - complex expression
    - a single MIPS instruction can handle at most two source operands
    - so need to break a complex statement into multiple MIPS instructions (store in temp register $t0 - $t7)
    - can keep a register as dest and just add new values to it (e.g. $s4, $s0, $s1; $s4, $s4, $s2)
  - constant/immediate operands
    - immediate values are numerical constants that is frequently used in operations and MIPS supplies a set of operations specially for them
    - add immediate (addi)
      - syntax is similar to add instruction, but source2 is a constant instead of register
      - constant ranges from [-2^15 to 2^(15-1)] (16 bit 2s complement)
      - note: 1s -> [-(2^n-1 - 1) to (2^n-1 - 1)]; 2s -> [-2^n-1 to (2^n-1 - 11)]
    - no subi because can use addi with negative constant (want to have minimal number of instructions)

Register zero ($0 or $zero) 
- number zero (0), appears very often in code -> provide register zero ($0 or $zero) which always have the value 0
- for assignment (e.g. f = g)
- MIPS has an equivalent pseudo-instruction (move): move $s0, $s1 (MIPS Assembly code)
- peudo-ins are fake instructions that gets translated to corresponding MIPS instruction(s). Provided for convenience in coding only

Logical Operations 
- arithmetic instructions view the content of a register as a single quantity (signed or unsigned integer)
- new perspective
  - view register as 32 raw bits rather than as a single 32-bit number
  - possible to operate on individual bits or btyes within a word
  - shift left, shift right, bitwise AND, bitwise OR, bitwise NOR/NOT(OR), bitwise XOR
  - truth tables of logicaloperations (0 is false, 1 is true)
  - bitwise operation 
- list
  - sl (shift left logical): move all the bits ina word to the left by a number of positions; filled empited positions with zeros (sll $t2, $s0, 4)
  - srl 9shift right logical): shifts right and fills emptied positions with zeros
    - equivalent math op for shifting left/right n bits: multiplication by 2^n for left; division by 2^n for right shift
    - shifting is faster than mult/division -> good compiler translates such mult/division into shift instructions
  - and (bitwise AND): bitwise op that leaves a 1 only if both the bits of the op are 1 (and $t0, $t1, $t2)
    - also masking op (bit-mask is setting the irrelevant part to 0 i.e. masked)
    - place 0s into the positions to be ignored
    - place 1s for interested positions -> remain the same as original
    - $t2 is the mask
    - immediate version: andi
  - or (bitwise OR): bitwise op that places a 1 in the result if either op bit is 1 (or $t0, $t1, $t2)
    - immediate version: ori -> become 32-bit number
  - NOR (bitwise nor)
    - strange fact: no NOT instruction in MIPS to toggle the bits from 1 to 0 and 0 to 1
    - NOR instruction is provided: nor $t0, $t1, $t2
    - NOT op: nor $t0, $t0, $zero
    - nor instruction can help perform not op, os keep the instruction set small (one of the design principles)
  - xor (bitwise XOR): xor $t0, $t1, $t2
    - get NOT op from XOR: xor $t0, $t0, $t2(all 1s)
    - fact: there is no NORI but XORI because there is not much need for NORI (keep processor design simple)
   
  **more instructions**

  Mem organisation (general) RAM:
  - main mem can be viewed as a large, single dimension array of mem locations
  - each location of the mem has an address, which is an index into the arr (given a k-bit address, the address space is of size 2^k)
  - mem map on the right contains one byte in every location/add (byte addressing)
 
  Mem: transfer unit:
  - using distinct mem address, we can access a single byte (byte addressable) or a single word (word addressable)
    - word is usually 2^n bytes
    - word is the common unit of transfer between processor and mem
    - word is also commonly coincide with the register size, the int size and instruction size in most architectures -> design simplicity
  - word alignment
    - words are aligned in mem if they begin at a byte address that is a mulyiple of the number of bytes in a word
   
MIPS Mem instruction
- MIPS is a load-store register architecture
  - 32 registers, each 32-bit (4 byte) long
    - fast processor storage for data
    - in MIPS, data must be in registers to perform arithmetic
  - each word contains 32 bit
    - 2^30 mem words ( / 2^2 since each word is 2^2 byte long)
    - accessed only by data transfer instructions
    - MIPS uses byte addresses, so consecutive words differ by 4
    - mem holds data structures, such as arrays, and spilled registers, such as those saved on procedure calls
  - memory addresses are 32-bit long
    - word address should be divided by 4 (byte address)
- Load Word
  - lw $t0, 4($s0)
  - displacement, offset = + 4
  - steps
    1. mem address = $s0 + 4 = 8000 + 4 = 8004
    2. **mem word at Mem[8004] is loaded into $t0**
- Store Word
  - sw $t0, 13($s0)
  - 8000: base addresses
  - store the word into (content copied over to the new address)
  - steps:
    1. mem address: $s0 + 12 = 8000 + 12 = 8012
    2. content of $t0 is stored into word at Mem[8012]
- only load and store instructions can access data in mem
- arithemetic op (for add) are registers, not memory
- Others
  - load bytw (lb) and store byte (sb)
  - lb $t1, 12($s3)
  - sb $t2, 13($s3)
  - similar in working except that one byte instead of one word is loaded or stored
    - offset no longer needs to be a multiple of 4
  - MIPS disallows loading.storing unaligned word using lw/sw (throw exception)
    - psedo-instructions unalighed load word(ulw) and unaligned store word (usw) are provided for this purpose
    - ulw/usw can be translated to sequene of lb/sb + other operations
  - other mem instructions
    - lh and sh (load halfword and store half)
    - lwl, lwr, swl, swr
   
Common question: 
1. address vs value
- registers do not have types ❗
- a register can hold any 32-bit number
  - the no has no implicit data type and is interpreted according to the instruction that uses it (weakly-typed)
2. byte vs word
- consecutive word addresses in machines with byte-addressing do not differ by 1
- common error: assume that the address of the next word can be found by incrementing the address in a register by 1 instead of the word size in bytes
- for both lw and sw: the sum of base address and offset must be a multiple of 4 (i.e. adhere to word boundary)

**Making decision**
- to perform general computing tasks, we need to make decisions (if-else) and perform iterations (loop)
- DM in high level lang:
  - if anf goto statements
  - MIPS decision making instructions are similar to if statement with goto
    - goto is discouraged in high level lang but necessary in assembly
- DM instructions
  - alter the control flow of the program
  - change the next instruction to be executed (if-else for e.g.)
  - two types of DM statemetns in MIPS
    - conditional (branch)
      - bne $t0, $t1, label
        - to next instruction if $t0 and $t1 are equal, else branch to label
      - beq $t0, $t1, label
        - branch if $t0 === $t1 (opposite to bne)
    - unconditional (jump)
      - j label
        - jump to the instruction pointed to the label, no question/condition asked
    - NOTE:
      - selection: branch/jump down
      - repetition: branch/jump up
      - both cases, it's a goto operation 
  - a label is an "anchor" in the assembly code to indicate point of interest, usually as branch target (a pointer to the instruction)
    - NOT instructions NOR var (no mem) ❗

**Conditional branch: beq and bne**
- processor follows the branch only when the condition is satisfied (true)
- beq
  - go to statement label if value in registers are equal ($r1 === $r2, then to L1)
  - beq: branch if equal
  - C code: if (a == b) goto L1
- bne
  - go to statement labelled L1 if values in the two registers differ
  - bne: branch if not equal
  - C code: if (a!=b) goto L1
- e.g. L1: add $s0, $s1, $s2 (pointing to an instruction)
- Exit (label)

**Unconditional jump j**
- processor alwyas follow the branch
- j L1
  - jump to label L1 unconditionally
  - C code: goto L1
- technically equivalene to such statement: beq $s0, $s0, L1

**IF statements**
- condition instructions -> can use bne/beq
  - common technique is to invert the condition for shorter code (the lesser the instructions, the more efficient the code
- decompilation "reverse" process, invert -> beq becomes if (i != j)

**loop**
- any form of loop can be written in assebly with the help of conditional branched and jumps (use goto statements too)
- note: labels don't occupy memory, it is represented as address
- addi can be useful in for loop to check the "constant" value that results in termination (e.g. i < 10)
- can translate for loop to while loop it that's easier

**inequalities**
- no blt/bgt instruction in MIPS (for </>)
- use slt (set on less than) or slti
  - slt $t0, $s1, $s2 => $t0 set to 1 if less than, 0 is not
  - slti $t0, $s1, C
- to build a blt instruction
  1. slt $t0, $s1, $s2
  2. bne $t0, $zero, L
- blt is another eg of pseudo-instruction; aseembler translates (blt) instruction in an assemble program into the equivalent MIPS (two) instructions

**array and loop**
- use an index i/address to loop through the array
- use of "pointers" can produce more efficient code
- steps (algorithm)
  1. initialisation for result var, loop counter, and array pointers
  2. label
    1. calculate address
    2. load data
    3. perform task
  3. update loop counter and array pointers
  4. compare and branch
- to understand how many instructions are being executed, can try converting the code into C code


## MIPS Instruction Formats & Encoding

**Overview and motivation**
- assembly instructions transte to machine code for actual execution
- this section shows how to translate MIPS assembly code into binary patterns
- explains strange facts
  - why is immediate limited to 16 bits
  - whi is shift amount only 5 bits
- buiild a MIPS processor later

**MIPS Encoding**
- each MIPS instruction has a fixed length of 32 bits ❗
  - al relevant info for an operation must be encoded with these bits
  - fun fact: [encoding vs encrypting](https://www.geeksforgeeks.org/encryption-encoding-hashing/)
  - MIPS format
- consideration, additional challenge
  - to reduce the complexity of processor deisgn --> instruction encodings should be as regular as posisble
    - small number of formas (few variations as possible)
   
**Instruction classifications**
- instructions are classified according to their operands.
- instructions with same operand types have same encoding
  - R-format
    - register format: op $r1, $r2, $r3
    - instruction which use 2 source registers and 1 destination register
    - e.g. add, sub, and, or, nor, alt
    - special cases: srl, sll
    - details (page 8)
    - note: only 32 registers, so 5 bits for each registers is enough. It is enough for shamt field since shifting 32 bits clears the entire register (to 0)
    - 6, 5, 5, 5, 5, 6: opcode, rs, rt, rd, shamt, funct
    - log2 32 = 5
    - each field has a name: opcode...
    - each field is an independent 5 or 6-bit unsigned integer
      - 5 bit: represent any number from 0 - 31
      - 6 bit: represents any number from 0 - 63
    - fields:
      - opcode: partially specifies the instruction, equal to 0 for all R-Format instructions
      - funct: combined with opcode exactly specifies the instruction
      - rs (source reg): specify register containing first operand
      - rt (target reg): specify register containing second operand
      - rd (dest reg): specifiy reg which will receive result of computation
      - shamt: amount a shift instruction will shift by
        - 5 bits (0 - 31)
        - set to 0 in all non-shift instruction
  - I-format
    - immediate format: op $r1, $r2, Immd
    - instructions which use 1 source register, 1 immediate value and 1 destination register
    - e.g. addi, andi, ori, slti, lw, sw, beq, bne
    - (page 15)
    - problem with shamt: 5-bit, can only represent 0 -31 but immediates may be much larger than this (e.g. lw, sw instructions require bigger offset)
    - compromise: define a new instruction format partially consistent with R-format
      - if instruction has immediate, then uses at most 2 registers
    - note: keep some fields in the same position so that looking at the binary, we can quickly identify the instruction format. + ensure that retrieving rs and rt will be consistent across R and I-format
    - we merge rd, shamt, and funct to form a 16-bit field used for a constant value (immediate)
    - opcode (no funct field, opcode uniquely specifies an instruction), rs (specifies the source reg oprend if any), rt (speicifes reg to receive result -> difference with R-format)
    - immediate: treated as signed integer (2s complements) except for bitwise operations
      - 16-bits -> used to represent a constant up to 2^16 different values
      - large enough to handle offset in a typical lw and sw + most of the values in the addi, slti instructions
      - ❗therefore, cant store 32-bit constants in the instruction because the instruction itself is only 32-bit wide -> can only use parts of it + still need to encode opcode, rs, and rt
  - J-format
    - Jump formath: op Immd
    - j instruction uses only one immediate value

MIPS ref sheet:
![MIPS reference sheet](https://d20ohkaloyme4g.cloudfront.net/img/document_thumbnails/309c0dbde82179fa7e2ba89bff63e5da/thumb_1200_1480.png)

**Instruction Address**
- instructions store in mem -> they too have addresses
  - control flow instructions uses these addresses -> beq, bne, j
- instructions are 32-bit long -> so instruction addresses are word-aligned as well
- program counter ❗
  - > a special counter register that keeps address of next instruction being executed in the processor

**BRANCH: PC-relative addressing**
- uses I-Format
- opcode: specifies beq/bne
  - change value of the PC -> in other words, change address of next instruction 
- rs and rt specify registers to compare (source reg) 
- immediate
  - 16 bits, and mem address if 32 bits --> immediate not enough to specify the entire target address
  - question is how to store the address of the next instrucion then
- how to use branches (usual)
  - if-else, while, for
  - loops are generally small -> up to 50 instructions (means within the loop block, not too many instructions?) 
  - unconditional jumps are done using jump instructions (j), not the branches
  - conclusion: a branch often changes PC by a small amount
- therefore, solution: specify target address relative to the PC
  - target address is generated as : PC + 16-bit immediate field
  - the immediate field is a signed 2s complement int
  - can branch up to +-2^15 bytes from the PC --> should be enough to cover most loops
- can branch target range be enlarges ( > +- 2^15)
  - firstly, instructions are word-aligned
    - no of bytes to add to the PC will always be a multiple of 4
    - interpret the immediate as number of words (automatically multiplied by 4 (100 in base 2)
  - so we can extend range from +-2^15 _bytes_ to +-2^15 _words_ from the PC -> +-2^17 bytes from the PC --> can branch 4 times faster

**Branch calculation**
1. if branch is not taken
   - PC = PC + 4 (address of the next instruction)
2. branch is taken
   - PC = (PC + 4) + (immediate * 4)
- Observation:
  - immediate field specifies the number of words to jump, which is the same as the number of instructions to "skip over"
    - \+ / - depending on whether you are moving forward or backwards (offset)
    - count starting from the next instruction (PC is pointing to the next instruction PC + 4)
  - immediate field can be positive or negative
  - due to hardware design, add immediate to (PC + 4), not to PC (kiv) -> PC is always pointing to the next instruction to be executed
- L9P7
- pg 32-33 for summary

**encoding instructions in J format**
- for branches, PC-relative addressing was used (cuz we do not need to branch too bar)
- for general jumps -> may jump anywhere in the memory
- can't specify a 32-bit memory address to jump up --> need to represent opcode (6 bit)
- J format:
  - opcode 6 bits, target address 26 bits (label)
  - keep opcode field identical to R-format and I-format for consistency (6 bits)
  - combine all other fields to make room larger for target address
  - we can only specify 26 bits of 32-bit address
    - optimisation, like branches, jumps will only jump to word-aligned addresses (multiples of 4) --> last 2 bits always 0 0
    - we can leave then out and specify instructions instead 
    - we can specify 28 bits of 32-bit address
    - to get other 4 bits:
      - MIPS choose to take the 4 most sig bits from PC + 4 (next instruction after jump instruction) --> means that we cannot jump to anywhere in mem, but it should be sufficient most of the time
      - max jump range: 256 MB -> 2^28 bits
      - to jump to further range: special instruction _jr_ (target address is specified through a reg)

**addressing modes**
> different ways to calculate the final address of the operand 
1. register addressing: operand is a reg (add, sub, and, or, xor, nor, slt, sll, srl)
2. immediate addressing: operand is a constant (16-bit) within the instruction itself (addi, andi, ori, slti)
3. base addressing (displacement ~): operand is at the mem location whose address is sum of a reg and a constant in the instruction (lw, sw)
  - offset specifies how many bytes away from your base address
4. PC-relative addressing: address is sum of PC and constant in the instruction (beq, bne)
  - base address stores in PC
  - dislacement or offset is number of instructions (4 byte each instruction)
5. Pseudo-direct addrssing: 26-bit of instruction concatenated with upper 4-bits of PC (j)
  - since we gave some of the address (4 MSB in PC and last 2 00), it's called pseudo

## Instruction set architecture 

> part of the processor that is visible to the programmer or compiler writer -> the abstraction, the boundary between software and hardware

**RISC vs CISC**
> two major design philosophies for ISA
1. Complex Instruction Set Computer (CISC)
  - e.g. x86-32 (IA32) ..intel
  - use single instruction performs complex operation
    - VAX (mini computer) architecture has an instruction to multiply polynomials, string copying, FFT of images
  - smaller program size as mem was premium
    - because mem was expensive --> want to reduce program size 
  - complex implementation, no room for hardware optimisation

2. Reduced Instruction Set Computer (RISC)
  - e.g. MIPS, ARM (TV/Washing M/Mobiles, M1)
  - keep the instruction set small and **simple**, makes it easier to build/optimise hardware
  - burden on software to combine simpler operations to implement high-levle language statement
    - more and cheaper mem compred to history
    - compiler optimisation
   
**5 CONCENPTS IN ISA DESIGN**
1. Date Storage (where we get data?)

- Storage architecture
  - operands may be implicit (storage architecture) or explicit (reg thru MIPS)
  - von Neumann architecture
    - data (operands) are stored in mem
  - for a processor, storage architecture concerns with
    - where do we store the operands so that the computation can be performed?
    - where do we store the computation result _afterwards_?
    - how do we specify the operands?
  - major storage architectures
    - stack architecture
      - operands are implicitly on top of the stack
      - push and pop -- LIFO basis
      - no value in the stack after end of operation
      - e.g. add --> operands, add, pop result
    - accumulator architecture
      - one operand is implicitly in the accumulator (a special reg)
      - e.g. IBM 701, DEC PDP-8, Synatak 6502
      - load value of 1st operand into accumulator, then 2nd operand implicitly taken from the accumulator (added into the accumulator and stored) --> result taken from accumulator at the end
    - General purpose reg architecture
      - only explicit operands
      - load operands into respective source reg and specify dest reg 
      - reg-mem architecture
        - one operand in mem
        - Motorola 68000, intel 80386
      - reg-reg (or load-store) architecture
        - MIPS, DEC Alpha, ARM, M1
    - mem-mem architecture
      - all operands in mem
      - e.g. DEC VAX (mini comp but size of 4 refrigerators)
      - no use of reg; read the mem and perform operation and store directly 
  - slide 9 for comparison of addition operator (L10P4)
  - modern processors
    - GPR is the most common choice for storage design
    - RISC computers typically use reg-reg (load/store) deisgn (e.g. MIPS, ARM)
      - simplify hardware design and balanced pipeline (optimise performance)
    - CISC com use a miXture of reg-reg and reg-mem (e.g. IA32)

- General purpose reg architecture (MIPS)
  - add, $s1, $s2, $s3 (specify instr through reg)

2. mem addressing modes (how we access data from mem?)

- given k-bit address, the address space is of size 2^k
- each mem transfer consists of one word of n bits
- L10P5 explain the various address/data bus and control lines connecting the processor to the memory
- Endianness:
  - > the relative ordering of the bytes in a multiple-byte word stored in memory
  - Store LSB/MSB first (read from lowest/highest to highest/lowest address respectively)
    - big endian
    - little endian
    - collectively known as endianness
  - the endianness of MIPS is actually implementation specific
  - big-endian
    - MSB stored in the lowest address
    - e.g. IBM 360/370, Motorola 68000, MIPS (Silicon Graphics), SPARC
  - little-endian
    - LSB stores in lowest address
    - e.g. Intel 80x86, DEC VAC, DEC Alpha
    - but no need change ordering in pair in address (the 8 bits)

**Addressing modes**
- > ways to specify an operand in an assembly language
- in MIPS, only 3 addressing modes:
  - reg
    - operand is in a reg (e.g add $t1, $t2, $t3)
  - immediate
    - operand in specified in the instruction directly (e.g. addi $t1, $t2, 98)
  - displacement
    - operand is in mem with address calcuated as Base + Offset (e.g. lw $t1, 20($t2))
  - there are other addressing modes (reg indirect, indexed/based, direct or absolute, mem indirect, auto-increment, auto-decrement, scaled) (slide 19) 

3. operations in the instruction set (types of oprs supported)

**Standard Operations in an instruction set**
- arithmetic operations, logical operations, shift, data movement, control flow, subroutine linkage, interrupt, synchronisation, string, graphics
- slide 21 

**Frequently used instructions** 
- optimisation
- slide 22
  - make these (fui) instructions fast 
- profiler (SW)
  - code
  - mem
  - cache performance
  - most freq used instructions

4. instruction formats (types insr formats supported)

ISA design, need to consider: 
- instr length (32 bits in MIPS)
  - var-length instructions (CISC) 
    - Intel 80x86 -- instructions vary from 1 to 17 bytes long
    - Digital VAX -- instructions vary from 1 to 54 bytes long
    - require muti-step fetch and decode
    - allow for more flexible (but complex) and compact instruction set
  - fixed-length instructions (RISC)
    - used in most RISC
    - MIPS, PowerPC, ARM: instructions are 4 bytes long
      - ARM (64 bit): VLIW arch (Very Long Instr Word) -- 64 bit instr size
    - allow for easy fetch and decode
    - simplify pipelinging and parallelism
    - instructions bits are scarce
  - Hybrid instructions: a mix of var and fixed length instr
- instr fields (divide into smaller fields) 
  - types and szie of operands
  - R,I, J format
  - an instruction consists of
    - opcode: unique code to specify the desired operation
    - operands: zero or more additional info needed for the operation
  - operation designates the type and size of the operands
    - typical type and size: character (8 bits), half-word (eg. 16 bits), word (eg. 32 bits), single-precision floating point (eg 1 word), double-precision floating point (eg 2 words)
  - expectations from any new 32-bit arch
    - support for 8-, 16-, 32-bit int and 32-bit and 64-bit floating point operations. A 64-bit arch would need to support 64-bit int as well

5. encoding the instruction set (how: instr -> binary bits)

- **instruction encoding**
  - how are instrcutions represented in bin format for execution by the processor
    - assembly instr (R, I, J) -> binary bits
  - issues: code size (program size vs complexity of instr -- trade-off, RISC) , speed/performance, design complexity
  - things to be decided
    - no of reg (e.g. 32 reg, 5 bits to index them, for instr format -- need to allocate for instr encoding) 
    - no of addressing modes (more addressing modes, higher complexity)
    - no of operands in an instr (e.g. MIPS -> 3 reg OR 2 reg + 1 immed OR reg + mem)
  - different competing forces
    - have many reg and addressing modes
    - reduce code size (RISC vs CISC) 
    - have instr length that is easy to handle (fixed-length instr (vs var legnth) are easier to handle)
      - one problem with fixed-length: inflexible and need to have an opcode bits
     
- **encoding choices**
  - 3 choices: var, fixed, hybrid
  - var (VAX, Intel 80x86)
    - operation and no of operands, address speficer 1, address field 1..
  - fixed (Alpha, ARM, MIPS, PowerPC, SPARC, SuperH)
    - operation, address field 1, add field 2, add field 3
    - presents a much more interesting challenge:
      - how to fit multiple sets of instr types into same (limited) no of bits --> work with the most constrained instr types first
      - Expanding opcode scheme:
        - opcode has var lengths for different instr
        - > extend opcode for certain instr that may result in unused bits
        - a good way to max the instr bits
        - a fixed length opcode may waste instructions bits (e.g. only 1 operand) and max total no of instr is 2^6 or 64 (for 6 bit opcode)
        - how to distinguish between operantion types 9Type A and Type B): think about MIPS, simply set the opcode as all 0 for R-format but use the extended opcode called funct to distinguish
        - how many diff instr do we really have: different ways to compute the many diff instr depending on waht to max and/or minimise❗
      - max no of instructions
        - first to max the instr that has more no of bits for the opcode (min instr for lesser bits)
        - detailed walkthrough (L10P8 20:24, slide 32) (2^6 - 1) * 2^5
  - hybrid
    - not focused
- example:
  - Design an expanding opcode for the following to be encoded in a 36-bit instruction format. An address takes up 15 bits and a register number 3 bits. 7 instructions with two addresses and one register number. § 500 instructions with one address and one register number. § 50 instructions with no address or register.
    - start with the most restrictive cast (in this case, the first one, 7 instructions..)
    - to find number of bits needed to encode the instr: math.ceiling( log2 (x) ) where x is the number of instr
  - A certain machine has 12-bit instructions and 4-bit addresses. Some instructions have one address and others have two. Both types of instructions exist in the machine
  1. What is the maximum number of instructions with one address?
    - minimise type A instruction (with 2 addresses) to max type B (with one address) 
  2. What is the minimum total number of instructions, assuming the encoding space is completely utilised (that is, no more instructions can be accommodated)?
    - encoding space --> no unsed bit in opcode/funct
    - minimise instr that have more no of bits (type B) to minimise the no of instr

## The processor: Datapath

- for processor, need to understand how to design (1) datapath (2) control path (2 major components)

### (1) Datapath
- collection of components that process data
- performs the arithmetic, logical, and mem operations (including writing data back to the mem/reg, loading data from mem/reg)

**MISP Processor implmentation**
- simplest possible implementation of a subset of the core MIPS ISA:
  - arithmetic and logical operations
    - note: andi and ori is not supported in this current processor design because we always do "sign xtension" on immediate value
  - data transfer instructions
  - branches
- shift instructions (sll, srl) and J-type instructions (found out)
  - sll and srl can be done by multiplication which can be done by add with loop. j can be done by beq $zero, $zero, label if we ignore the difference related to 256MB blocks
 
**Basic instruction execution cycle**
Executed sequentially one by one until a control flow change occurs
1. fetch
  - get instruction from mem
  - address is in PC reg --> which stores add of next instr being executed 
2. decode
  - find out the operation required (e.g. add or sub, srl...)
3. operand fetch
  - get operand(s) needed for operation
  - in reg/temp reg... ($s1...)
4. execute
  - perform require operation (e.g. ALU) 
5. result write (store) 
  - store the result of the operation
- slide 7 for picture of examples
- slide 8 for deisgn changes to make it simpler
  - merge deocde and operand fetch stage
  - split execute into ALU (calculation) and memory access
 
**details for each stage**
note: has to look from pov of CPU designer (write better codes) 
1. FETCH
- use PC to fetch the instruction from mem
  - PC is implemented as a special reg in the processor
- increment the PC by 4 to get the address of the next instruction
  - each instruction is 32 bits -> 4 bytes (we know next instruction is PC + 4)
  - note the exception when branc/jump instruction is executed
- output (pass) to decode stage

elem 1 -- instruction mem:
- > storage element for the instruction
  - has an internal state that stores info
  - is a sequential circuit (circuits for storing some data) 
  - clock signal is assumed and not shown
  - supply instruction given the address
    - given instruction address M as input, the mem outputs the content at address M
    - conceptual diagram of the mem layout (slide 15)

elem 2 -- adder
- > combination logic to implement the addition of two numbers
- inputs: 2 32-bit numbers A.B --> output: sum (32-bit) of the input numbers, A + B

**the idea of clocking**
- slide 17
- to read and update the PC "at the same time"
- to make this work properly, use a "clock"
  - PC is read during the first half of the clock period and it is updated with PC + 4 at th next rising clock edge
  - between the two rising clock edge, the value of the PC is stable and can be read
  - PC is nth but a special form of reg --> data stored in the sequential circuit 

2. Decode
- Firstly, gather data from the instruction fields
  - read the opcode to determine instruction type and field lengths
  - read data from all necessary reg (can be two, one or zero)
- input from previous stage (fetch): instruction to be executed
- output to the next stage (ALU): operation and the necessary operands
- slide 19 for block diagram
  - read and write reg
  - collection of reg known as reg file
  - assembled instruction

- reg file
  - > a collection of 32 reg
  - each reg is 32-bit wide, can be read/written by specifying reg number
  - read at most two reg per instruction
  - write at most one reg per instruction
  - have a write data (data write into write reg if regwrite is 1) 
- RegWrite
  - is a control signal to indicate the (1) writing of reg --> (2) 1(True) = Write, (False) = No write
- multiplexer, the device (RegDst, the control signal) -- choice in destination 
  - a control signal to choose either Inst\[20:16] or Inst\[15:11] as the write reg number
  - use a multiplexer to choose the correct write reg number based on instr type
  - 1 = rd reg, 0 = rt reg as the write reg
  - multiplexer
    - > a device that takes n inputs and output 1 of the n inputs
    - 

3. 

### (2) Control path
- tells the datapath, mem and I/O devices what to do according to program instructions
- control signals 
 
