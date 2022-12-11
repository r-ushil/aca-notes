#Software

Loop unrolling - allows for loops to be efficienty pipelined

VLIW - Very Long Instruction Word
- Uses multiple, independent functional units
- Packages multiple, independent instructions into one VLIW
- Usually padded with NoOp instructions, increased code size as a result
- Ambitiously unrolls loops for pipelining, increased code size as a result, can compress in memory and unpack when fetching
- Lockstep - any stall in FU must cause the entire CPU to stall, no hazard-detection hardware, and all components must be kept in sync
- Binary compatibility between processors was difficult