# Beyond Slides

<span style="font-size:20px;">


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

--- 

# Flash Memory 

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
