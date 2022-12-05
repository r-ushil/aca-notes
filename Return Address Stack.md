#BranchPrediction 

Jump instructions push the next instruction onto the Return Address Stack.

Ret instructions pop the instruction on top of the RAS into the PC, returning to the caller's next instruction.

Used when [[Branch Target Buffer]] thinks an address is a RET instruction.

After decode, the instruction is checked:
- If JSR, add PC to RAS
- If ret, pop RAS, prediction was correct

If the call stack is deeper than the RAS:
- RAS will be empty at some point - stack overflow
- RAS prediction may be wrong:
	- Switching threads would change the stack pointer


Updating the RAS:
- On commit - might not have a prediction in time for addresses deeper in the stack.

[[SonicBOOM]]

If a conditional branch is mispredicted, and inside the taken version of that branch is a function call, then a return address is going to be pushed onto the stack.

To mitigate this and optimise for loops - we can have a shift register that records *prediction state*.

On every prediction, every time we hit a JSR instruction, we increment this register and let it push a return address onto the stack.

If we suffer a misprediction - we pop the RAS n times, where n is the value in this shift register, and we're back to the original state.

BTB entries would be affected though -> we'd have entries for return addresses when they shouldn't be there. That's fine though - as we shouldn't get to those return addresses unless we were supposed to be there, assuming there are no erroneous jumps.

