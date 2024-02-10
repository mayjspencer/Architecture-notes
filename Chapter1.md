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




















