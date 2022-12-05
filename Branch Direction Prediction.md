#BranchPrediction

Alternatives:
- [[Predicated Instructions]]
- [[Simulataneous Multithreading]]
- Delayed Branch
	- Delay by one instruction

Superscalar - Multiple instructions are issued per clock cycle

Branch direction predicts ***conditional*** branches.


### Branch History Table

Lower bits of PC used to index BHT.
1 or 0 represents taken or not-taken.

No address check:
- Aliasing: possible misprediction if 2 different branch instructions map to same BHT entry.

Using a 2-bit scheme adds hysteresis to decision making process - a lot like second-chance with page evicition

Most branches are highly biases: either almost always taken or almost always not-taken.

BHT uses local history.

### Global History

Use *m* most recently-executed branches to influence decision.

Keep an *m*-bit branch-history register (BHR) - a shift regsiter recording taken and not-taken direction of the last m branches.

Use (m, n) together -> use the shift register to index which BHT to use.

### Tournament Predictors

Use 2 predictors:
- One based on global info
- One based on local info

Combine info with a selector - driven by a predictor.


### Warm-Up and Context Switching

Simple predictors re-learn faster
Sophisticated predictors re-learn slower
Selective predictors may choose faster learning predictors until better predictor ***warms up.***
