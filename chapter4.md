# Chapter 4

## 4.1 Intro

### A basic MIPS implementation

We will be examining an implementation that includes a subset of the core MIPS instruction set:

- The memory-reference instructions load word (lw) and store word (sw)
- The arithmetic-logical instructions add, sub, AND, OR, and slt
- The instructions branch equal (beq) and jump (j), which we add last
This illustrates the key principles used in creating a datapath and designing the control. The implementation of the remaining instructions is similar.

### Overivew
We looked at the core MIPS instructions, including the integer arithmetic-logical instructions, the memory-reference instructions, and the branch instructions. Much of what needs to be done to implement these instructions is the same, independent of the exact class of instruction. For every instruction, the first two steps are identical:

Send the program counter (PC) to the memory that contains the code and fetch the instruction from that memory.
Read one or two registers, using fields of the instruction to select the registers to read. For the load word instruction, we need to read only one register, but most other instructions require reading two registers.
