#Caches 

Direct-mapped caches are better than set associative caches for cache hit time -> less tags to compare.

Set associative caches give you a better hit *rate* -> more chance of getting a cache hit.

Way prediction - extra bits are kept in the cache to predict the way of the *next* cache access. Means that you can access the correct set for the desired way first on a correct prediction, getting the performance benefit of direct-mapped caches (better hit time) and good hit rate with associativity. 

