# Pipelining

> a data pipeline is a set of data processing elements connected in series, where the output of one element is the input of the next one.
- Pipelining doesn’t help latency of single task:
  - § It helps the throughput of entire workload
  - § Multiple tasks operating simultaneously using different resources
- Possible delays:
  - Pipeline rate limited by slowest pipeline stage
  - Stall for dependencies

**MIPS Pipeline**
- Five Execution Stages
  - § IF: Instruction Fetch
  - § ID: Instruction Decode and Register Read
  - § EX: Execute an operation or calculate an address
  - § MEM: Access an operand in data memory
  - § WB: Write back the result into a register
- Idea:
  - § Each execution stage takes 1 clock cycle
  - § General flow of data is from one stage to the next
  - pipelined execution: several instructions are in the pipeline simultaneously 
- Exceptions:
  - Update of PC and write back of register file

**MIPS Pipeline: Datapath**
- Single-cycle implementation:
  - Update all state elements (PC, register file, data memory) at the end of a clock cycle
- Pipelined implementation:
  - One cycle per pipeline stage
  - Data required for each stage needs to be stored separately --> register value is not overwritten(several instructions are in the pipeline simultaneously)
- Data used by subsequent instructions:
  - Store in programmer-visible state elements: PC, register file and memory
- Data used by same instruction in later pipeline stages:
  - Additional registers in datapath called pipeline registers (to store register value)
  - IF/ID: register between IF and ID
  - ID/EX: register between ID and EX
  - EX/MEM: register between EX and MEM
  - MEM/WB: register between MEM and WB
  - no register at the end of WB stage because there is no more value to be stored temporaily

IF Stage:
- At the end of a cycle, IF/ID receives (stores):
  - Instruction read from InstructionMemory\[ PC ]
  - PC + 4
- PC + 4 is also connected to one of the MUX's inputs

ID Stage:
- At the beginning of a cycle IF/ID register supplies:
  - Register numbers for reading two registers
  - 16-bit offset to be signextended to 32-bit
  - PC + 4
- At the end of a cycle ID/EX receives:
  - Data values read from register file
  - 32-bit immediate value
  - PC + 4
 
EX Stage
- At the beginning of a cycle ID/EX register supplies:
  - Data values read from register file
  - 32-bit immediate value
  - PC + 4
- At the end of a cycle EX/MEM receives:
  - (PC + 4) + (Immediate x 4)
  - ALU result
  - isZero? signal
  - Data Read 2 from register file

  MEM Stage
  - At the beginning of a cycle EX/MEM register supplies:
    - (PC + 4) + (Immediate x 4)
    - ALU result
    - isZero? signal
    - Data Read 2 from register file
  - At the end of a cycle MEM/WB receives:
    - ALU result
    - Memory read data

WB Stage
- At the beginning of a cycle MEM/WB register supplies:
  - ALU result
  - Memory read data
- At the end of a cycle
  - Result is written back to register file (if applicable)
  - Pass “Write register” number from ID/EX through EX/MEM to MEM/WB pipeline register for use in WB stage
  - let the "Write register" number follows the instruction through the pipeline until it is needed in WB stage
 
**Pipeline Control**
- Same control signals as single-cycle datapath
- Difference: Each control signal belongs to a particular pipeline stage
- can group control signals according to the pipeline stage --> e,g, EX Stage: RegDst, ALUSrc, ALUop
- signals generated in ID stage and is used by the subsequent stages onwards, propagated along until utilised

**Different implementations and comparison of performace**
- single cycle vs multi cycle vs pipeline
- single cycle
  - run sequentially, one instruction is one cycle
  - cycle length takes the slowest instruction
  - Cycle time: CTseq = max(sum N k = 1 (Tk))
    - N = no of stages
    - Tk = time for operation stage k
  - execution time for I instructions: Timeseq = I * CTseq
- multi-cycle
  - run sequentially, but one stage is one cycle, **each stage is given a cycle time**
  - cycle time: CTmulti = max(Tk)
    - time taken for each stage
  - execution time for I instruction: Timemulti = I * Average CPI * CTmulti
    - Average CPI is the average clock cycle per instruction, it is needed as each instruction takes different number of cycles 
- pipeline
  - overlapped execution
  - Cycle time: CTpipeline = max(Tk) + Td
    - Td = overhead for pipelining e.g. pipeline register
  - **cycles** needed for I instructions: I + N - 1
    - need N - 1 cycles to fill up the pipeline --> ideal format, where each instr can be executed one stage after another 
  - execution time for I instructions: Timepipeline = (I + N - 1) * CTpipeline
 
**pipeline ideal speedup**
- Assumptions for ideal case: Every stage takes the same amount of time
  - sum N k = 1 (Tk) = N * T1
  - No pipeline overhead --> Td = 0
  - I >> N (Number of instructions is much larger than number of stages)
- speedup = timeseq / timepipeline = N
- Pipeline processor can gain N times speedup, where N is the number of pipeline stages

## Pipelining hazards

1. Pipeline harzards
  - Speedup from pipeline implementation: Based on the assumption that a new instructions can be "pumped" into pipeline every cycle
  - However, there are pipeline hazards: Problems that prevent next instruction from immediately following previous instruction
  - § Structural hazards: Simultaneous use of a hardware resource
    - e.g. only a single mem module --> if two instructions reach memory stage at the same cycle, there is a problem
    - to reolve this hazard, stall the pipeline (one solution)
    - alternate solution: separate mem, split mem into data and instr mem
    - single register module is also a hazard, but solution is toSplit cycle into half; first half for writing into a register; second half for reading from a reg, since **reg are very fast mem**
    - and for reg, need to write first then read, because instruction is executed in order, the write instr is definitely from the prev instr
  - § Data hazards: Data dependencies between instructions (instr dependencies)
  - § Control hazards: Change in program flow (instr dependencies)
  - can visualise execution via a horizontal-vaertical axes --> horizontal = the stages of an instr, vertical = the instructions in different pipeline stages (instr order)

**Data hazard: data dependencies**
- Instructions can have relationship that prevent pipeline execution, although a partial overlap maybe possible in some cases
- When different instructions accesses (read/write) the same register
  - Register contention is the cause of dependency: known as data dependency
- When the execution of an instruction depends on another instruction
  - Control flow is the cause of dependency, known as control dependency
- Failure to handle dependencies can affect program correctness
- "Read-After-Write" Definition: Occurs when a later instruction reads from the destination register written by an earlier instruction
  - also known as true data dependency
  - if i2 reads result from the reg before i1 can write the sult to the reg, i2 will get a stale result (old result)
  - a solution to RAW: Forward the result to any trailing (later) instructions before it is reflected in register file --> Bypass (replace) the data read from register file
  - but for **lw** instruction, data is needed before it is actually produced (read at the end of DM stage) so cannot be solved with forwarding, hence we need to **stall the pipeline**
- WAR: Write-after-Read dependency and WAW: Write-after-Write dependency --> affect the processor only when instructions are executed out of program order, hence do not cause pipeline hazard
- draw pipeline diagram to visualise data hazard

**Control dependency**
- Definition: An instruction j is control dependent on i if i controls whether or not j executes
- Typically i would be a branch instruction
- Incorrect execution: If i2 is allowed to execute before i1 is determined, register $1 maybe incorrectly changed
- tracing the control path, decision of branch instr is made in MEM stage but may be too late in the pipeline processor (partially executed)
- one solution is to stall pipeline which introduces 3 clock cycles delay (MEM statge): 20% is going to be branch on average, so there will be too heavy a stall penalty
- alternate solutions: early branch resolution, branch prediction, delayed branching
Early branch
- Move branch decision calculation to earlier pipeline stage
- Make decision in ID stage instead of MEM: Move branch target address calculation and move register comparison --> cannot use ALU for register comparison any more
- wait until branch decision is known then fetch the correct instruction --> reduce from 3 to 1 clock cycle delay
- problems: if the register(s) involved in the comparison is produced by preceding instruction --> further stall is needed (e.g. having an add's WR as the comparison reg for the beq instr next line)
  - solution: Add forwarding path from ALU to ID stage though One clock cycle delay is still needed
- problem is worse with load followed by branch
  - solution: MEM to ID forwarding and 2 more stall cycles, but in this case, we ended up with 3 total stall cycles --> ALU to IF forwarding cannot help 
Branch prediction
- guess the outcome before it is products to reduce stalls
- many branch prediction schemes, covering the simple prediction here
- Simple prediction: All branches are assumed to be not taken --> Fetch the successor instruction and start pumping it through the pipeline stages
- When the actual branch outcome is known:
  - Not taken: Guessed correctly è No pipeline stall
  - Taken: Guessed wrongly --> Wrong instructions in the pipeline --> Flush successor instruction from the pipeline
- decision making moved to ID stage
- as we calculate total execution cycles, can add the number of delays to the ideal pipeline case (e.g. if there are 10 iterations of the branch instr, and each bne instr incurs 1 cycle of delay, then there are 10 cycles of delay. Every bne incurs a cycle of delay to execute the next instr, so there are additional 10 cycles of delay. Total delay cycles = 20)
- for branch prediction simple, since the last iteration prediction is correct, there will be no cycle of delay --> minus one. Not taken, then still delay 1 cycle/2
Delayed Branching
- Do something useful while waiting for the outcome
- Observation: Branch outcome takes X number of cycles to be known --> X cycles stall
- Idea: Move non-control dependent instructions into the X slots following a branch
  - Known as the branch-delay slot --> These instructions are executed regardless of the branch outcome 
- In MIPS processor: Branch-Delayed slot = 1 (with the early branch)
- Best case scenario: There is an instruction preceding the branch which can be moved into the delayed slot
  - note: Program correctness must be preserved!
- Worst case scenario: Such instruction cannot be found --> Add a no-op (nop) instruction in the branch-delay slot
- Re-ordering instructions is a common method of program optimization
  - Compiler must be smart enough to do this
  - Usually can find such an instruction at least 50% of the time
