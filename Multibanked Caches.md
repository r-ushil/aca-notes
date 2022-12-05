#Caches 

Can pipeline cache access

Can widen the cache with multiple banks to allow multiple accesses per clock


Pipelining L1:
- Higher clock cycle
- Increased latency

Pipelining the instruction cache -> increases number of pipeline stages -> greater branch mispredict penalty

Better to pipeline the instruction cache, better branch prediction than data cache

Pipelining the data cache -> more clock cylces between load issue and load completion

Pipelining is useful for seperating access and hit detection


To handle multiple loads / stores per cycle:
- Divide cache into independent banks, each for an indepedent access

Must spread accesses naturally across banks:
- Sequential interleaving - spread addresses of a block across banks

Multiple banks in L2 allows for [[Non-Blocking Caches]] to use hit-under miss
