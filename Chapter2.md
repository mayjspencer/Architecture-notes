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
~~~

  add a, b, c   # The sum of b and c is placed in a
  
  add a, a, d   # The sum of b, c, and d is now in a
  
  add a, a, e   # The sum of b, c, d, and e is now in a
~~~

<strong> sub a, b, c </strong>computes b - c and puts the result in a.

### Storage in MIPS

#### MIPS has 32 registers
~~~
$s0..$s7  |  $t0..$t9  |  $zero  |  $a0..$a3  |  $v0..$v1  |  $gp  |  $fp  |  $sp  |  $ra  |  $at
~~~
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

In MIPS, words must start at addresses that are multiples of 4. This requirement is called an alignment restriction, and many architectures have it. 

### Store
Copies data from a register to memory.

The format of a store is: the name of the operation, followed by the register to be stored, then offset to select the array element, and finally the base register. 

The MIPS address is specified in part by a constant and in part by the contents of a register. 

The actual MIPS name is sw, standing for store word.

### When #variables > #registers
Many programs have more variables than computers have registers. 

Consequently, the compiler tries to keep the most frequently used variables in registers and places the rest in memory, using loads and stores to move variables between registers and memory. 

The process of putting less commonly used variables (or those needed later) into memory is called _spilling registers_.

Data is more useful when in a register.

### Immediate Operands
~~~
addi $s3, $s3, 4 
~~~

## 2.4 Signed and Unsigned Numbers

#### Binary digit
- Also called a bit. One of the two numbers in base 2 (0 or 1) that are the components of information.

#### Least significant bit
- The rightmost bit in a MIPS word.

#### Most significant bit
- The leftmost bit in a MIPS word.

#### Overflow
 - when the results of an operation are larger than can be represented in a register.

### Signed Numbers

#### Two's complement
 - A signed number representation where a leading 0 indicates a positive number and a leading 1 indicates a negative number. The complement of a value is obtained by complementing each bit (0 → 1 or 1 → 0), and then adding one to the result (explained further below).

Two's complement does have one negative number, −2,147,483,648, that has no corresponding positive number.

<strong>Overflow</strong> occurs when the leftmost retained bit of the binary bit pattern is not the same as the infinite number of digits to the left (the sign bit is incorrect): a 0 on the left of the bit pattern when the number is negative or a 1 when the number is positive.

## 2.5 Representing Instructions in the Computer

Since registers are referred to in instructions, there must be a convention to map register names into numbers. 

In MIPS assembly language, registers <strong>$s0 to $s7</strong> map onto registers 16 to 23, and registers <strong>$t0 to $t7</strong> map onto registers 8 to 15.

### Instruction format
- a form of representation of an instruction composed of fields of binary numbers.
- all MIPS instructions are 32 bits long.

### R-type Instruction Breakdown

A MIPS instruction is made like this in 32 bits:

![Alt text](https://github.com/mayjspencer/Architecture-notes/blob/main/Rtype.png?raw=true)

Here is the meaning of each name of the fields in MIPS instructions:

#### op
Basic operation of the instruction, traditionally called the opcode.

#### rs
The first register source operand.

#### rt
The second register source operand.

#### rd
The register destination operand. It gets the result of the operation.

#### shamt
Shift amount

#### funct
Function. This field, often called the function code, selects the specific variant of the operation in the op field.

.

.

#### Opcode Definition
 - The field that denotes the operation and format of an instruction.

### I-Type Instruction Breakdown
Used by the immediate and data transfer instructions.

![Alt text](https://github.com/mayjspencer/Architecture-notes/blob/main/IType.png?raw=true)

The 16-bit address means a load word instruction can load any word within a region of ±215 or 32,768 bytes (±213 or 8192 words) of the address in the base register rs. 

Similarly, add immediate is limited to constants no larger than ±215. 

### Example
~~~
lw   $t0, 32($s3)   # Temporary reg $t0 gets A[8]
~~~
19 (for $s3) is placed in the rs field

8 (for $t0) is placed in the rt field

32 is placed in the address field

Note that the meaning of the rt field has changed for this instruction: in a load word instruction, the rt field specifies the destination register, which receives the result of the load. 

A destination register is a register that receives the result of an operation.

## 2.6 Logical Operators

### Shift Left / Right

Java Operator: << / >>

MIPS Instructions: sll / srl

#### Example: Shift Left by 4

Instruction: sll $t2, $s0, 4
- A shift moves bits left or right. This instruction moves the bits over by 4 places. The leftmost 4 bits are discarded, and 4 0's are shifted into the rightmost 4 bits.
- This instruction would shift $s0's value and store the result in $t2.

Note: Shifting Left by n = mulitplying by 2^n
- Example: Left shift by 2 = multiplying by 16

Note: Shifting Right by n = dividing by 2^n
- Example: Right shift by 2 = dividing by 16

### SHAMT Field

The shamt field in the R-format is used in shift instructions. It stands for shift amount.

### AND 
A logical bit- by-bit operation with two operands that calculates a 1 only if there is a 1 in both operands.

AND can apply a bit pattern to a set of bits to force 0s where there is a 0 in the bit pattern. Such a bit pattern in conjunction with AND is traditionally called a mask, since the mask "conceals" some bits.
~~~
and $t0, $t1, $t2
~~~

### OR
A bit-by-bit operation that places a 1 in the result if either operand bit is a 1.
~~~
or $t0, $t1, $t2
~~~

### NOT 
A logical bit-by-bit operation with one operand that inverts the bits; that is, it replaces every 1 with a 0, and every 0 with a 1.

### NOR
A logical bit-by-bit operation with two operands that calculates the NOT of the OR of the two operands. That is, it calculates a 1 only if there is a 0 in both operands.

~~~
nor $t0, $t1, $t3
~~~

## 2.7 Making Decisions

### Conditional Branches
An instruction that requires the comparison of two values and that allows for a subsequent transfer of control to a new address in the program based on the outcome of the comparison.

### BEQ 
~~~
beq register1, register2, L1
~~~

This instruction means go to the statement labeled L1 if the value in register1 equals the value in register2. The mnemonic beq stands for branch if equal. 

### BNE
~~~
bne register1, register2, L1
~~~

It means go to the statement labeled L1 if the value in register1 does not equal the value in register2. The mnemonic bne stands for branch if not equal. 

### Unconditional Branches
An unconditional branch is an instruction that always follows the branch, as in the "j" instruction

### J
~~~
~~
~~
j EXIT
~~
EXIT:
~~~

### While Loop
~~~
Loop: bne $s0, $s1, Exit
Loop body
j Loop
Exit:
~~~

### For Loop
Given: for (i = 1; i < j; ++i) { loop body } where i is $s0, j is $s1.

~~~
Loop: slt   $t3, $s0, $s1
      beq $t3, $zero, Exit
      # Loop body
      j Loop
~~~

Basic block: A sequence of instructions without branches (except possibly at the end) and without branch targets or branch labels (except possibly at the beginning).

### SLT - Set on Less Than
Compares two registers and sets a third register to 1 if the first is less than the second; otherwise, it is set to 0.

#### SLT
~~~
slt  $t0, $s3, $s4   // $t0 = 1 if $s3 < $s4
~~~
#### SLTI
~~~
slti $t0, $s2, 10    // $t0 = 1 if $s2 < 10
~~~

MIPS offers two versions of the set on less than comparison to handle unsigned/signed. Set on less than (slt) and set on less than immediate (slti) work with signed integers. Unsigned integers are compared using set on less than unsigned (sltu) and set on less than immediate unsigned (sltiu).

### Comparisons
MIPS compilers use the slt, slti, beq, bne, and the fixed value of 0 (always available by reading register $zero) to create all relative conditions: equal, not equal, less than, less than or equal, greater than, greater than or equal.

## 2.8 Procedures / Functions in Hardware

Procedure: A stored subroutine that performs a specific task based on the parameters with which it is provided.

### Procedure Registers
MIPS uses these registers for procedure use:
~~~
$a0 - $a3: four argument registers in which to pass parameters
~~~
~~~
$v0 - $v1: two value registers in which to return values
~~~
~~~
$ra: one return address register to return to the point of origin
~~~

### jal
In addition to allocating these registers, MIPS assembly language includes an instruction just for the procedures: it jumps to an address and simultaneously saves the address of the following instruction in register $ra. The jump-and-link instruction (jal) is simply written
~~~
jal ProcedureAddress
~~~
jump-and-link instruction: An instruction that jumps to an address and simultaneously saves the address of the following instruction in a register ($ra in MIPS).

The link portion of the name means that an address or link is formed that points to the calling site to allow the procedure to return to the proper address. This "link", stored in register $ra (register 31), is called the return address. The return address is needed because the same procedure could be called from several parts of the program.

### jr
To support such situations, computers like MIPS use jump register instruction (jr), introduced above to help with case statements, meaning an unconditional jump to the address specified in a register:
~~~
jr $ra
~~~
The jump register instruction jumps to the address stored in register $ra—which is just what we want. Thus, the calling program, or caller, puts the parameter values in $a0 - $a3 and uses jal X to jump to procedure X (sometimes named the callee). The callee then performs the calculations, places the results in $v0 and $v1, and returns control to the caller using jr $ra.

### Program Counter
Implicit in the stored-program idea is the need to have a register to hold the address of the current instruction being executed. 

For historical reasons, this register is almost always called the program counter, abbreviated PC in the MIPS architecture.

The jal instruction actually saves PC + 4 in register $ra to link to the following instruction to set up the procedure return.

jal sets $ra with the address of the next instruction, which is 4 more than 1000, so that the procedure will know where to return.

### Using more registers

Sometimes, the procedure may need more registers than the 4 arguement and 2 return registers. We need to spill registers to memory. 

The ideal data structure for spilling registers is a stack—a last-in-first-out queue.

A stack needs a pointer to the most recently allocated address in the stack to show where the next procedure should place the registers to be spilled or where old register values are found. The stack pointer is adjusted by one word for each register that is saved or restored. MIPS software reserves register 29 for the stack pointer, giving it the obvious name $sp.

By historical precedent, stacks "grow" from higher addresses to lower addresses. This convention means that you push values onto the stack by subtracting from the stack pointer. Adding to the stack pointer shrinks the stack, thereby popping values off the stack.

![Alt text](https://github.com/mayjspencer/Architecture-notes/blob/main/ss.png?raw=true)


In the previous example, we used temporary registers and assumed their old values must be saved and restored. To avoid saving and restoring a register whose value is never used, which might happen with a temporary register, MIPS software separates 18 of the registers into two groups:

$t0 - $t9: temporary registers that are not preserved by the callee (called procedure) on a procedure call

$s0 - $s7: saved registers that must be preserved on a procedure call (if used, the callee saves and restores them)

This simple convention reduces register spilling. In the example above, since the caller does not expect registers $t0 and $t1 to be preserved across a procedure call, we can drop two stores and two loads from the code. We still must save and restore $s0, since the callee must assume that the caller needs its value.

### Nested Procedures

Procedures that do not call others are called leaf procedures

Some procedures call other procedures, leading them to both want to use the same argument registers and return address register $ra. 

One solution is pushing everything to memory when calling a child function. 

The caller pushes any argument registers ($a0 - $a3) or temporary registers ($t0 - $t9) that are needed after the call. The callee pushes the return address register $ra and any saved registers ($s0 - $s7) used by the callee.

Global pointer: The register that is reserved to point to the static area.

<strong>Preserving</strong>: guaranteeing that the caller will get the same data back on a load from the stack as it stored onto the stack.

#### Preserved Across a Procedure Call
- Saved registers: $s0-$s7
- Stack pointer register: $sp
- Return address register: $ra
- Stack above the stack pointer

#### Not Preserved
- Temporary registers: $t0-$t9
- Argument registers: $а0-$а3
- Return value registers: $v0-$v1
- Stack below the stack pointer

The stack above $sp is preserved simply by making sure the callee does not write above $sp; $sp is itself preserved by the callee adding exactly the same amount that was subtracted from it; and the other registers are preserved by saving them on the stack (if they are used) and restoring them from there.

<strong>Procedure frame</strong>: Also called activation record. The segment of the stack containing a procedure's saved registers and local variables.

![Alt text](https://github.com/mayjspencer/Architecture-notes/blob/main/ss1.png?raw=true)

<strong>Frame pointer</strong>: A value denoting the location of the saved registers and local variables for a given procedure.

### Allowing space for new data on the heap
In addition to automatic variables that are local to procedures, C programmers need space in memory for static variables and for dynamic data structures.

The stack starts in the high end of memory and grows down. The first part of the low end of memory is reserved, followed by the home of the MIPS machine code, traditionally called the text segment. Above the code is the static data segment, which is the place for constants and other static variables.

Although arrays tend to be a fixed length and thus are a good match to the static data segment, data structures like linked lists tend to grow and shrink during their lifetimes. The segment for such data structures is traditionally called the heap, and it is placed next in memory.

Note that this allocation allows the stack and heap to grow toward each other, thereby allowing the efficient use of memory as the two segments wax and wane.

This convention is another example of making the common case fast: most procedures can be satisfied with up to 4 arguments, 2 registers for a return value, 8 saved registers, and 10 temporary registers without ever going to memory.

### C vs Java

C allocates and frees space on the heap with explicit functions. malloc() allocates space on the heap and returns a pointer to it, and free() releases space on the heap to which the pointer points. Memory allocation is controlled by programs in C, and it is the source of many common and difficult bugs. Forgetting to free space leads to a "memory leak", which eventually uses up so much memory that the operating system may crash. Freeing space too early leads to "dangling pointers", which can cause pointers to point to things that the program never intended.

Java uses automatic memory allocation and garbage collection primarily to avoid such bugs.

## 2.10 MIPS for 32 bit immediates or addresses

### Sometimes 16 bit immediates aren't enough
Although constants are frequently short and fit into the 16-bit field, sometimes they are bigger. 

The MIPS instruction set includes the instruction load upper immediate <strong>(lui)</strong> specifically to set the upper 16 bits of a constant in a register, allowing a subsequent instruction to specify the lower 16 bits of the constant.

![Alt text](https://github.com/mayjspencer/Architecture-notes/blob/main/lui.png?raw=true)

This is lui and ori working to create a 32 bit integer 16 bits at a time.

### Addressing in branches and jumps

#### J 
Jumps use the final MIPS instruction format, called the J-type, which consists of 6 bits for the operation field and the rest of the bits for the address field.

#### Conditionals
Unlike the jump instruction, the conditional branch instruction must specify two operands (5 bits, 10 bits total) in addition to the branch address. Thus, leaving only 16 bits for the branch address: 6, 5, 5, 16, = 32

To get more than 2^16 addresses available: MIPS uses <strong>PC-relative addressing</strong>: An addressing regime in which the address is the sum of the program counter (PC) and a constant in the instruction.

## 2.11 Paralellism

Parallel Execution makes things faster but must be done in sync. 

To know when a task is finished writing so that it is safe for another to read, the tasks need to synchronize.

If they don't synchronize, there is a danger of a data race, where the results of the program can change depending on how events happen to occur.

<strong>Data race</strong>: Two memory accesses form a data race if they are from different threads to same location, at least one is a write, and they occur one after another.

### Locks
Lock and unlock can be used straightforwardly to create regions where only a single processor can operate, called a mutual exclusion (mutex).

A memory location must have atomic read/write: you can't do both at once.

One typical operation for building synchronization operations is the <strong>atomic exchange or atomic swap</strong>, which interchanges a value in a register for a value in memory.

To see how to use this to build this, we build a  lock where 0 is used to indicate that the lock is free and 1 is used to indicate that the lock is unavailable. A processor tries to set the lock by doing an exchange of 1, which is in a register, with the memory address corresponding to the lock. The value returned from the exchange instruction is 1 (unavailable) if some other processor had already claimed access, and 0 (free) otherwise. In the latter case, the value is also changed to 1 (unavailable), preventing any competing exchange in another processor from also retrieving a 0 (free).

In MIPS this pair of instructions includes a special load called a load linked and a special store called a store conditional. These instructions are used in sequence: if the contents of the memory location specified by the load linked are changed before the store conditional to the same address occurs, then the store conditional fails

The store conditional is defined to both store the value of a (presumably different) register in memory and to change the value of that register to a 1 if it succeeds and to a 0 if it fails. Since the load linked returns the initial value, and the store conditional returns 1 only if it succeeds, the following sequence implements an atomic exchange on the memory location specified by the contents of $s1:

~~~
again: add  $t0, $zero, $s4    #copy locked value
       ll   $t1, 0($s1)        #load linked
       sc   $t0, 0($s1)        #store conditional
       beq  $t0, $zero, again  #branch if store fails
       add  $s4, $zero, $t1    #put load value in $s4
~~~

Any time a processor intervenes and modifies the value in memory between the ll and sc instructions, the sc returns 0 in $t0, causing the code sequence to try again. At the end of this sequence the contents of $s4 and the memory location specified by $s1 have been atomically exchanged.

## 2.12 Starting a Program
This section describes the four steps in transforming a C program in nonvolatile storage into a program running on a computer.

1. A <strong>compiler</strong> converts a high-level language program, like a C program, to an assembly language program.
2. An <strong>assembler</strong> converts an assembly language program to an object module in machine language.
3. A <strong>linker</strong> combines multiple object modules, such as library routines, into an executable machine language program.
4. Finally, a <strong>loader</strong> places the executable file into memory, to be run by the computer.

### Compiler
The compiler transforms the C program into an assembly language program, a symbolic form of what the machine understands.

### Assembler
Assembly language uses instructions that are converted into machine code by an assembler. Assemblers can also interpret common variations of instructions, known as pseudoinstructions, simplifying programming. For example, the MIPS assembler treats the instruction `move $t0, $t1` as `add $t0, $zero, $t1`.

Pseudoinstructions in MIPS include `blt`, `bgt`, `bge`, and `ble`, which are converted into `slt` and `bne` instructions. MIPS assemblers also allow loading 32-bit constants into registers, exceeding the 16-bit immediate instructions limit.

Assemblers can accept numbers in different bases, such as hexadecimal in MIPS. The main task of an assembler is to convert assembly language programs into object files, which contain machine language instructions, data, and necessary information for memory placement.

Object files in UNIX typically consist of a header, text segment (machine code), static data segment, relocation information, symbol table, and debugging information. The symbol table matches labels with memory addresses.

Overall, pseudoinstructions and other assembler features simplify assembly programming, but understanding the underlying architecture is essential for optimal performance.

### Linker
What we have presented so far suggests that a single change to one line of one procedure requires compiling and assembling the whole program.

An alternative to rerunning the entire program is to only rerun the procedure where the change happened. This alternative requires a new systems program, called a link editor or linker, which takes all the independently assembled machine language programs and "stitches" them together.

<strong>Linker</strong>: A program that takes independently assembled machine language programs and combines them into an executable file. 

#### It performs three main tasks:

Symbolic Placement: It places code and data modules in memory symbolically.
Address Resolution: It determines the addresses of labels in the code and data.
Patching: It updates internal and external references in the code.

The linker uses information from each module's relocation information and symbol table to resolve undefined labels. It then determines the memory locations for each module, considering the MIPS convention for memory allocation.

The output of the linker is an executable file that can be run on a computer. This file has the same format as an object file but contains no unresolved references. Partially linked files, like library routines, may still have unresolved addresses and remain as object files.

### Loader
Now that the executable file is on disk, the operating system reads it to memory and starts it. The loader follows these steps in UNIX systems:

1. Reads the executable file header to determine size of the text and data segments.
2. Creates an address space large enough for the text and data.
3. Copies the instructions and data from the executable file into memory.
4. Copies the parameters (if any) to the main program onto the stack.
5. Initializes the machine registers and sets the stack pointer to the first free location.
6. Jumps to a start-up routine that copies the parameters into the argument registers and calls the main routine of the program. When the main routine returns, the start-up routine terminates the program with an exit system call..

### Dynamically Linked Libraries
Dynamically linked libraries (DLLs) are a way to link library routines to a program during its execution, rather than at compile time. 
This approach has several advantages over static linking:

- Updates: With DLLs, programs can use updated versions of libraries without needing to recompile. This allows for bug fixes and support for new hardware devices.
- Efficiency: DLLs only load the library routines that are actually called during program execution, reducing the size of the executable and improving efficiency.
- Lazy Procedure Linkage: In this approach, routines are linked only when they are called for the first time, further optimizing the loading process.

The initial overhead of DLLs includes extra space for dynamic linking information and some additional processing time the first time a routine is called. However, subsequent calls incur minimal overhead.

### Static Linked Libraries
Static linking is the process of combining all the necessary library code into the executable file of a program before it is run. This means that all the code from the libraries that the program uses is included in the final executable.
- Benefits: This makes the program self-contained and easier to distribute, as all the necessary code is included.
- Drawbacks: However, if the libraries are updated or fixed, the program needs to be recompiled and redistributed to take advantage of these changes. Additionally, static linking can result in larger executable files.


## 2.13 Translating C to MIPS

### Example 1:

~~~
void swap(int v[], int k)
{
    int temp;
    temp = v[k];
    v[k] = v[k+1];
    v[k+1] = temp;
}
~~~

When translating from C to assembly language by hand, we follow these general steps:

1. Allocate registers to program variables.
2. Produce code for the body of the procedure.
3. Preserve registers across the procedure invocation.

Steps: 
1. The MIPS convention on parameter passing is to use registers  $a0, $a1, $a2, and $a3.
Since swap has just two parameters, v and k, they will be found in registers $a0 and $a1.

The only other variable is temp, which we associate with register $t0 since swap is a leaf procedure.

2. Body of code
To get v[k] we have to first get k and then add v (v is just a starting addess of a section of memory).

This MIPS code will first get the actual memory value of k: (k*4) and add it to v and store the address v[k] in temp $t1
~~~
sll   $t1, $a1, 2     # reg $t1 = k * 4
add   $t1, $a0, $t1   # reg $t1 = v + (k * 4)
                      # reg $t1 has the address of v[k]
~~~

Now we can use that address stored in $t1 to access v[k] and v[k+1] in memory - loading them into temp registers.
~~~
lw    $t0, 0($t1)     # reg $t0 (temp) = v[k]
lw    $t2, 4($t1)     # reg $t2 = v[k + 1]
                      # refers to next element of v
~~~

Now we store them back, but in swapped locations:
~~~
sw    $t2, 0($t1)     # v[k] = reg $t2
sw    $t0, 4($t1)     # v[k + 1] = reg $t0 (temp)
~~~

Since we are not using saved registers in this leaf procedure, there is nothing to preserve.
~~~
jr $ra
~~~

### Example 2: 

Bubble Sort
~~~
void sort (int v[], int n)
{
    int i, j;
    for (i = 0; i < n; i += 1) {
        for (j = i - 1; j >= 0 && v[j] > v[j + 1]; j -= 1) {
            swap(v, j); 
        }
    } 
}
~~~
1. The two parameters of the procedure sort, v and n, are in the parameter registers $a0 and $a1, and we assign register $s0 to i and register $s1 to j.
2. Code body
First for loop:

It takes just one instruction to initialize i to 0, the first part of the for statement:
~~~
move $s0, $zero          # i = 0
~~~

4. 









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

.

.

.

.

.

