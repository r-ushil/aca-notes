#Caches 

Extra block fetched placed in a ***stream buffer***.

After a cache miss, the stream buffer prefetches the **next** successive cache line.

On future misses, check the head of the stream buffer:
- If a hit, allocate into cache and prefetch the next line for the stream buffer
- If a miss, clear the stream buffer and start over.

Relies on having **extra memory bandwidth**.

Have multiple stream buffers - because programs often make interleaved, sequential streams of accesses.