#Caches 

Add a buffer to place data discarded from the cache.

On a cache miss - allocate into direct-mapped data cache.
On replacement - allocate into smaller, fully associative victim cache.

On access, search both.
On victim cache hit - reallocate into direct-mapped data cache.

Get the best of both worlds - competitive algorithm.
