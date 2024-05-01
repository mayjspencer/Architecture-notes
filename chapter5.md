# Chapter 5

## 5.1 Intro

### Illusion of Speed and Space

The principle of locality is important for creating the illusion of a large, fast memory.

It says that programs usually only access a small part of their memory at once, much like how a student uses only a few books from a library at a time.

There are two types of locality:

1. Temporal locality: If a program accesses a piece of data, it's likely to access it again soon.
2. Spatial locality: If a program accesses a piece of data, it's likely to access nearby data soon after.

Programs exhibit these types of locality because of their structure.

For example, loops in programs often cause repeated access to the same data, showing temporal locality.

Also, since programs tend to access data sequentially, they show spatial locality.

Memory systems use these principles to speed up access to data by keeping frequently accessed data closer to the processor. This reduces the need to access slower, higher-level memory.

### Memory Hierarchy

- **Definition:** A structure using multiple memory levels with different speeds and sizes.
- **Goal:** Provide the user with a large memory at the speed of the fastest memory.
- **Levels:** 
  - **Level 1:** Smallest and closest to the processor, using SRAM technology.
  - **Level 2:** Larger and farther away, typically using DRAM technology.
  - **Level 3:** Largest and farthest from the processor, often using magnetic disk technology.
- **Data:** 
  - Hierarchical, with each level being a subset of the next higher level.
  - Copied between only two adjacent levels at a time.
- **Block (or Line):** 
  - Minimum unit of information that can be present or not present in the hierarchy, akin to a book in a library.
 
### Memory Hierarchy Performance Metrics

- **Hit:** Data requested by the processor found in the upper level.
- **Miss:** Data not found in the upper level, requiring access to the lower level.
- **Hit Rate (Hit Ratio):** Fraction of memory accesses found in the upper level.
- **Miss Rate:** Fraction of memory accesses not found in the upper level.
- **Hit Time:** Time to access the upper level, including hit/miss determination.
- **Miss Penalty:** Time to replace a block in the upper level with one from the lower level, including block delivery to the processor.

This chapter explores how memory systems impact computer architecture, including OS management, I/O, compilers, and application performance. 

Memory access, a major program activity, heavily influences system performance. Programmers need to understand memory hierarchy for optimal performance. 

Designers focus on memory systems, using advanced mechanisms to improve performance.

A true memory hierarchy ensures data cannot be in a level without being in the next higher level. 

This allows the processor to maintain a fast access time primarily determined by the highest level, while benefiting from a memory as large as the lowest level.

![Alt text](https://zytools.zybooks.com/zyAuthor/CompOrgAndDesign_PattersonHennesy/56/IMAGES/embedded_image_1mips_46657b8a-42a4-7cf3-75eb-b5f0219b06ee_AD51wvhR9FHqR4FTsJ2V.png)


## 5.2 Memory Technologies

- Main memory is implemented using DRAM, which is less costly per bit than SRAM but substantially slower.
- Caches closer to the processor use SRAM, which is faster but more expensive per bit compared to DRAM.
- Flash memory is nonvolatile and is used as secondary memory in Personal Mobile Devices.
- Magnetic disks are used to implement the largest and slowest level in the memory hierarchy in servers.

![Alt text](https://zytools.zybooks.com/zyAuthor/CompOrgAndDesign_PattersonHennesy/56/IMAGES/embedded_image_1mips_51382f1d-c2d5-ba73-83e8-567ebf198fc0_AD51wvhR9FHqR4FTsJ2V.png)

### SRAM
- SRAMs are integrated circuits with a single access port for read or write operations, typically using six to eight transistors per bit to prevent data disturbance.
- SRAMs do not require refreshing and have an access time close to the cycle time, requiring minimal power in standby mode.
- In the past, PCs and servers used separate SRAM chips for caches, but today, all levels of caches are integrated onto the processor chip.

### DRAM
- DRAMs store data as a charge in a capacitor, using a single transistor per bit for access. They are denser and cheaper per bit than SRAM but require periodic refreshing.
- DRAMs refresh cells by reading and writing back the contents of entire rows, thanks to a two-level decoding structure, allowing for efficient refreshing without constant individual bit access.
- They do this becuase they must refresh every charge.
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

