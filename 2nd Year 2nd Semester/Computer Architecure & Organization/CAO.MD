# Beyond Slides

<span style="font-size:24px;">

---

# A Top-Level View of Computer Function and Interconnection: 

## Basic instruction cycle: 

 The basic function performed by a computer is execution of a program, which consists
of a set of instructions stored in memory. The processor does the actual work by
executing instructions specified in the program. This section provides an overview of
the key elements of program execution. In its simplest form, instruction processing
consists of two steps: The processor reads (fetches ) instructions from memory one
at a time and executes each instruction. Program execution consists of repeating
the process of instruction fetch and instruction execution. The instruction execution
may involve several operations and depends on the nature of the instruction (see, for
example, the lower portion of Figure 2.4).

The processing required for a single instruction is called an instruction cycle.
Using the simplified two-step description given previously, the instruction cycle is
depicted in Figure 3.3. The two steps are referred to as the fetch cycle and the execute
cycle. Program execution halts only if the machine is turned off, some sort of unrecoverable
error occurs, or a program instruction that halts the computer is encountered.

## Fetch Cycle: 

At the beginning of each instruction cycle, the processor fetches an instruction
from memory. In a typical processor, a register called the program counter (PC)
holds the address of the instruction to be fetched next. Unless told otherwise, the
processor always increments the PC after each instruction fetch so that it will fetch
the next instruction in sequence (i.e., the instruction located at the next higher memory
address). So, for example, consider a computer in which each instruction occupies
one 16-bit word of memory. Assume that the program counter is set to memory
location 300, where the location address refers to a 16-bit word. The processor will
next fetch the instruction at location 300. On succeeding instruction cycles, it will
fetch instructions from locations 301, 302, 303, and so on. This sequence may be
altered, as explained presently.

The fetched instruction is loaded into a register in the processor known as
the instruction register (IR). The instruction contains bits that specify the action
the processor is to take. The processor interprets the instruction and performs the
required action. 


## Example of a partial program execution:

Figure 3.5 illustrates a partial program execution, showing the relevant
portions of memory and processor registers. The program fragment shown adds
the contents of the memory word at address 940 to the contents of the memory
word at address 941 and stores the result in the latter location. Three instructions,
which can be described as three fetch and three execute cycles, are required:

1. The PC contains 300, the address of the first instruction. This instruction (the
value 1940 in hexadecimal) is loaded into the instruction register IR, and
the PC is incremented. Note that this process involves the use of a memory
address register and a memory buffer register. For simplicity, these intermediate
registers are ignored.

2. The first 4 bits (first hexadecimal digit) in the IR indicate that the AC is to be
loaded. The remaining 12 bits (three hexadecimal digits) specify the address
(940) from which data are to be loaded.

3. The next instruction (5941) is fetched from location 301, and the PC is
incremented.

4. The old contents of the AC and the contents of location 941 are added, and
the result is stored in the AC.

5. The next instruction (2941) is fetched from location 302, and the PC is
incremented.

6. The contents of the AC are stored in location 941.

In this example, three instruction cycles, each consisting of a fetch cycle and an
execute cycle, are needed to add the contents of location 940 to the contents of 941.
With a more complex set of instructions, fewer cycles would be needed. Some older
processors, for example, included instructions that contain more than one memory
address. Thus, the execution cycle for a particular instruction on such processors could
involve more than one reference to memory. Also, instead of memory references, an
instruction may specify an I/O operation.

## Instruction Cycle State Diagram: 

The execution cycle for a particular instruction may involve more than one
reference to memory. Also, instead of memory references, an instruction may specify
an I/O operation. With these additional considerations in mind, Figure 3.6 provides
a more detailed look at the basic instruction cycle of Figure 3.3. The figure is in the
form of a state diagram.

For any given instruction cycle, some states may be null and
others may be visited more than once. The states can be described as follows:

### Instruction address calculation (iac): 
Determine the address of the next
instruction to be executed. Usually, this involves adding a fixed number to
the address of the previous instruction. For example, if each instruction is 16
bits long and memory is organized into 16-bit words, then add 1 to the previous
address. If, instead, memory is organized as individually addressable 8-bit
bytes, then add 2 to the previous address.

 ### • Instruction fetch (if): 
 Read instruction from its memory location into the
processor.

### • Instruction operation decoding (iod): 
Analyze instruction to determine type
of operation to be performed and operand(s) to be used.

### • Operand address calculation (oac): 
If the operation involves reference to an
operand in memory or available via I/O, then determine the address of the
operand.

### • Operand fetch (of): 
Fetch the operand from memory or read it in from I/O.

### • Data operation (do): 
Perform the operation indicated in the instruction.

### • Operand store (os): 
Write the result into memory or out to I/O.

States in the upper part of Figure 3.6 involve an exchange between the
processor and either memory or an I/O module. States in the lower part of the
diagram involve only internal processor operations. The oac state appears twice,
because an instruction may involve a read, a write, or both. However, the action performed
during that state is fundamentally the same in both cases, and so only a single
state identifier is needed.

Also note that the diagram allows for multiple operands and multiple results,
because some instructions on some machines require this. For example, the PDP-11
instruction ADD A,B results in the following sequence of states: iac, if, iod, oac, of,
oac, of, do, oac, os.

Finally, on some machines, a single instruction can specify an operation to be performed
on a vector (one-dimensional array) of numbers or a string (one-dimensional
array) of characters. As Figure 3.6 indicates, this would involve repetitive operand fetch
and/or store operations.


## Instruction Cycle without Interrupts: 

To accommodate interrupts, an interrupt cycle is added to the instruction
cycle, as shown in Figure 3.9. In the interrupt cycle, the processor checks to see if
any interrupts have occurred, indicated by the presence of an interrupt signal. If no
interrupts are pending, the processor proceeds to the fetch cycle and fetches the
next instruction of the current program. If an interrupt is pending, the processor
does the following:

• It suspends execution of the current program being executed and saves its
context. This means saving the address of the next instruction to be executed
(current contents of the program counter) and any other data relevant to the
processor’s current activity.

• It sets the program counter to the starting address of an interrupt handler routine.

The processor now proceeds to the fetch cycle and fetches the first instruction
in the interrupt handler program, which will service the interrupt. The interrupt
handler program is generally part of the operating system. Typically, this program
determines the nature of the interrupt and performs whatever actions are needed.
In the example we have been using, the handler determines which I/O module
generated the interrupt and may branch to a program that will write more data out
to that I/O module. When the interrupt handler routine is completed, the processor
can resume execution of the user program at the point of interruption.

It is clear that there is some overhead involved in this process. Extra instructions
must be executed (in the interrupt handler) to determine the nature of the interrupt
and to decide on the appropriate action. Nevertheless, because of the relatively large
amount of time that would be wasted by simply waiting on an I/O operation, the
processor can be employed much more efficiently with the use of interrupts.

## Computer Modules: 

A computer consists of a set of components or modules of three basic types
(processor, memory, I/O) that communicate with each other. In effect, a computer is
a network of basic modules. Thus, there must be paths for connecting the modules.

The collection of paths connecting the various modules is called the interconnection
structure. The design of this structure will depend on the exchanges that
must be made among modules.

Figure 3.15 suggests the types of exchanges that are needed by indicating the
major forms of input and output for each module type:

### • Memory: 
Typically, a memory module will consist of N words of equal length.
Each word is assigned a unique numerical address (0, 1, …, N - 1). A word of
data can be read from or written into the memory. The nature of the operation
is indicated by read and write control signals. The location for the operation is
specified by an address.

### • I/O module: 
From an internal (to the computer system) point of view, I/O
is functionally similar to memory. There are two operations, read and write.
Further, an I/O module may control more than one external device. We can
refer to each of the interfaces to an external device as a port and give each
a unique address (e.g., 0, 1, …, M - 1). In addition, there are external data
paths for the input and output of data with an external device. Finally, an I/O
module may be able to send interrupt signals to the processor.

### • Processor: 
The processor reads in instructions and data, writes out data after
processing, and uses control signals to control the overall operation of the
system. It also receives interrupt signals.




--- 
# Characteristics of Memory Systems

The term location in Table 4.1 refers to whether memory is internal and external
to the computer. Internal memory is often equated with main memory. But there
are other forms of internal memory. The processor requires its own local memory, in
the form of registers (e.g., see Figure 2.3). Further, as we shall see, the control unit
portion of the processor may also require its own internal memory. We will defer
discussion of these latter two types of internal memory to later chapters. Cache is
another form of internal memory. External memory consists of peripheral storage
devices, such as disk and tape, that are accessible to the processor via I/O controllers.

An obvious characteristic of memory is its capacity. For internal memory, this is
typically expressed in terms of bytes (1 byte = 8 bits) or words. Common word lengths
are 8, 16, and 32 bits. External memory capacity is typically expressed in terms of bytes.

A related concept is the unit of transfer. For internal memory, the unit
of transfer is equal to the number of electrical lines into and out of the memory
module. This may be equal to the word length, but is often larger, such as 64, 128, or
256 bits. To clarify this point, consider three related concepts for internal memory:

### Word: 
The “natural” unit of organization of memory. The size of a word is typically
equal to the number of bits used to represent an integer and to the instruction
length. Unfortunately, there are many exceptions. For example, the CRAY
C90 (an older model CRAY supercomputer) has a 64-bit word length but uses
a 46-bit integer representation. The Intel x86 architecture has a wide variety of
instruction lengths, expressed as multiples of bytes, and a word size of 32 bits.

### Addressable units:
In some systems, the addressable unit is the word. However,
many systems allow addressing at the byte level. In any case, the relationship
between the length in bits A of an address and the number N of addressable
units is 2A = N.

### Unit of transfer: 
For main memory, this is the number of bits read out of or
written into memory at a time. The unit of transfer need not equal a word or
an addressable unit. For external memory, data are often transferred in much
larger units than a word, and these are referred to as blocks

--- 

# Method of Accessing Units of Data

Another distinction among memory types is the method of accessing units of
data. These include the following:

### Sequential access:  
Memory is organized into units of data, called records.
Access must be made in a specific linear sequence. Stored addressing information
is used to separate records and assist in the retrieval process. A shared
read–write mechanism is used, and this must be moved from its current location
to the desired location, passing and rejecting each intermediate record.
Thus, the time to access an arbitrary record is highly variable. Tape units, discussed
in Chapter 6, are sequential access.

### Direct access: 
As with sequential access, direct access involves a shared
read–write mechanism. However, individual blocks or records have a unique
address based on physical location. Access is accomplished by direct access
to reach a general vicinity plus sequential searching, counting, or waiting to
reach the final location. Again, access time is variable. Disk units, discussed in
Chapter 6, are direct access.

### Random access: 
Each addressable location in memory has a unique, physically
wired-in addressing mechanism. The time to access a given location is independent
of the sequence of prior accesses and is constant. Thus, any location
can be selected at random and directly addressed and accessed. Main memory
and some cache systems are random access.

### Associative: 
This is a random access type of memory that enables one to make
a comparison of desired bit locations within a word for a specified match, and
to do this for all words simultaneously. Thus, a word is retrieved based on a
portion of its contents rather than its address. As with ordinary random-access
memory, each location has its own addressing mechanism, and retrieval time
is constant independent of location or prior access patterns. Cache memories
may employ associative access.

# Memory Hierarchy: 

The design constraints on a computer’s memory can be summed up by three questions:
How much? How fast? How expensive?

The question of how much is somewhat open ended. If the capacity is there,
applications will likely be developed to use it. The question of how fast is, in a sense,
easier to answer. To achieve greatest performance, the memory must be able to
keep up with the processor. That is, as the processor is executing instructions, we
would not want it to have to pause waiting for instructions or operands. The final
question must also be considered. For a practical system, the cost of memory must
be reasonable in relationship to other components.

As might be expected, there is a trade-off among the three key characteristics
of memory: capacity, access time, and cost. A variety of technologies are used to
implement memory systems, and across this spectrum of technologies, the following
relationships hold:

• Faster access time, greater cost per bit

• Greater capacity, smaller cost per bit

• Greater capacity, slower access time

The dilemma facing the designer is clear. The designer would like to use memory
technologies that provide for large-capacity memory, both because the capacity
is needed and because the cost per bit is low. However, to meet performance
requirements, the designer needs to use expensive, relatively lower-capacity memories
with short access times.
The way out of this dilemma is not to rely on a single memory component or
technology, but to employ a memory hierarchy.

-- 

A typical hierarchy is illustrated in
Figure 4.1. As one goes down the hierarchy, the following occur:

a. Decreasing cost per bit

b. Increasing capacity

c. Increasing access time

d. Decreasing frequency of access of the memory by the processor

Thus, smaller, more expensive, faster memories are supplemented by larger,
cheaper, slower memories. The key to the success of this organization is item (d)
:decreasing frequency of access. We examine this concept in greater detail when we
discuss the cache, later in this chapter, and virtual memory in Chapter 8. A brief
explanation is provided at this point.

The use of two levels of memory to reduce average access time works in principle,
but only if conditions (a) through (d) apply. By employing a variety of technologies,
a spectrum of memory systems exists that satisfies conditions (a) through
(c). Fortunately, condition (d) is also generally valid.

The basis for the validity of condition (d) is a principle known as locality of
reference [DENN68]. During the course of execution of a program, memory references
by the processor, for both instructions and data, tend to cluster. Programs
typically contain a number of iterative loops and subroutines. Once a loop or subroutine
is entered, there are repeated references to a small set of instructions.
Similarly, operations on tables and arrays involve access to a clustered set of data
words. Over a long period of time, the clusters in use change, but over a short period
of time, the processor is primarily working with fixed clusters of memory references.






---

# Read Only Memory-ROM 

As the name suggests, a read-only memory (ROM) contains a permanent pattern
of data that cannot be changed. A ROM is nonvolatile; that is, no power source is
required to maintain the bit values in memory. While it is possible to read a ROM,
it is not possible to write new data into it. An important application of ROMs is
microprogramming, discussed in Part Four. Other potential applications include

• Library subroutines for frequently wanted functions

• System programs

• Function tables

For a modest-sized requirement, the advantage of ROM is that the data or program
is permanently in main memory and need never be loaded from a secondary storage
device.

A ROM is created like any other integrated circuit chip, with the data actually
wired into the chip as part of the fabrication process. This presents two problems:

• The data insertion step includes a relatively large fixed cost, whether one or
thousands of copies of a particular ROM are fabricated.

• There is no room for error. If one bit is wrong, the whole batch of ROMs must
be thrown out.


# The Performance of a Simple 2 level Memory: 

Suppose that the processor has access to two levels of memory. Level
1 contains 1000 words and has an access time of 0.01 μs; level 2 contains 100,000 words
and has an access time of0.1 μs. Assume that if a word to be accessed is in level 1, then the
processor accesses it directly. If it is in level 2, then the word is first transferred to level 1
and then accessed by the processor. For simplicity, we ignore the time required for the processor
to determine whether the word is in level 1 or level 2. Figure 4.2 shows the general
shape of the curve that covers this situation. The figure shows the average access time to
a two-level memory as a function of the hit ratio H, where H is defined as the fraction of
all memory accesses that are found in the faster memory (e.g., the cache), T1 is the access
time to level 1, and T2 is the access time to level 2. As can be seen, for high percentages
of level 1 access, the average total access time is much closer to that of level 1 than that
of level 2.

In our example, suppose 95% of the memory accesses are found in level 1. Then the
average time to access a word can be expressed as

(0.95)(0.01 μs) + (0.05)(0.01 μs + 0.1 μs) = 0.0095 + 0.0055 = 0.015 μs

The average access time is much closer to 0.01 μs than to 0.1 μs, as desired.

Accordingly, it is possible to organize data across the hierarchy such that the
percentage of accesses to each successively lower level is substantially less than that
of the level above. Consider the two-level example already presented. Let level 2
memory contains all program instructions and data. The current clusters can be
temporarily placed in level 1. From time to time, one of the clusters in level 1 will
have to be swapped back to level 2 to make room for a new cluster coming in to
level 1. On average, however, most references will be to instructions and data contained
in level 1.

This principle can be applied across more than two levels of memory, as suggested
by the hierarchy shown in Figure 4.1. The fastest, smallest, and most expensive
type of memory consists of the registers internal to the processor. Typically, a
processor will contain a few dozen such registers, although some machines contain
hundreds of registers. Main memory is the principal internal memory system of
the computer. Each location in main memory has a unique address. Main memory
is usually extended with a higher-speed, smaller cache. The cache is not usually
visible to the programmer or, indeed, to the processor. It is a device for staging
the movement of data between main memory and processor registers to improve
performance.






--- 

# Flash Memory 

As the name suggests, a read-only memory (ROM) contains a permanent pattern
of data that cannot be changed. A ROM is nonvolatile; that is, no power source is
required to maintain the bit values in memory. While it is possible to read a ROM,
it is not possible to write new data into it. An important application of ROMs is
microprogramming, discussed in Part Four. Other potential applications include

### 1. Library subroutines for frequently wanted functions

### 2. System programs

### 3. Function tables

For a modest-sized requirement, the advantage of ROM is that the data or program
is permanently in main memory and need never be loaded from a secondary storage
device.

A ROM is created like any other integrated circuit chip, with the data actually
wired into the chip as part of the fabrication process. This presents two problems:

• The data insertion step includes a relatively large fixed cost, whether one or
thousands of copies of a particular ROM are fabricated.

• There is no room for error. If one bit is wrong, the whole batch of ROMs must
be thrown out.

# Cache Memory & Main Memory: 

Cache memory is designed to combine the memory access time of expensive, high-speed
memory combined with the large memory size of less expensive, lower-speed
memory.

The concept is illustrated in Figure 4.3a. There is a relatively large and slow
main memory together with a smaller, faster cache memory. The cache contains a
copy of portions of main memory. When the processor attempts to read a word of
memory, a check is made to determine if the word is in the cache. If so, the word is
delivered to the processor. If not, a block of main memory, consisting of some fixed
number of words, is read into the cache and then the word is delivered to the processor.
Because of the phenomenon of locality of reference, when a block of data is
fetched into the cache to satisfy a single memory reference, it is likely that there will
be future references to that same memory location or to other words in the block.

Figure 4.3b depicts the use of multiple levels of cache. The L2 cache is slower
and typically larger than the L1 cache, and the L3 cache is slower and typically
larger than the L2 cache.


# Typical Cache Organization: 

In this organization, the cache
connects to the processor via data, control, and address lines. The data and address
lines also attach to data and address buffers, which attach to a system bus from
which main memory is reached. When a cache hit occurs, the data and address buffers
are disabled and communication is only between processor and cache, with no
system bus traffic. When a cache miss occurs, the desired address is loaded onto the
system bus and the data are returned through the data buffer to both the cache and
the processor. In other organizations, the cache is physically interposed between
the processor and the main memory for all data, address, and control lines. In this
latter case, for a cache miss, the desired word is first read into the cache and then
transferred from cache to processor.

 A discussion of the performance parameters related to cache use is contained
in Appendix 4A.

# Logical & Physical Cache: 

When virtual addresses are used, the system designer may choose to place the
cache between the processor and the MMU or between the MMU and main memory
(Figure 4.7). A logical cache, also known as a virtual cache, stores data using
virtual addresses. The processor accesses the cache directly, without going through
the MMU. A physical cache stores data using main memory physical addresses.

One obvious advantage of the logical cache is that cache access speed is faster
than for a physical cache, because the cache can respond before the MMU performs
an address translation. The disadvantage has to do with the fact that most virtual
memory systems supply each application with the same virtual memory address
space. That is, each application sees a virtual memory that starts at address 0. Thus,
the same virtual address in two different applications refers to two different physical
addresses. The cache memory must therefore be completely flushed with each
application context switch, or extra bits must be added to each line of the cache to
identify which virtual address space this address refers to.



--- 

# Dynamic RAM (DRAM) 

RAM technology is divided into two technologies: dynamic and
static. A dynamic RAM (DRAM) is made with cells that store data as charge on
capacitors. The presence or absence of charge in a capacitor is interpreted as a
binary 1 or 0. Because capacitors have a natural tendency to discharge, dynamic
RAMs require periodic charge refreshing to maintain data storage. The term
dynamic refers to this tendency of the stored charge to leak away, even with power
continuously applied.

--- 

# Static RAM (SRAM) 

In contrast, a static RAM (SRAM) is a digital device that uses the
same logic elements used in the processor. In a SRAM, binary values are stored
using traditional flip-flop logic-gate configurations (see Chapter 11 for a description
of flip-flops). A static RAM will hold its data as long as power is supplied to it.

 As in the DRAM, the SRAM address line is used to open or close a switch.
The address line controls two transistors (T5  and T6 ). When a signal is applied to
this line, the two transistors are switched on, allowing a read or write operation. For
a write operation, the desired bit value is applied to line B, while its complement
is applied to line B. This forces the four transistors (T1 , T2 , T3 , T4 ) into the proper
state. For a read operation, the bit value is read from line B.

--- 

# SRAM VS DRAM 

Both static and dynamic RAMs are volatile; that is,
power must be continuously supplied to the memory to preserve the bit values.
A dynamic memory cell is simpler and smaller than a static memory cell. Thus, a
DRAM is more dense (smaller cells = more cells per unit area) and less expensive
than a corresponding SRAM. On the other hand, a DRAM requires the supporting
refresh circuitry. For larger memories, the fixed cost of the refresh circuitry is more
than compensated for by the smaller variable cost of DRAM cells. Thus, DRAMs
tend to be favored for large memory requirements. A final point is that SRAMs are
somewhat faster than DRAMs. Because of these relative characteristics, SRAM is
used for cache memory (both on and off chip), and DRAM is used for main memory.


--- 

# RAID & All it's Properties

With the use of multiple disks, there is a wide variety of ways in which the
data can be organized and in which redundancy can be added to improve reliability.
This could make it difficult to develop database schemes that are usable
on a number of platforms and operating systems. Fortunately, industry has
agreed on a standardized scheme for multiple-disk database design, known as
RAID (Redundant Array of Independent Disks). The RAID scheme consists
of seven levels, zero through six. These levels do not imply a hierarchical relationship
but designate different design architectures that share three common
characteristics:

1. RAID is a set of physical disk drives viewed by the operating system as a single
logical drive.

2. Data are distributed across the physical drives of an array in a scheme known
as striping, described subsequently.

3. Redundant disk capacity is used to store parity information, which guarantees
data recoverability in case of a disk failure.

The details of the second and third characteristics differ for the different RAID
levels. RAID 0 and RAID 1 do not support the third characteristic.

 The term RAID  was originally coined in a paper by a group of researchers
at the University of California at Berkeley [PATT88].  The paper outlined various
RAID configurations and applications and introduced the definitions of the
RAID levels that are still used. The RAID strategy employs multiple disk drives
and distributes data in such a way as to enable simultaneous access to data from
multiple drives, thereby improving I/O performance and allowing easier incremental
increases in capacity.

---

# Data Mapping for a RAID Level 0 Array

RAID level 0 is not a true member of the RAID family because it does not include
redundancy to improve performance. However, there are a few applications, such as
some on supercomputers in which performance and capacity are primary concerns
and low cost is more important than improved reliability.

For RAID 0, the user and system data are distributed across all of the disks in
the array. This has a notable advantage over the use of a single large disk: If two-
different I/O requests are pending for two different blocks of data, then there is a
good chance that the requested blocks are on different disks. Thus, the two requests
can be issued in parallel, reducing the I/O queuing time.

But RAID 0, as with all of the RAID levels, goes further than simply distributing
the data across a disk array: The data are striped  across the available disks. This
is best understood by considering Figure 6.7. All of the user and system data are
viewed as being stored on a logical disk. The logical disk is divided into strips; these
strips may be physical blocks, sectors, or some other unit. The strips are mapped
round robin to consecutive physical disks in the RAID array. A set of logically consecutive
strips that maps exactly one strip to each array member is referred to as a
stripe.  In an n-disk array, the first n  logical strips are physically stored as the first
strip on each of the n  disks, forming the first stripe; the second n  strips are distributed
as the second strips on each disk; and so on. The advantage of this layout is that if a
single I/O request consists of multiple logically contiguous strips, then up to n  strips
for that request can be handled in parallel, greatly reducing the I/O transfer time.

Figure 6.7 indicates the use of array management software to map between
logical and physical disk space. This software may execute either in the disk subsystem
or in a host computer.

The performance of any of the
RAID levels depends critically on the request patterns of the host system and on
the layout of the data. These issues can be most clearly addressed in RAID 0, where
the impact of redundancy does not interfere with the analysis. First, let us consider
the use of RAID 0 to achieve a high data transfer rate. For applications to experience
a high transfer rate, two requirements must be met. First, a high transfer capacity
must exist along the entire path between host memory and the individual disk drives.
This includes internal controller buses, host system I/O buses, I/O adapters, and host
memory buses.

The second requirement is that the application must make I/O requests that
drive the disk array efficiently. This requirement is met if the typical request is for
large amounts of logically contiguous data, compared to the size of a strip. In this
case, a single I/O request involves the parallel transfer of data from multiple disks,
increasing the effective transfer rate compared to a single-disk transfer.

In a transaction-oriented environment, the user is typically more concerned with 
response time than with transfer rate. For
an individual I/O request for a small amount of data, the I/O time is dominated by the
motion of the disk heads (seek time) and the movement of the disk (rotational latency).

In a transaction environment, there may be hundreds of I/O requests per second.
A disk array can provide high I/O execution rates by balancing the I/O load
across multiple disks. Effective load balancing is achieved only if there are typically
multiple I/O requests outstanding. This, in turn, implies that there are multiple independent
applications or a single transaction-oriented application that is capable of
multiple asynchronous I/O requests. The performance will also be influenced by the
strip size. If the strip size is relatively large, so that a single I/O request only involves
a single disk access, then multiple waiting I/O requests can be handled in parallel,
reducing the queuing time for each request.

---

# RAID L1 

RAID 1 differs from RAID levels 2 through 6 in the way in which redundancy is
achieved. In these other RAID schemes, some form of parity calculation is used to
introduce redundancy, whereas in RAID 1, redundancy is achieved by the simple
expedient of duplicating all the data. As Figure 6.6b shows, data striping is used, as
in RAID 0. But in this case, each logical strip is mapped to two separate physical
disks so that every disk in the array has a mirror disk that contains the same data.
RAID 1 can also be implemented without data striping, though this is less common.

There are a number of positive aspects to the RAID 1 organization:

1. A read request can be serviced by either of the two disks that contains the requested
data, whichever one involves the minimum seek time plus rotational
latency.

2. A write request requires that both corresponding strips be updated, but this
can be done in parallel. Thus, the write performance is dictated by the slower
of the two writes (i.e., the one that involves the larger seek time plus rotational
latency). However, there is no “write penalty” with RAID 1. RAID levels
2 through 6 involve the use of parity bits. Therefore, when a single strip is
updated, the array management software must first compute and update the
parity bits as well as updating the actual strip in question.

3. Recovery from a failure is simple. When a drive fails, the data may still be
accessed from the second drive.

The principal disadvantage of RAID 1 is the cost; it requires twice the disk
space of the logical disk that it supports. Because of that, a RAID 1 configuration
is likely to be limited to drives that store system software and data and other highly
critical files. In these cases, RAID 1 provides real-time copy of all data so that in the
event of a disk failure, all of the critical data are still immediately available.

In a transaction-oriented environment, RAID 1 can achieve high I/O request
rates if the bulk of the requests are reads. In this situation, the performance of RAID 1
can approach double of that of RAID 0. However, if a substantial fraction of the I/O
requests are write requests, then there may be no significant performance gain over
RAID 0. RAID 1 may also provide improved performance over RAID 0 for data
transfer intensive applications with a high percentage of reads. Improvement occurs
if the application can split each read request so that both disk members participate.

---

# RAID L2

RAID levels 2 and 3 make use of a parallel access technique. In a parallel access
array, all member disks participate in the execution of every I/O request. Typically,
the spindles of the individual drives are synchronized so that each disk head is in the
same position on each disk at any given time.

As in the other RAID schemes, data striping is used. In the case of RAID 2
and 3, the strips are very small, often as small as a single byte or word. With RAID 2,
an error-correcting code is calculated across corresponding bits on each data disk,
and the bits of the code are stored in the corresponding bit positions on multiple
parity disks. Typically, a Hamming code is used, which is able to correct single-bit
errors and detect double-bit errors.

Although RAID 2 requires fewer disks than RAID 1, it is still rather costly.
The number of redundant disks is proportional to the log of the number of data
disks. On a single read, all disks are simultaneously accessed. The requested data
and the associated error-correcting code are delivered to the array controller. If
there is a single-bit error, the controller can recognize and correct the error instantly,
so that the read access time is not slowed. On a single write, all data disks and parity
disks must be accessed for the write operation.

RAID 2 would only be an effective choice in an environment in which many
disk errors occur. Given the high reliability of individual disks and disk drives,
RAID 2 is overkill and is not implemented.

---

# RAID L3

RAID 3 is organized in a similar fashion to RAID 2. The difference is that RAID
3 requires only a single redundant disk, no matter how large the disk array. RAID
3 employs parallel access, with data distributed in small strips. Instead of an error correcting
code, a simple parity bit is computed for the set of individual bits in the
same position on all of the data disks.

In the event of a drive failure, the parity drive is accessed and data
is reconstructed from the remaining devices. Once the failed drive is replaced, the
missing data can be restored on the new drive and operation resumed.

In the event of a disk failure, all of the data are still available in what is referred
to as reduced mode. In this mode, for reads, the missing data are regenerated on the
fly using the exclusive-OR calculation. When data are written to a reduced RAID 3
array, consistency of the parity must be maintained for later regeneration. Return to
full operation requires that the failed disk be replaced and the entire contents of the
failed disk be regenerated on the new disk.

Because data are striped in very small strips, RAID 3 can achieve
very high data transfer rates. Any I/O request will involve the parallel transfer of
data from all of the data disks. For large transfers, the performance improvement is
especially noticeable. On the other hand, only one I/O request can be executed at a
time. Thus, in a transaction-oriented environment, performance suffers.

---

# RAID L4

RAID levels 4 through 6 make use of an independent access technique. In an independent
access array, each member disk operates independently, so that separate
I/O requests can be satisfied in parallel. Because of this, independent access arrays
are more suitable for applications that require high I/O request rates and are relatively
less suited for applications that require high data transfer rates.

As in the other RAID schemes, data striping is used. In the case of RAID
4 through 6, the strips are relatively large. With RAID 4, a bit-by-bit parity strip
is calculated across corresponding strips on each data disk, and the parity bits are
stored in the corresponding strip on the parity disk.

RAID 4 involves a write penalty when an I/O write request of small size is performed.
Each time that a write occurs, the array management software must update
not only the user data but also the corresponding parity bits.

To calculate the new parity, the array management software must read the old
user strip and the old parity strip. Then it can update these two strips with the new
data and the newly calculated parity. Thus, each strip write involves two reads and
two writes.

In the case of a larger size I/O write that involves strips on all disk drives, parity
is easily computed by calculation using only the new data bits. Thus, the parity drive
can be updated in parallel with the data drives and there are no extra reads or writes.

In any case, every write operation must involve the parity disk, which therefore
can become a bottleneck.

--- 

# RAID L5 & L6

RAID 5 is organized in a similar fashion to RAID 4. The difference is that RAID
5 distributes the parity strips across all disks. A typical allocation is a round-robin
scheme, as illustrated in Figure 6.8f. For an n-disk array, the parity strip is on a
different disk for the first n stripes, and the pattern then repeats.

The distribution of parity strips across all drives avoids the potential I/O
bottle-neck found in RAID 4.

RAID 6 was introduced in a subsequent paper by the Berkeley researchers
[KATZ89]. In the RAID 6 scheme, two different parity calculations are carried out
and stored in separate blocks on different disks. Thus, a RAID 6 array whose user
data require N disks consists of N + 2 disks.

Figure 6.6g illustrates the scheme. P and Q are two different data check algorithms.
One of the two is the exclusive-OR calculation used in RAID 4 and 5. But
the other is an independent data check algorithm. This makes it possible to regenerate
data even if two disks containing user data fail.

The advantage of RAID 6 is that it provides extremely high data availability.
Three disks would have to fail within the MTTR (mean time to repair) interval to
cause data to be lost. On the other hand, RAID 6 incurs a substantial write penalty,
because each write affects two parity blocks. Performance benchmarks [EISC07]
show a RAID 6 controller can suffer more than a 30% drop in overall write performance
compared with a RAID 5 implementation. RAID 5 and RAID 6 read
performance is comparable.

--- 


# SSD VS HDD  

SSDs have the following advantages over HDDs:

• High-performance input/output operations per second (IOPS): Significantly
increases performance I/O subsystems.

• Durability: Less susceptible to physical shock and vibration.

• Longer lifespan: SSDs are not susceptible to mechanical wear.

• Lower power consumption: SSDs use considerably less than comparable-size HDDs.

• Quieter and cooler running capabilities: Less floor space required, lower
energy costs, and a greener enterprise.

• Lower access times and latency rates: Over 10 times faster than the spinning
disks in an HDD.

Currently, HDDs enjoy a cost per bit advantage and a capacity advantage, but
these differences are shrinking.

--- 

# SSD ARCHITECTURE 

Figure 6.8 illustrates a general view of the common architectural system component
associated with any SSD system. On the host system, to operating system invokes
file system software to access data on the disk. The file system, in turn, invokes I/O
driver software. The I/O driver software provides host access to the particular SSD
product. The interface component in Figure 6.8 refers to the physical and electrical
interface between the host processor and the SSD peripheral device. If the device is
an internal hard drive, a common interface is PCIe. For external devices, one common
interface is USB.

In addition to the interface to the host system, the SSD contains the following
components:

• Controller: Provides SSD device level interfacing and firmware execution.

• Addressing: Logic that performs the selection function across the flash
memory components.

• Data buffer/cache: High speed RAM memory components used for speed
matching and to increased data throughput.

• Error correction: Logic for error detection and correction.

• Flash memory components: Individual NAND flash chips.


--- 

# Practical Issues of SSDs & HDDs

There are two practical issues peculiar to SSDs that are not faced by HDDs. First,
SDD performance has a tendency to slow down as the device is used. To understand
the reason for this, you need to know that files are stored on disk as a set of pages,
typically 4 KB in length. These pages are not necessarily, and indeed not typically,
stored as a contiguous set of pages on the disk. The reason for this arrangement is
explained in our discussion of virtual memory in Chapter 8. However, flash memory
is accessed in blocks, with a typically block size of 512 KB, so that there are typically
128 pages per block. Now consider what must be done to write a page onto a flash
memory.

1. The entire block must be read from the flash memory and placed in a RAM
buffer. Then the appropriate page in the RAM buffer is updated.

2. Before the block can be written back to flash memory, the entire block of flash
memory must be erased—it is not possible to erase just one page of the flash
memory.

3. The entire block from the buffer is now written back to the flash memory.

Now, when a flash drive is relatively empty and a new file is created, the
pages of that file are written on to the drive contiguously, so that one or only a few
blocks are affected. However, over time, because of the way virtual memory works,
files become fragmented, with pages scattered over multiple blocks. As the drive
become more occupied, there is more fragmentation, so the writing of a new file can
affect multiple blocks. Thus, the writing of multiple pages from one block becomes
slower, the more fully occupied the disk is. Manufacturers have developed a variety
of techniques to compensate for this property of flash memory, such as setting aside
a substantial portion of the SSD as extra space for write operations (called over provisioning),
then to erase inactive pages during idle time used to defragment the
disk. Another technique is the TRIM command, which allows an operating system
to inform a solid state drive (SSD) which blocks of data are no longer considered in
use and can be wiped internally.

A second practical issue with flash memory drives is that a flash memory
becomes unusable after a certain number of writes. As flash cells are stressed,
they lose their ability to record and retain values. A typical limit is 100,000 writes
[GSOE08]. Techniques for prolonging the life of an SSD drive include front-ending
the flash with a cache to delay and group write operations, using wear-leveling algorithms
that evenly distribute writes across block of cells, and sophisticated bad-block
management techniques. In addition, vendors are deploying SSDs in RAID configurations
to further reduce the probability of data loss. Most flash devices are also
capable of estimating their own remaining lifetimes so systems can anticipate failure
and take preemptive action.

--- 





</span>
