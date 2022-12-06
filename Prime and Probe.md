#Sidechannels 

Attacking thread primes the cache by filling one or more cache sets with its own lines

Once the victim thread has executed, the attacker probes by timing accesses to its previously loaded lines - longer accesses mean cache misses, so victim must have touched an address that maps to the same set

Works with shared caches