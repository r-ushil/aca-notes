#Caches

Average Memory Access Time (AMAT) = Hit Time + Miss Rate * Miss Penalty

Types of Cache Misses:
- Compulsory - First access to a block not in cache (cold start)
- Capacity - Cache cannot contain all blocks needed by the program
- Conflict - Happens with set associativity, different cache lines map to the same set
- Coherence - Invalidated by another processor or I/O


Reducing capacity misses:
- Change block size of cache

Reducing conflict misses:
- Change associativity of cache

Direct mapped cache:
- Each cache line maps to some lower order bits of an address
Fully associative cache:
- Each cache line is indexed by the full address

Cache entry:
- Cache block / cache line - unit of allocation
- Tag - memory address of cached block
- Set - Set of cache blocks index by a tag (column)
- Way - Set of alternate locations for an address of the same tag (row)

Bigger blocks -> exploit more spatial locality

Blocks that are too large cause miss rate to increase, as space is wasted speculatively loading data for spatial locality.

Large blocks take longer to load - higher miss penalty

Make use of [[Way Prediction]] to increase hit time (get closer to hit times of direct-mapped caches).

Can use [[Victim Caches]] and [[Skewed-Associative Caches]] to reduce associativity conflict misses.

Reduce misses by [[Hardware Prefetching]] of instructions and data.

Can reduce *miss delays* by issuing loads early enough - using a **decoupled access-execute**:
- Seperate instructions that generate addresses from the instructions that use memory results
- Let address-generation side run ahead