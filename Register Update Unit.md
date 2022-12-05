[#DynamicScheduling]
Combines [[Reorder Buffer]] and Reservation Stations into a single pool.

RUU entry contains:
- Tag - calculated through instruction number - used to index RUU
- Opcode
- Operands - Can be results or tags

Algorithm:
- Instructions are fetch from I$
- Instructions are issued to the RUU and given a tag (`i = i + 1 % RUU_SIZE`)
- RUU sends next ready entry to the dispatcher
- Dispatcher sends instruction to available FU
- On completion, FU uses CDB to broadcast result to RUU and issue-side registers
- Once an instruction is at the head of RUU and complete, it's commited
	- Updates commit-side registers
	- If misprediction detected:
		- Fetch correct instruction
		- Reset commit tag `j` to `i`
		- Update issue side registers with commit side

Removes dependence on functional units per reservation station.

RUU can now be out-of-order, can just poll the RUU tag.