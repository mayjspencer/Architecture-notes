# Chapter 4

## 4.1 Intro

### A basic MIPS implementation

We will be examining an implementation that includes a subset of the core MIPS instruction set:

- The memory-reference instructions load word (lw) and store word (sw)
- The arithmetic-logical instructions add, sub, AND, OR, and slt
- The instructions branch equal (beq) and jump (j), which we add last
This illustrates the key principles used in creating a datapath and designing the control. The implementation of the remaining instructions is similar.

### Overivew
We looked at the core MIPS instructions, including the integer arithmetic-logical instructions, the memory-reference instructions, and the branch instructions.<br>
Much of what needs to be done to implement these instructions is the same, independent of the exact class of instruction.<br>
For every instruction, the first two steps are identical:

1. Send the program counter (PC) to the memory that contains the code and fetch the instruction from that memory.
2. Read one or two registers, using fields of the instruction to select the registers to read. For the load word instruction, we need to read only one register, but most other instructions require reading two registers.

The 3rd step is often very similar too. For example, all instruction classes, except jump, use the arithmetic-logical unit (ALU) after reading the registers. 
- The memory-reference instructions use the ALU for an address calculation,<br>the arithmetic-logical instructions for the operation execution,<br>and branches for comparison.

After using the ALU, the actions required to complete various instruction classes differ. 
- A memory-reference instruction will need to access the memory either to read data for a load or write data for a store.
- An arithmetic-logical or load instruction must write the data from the ALU or memory back into a register.
- Lastly, for a branch instruction, we may need to change the next instruction address based on the comparison; otherwise, the PC should be incremented by 4 to get the address of the next instruction.
