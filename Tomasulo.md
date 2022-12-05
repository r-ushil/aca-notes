[#DynamicScheduling]

All instructions in a dynamically scheduled processor pass through the **issue stage in order**.

The issue stage:
- Decodes instructions
- Checks for structural hazards
- Operands from registers are either values or reservation station tags

The write-back stage:
- Results from functional units are broadcast on CDB, with tag from RS
- Any RS or register monitoring that tag with collect value on match from CDB


Tomasulo Benefits:
- Enables OoO execution
- Allows for register renaming - so no WAW or WAR hazards, fixes name dependence
- Dynamic loop unrolling - due to register renaming, great for pipelining
- CDB acts like it's forwarding

Tomasulo Drawbacks:
- Lots of associative stores from the CDB at high speed
- High wiring density from CDB (Turing tax)
- Number of FUs that can complete per cycle is only one
- Non-precise interrupts [[Speculative Execution]]