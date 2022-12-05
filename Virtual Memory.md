#Caches 

Pros:
- Run code in an isolated environment
	- Won't crash whole system on fail
	- Malicious code doesn't have total access
- Run more than one application at a time
	- Applications can't interfere with each other
	- Applications don't need to know about each other


Achieved using address translation

Physically-indexed, Physically tagged (**PIPT**):
- CPU issues virtual address
- TLB translates virtual to physical address
- Memory hierarchy indexed using physical address
- Handles context switches

Virtually-indexed, virtually tagged (**VIVT**):
- CPU issues virtual address
- Cache is indexed using virtual address
- TLB translates to physical address
- Memory is indexed using physical address
- Don't translate until we get a cache miss
- Hit time is **reduced**, translation is out of the critical path

Virtually-indexed, physically tagged (**VIPT**):
- CPU issues virtual address (4KB pages, 12 bit offset, 20 bit page number in 32 bit machine)
- Offset used to index cache, offset is not translated and used to get tag (parallel)
- Use page number to index TLB and get physical address (parallel)
- Compare TLB physical address with cache tag
	- If match -> cache hit
	- If miss -> go to L2 $, and index using physical address

- Limits cache to page offset (2^12 = 4KB), as offset used to index
	- Fix by using associativity -> index ways with same bits, but bigger cache
	- So associativity is important in L1 D$


When the **same virtual addresses** points to **different physical addresses** in different processes - in a virtually indexed cache:
- Flush the cache between context switches, or use a PID in the cache tag

When **different virtual addresses** point to the **same physical addresses** - in a virtually indexed cache:
- Updates to one cached copy (virtual address) will not be reflected in the other cached copy
- Make it so this doesn't exist - get OS to force the same index bit for the cache (page colouring)