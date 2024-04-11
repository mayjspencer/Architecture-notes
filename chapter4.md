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


## 4.2 Logic Design Conventions

### Combinational vs Sequential

- **Combinational Elements**: These elements operate on data values and produce outputs based solely on their current inputs. The ALU is an example of a combinational element because it produces the same output for the same set of inputs and has no internal storage.

- **State Elements**: These elements contain internal storage and are not solely dependent on their inputs. Examples include registers, memories, and flip-flops. State elements retain their values even when the power is turned off and completely characterize the computer's state.

- **Inputs and Outputs of State Elements**: State elements have at least two inputs (data value to be written and clock signal) and one output (the value that was written in an earlier clock cycle). The clock signal determines when the data value should be written into the state element.

- **Sequential Logic**: Components that contain state are also known as sequential logic elements because their outputs depend on both their inputs and the internal state. For example, the output from a register depends on both the data value supplied to it and on what was written into the register previously.

### Clocking Methodology

- **Clocking Methodology**: It defines when signals can be read and when they can be written, ensuring hardware predictability. It specifies the timing of reads and writes to avoid conflicts that could lead to unpredictable behavior.

- **Edge-Triggered Clocking**: This methodology updates values in sequential logic elements only on a clock edge, which is a quick transition from low to high or vice versa. Combinational logic must have inputs from and outputs to state elements, ensuring that outputs are stable and valid for the next clock cycle.

- **Inputs and Outputs in Edge-Triggered Clocking**: Inputs to combinational logic are values stored in state elements from the previous clock cycle. Outputs from combinational logic are written into state elements and become stable and valid for the following clock cycle.

- **Importance of Clocking Methodology**: Clocking methodologies, like edge-triggered clocking, are crucial for maintaining the integrity and predictability of data flow within a computer system. They ensure that data is read and written at the appropriate times, preventing conflicts and ensuring correct operation of the hardware.

### Clock Cycle Walkthrough
To explain and summarize:

- **First Rising Clock Edge**: Both state elements are written with new values on this edge. This means that any data stored in these elements is updated based on the inputs they receive.

- **Propagation of Values**: When a new value is written into state element 1, it triggers a series of calculations or operations in the combinational logic. This means that the combinational logic processes the input it receives from state element 1 and produces an output based on this input. This output is then passed to state element 2.

- **Combinational Logic and Memory**: Combinational logic does not have any memory. This means that its output at any given moment is solely determined by its current input. It doesn't "remember" past inputs or outputs; each output is a direct result of the current input.

- **Stable Values**: For the system to work correctly, the new value computed by the combinational logic must be stable before it enters state element 2. A value is considered stable when it has settled and no longer changes. This ensures that when the new value is latched into state element 2 on the next rising clock edge, it is a reliable and accurate representation of the output from the combinational logic.

- **Timing Considerations**: The new value computed by the combinational logic must be stable and ready to enter state element 2 well before the next rising clock edge. This is crucial for ensuring that the updated data is available and stable for the next clock cycle.

- **Clock Cycle Length**: The time required for signals to propagate from state element 1, through the combinational logic, and to state element 2 defines the length of the clock cycle. This length determines the speed at which the computer can operate reliably.

### Control Signals and Definitions

1. **Write Control Signal**: In the context of updating state elements (like registers or memory) in a digital system, a write control signal is used to indicate when a new value should be written into a state element. This signal is typically synchronized with the clock signal, which determines the timing of operations in the system.

2. **Clock Signal**: The clock signal is a periodic signal that oscillates between two voltage levels (usually 0 and 1) and is used to synchronize the operations of the digital system. State elements are typically updated on the rising or falling edge of the clock signal, depending on the specific design.

3. **Clock Edge**: State elements are updated only when a clock edge occurs (either rising or falling edge, depending on the design). The write control signal must be asserted (logically high) at the same time as the clock edge for the update to occur.

4. **Control Signal**: A control signal is a signal used in digital systems to control the operation of various components, such as multiplexors or functional units. It determines which inputs are selected or how a unit should operate.

5. **Asserted and Deasserted Signals**: When a signal is asserted, it means that the signal is logically high or true. Conversely, when a signal is deasserted, it means that the signal is logically low or false.

For the 32-bit MIPS architecture, most state and logic elements handle 32-bit data.<br>Buses, which are wider signals, are shown with thicker lines.<br>Sometimes, we combine buses to form a wider bus, indicated by labels on the bus lines.<br>Arrows show the direction of data flow between elements.<br>Control signals are distinguished from data signals using color.






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
