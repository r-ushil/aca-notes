[#DynamicScheduling]

Tomasulo allowed for out-of-order **completion**, which doesn't work when you need to break at a specific point in the instruction stream (interrupts).

Need to break because:
- Page faults (runtime issues)
- Branch speculation, on mispredict


*Speculative* Tomasulo:
- Issue (sometimes called Dispatch)
	- If RS and ROB slot free issue instruction, send operands and reorder buffer number for destination
- Execution (sometimes called Issue)
	- If both operands ready - execute
	- If not ready, watch CDB
	- Checks for RAW issue
- Write
	- Write result on CDB to all awaiting FUs and to the ROB
	- Mark RS as available
- Commit
	- When instruction is at the head of the ROB **and** its result is present update the commit side register with result (or store to memory)
	- Remove instruction from ROB


Makes use of a [[Reorder Buffer]] to commit out-of-order instructions in order for handling precise interrupts.

Makes use of a Load / Store Unit ([[Loads & Stores]]) to deal with buffered, uncommitted store instructions.


