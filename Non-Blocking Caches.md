#Caches 

[[SonicBOOM]]
Non-blocking cache - allows data cache to continue to supply cache hits during a miss
- Needs out-of-order execution, or full/empty bits on each register
- Needs multi-bank memories
- Only blocks when it hits a register that is the target of an uncompleted load instruction

Hit under miss - reduces the effective miss penalty by working during miss instead of ignoring CPU requests
- Needs multiple memory banks

Prefetcing - overlap memory accesses with pre-miss instructions
Non-blocking cache - overlap memory accesses with post-miss instructions

### Cache Miss

Use full / empty bits in registers and use MSHR queue:
- MSHR - MIss Status / Handler Registers
	- Each entry in this queue keeps track of the status of outstanding memory requests to one complete memory line (register full/empty bits)
	- Knows when to stall
	- Important to know where a cache miss return should go, because of OoO


### Hit Under Miss

Creates the opportunity for load instructions to execute out-of-order

Need special instructions (memory fences) to enforce the relative order of memory accesses in a OoO processor.
