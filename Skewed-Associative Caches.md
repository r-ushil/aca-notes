#Caches 

Reduce conflict misses by using *different* indices in each cache way.

Hash the cache index and some tag bits (i.e. XOR)

As the indexes are pseudo random, conflict misses are reduced as they don't map to the same index anymore -> useful for loops.

Costs:
- Must have an address decoder per way
- Latency of hash function
- Harder to implement LRU


