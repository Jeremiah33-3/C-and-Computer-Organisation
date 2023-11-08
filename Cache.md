# Cache 

> basic idea: Keep the frequently and recently used data in smaller but faster memory, cache memory.

And refer to bigger and slower memory only when you cannot find data/instruction in the faster memory.
- worked because of the principle of locality: Program accesses only a small portion of the memory address space within a small time interval.
- Direct Mapped Cache

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

**cache (direct mapped cache)**
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
  - hit: data wanted is in cache
    - hit rate: fraction of mem accesses that hit
    - hit time: time to access cache 
  - miss: data wanted is not in cache
    - miss rate = 1 - hit rate
    - miss penalty: time to replace cache block + hit time
  - hit time < miss penalty
  - MAT formula: average access time = Hit rate x Hit Time + (1-Hit rate) x Miss penalty
 
**Memory to Cache Mapping**
- Cache Block/Line: Unit of transfer between memory and cache
- Block size is typically one or more words (16-byte block = 4-word block)
- observations:
  - 1. 2^N-byte blocks are aligned at 2^N-byte boundaries
    2. The addresses of words within a 2^N-byte block have identical (32-N) most significant bits (MSB).
    3. Bits \[31:N] --> the block number
    4. Bits \[N-1:0] --> the byte offset within a block 
- block number vs address (not the same) (N-1:0) bit is the block address --> cache index, map the blocks number to the cache index (smaller)
- mapping function: cache index = (Blocknumber) % (number of cache blocks)
- tag = block number / number of cache blocks
  - multiple mem blocks an map to the same cache block, so same cache index; however they have a unique tag number (the left bits)
- in sum, an mem address: block number, offset => break down further into tag, index, offset
- along with a data block (line), cache also contais other admin info (overheads)
  - tag of the mem block
  - valid bit indicating whether the cache line contains valid data
  - when there is a cache hit: Valid\[index] = TRUE && Tag\[index] = Tag\[mem addresss]
- number of cache blocks = total bytes / byte of one block

**Types of cache misses**
- compulsory misses
  - happens on the first access to a block; the blocl must be brought into the cache
  - aka cold start misses or first reference misses 
- conflict misses
  - occur in the case of direct mapped cache or set associative cache, when several blocks are mapped to the same block/set
  - aka collision misses or interference misses
- capacity misses
  - occur when blocks are discarded from cache as cache cannot contain all blocks needed(fully associated cache)

handling cache misses:
- on a read miss: data loaded into cache and then load from there to reg
- write miss option 1: write allocate
  - load the complete block from mem into cache
  - change only the required word in cache
  - write to main mem depends on write policy (write thru or write back)
- write miss option 2: write around
  - do not load the block to cache
  - write directly to main mem only
 
Store data in memory (sw); changing cache content: write policy
- when cache and main mem are inconsistent (modified data only in cache, not in mem)
  - solution 1: write-thru cache (write both to cache and to main mem)
    - disadvantage: main mem is altered --> operate at the speed of main mem
    - to counter inefficieny, put a write buffer between cache and main mem
      - processor: writes data to cache + write buffer
      - mem controller: write contents of the buffer to mem
  - solution 2: write-back cache (only write to cache, write to main mem only when cache block is replaced or evicted)
    - more popular
    - problem: quite wasteful if we write back every evicted cache blocks
    - solution: add an additional bit (dirty bit) to each cache block
      - write operation will change dirty bit to 1 (only cache block is updated, no write to mem)
      - when a cache is replaced --> only write back to mem if dirty bit is 1
