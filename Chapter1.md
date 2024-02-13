# Chapter 1 - Computer Technology

## 1.1 Intro
- Embedded computers
    - a computer inside another device used for running one predetermined application or collection of software
- PC
- Server
    - a computer used for running larger programs for multiple users, often simultaneously, and typically accessed only via a network
  
  kilobyte	KB	1000^1	kibibyte	2^10 KiB		2%
  
  megabyte	MB	1000^2	mebibyte	2^20 MiB		5%
  
  gigabyte	GB	1000^3	gibibyte	2^30 GiB		7%
  
  terabyte	TB	1000^	tebibyte	2^40 TiB		10%
  
  petabyte	PB	1000^	pebibyte	2^50 PiB		13%
  
  exabyte	EB		1000^  exbibyte	2^EiB		15%
  
  zettabyte	ZB	1000^	zebibyte	2^ZiB		18%
  
  yottabyte	YB	1000^8	yobibyte	2^YiB		21%
  
  ronnabyte	RB	1000^9	robibyte	2^90 RiB		24%
  
  queccabyte	QB 1000^10	quebibyte	2^100 QiB		27%

## 1.2 Seven fundamentals

#### Use abstracion to simplify

#### Make the common case fast

#### Performance via parallelism

#### Performance via pipelining

#### Performance via prediction

#### Hierarchy of memories

#### Dependability via redundancy

## 1.3 Below the Program

#### Systems software: 
Software that provides services that are commonly useful, including operating systems, compilers, loaders, and assemblers. Runs on the hardware

#### Compiler: 
A program that translates high-level language statements into assembly language statements.

#### Assembly Language 
A symbolic representation of machine instructions.

#### Machine Language
A binary representation of machine instructions.

## 1.4 Under the Covers

The five classic components of a computer are input, output, memory, datapath, and control, with the last two sometimes combined and called the processor. 

- Input data from a keyboard, file, network, etc., is written in memory.

- A datapath operates on data.

- Output reads data from memory.

- Control sends the signals that determine the operations of the datapath, memory, input, and output.


<strong>Liquid crystal display</strong>: A display technology using a thin layer of liquid polymers that can be used to transmit or block light according to whether a charge is applied.

<strong>Active matrix display</strong>: A liquid crystal display using a transistor to control the transmission of light at each individual pixel.

#### A processor consists of 2 main components:
- Datapath - the component of the processor that performs math operations
- Control - the component of the processor that commands the datapath, memory, and I/O devices according to the instructions of the program.

### Memory
<strong>Memory</strong>: The storage area in which programs are kept when they are running and that contains the data needed by the running programs.

<strong>Dynamic random access memory (DRAM)</strong>: Memory built as an integrated circuit; it provides random access to any location. Access times are 50 nanoseconds and cost per gigabyte in 2020 was $3 to $6.

Inside the processor is a different kind of memory - cache. 

<strong>Cache memory</strong> consists of a small, fast memory that acts as a buffer for the DRAM memory.
- cache is built using static random access memory

<strong>Static random access memory (SRAM)</strong>: Also memory built as an integrated circuit, but faster and less dense than DRAM.

### Instruction Set Architecture

The combination of the basic instruction set and the operating system interface provided for application programmers is called the <strong>application binary interface (ABI)</srtong>.

<srtong>Instruction set architecture</strong> -  An abstract interface between the hardware and the lowest-level software that encompasses all the information necessary to write a machine language program that will run correctly, including instructions, registers, memory access, I/O, and so on.

### Memory

<strong>Main memory</strong>: Also called primary memory. Memory used to hold programs while they are running; typically consists of DRAM in today's computers.

<strong>Secondary memory</strong>: Nonvolatile memory used to store programs and data between runs; typically consists of flash memory in PMDs and magnetic disks in servers.

<strong>Magnetic disk</strong>: Also called hard disk. A form of nonvolatile secondary memory composed of rotating platters coated with a magnetic recording material.

<srtong>Flash memory</strong>: A nonvolatile semiconductor memory. It is cheaper and slower than DRAM but more expensive per bit and faster than magnetic disks. 



## 1.5 Building processors and memoru

<strong>Transistor</strong>: An on/off switch controlled by an electric signal.

DRAM capacity growth has slowed down and doubles, rather than quadruples, every two to three years.

<strong>Silicon</strong>: A natural element that is a semiconductor - a substance that does not conduct electricity well.

With a special chemical process, it is possible to add materials to silicon that allow tiny areas to transform into one of three devices:

- Excellent conductors of electricity (using either microscopic copper or aluminum wire)

- Excellent insulators from electricity (like plastic sheathing or glass)

- Areas that can conduct or insulate under special conditions (as a switch)


#### Building Chips
The process starts with a silicon crystal ingot, which looks like a giant sausage.

An ingot is finely sliced into wafers no more than 0.1 inches thick.

These wafers then go through a series of processing steps, during which patterns of chemicals are placed on each wafer, creating the transistors, conductors, and insulators discussed earlier. 

These patterned wafers are then tested with a wafer tester, and a map of the good parts is made.

Then, the wafers are diced into dies.

<strong>Die</strong>: The individual rectangular sections that are cut from a wafer, more informally known as chips.

These good dies are then bonded into packages and tested one more time before shipping the packaged parts to customers.

<strong>Yield</strong>: The percentage of good dies from the total number of dies on the wafer.

#### Equations

Cost per die = 
(Cost per Wafer) 
\ 
(Dies per wafer * yield)

Dies per wafer ~= Wafer area / Die area

Yield = 1 / ( 1 + (Defects per area * (Die area/2)))^2


## 1.6 Performance

### Metrics

<strong>Execution time</strong>: The total time required for the computer to complete a task, including disk accesses, memory accesses, I/O activities, operating system overhead, CPU execution time, and so on.

<strong>Throughput</strong>: Also called bandwidth. Another measure of performance, it is the number of tasks completed per unit time.

### Equations

X is n times faster than Y 
### - Performance X / Performance Y = n

If X is n times as fast as Y, then the execution time on Y is n times as long as it is on X:
### - Performance X / Performance Y = Exectution Time Y / Execution Time X = n

<strong>Example:</strong> If computer A runs a program in 10 seconds and computer B runs the same program in 15 seconds, how much faster is A than B?

Execution Time B / Execution Time A = <strong>15 / 10 = 1.5</strong>

### CPU Time
CPU time is the actual time the CPU spends computing for a specific task. It does not include time spent waiting on I/O instructions.

User CPU time: The CPU time spent in a program itself.

System CPU time: The CPU time spent in the operating system performing tasks on behalf of the program.

System performance refers to elapsed time on an unloaded system and CPU performance refers to user CPU time

### The Clock
Clock Cycle: The time for one clock period, usually of the processor clock, which runs at a constant rate.

Clock period: The length of each clock cycle.  = 1 / Clock Cycle

A particular processor has a clock rate of 1 GHz. The clock thus ticks one billion times per second

A clock rate of 1 GHz corresponds to a period of 1 nanosecond, which is 1x10-9 seconds.

#### CPU clock cycles = Instructions for a program X Average clock cycles per instruction (CPI)
- CPI provides one way of comparing two different implementations of the same instruction set architecture
- <strong>Clock cycles per instruction (CPI)</strong>: Average number of clock cycles per instruction for a program or program fragment.

#### CPU Time = Clock Cycles X Clock Cycle Time
<strong>Example:</strong> Computer A: clock cycle time of 250 ps and a CPI of 2.0    |     Computer : clock cycle time of 500 ps and a CPI of 1.2

CPU Time A = Clock Cycles X Clock Cycle Time
= I * 2.0 * 250 = 500 * I ps

CPU Time B = Clock Cycles X Clock Cycle Time
= I * 1.2 * 500 = 600 * I ps

A is faster by 1.2 ratio

### Classic CPU Perfomance Equation

#### CPU time = Instruction Time X CPI X Clock Cycle Time

#### CPU tmime = (Instruction Time X CPI) / Clock Rate


## 1.7 The Power Wall

#### Clock rates stopped increasing around 2004 because of power.

The power required per transistor is just the product of energy of a transition and the frequency of transitions:

#### Power = 1/2 * Capacitative Load * Voltage^2 * Frequency

Frequency switched is a function of the clock rate. 

The capacitive load per transistor is a function of both the number of transistors connected to an output (called the fanout) and the technology, which determines the capacitance of both wires and transistors.

#### Why can't we get more power ? 
The problem today is that further lowering of the voltage appears to make the transistors too leaky, like water faucets that cannot be completely shut off.









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

.




















