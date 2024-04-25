# Chapter 4.5 - 4.8

## Section 4.5  - Multi Cycle Implementation

### Advantages
- The ability to allow instructions to take different numbers of clock cycles
- The ability to share functional units within the execution of a single instruction

### Abstract Version of a Multi Cycle Datapath
![Alt text](https://zytools.zybooks.com/zyAuthor/CompOrgAndDesign_PattersonHennesy/56/IMAGES/8c6d4c5b-a263-7ae0-923f-66d41924cb0a)

#### Differences from Single Cycle
- A single memory unit is used for both instructions and data.
- There is a single ALU, rather than an ALU and two adders.
- One or more registers are added after every major functional unit to hold the output of that unit until the value is used in a subsequent clock cycle.

### Data used in later clock cycles
- At end of a cycle, all data used in later cycles must be stored in a state element.
- Data used by later instructions in a later cycle is stored into one of the programmer-visible state elements: the register file, the PC, or the memory.
- Data used by the same instruction in a later cycle must be stored into one of the additional registers.

### Added Registers
The position of the additional registers is determined by these 2 factors:
- what combinational units will fit in one clock cycle
-what data is needed in later cycles for the instruction.

In this multicycle design, we assume that the clock cycle can have at most one of: a memory access, a register file access (two reads or one write), or an ALU operation. 

Hence, any data produced by one of these three units must be saved into a temporary register for use on a later cycle.

If it were not saved, then the possibility of the use of an incorrect value could occur.

#### New Registers
- The Instruction register (IR) and the Memory data register (MDR)
- The A and B registers
- The ALUOut register





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

.

.



.


.
