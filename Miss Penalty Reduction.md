#Caches 

Write policies:
- [[Write Through]]
- [[Write Back]]
- [[Write Allocate]]


### Write Buffers

Read Priority over Write on Miss:
If using a write buffer, when using the [[Write Through]] strategy (buffer writes to lower levels), and face a RAW:
- Wait for write buffer to empty (large miss penalty)
- Check write buffer before read in parallell (expensive)

If using a write buffer when using the [[Write Back]] strategy (holds displaced blocks as a result of the write):
- TODO

Write Buffers must be able to handle ***store bursts***, otherwise stalls until there is a space

Coalescing write buffers - Merge adjacent writes into single entry


### Early Restart

Processor can continue as soon as requested word arrives - restart CPU as soon as the requested word of the block arrives.

Request the missing word first (critical word first)

Useful in large blocks

Divide cache line into sectors - each with its own validity bit.

[[Non-Blocking Caches]]

### Multiple Levels of Cache

Global miss rate - misses in a cache divided by total number of memory accesses

### Multilevel Inclusion

Ln+1 cache contains everything in Ln

Last level caches are sometimes used as [[Victim Caches]]

Replacing dirty lines:
- Must keep track of which lines are in higher level caches

Cache coherency:
- If the line is not in L2, don't need to invalidate in L1.
