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
