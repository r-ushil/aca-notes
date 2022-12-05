#BranchPrediction 

Makes extensive use of the [[Branch Target Buffer]].

Both [[Branch Target Prediction]] and [[Branch Direction Prediction]] happen in parallel.

If a slower, direction predictor differs, re-steer:
- Squash first prediction by re-writing PC
- Fetch from improved prediction

Can use [[Branch Folding]], to reduce CPI for branch instruction on a BTB hit.

Updating the branch predictor:
- Can update BTB as **SOON** as branch outcome is known (before committing)
	- This means that later branches have correct BTB predictions.
- Update BTB after commit - just in case of a branch misprediction.

### Return Addresses

As a function may be called from different places, it must return to the right place.
The address of the next instruction must be saved and restored.

A [[Return Address Stack]] is used.