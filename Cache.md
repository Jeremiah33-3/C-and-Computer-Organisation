# Cache 

> basic idea: Keep the frequently and recently used data in smaller but faster memory, cache memory.

And refer to bigger and slower memory only when you cannot find data/instruction in the faster memory.
- worked because of the principle of locality: Program accesses only a small portion of the memory address space within a small time interval.

Pre-concepts to meditate on:
1. Data transfer
- Registers are in the datapath of the processor. If operands are in memory we have to load them to processor (registers), operate on them, and store them back to memory.
- datapath + registers; from mem to reg and back
2. Memory technology
- DDR = Double Data Rate, synchronous dynamic RAM
- capacity increases, yet latency can increases too

We want to best of both worlds: A BIG and FAST memory; Memory system should perform like 1GB of SRAM (1ns access time) but cost like 1GB of slow memory
Key concept: Use a hierarchy of memory technologies -- Small but fast memory near CPU, Large but slow memory farther away from CPU
- understand memory hierarchy: speed = harddisk -> DRAM -> SRAM -> registers; sise = harddish > DRAM > SRAM > registers

**cache**
- temporal locality:
  - If an item is referenced, it will tend to be referenced again soon
- spatial locality
  - If an item is referenced, nearby items will tend to be referenced soon
- different locality for instructions and data
- working set: set of locations accesed during a change in t
  - Different phases of execution may use different working sets
  - aim is to capture the working set and keep it in the memory closest to CPU
- two aspects of memory access
  - how to make slow main mem appear fast and
    - cache -- a small but fast SRAM near CPU
    - hardware managed -  transparent to programmer 
  - how to make small main mem appear bigger than it is
    - virtual mem
    - OS managed: transparent to programmer (not in cs2100)
- memory access time terminology
  - hit: data is in cache
    - hit rate: fraction of mem accesses that hit
    - hit time: time to access cache 
  - miss: data is not in cache
    - miss rate = 1 - hit rate
    - miss penalty: time to replace cache block + hit time
  - hit time < miss penalty
  - MAT formula: average access time = Hit rate x Hit Time + (1-Hit rate) x Miss penalty
 
**Memory to Cache Mapping**
- Cache Block/Line: Unit of transfer between memory and cache
- Block size is typically one or more words (16-byte block = 4-word block)
- observations:
  - 1. 2N-byte blocks are aligned at 2N-byte boundaries
    2. The addresses of words within a 2N-byte block have identical (32-N) most significant bits (MSB).
    3. Bits \[31:N] --> the block number
    4. Bits \[N-1:0] --> the byte offset within a block 
