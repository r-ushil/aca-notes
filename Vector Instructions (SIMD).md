Vector Instructions:
- Less fetching from instruction cache, but exploits parallelism
- Lanes execute in parallel
- Have vector predicate registers (512 bit wide - 1 bit per lane)
- Zero masking - when predicate is false, register for lane set to 0
- Masking - when predicate is false, register for lane retains old value
- If trip count is not divisible by vector instruction, need additional non-vector instruction to mop up
- If arrays are potentially aliased or are data dependent, cannot use vector instructions
- Use 'gather' instruction for indirect array indexing
- If the alignment of the operand pointers is not known, need instructions to align onto a 32 byte boundary