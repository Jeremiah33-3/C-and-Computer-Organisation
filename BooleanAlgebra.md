# Booooo

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
- Complement functions: given a boo func F, the complement of , denoted as F', is obtained by interchanging 1 with 0 in the function's output values
  - can use demorgan's law
