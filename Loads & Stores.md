[#DynamicScheduling]
Stores are buffed in the ROB and committed only when the instruction is committed.

Loads can be issues while several stores are uncommited - data inconsistency.

When the addresses of a load and all preceding uncommitted stores are known:
- If none of the store addresses match the load, then it can proceed
- If it matches the address of an uncommitted store, then forward the store's data

Need to **STALL** loads until all possibly aliasing store addresses are known.

Store buffer contains:
- Address to store
- Data to store

Load check - checks for matching address in the store buffer
Load unit - buffers load instructions


## Memory Dependence Speculation
[[SonicBOOM]] - check below

As loads and stores use **COMPUTED ADDRESSES**, they may not be known at issue time, so any store / load instruction could be a data dependence (RAW). Could wait as above, or:
- Speculate whether it is or isn't - then check for misprediction
- Add a fowarding predictor to improve this speculation

Allow a load to proceed **BEFORE** we know for sure if / which any prior uncommited store instruction writes to its address.

Proceed by either:
- Forwarding a value for some store whose value is known
- Go to memory

Memory dependence speculation - use a forwarding predictor to do so.
https://www.jilp.org/vol2/v2paper13.pdf
https://en.wikipedia.org/wiki/Memory_dependence_prediction

Can use the idea of **store-wait** (Alpha 21264):
- Guess that there is no memory dependence
- Squash if there is, and mark the load instruction as *store-wait* in the load unit
- Next time that load is needed, it will wait for all previous stores to complete

Can also use the idea of a store set to further improve this, so that you're not waiting on EVERY store.

Store unit can mark entries as valid / speculative, so speculative instructions aren't stored in memory.
