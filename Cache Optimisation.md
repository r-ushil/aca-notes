#Caches 

### Small and Simple First-Level Caches to Reduce Hit Time and Power

Lower levels of associativity -> less associativity conflict, less time looking up

Can "bank" caches, so that an access only activates a portion of the cache

Why is higher associativity needed:
- Keep TLB out of the critical path (using VIPT), and remove the limit on cache size = page size

### Way Prediction to Reduce Hit Time

[[Way Prediction]]

### Pipelined Access and Multibanked Caches to Increase Bandwidth

[[Multibanked Caches]]