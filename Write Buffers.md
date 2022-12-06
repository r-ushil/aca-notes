#Caches 

[[Write Through]] and [[Write Back]] caches rely on write buffers, to contain all stores that must be sent to the next level of the memory hierarchy.

Read Priority over Write on Miss:
If using a write buffer, when using the [[Write Through]] strategy (buffer writes to lower levels), and face a RAW:
- Wait for write buffer to empty (large miss penalty)
- Check write buffer before read in parallell (expensive)

Write Buffers must be able to handle ***store bursts***, otherwise stalls until there is a space

Coalescing write buffers - Merge adjacent writes into single entry

Write merging - Merges consecutive word writes to memory addresses to take up less space in the write buffer
- Reduces stalls, less space taken up in the write buffer
- Takes advantage of spatial locality (writing)

![[write_merging.png]]