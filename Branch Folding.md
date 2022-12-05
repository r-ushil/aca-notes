#BranchPrediction 

Instead of just the branch target address in the [[Branch Target Buffer]], store the entire target *instruction*.

This way, you can skip the Instruction Fetch stage for the next instruction, so the effective CPI for the branch is zero.

Could stash target instruction for both taken and not-taken to reduce mispredicition delay.