
## Instruction Fetch Stage

Additional pipeline stage is added *after* the frontend-decoders shift the decoded instructions into a dense fetch packet:
- Needed to pass into the **backend**
- Provides an interface - decoder always gets 4 instructions, even if 4-8 instructions are issued
- Overflow of instructions (fetched instructions - 4) are stored in the fetch buffer


Next Line Predictor (micro-BTB):
- Small, fully-associative cache that stores branch address and target address
- Can be improved with [[Branch Folding]]
- Improves fetch throughput on small-bodied loops (JMP to top predicted)


Repair mechanisms - restores predictor state after misspeculation:
- Loop-predictor and RAS are snapshotted and repaired on mispredict
- Maybe use a RAS pop shift register?


Superscalar branch resolution, with multiple branch resolution units:
- Handles when multiple branches are in the same packet
- Additional pipeline stage after WB to read the fetch-PC queue - a queue for PCs to fetch soon - and determine the target address for the *oldest mispredicted branch* from a vector of branch mispredictions
- Allows for aggressive scheduling of branches - don't need to wait for a branch resolution unit to finish

TAGE:
- High accuracy for dense areas with many conditional branches
- Provides bit vector of taken / not taken, each bit for each instruction in the fetch packet
- Updated during commit stage

### Execute Stage

SFB recorder:
- Records difficult to predict branches into internal predicated microOps
- Detects short-forwards and translates into *set-flag* and *conditionally execute* instructions
- Set-flag writes outcome of branch to predicate register
- Conditionally execute either
	- True - Executes instruction and places into target register
	- False - Copies original value of (stale physical) destination register into physical destination register


### Load-Store Stage

Dual Ported L1 Data $:
- Two banks - for odd and even addresses (implemented as 1R1W SRAMs)
- Good with load-heavy bursts
- Can use [[Loads & Stores]] - memory dependence prediction
- Is a [[Non-Blocking Caches]]


Line-fill buffers:
- Cache requests to populate the line-fill buffer
- Allows for cache eviction and requests to happen in parallel
- Flushed into L1 D$ when evictions are complete
- Misspeculated cache refills stay in line-fill buffers, which means they must be searched in parallel
- Flushed on context switch?
- Uses a next-line prefetcher - [[Hardware Prefetching]] - after a cache miss 
- Updates L1 D$ during speculation window - if there are no cache evictions in queue


### Side Channel Vulnerabilities

SonicBOOM vulnerabilities - speculative execution changes the microarchitectural state temporarily:
- Spectre-v1: bypassing bounds checks
- Spectre-v2: branch target injection
- Spectre-v5: return stack buffer attack

Issues with Load / Store Unit:
- 3 cycle delay to allocate misses in the MSHRs and request data from L2
- Loads are optimistically fired to use OoO execution

Attack methodology:
- Attacker establish desired conditions
- Trigger victim execution with invalid instruction
- Victim loads secret into covert channel (data cache)
- Processor resets pipeline by squashing and rolling back
- Attacker probes data cache for information (flush + reload)


Bypassing Bounds Checks:
- Mis-train conditional branch direction prediction
- Trigger using a conditional branch

Branch Target Injection:
- Mis-train BTB for branch target prediction
- Trigger using a call to a mis-speculated target (malicious function)

Return Stack Buffer Attack:
- Craft malicious gadget after a call site
- Trigger using a return, as exploiting RAS miss-match with software stack


RIDL (Line Buffers - MDS Attacks)


#### Mitigations:

Speculative Taint Tracking:
- Allow OoO execution
- Destination of speculative load is marked as tainted in a hardware taint file
- Subsequent loads that use tainted addresses activate data memory fencing for all loads in the LSQ (*fence_dmem*).
	- This is detected at AGU (*memaddrcalc*)
	- All loads in LSQ - as we are in danger zone
- Also notifies frontend to send out dispatch hazards (dis), forcing the pipeline to stall and the processor to run in order temporarily.
- When fencing used, data cache refill is temporarily disabled and MSHRs are cleared until load is no longer speculative (and data is untainted)
- Untaint when instruction is commitable
- On misprediction, data in tainted registers is invalid

Retpolines:
- Use a direct branch to a function that evaluates the indirect address and places it in a register, using a call instruction
- Ret back once evaluated
- Removes need for target address speculation



Cache formula:
log2(cache line size) = offset bits
log2(cache size / no of ways * address bits) = index bits
tag bits = address bits - offset bits - index bits



