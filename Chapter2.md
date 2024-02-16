# Chapter 2 - Instructions

## 2.1 Intro

The words of a computer's language are called instructions, and its vocabulary is called an instruction set.

<strong>Instruction set</strong>: The vocabulary of commands understood by a given architecture.

Computer languages are quite similar.

The chosen instruction set comes from <strong>MIPS Technologies</strong>.

A quick look at three other popular instruction sets:
- ARMv7 is similar to MIPS. More than 100 billion chips with ARM processors will be manufactured in between 2017 and 2020, making it the most popular instruction set in the world.
- Intel x86, which powers both the PC and the cloud of the PostPC Era.
- ARMv8, which extends the address size of the ARMv7 from 32 bits to 64 bits. Ironically, as we shall see, this 2013 instruction set is closer to MIPS than it is to ARMv7.

This similarity of instruction sets occurs because all computers are constructed from hardware technologies based on similar underlying principles and because there are a few basic operations that all computers must provide. Moreover, computer designers have a common goal: to find a language that makes it easy to build the hardware and the compiler while maximizing performance and minimizing cost and energy. 

By learning how to represent instructions, you will also discover the secret of computing: <strong>the stored-program concept</strong>.

<strong>Stored-program concept</strong>: The idea that instructions and data of many types can be stored in memory as numbers, leading to the stored-program computer.

## 2.2 Operations of the Computer Hardware
The MIPS assembly language notation: 

<strong>add a, b, c</strong> instructs a computer to add the two variables b and c and to put their sum in a.

Each MIPS arithmetic instruction performs only one operation and must always have exactly three variables. 
- For example, suppose we want to place the sum of four variables b, c, d, and e into variable a.

  add a, b, c   # The sum of b and c is placed in a
  
  add a, a, d   # The sum of b, c, and d is now in a
  
  add a, a, e   # The sum of b, c, d, and e is now in a

<strong> sub a, b, c </strong>computes b - c and puts the result in a.

### Storage in MIPS

#### MIPS has 32 registers

$s0..$s7  |  $t0..$t9  |  $zero  |  $a0..$a3  |  $v0..$v1  |  $gp  |  $fp  |  $sp  |  $ra  |  $at

Fast locations for data. In MIPS, data must be in registers to perform arithmetic, register $zero always equals 0, and register $at is reserved by the assembler to handle large constants.

#### MIPS has 230 memory words	

Memory[0], Memory [4], ...., Memory[4294967292]	

Accessed only by data transfer instructions. MIPS uses byte addresses, so sequential word addresses differ by 4. Memory holds data structures, arrays, and spilled registers.

## 2.3 Operands of the Computer Hardware

<strong>Word</strong>: The natural unit of access in a computer, usually a group of 32 bits; corresponds to the size of a register in the MIPS architecture.

Computers typically only have 32 registers. With fewer registers, the clock frequency can be made faster, because the clock signal requires less time to reach every register.

### Memory Operands

Data structures (arrays and structures) are kept in memory since they are too large to fit in registers.

Arithmetic operations occur only on registers in MIPS instructions; thus, MIPS must include instructions that transfer data between memory and registers. 

Such instructions are called data transfer instructions. 

To access a word in memory, the instruction must supply the memory address. 

Memory is just a large, single-dimensional array, with the address acting as the index to that array, starting at 0. 

For example, in the figure below, the address of the third data element is 2, and the value of Memory [2] is 10.

### Load
The format of the load instruction is the name of the operation followed by the register to be loaded, then a constant and register used to access memory. 

The actual MIPS name for this instruction is lw, standing for load word.

In an lw instruction, a <strong>base address</strong> is the starting address of an array in memory, a <strong>base register</strong> is a register that holds an array's base address, and an <strong>offset</strong> is a constant value added to a base address to locate a particular array element.
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

.

.