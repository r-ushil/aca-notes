[[SonicBOOM]]

- VIPT
	- Cache is 32KiB, 8 way -> each way is 4Kib in size, same as page size
	- Allows for indexing of cache using untranslated address to get physical tag
	- Exactly this size because there's no point in having a larger cache way
	- High number of ways -> larger cache, can use [[Way Prediction]]
- Branch bubbles / branch resolution / fetch target queue (Fetch PC)
- Sidechannel attacks (line buffers, store and load queues, BTB poisoning, RAS) and mitigations
- Load store forwarding
- Multicore processors and cache coherency
- GPU
- Line Fill Buffers