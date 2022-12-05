#BranchPrediction 

Need addresses at the same time as prediction
Check for branch match - can't use wrong branch address

BTB entry:
- Branch PC
- Predicited PC
- Extra prediction state bits

BTB is:
- ***Indexed*** with low-order PC address bits
- ***Tagged*** with high-order PC address bits
- A cache of branch target addresses

You **don't** have to know if the current instruction is a branch instruction to predict a branch:
- In parallel with every instruction fetch - check whether BTB predicts instruction *will* be a taken branch
- When a **taken** branch is committed, update BTB with branch's target address

Check in the Instruction Decode stage whether BTB predicition was correct - otherwise re-write the PC and squash the MEM and WB stages.
