##MSI 

1. IC

integrated circuit --> set of electronic circuits on one small flat piece of semiconductor material. 
Scale of integration: the number of components fitted into a standard size IC 
- medium scale integration (MSI): 10 - 500 transistors and 13 - 99 logic gates
We will look at four common and useful MSI circuits
- decoder
- demultiplexer
- encoder
- multiplexer
_note: get the block diagrams_

2. Decoder

> convert binary information from n input lines to a max of 2^n output lines

Code is frequently used to represent  entities, decoder thus is used to identidy or deocde the code to identify the entity.
- n-to-m-line decoder or n\:m, n*m (m <= 2^n)
- May be used to generate 2^n minterms of n input variables
- to design a decoder, look at the truth table --> possible to deduce the minterm

Implementing function:
-A Boolean function, in sum-of-minterms form a
  - decoder to generate the minterms, and
  - an OR gate to form the sum.
- Any combinational circuit with n inputs and m outputs can be implemented with an n:2n decoder with m OR gates.
- Good when circuit has many outputs, and each function is expressed with a few minterms.
- note: subscript 0, 1, 2: 2 is the MSB
- Larger decoders can be constructed from smaller ones. Example: A 3´8 decoder can be built from two 2´4 decoders (with one enable) and an inverter
- Decoders may also have zero-enable and/or negated outputs.
  - Normal outputs = active high outputs
  - Negated outputs = active low outputs
- implement functions based on the decoder and gates avaiable (e.g. active-high decoder with OR gate...)

Decoders with enable
- Decoders often come with an enable control signal, so that the device is only activated when the enable, E = 1. (when you don't wanna use decoder)
- In most MSI decoders, enable signal is zero-enable, usually denoted by E' or Ē. The decoder is enabled when the signal is zero (low)
- usually is E with an AND gatesup

3. Encoders

> converse of decoding: Given a set of input lines, of which exactly one is high and the rest are low, the encoder provides a code that corresponds to that high input line.
- Contains 2n (or fewer) input lines and n output lines.
- Implemented with OR gates
- At any one time, only one input line of an encoder has a value of 1 (high), the rest are zeroes (low).
- To allow for more than one input line to carry a 1,we need priority encoder
- priority encoder
  - is one with priority
  - If two or more inputs or equal to 1, the input with the highest priority takes precedence.
  - If all inputs are 0, this input combination is considered invalid
  - can be derived from compact function table
  - the bit with the highest precedence (e.g. D3)
 
4. Multiplexers and demultiplexers
 
Application: Helps share a single communication line among a number of devices. At any time, only one source and one destination can use the communication line

Demultiplexer:
- Given an input line and a set of selection lines, a demultiplexer directs data from the input to one selected output line
- the demux circuit is identical to a decoder with enable

Multiplexer:
- a device that has § A number of input lines § A number of selection lines § One output line
- It steers one of 2n inputs to a single output line, using n selection lines. Also known as a data selector
- output of multiplexer is “sum of the (product of data lines and selection lines)”
  - e.g. 4-to-1 mux output: Y = I0∙(S1'∙S0') + I1∙(S1'∙S0) + I2∙(S1∙S0') + I3∙(S1∙S0)
  - note expressing the above equation in minterms notation is equal to --> I0∙m0 + I1∙m1 + I2∙m2 + I3∙m3
- A 2n-to-1-line multiplexer, or simply 2n:1 MUX, is made from an n:2n decoder by adding to it 2n input lines, one to each AND gate
- Some IC packages have a few multiplexers in each package (chip). The selection and enable inputs are common to all multiplexers within the package
- Larger multiplexers can be constructed from smaller ones

Multiplexers: Implementing functions
- iplement boolean functions using mux
- A 2n-to-1 multiplexer can implement a Boolean function of n input variables
  - first express in sum-of-minterms form
  - (2) connect n var to the n sleection lines
  - (3) put '1' on a data line if it is a minterm of the function, or '0' otherwise
  - supply 0' to other var where minterm does not exists (from slide 34)
- can use smaller mux to implement boo function
  - apply n var as the selection lines, then apply the remaining var to the inputs line (provided the function is preserved)
  - procedue: 1) Express Boolean function in sum-of-minterms form. 2) Reserve one variable (may be the least significant one) for input lines of multiplexer, and use the rest for selection lines 3) Draw the truth table for function, by grouping inputs by selection line values, then determine multiplexer inputs by comparing input line (C) and function (F) for corresponding selection line values
