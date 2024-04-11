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

![Alt text](https://github.com/mayjspencer/Architecture-notes/blob/main/ALU1.png?raw=true)

1. **Instruction Fetch**: The first step in executing any instruction is fetching it from memory. This is done using the Program Counter (PC) to determine the memory address of the instruction.

2. **Register Read**: Most instructions require reading one or two registers. The instruction specifies which registers to read.

3. **ALU Operations**: After reading registers, most instructions use the Arithmetic Logic Unit (ALU) for some operation. This could be an arithmetic operation, logical operation, or a comparison for branches.

4. **Memory Access**: Memory-reference instructions (like load and store) access data memory. The ALU is used to calculate the memory address.

5. **Write Back**: The result of an ALU operation or data from memory is often written back to a register.

6. **Branch Handling**: For branch instructions, the ALU is used for comparison. Depending on the result, the next instruction address is either calculated by adding an offset to the current PC or by directly setting it to a new address.

7. **Control Unit**: A control unit interprets the instruction and generates control signals for various components of the processor (ALU, registers, memory, etc.) to perform the required operations.

8. **Multiplexors**: Multiplexors are used to select between different data sources or operations based on the type of instruction being executed.

9. **Clock Cycle**: Initially, the text describes a simple implementation where each instruction takes a single clock cycle to complete. This is not efficient for all instructions but is a starting point for understanding the basic concepts.

The text also mentions that this basic design is a foundation for more complex implementations, where instructions may take multiple clock cycles and where pipelining is used to improve performance.


.

.

.

.

.

.

.

.

.

.

.
