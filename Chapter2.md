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
