# Booooo

## Bitwise operators

| Operators | Sign | Language |
| :--- | :--- | :--- |
| AND | & | Python, C, Java |
| OR | \| | Python, C, Java |
| XOR | ^ | Python, C, Java |
| Negation/complement | ~ | Python, C, Java |
| Left shift | << | Python, C, Java |
| Right shift | >> | Python, C, Java |
| Unsigned Right Shift | >>> | Java |

**Masking**
- Making the number unsigned: creates a mask and set all bits to 1, then AND [e.g. `mask = (1 << 32) - 1` in python or directly `0xFFFFFFFFL`]

## Digital circuits
- two voltage levels (shaped like rec, like clock signals)
  - high/true/1/asserted
  - low/false/0/deasserted
- advantages of digital circuits over analog circuits (curvy) 
  - more reliable (simpler circuits, less noise-prone)
  - specified accuracy (determinable)
  - abstraction can be applied using simple mathematical model -- Boolean algebra
  - easer design, analysis and simplification of digital citcuit -- diital logic design
- Combinational
  - no mem, output depends solely on the input
  - e.g. gates, decoders, mux, adders, multipliers
- Sequential
  - with mem, output depends on both input and current states
  - e.g. mem, counters, registers
 
## Boolean algebra 
- > boolean values (T 1) or (F 0)
- connectives
  - conjunction (AND) A dot B
  - disjunction (OR) A + B
  - Negation (NOT) A'
- logic gates ❗

**truth tables**
- provide a listing of every possible combination of inputs and its corresponding outputs
- inputs are usually listed in binary sequence
- proof using truth tables for some boolean expression -- if two outputs columns are exactly identical for the same inputs, they equal 

**Precedence of operators**
- precedence from highest to lowest -- NOT, AND, OR
- use parenthesis to overwrite precedence

**Laws of boolean algebra**
1. identity laws
  - A + 0 = 0 + A = A | A dot 1 = 1 dot A = A
2. inverse/complement laws
  - A + A' = A' + A = 1 | A dot A' = A' dot A = 0 
3. commutative laws
  - A + B = B + A | A dot B = B dot A
4. associative laws
  - A + (B + C) = (A + B) + C | A dot (B dot C) = (A dot B) dot C
5. distributive laws
  - A dot ( B + C) = (a dot B) + (A dot C) | A + (B dot C) = (A + B) dot (A + C)
6. idempotency
  - X + X = X | X dot X = X
7. one elemnt/ zero elem
  - X + 1 = 1 + X = 1  | X dot 0 = 0 dot X = 0
8. involution
  - (X')' = X
9. absorption 1
  - X + X dot Y = X | X dot ( X + Y) = X 
10. absorption 2
  - X + X' dot Y = X + Y | X dot ( X' + Y ) = X dot Y 
11. deMorgans
  - ( X + Y )' = X' dot Y' | (X dot Y)' = X' + Y'   
12. Consensus
  - X dot Y + X' dot Z + Y dot Z = X dot Y + X' dot Z | (X+Y) dot (X'+Z) dot (Y+Z) = (X+Y) dot (X' + Z) 

**Duality**
- if the AND/OR  operators and identity elements 0/1 in a Boo equation are interchanged, it remains valid
- purpose: duality gives free theorems as a boo eq is logically equivalent to its dual -- so prove one theorem and the other comes for free
  - e.g. (x+y+x)' = x' dot y' dot x' is valid, then its dual (x dot y dot z)' = x' + y' + x' is valid
- not the same as negation ❗

**Proving theorem**
- using a truth table or by algebraic manipulation using other theorems/laws
- then by duality, we may also cite the dual

## Functions
- Boolean functions: logic equations as a function
  - F1(x,y,z) = x'doty'dotx + ... or just one term
- Complement functions: given a boo func F, the complement of , denoted as F', is obtained by interchanging 1 with 0 in the function's output values
  - can use demorgan's law

## Standard forms
- certain types of Boo expr lead to circuits that are desirable from an implementation viewpoint
- two standard forms
  - sum of products (SOP)
  - product of sums (POS)

 **Terminologies**
- literals
  - a Boo var on its own or in its complemented form (e.g. (1) x, (2) x' (3)y, (4), y'
- Product term
  - > a single literal or a logical product (AND) of several literals
  - e.g. (1)x, (2) x dot y dot z' (3) A' dot B, (4) A dot B
- Sum term
  - > a single literal or a logical sum (OR) of serveral literals
  - e.g. (1) x, (2) x+y+z' (3) A'+B (4) A+B
- sum of products expr
  - > a product term or a logical sum (OR) of several product terms
  - (1) x, (2) x + y dot z' (3) A dot B + A' dot B'
- product of sums expr
  - > a sum term or a logical product (AND) of several sum terms
  - (1) x, (2) x dot (y+z') (3) (A+B) dot (A'+B')
- claim: every boo expr can be expressed in SOP or POS form

**minterms maxterms**
- minterms
  - a minterm of n var is a product term that contains n literals from all the var
- maxterm
  - a maxterm of n var is a sum term that contains n literals from all the var
- general: n var --> up to 2^n minterms and 2^n maxterms
- the minterms and maxterms on 2 var are dnoted by m0 to m3 and M0 to M3 respectively
- note: ❗each minterm is the complement of its corresponding maxterm and each maxterm is the complement of its corresponding minterm
- the number m0, M0 is assigned to the fixed minterm/maxterm corresponds to the binary value of the true values of the n var (e.g. 0,0 for n = 2 means m0 and M0) ❗it's fixed, rmb it 

**canonical forms**
> or normal form: a unique form os representation
- sum of minterms = canonical sum of products, product of maxterms = canomical product of sums
- sum of minterms
  - given a truth table, obtain the sum-of-minterms expr by gathering the minterms of the function (where output is 1)
  - sum () 
- product of maxterms
  - given a truth table, obtain the product-of-maxterms expr by gathering the maxterms of the function (where output is 0)
  - pi

## Logic circuits

**Logic Gates**
- Gate symbols
  - AND: a- b- castle door rotate right
  - OR: a- b- castle door but curve
  - NOT: a- b- 🚩with open dot
  - NAND: a- b- castle door with dot
  - NOR: a- b- castle door with curve with dot
  - XOR: a- b- curvy castle door with outline at curve
- inverter
  - invert the input
  - A - 🚩with dot - A'
  - A - dot 🚩 - A'
- other gates: XOR/XNOR, how NAND and NOR gates can be combined from AND/OR and invert(NOT)

**Logic circuits deeo dive**
- fan-in: the number of inputs of a gate
- gates may have fan-in more than 2
- every input must be connected in a working circuit (multiple inputs circuit, can put 1/0 but no empty input)
- given a bool expr, can implement it as a logic circuit (boo func)
  - if complemented literals are availble, we don't need to use NOT operation
- when analysing logic circuits: may ask to analyse it to obtain the logic expression

**universal gates**
- AND/OR/NOT gates basically because they are sufficient for building any Boo func
- {AND, OR, NOT} aka **complete set of logic**
- however, other gates are used becuase: usefulness (XOR for parity bit generation), economical, and self-suufficiency (NAND/NOR gates)
- NAND Gate
  - {NAND} a complete set of logic: proof -- implement NOT/AND/OR using only NAND gates
- {NOR} is a complete set of logic

**SOP and NAND circuits**
- an SOP expr can be implemented using 2-level AND-OR circuit or 2-level NAND circuit

**POS and NOR circuits**
- can be implemented using 2-level OR-AND circuit or 2-level NOR circuit

**Integrated circuit**
- ~ chip

**Porgramming logic array (PLA)**
- a programmable integrated circuit - implements SOP circuits, allow multiple outputs
- 2 stages: AND gates = product terms and OR gates = outputs
- connection between inputs and the planes can be 'burned'

## simplification, functions, Kmap

**function simplification**
- why: simpler expr leads to circuit that uses fewer logic gates + cheaper + uses less power + sometimes faster
- technicues
  - algebraic: useing theorems, open-ended, require skills
  - Karnaugh maps: easy to use, limited to no more than 6 var
  - quine-mccluskey: suitable for automation, can handle many var (but computationally intensive)

**algebraic simplification**
- aims to minimise (1) number of literals and (2) number of terms
- usually try to minimise number of literals 

**half adder**
- half adder: circuit that addes 2 single bits (X ,Y) to produce a result of 2 bits (C, S)
- can be represented: black-boc representation and truth table
- in canonical form (sum of minterms)
  - C = X dot Y
  - S = X' dot Y + X dot Y'
- output of S can be simplified further into S = X XOR Y
- contrast to full-adder

**gray code**
- aka reflected binary code
- unweighted (not an arithmetic code) --> each position don't hold arithmetic weight 
- only a single bit change from one code value to the next
- not restricted to dec digits: n bits --> 2^n values
- advantages: good for error detection
- cannot have duplicate values too
- can generate standard Gray code by using reflection in 2s 

**Kmap**
- resource: https://www.youtube.com/watch?v=RO5alU6PpSU
- to figure out the function from Kmap, look at how output changes when input changes
- Kmap > a systematic method to obtain simplified SOP expressions
- objective: fewest possible product terms and literals
- special/abstract form of venn diagram, organised as a matrix of squares where each square represetns a minterm and two adj squares differ by exactly one literal (gray code sequence) 
- easy to use
- but limited to 5 to 6 var
- A k-map for a function is filled by putting a '1' in the square corresponds to a minterm of the function and a '0' otherwise
- in general, each cell in an n-variable K-map has n adj neighbours


Using K map
- Unifying theorem (complement)
- group as many cells as possible -- larger the group, the fewer the no of literals in the resulting product term
- select as few groups as possible to cover all the minterms of the function -- the fewer no of product terms in the simplified SOP expr
- valid grouping -- the terms are neighbours
- invalid -- usually diagonal groupings or too big a chunk
- If functions aren't in Sum of min form -- convert to SOP terms then expand the SOP exp into sum of minterms expr or fill in the k-map directly based on the SOP expr

Prime implication and essential PI
- to find the simplest (minimal) SOP expr from a k-map, you need to obtain
  - min no of literals per product term
  - min no of product terms
- achieved through k-map by
  - using bigger groupings of minterms (prime implicants) where possible and
  - using no redundant gorupings (look for epi)
- implicant: > a product term that could be used to cover minterms of the function
- PI: a product term obtained by combining the max possible no of minterms from adjacent squares in the map (biggest grouping possible) (PI can overlap)
- and no redundant group in PI --> look out for EPI, a PI that includes at least one mintern that is not covered by any other PI

Finding simplified SOP expr 
- algo
  1. circle all PI on the Kmap
  2. identify and select all EPI for the cover
  3. select a min subset of the remaining PI to complete the cover, that is, to cover those minterms not convered by the EPI
- simplified POS expr can be obtained by grouping the maxterms (0s) of the given function
  - can draw Kmap of F', 0 becomes 1, 1 becomes 0
- Don't-care condition is output that can be either 1 or 0 (denoted by X or d)
  - can be used to help simplify Boo expr further in Kmaps because they could be chosen to be either 0 or 1 depending on which choice results in a simpler expr 
