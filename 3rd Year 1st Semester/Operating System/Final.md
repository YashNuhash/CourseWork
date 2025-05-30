## 4th Batch Question Solution : 

### ✅ 1 (a) **"Operating system is a resource allocator" – Justification with Example**

---

### 🧠 **Explanation:**

An **Operating System (OS)** acts as a **resource allocator** because it manages and controls the hardware and software resources of a computer system. These resources include:

* **CPU time**
* **Memory space (RAM)**
* **Input/Output (I/O) devices**
* **Storage (disk, SSD)**
* **Network bandwidth**

Since many users and programs may compete for limited resources, the OS decides:

* **Who gets what resource**
* **For how long**
* **In what order**

The OS ensures **fairness**, **efficiency**, and **security** in this allocation.

---

### 💻 **Real-Life Example:**

Imagine a system running **three programs**:

* Program A: Needs CPU to do calculations.
* Program B: Needs to read a file from disk.
* Program C: Is downloading a file using the network.

Now consider the following roles of the OS:

| Resource     | OS Role as Allocator                                                                       |
| ------------ | ------------------------------------------------------------------------------------------ |
| **CPU**      | Schedules Program A to use the processor using a scheduling algorithm (e.g., Round Robin). |
| **Disk I/O** | Allocates disk access to Program B and queues I/O requests.                                |
| **Network**  | Manages bandwidth and socket access for Program C.                                         |
| **RAM**      | Allocates memory segments for each program so they don’t overwrite each other.             |

Without the OS coordinating this, multiple programs would **conflict** over hardware, potentially causing **crashes**, **corruption**, or **inefficiency**.

---

### 📌 Summary:

> The Operating System is called a **resource allocator** because it ensures optimal and fair distribution of limited system resources among competing tasks and users, enabling safe and efficient system operation.

---

### ✅ (2) (b) Dual-Mode Operation of Operating System

---

### 🧠 **What is Dual-Mode Operation?**

The **dual-mode operation** is a key feature of modern operating systems that helps **protect the system** from accidental or malicious damage by **separating user activities from system-level (privileged) operations**.

There are **two modes of operation**:

| Mode            | Description                                                                                                |
| --------------- | ---------------------------------------------------------------------------------------------------------- |
| **User Mode**   | Limited-access mode where user applications run. Cannot directly access hardware or critical OS functions. |
| **Kernel Mode** | Full-access mode where OS core functions (like memory management, I/O control, CPU scheduling) run.        |

---

### 🔁 **Transition Between User and Kernel Mode**

A **mode bit (1-bit flag)** in the hardware indicates the current mode:

* `0` → **Kernel mode**
* `1` → **User mode**

#### 📥 **Transition: User → Kernel Mode**

Occurs when the user program **requests a service** from the OS. This is done via a **system call**.

📌 **Example**:

```cpp
open("file.txt") → triggers a system call → OS switches to kernel mode
```

* Mode bit is set to 0
* Control is transferred to the OS via an **interrupt or system call handler**
* OS executes the requested service (like file access, memory allocation)

#### 📤 **Transition: Kernel → User Mode**

After completing the system call or handling an interrupt:

* OS sets mode bit back to 1 (user mode)
* Control returns to the user process at the next instruction

---

### 🔐 **Why Is Dual-Mode Important?**

* **Security**: Prevents users from executing harmful or critical instructions.
* **Stability**: Avoids corruption of memory or hardware misuse.
* **Controlled Access**: Only the OS can access hardware directly.

---

### 🧱 **Diagram:**

```text
+--------------------+        System Call / Interrupt         +--------------------+
|     User Mode      |  ------------------------------->      |    Kernel Mode     |
|  User Program Code |                                       |  OS Services/Drivers|
+--------------------+                                       +--------------------+
         ^                                                           |
         | <-------------------- Return to User Mode ---------------+
```

---

### 📌 Summary:

> Dual-mode operation divides execution into **user mode** (limited access) and **kernel mode** (full access). Transitions occur through **system calls** or **interrupts**, allowing the OS to safely manage system resources and protect hardware from unauthorized access.

---

To represent how each process flows through the system (CPU, I/O, Ready, etc.), we’ll draw **queuing diagrams** for each process.

Let’s first break down the behavior of each process as described:

---

### 📝 Process Characteristics Summary:

| Process    | Behavior                                                            |
| ---------- | ------------------------------------------------------------------- |
| **P1**     | Multiple I/O operations → frequently moves between CPU and I/O.     |
| **P2**     | No I/O but forks a child → includes fork system call.               |
| **P3**     | No I/O but interrupted → gets preempted due to an interrupt.        |
| **P4, P5** | Simple CPU-bound, no interruptions → completes in fixed time slice. |

---

### ✅ Queuing Diagrams:

We use the standard OS queues:

* **Ready Queue** (waiting for CPU)
* **CPU**
* **I/O Queue**
* **Blocked** (e.g., after fork or interrupt)

---

#### 🔷 **P1 – Frequent I/O Operations**

```
Ready → CPU → I/O → Ready → CPU → I/O → Ready → CPU → Terminate
```

* P1 uses CPU briefly, goes for I/O, then returns to ready queue. This repeats.

---

#### 🔷 **P2 – Forks a Child Process**

```
Ready → CPU (fork) → Blocked (child creation) → Ready → CPU → Terminate
```

* The process goes into a blocked state after fork, resumes later.

---

#### 🔷 **P3 – Interrupted During Execution**

```
Ready → CPU → Interrupted → Ready → CPU → Terminate
```

* Execution is paused due to an interrupt, goes back to ready queue, resumes later.

---

#### 🔷 **P4 – CPU-bound, No Interruptions**

```
Ready → CPU → Terminate
```

* Runs smoothly to completion within its time slice.

---

#### 🔷 **P5 – CPU-bound, No Interruptions**

```
Ready → CPU → Terminate
```

* Same as P4, no interruptions.

---

### 📊 Tabular View for Quick Comparison:

| Process | Ready → CPU | I/O | Interrupt | Fork/Blocked | Final Transition |
| ------- | ----------- | --- | --------- | ------------ | ---------------- |
| **P1**  | ✅ Repeats   | ✅   | ❌         | ❌            | CPU → Terminate  |
| **P2**  | ✅           | ❌   | ❌         | ✅ Fork       | CPU → Terminate  |
| **P3**  | ✅           | ❌   | ✅         | ❌            | CPU → Terminate  |
| **P4**  | ✅           | ❌   | ❌         | ❌            | CPU → Terminate  |
| **P5**  | ✅           | ❌   | ❌         | ❌            | CPU → Terminate  |

---

### ✅ (d) Communication Between Processes P1 and P2 in a Message Passing System

---

In a **message-passing system**, two processes like **P1** and **P2** communicate **without shared memory** by explicitly sending and receiving messages.

---

### 🔷 Ways P1 and P2 Can Communicate

There are **two major types** of message passing:

---

#### 1. **Direct Communication**

* **Processes must name each other explicitly.**

* **Example:**
  `send(P2, message)`
  `receive(P1, message)`

* **Types of communication:**

  * **Symmetric (both must name each other):**

    * `send(P2, msg)` by P1
    * `receive(P1, msg)` by P2
  * **Asymmetric (receiver doesn’t need to name sender):**

    * P1: `send(P2, msg)`
    * P2: `receive(msg)` (from anyone)

---

#### 2. **Indirect Communication (via Mailboxes/Ports)**

* **Processes communicate through a shared mailbox.**
* **Example:**

  * P1: `send(mailbox1, msg)`
  * P2: `receive(mailbox1, msg)`
* The mailbox is managed by the OS and acts as an intermediate buffer.

---

### 🔷 Message Passing Modes

1. **Synchronous (Blocking)**

   * **Sender** is blocked until the message is received.
   * **Receiver** is blocked until a message arrives.

2. **Asynchronous (Non-blocking)**

   * **Sender** continues immediately after sending.
   * **Receiver** may poll or wait later.

---

### 🔷 When Do We Get a **Rendezvous**?

A **rendezvous** occurs in **synchronous communication** when:

* **Both the sender and receiver are blocked** and **wait for each other** at the same time.
* Only when **both P1 and P2 are ready**, the message is passed, and both resume execution.

---

### ✅ Example of Rendezvous:

```text
P1                             P2
---                            ---
send(P2, msg)  <---BLOCKED     receive(P1, msg) <---BLOCKED
              ↘  rendezvous   ↙
          Message passed; both continue
```

> It ensures **tight synchronization** between the two processes.

---

### 🔚 Summary Table

| Mode       | Blocking?      | Intermediate Mailbox? | Example Use           |
| ---------- | -------------- | --------------------- | --------------------- |
| Direct     | May or may not | No                    | send/receive by name  |
| Indirect   | May or may not | Yes (Mailbox)         | send(mailbox)         |
| Rendezvous | Both blocking  | No or Yes             | Synchronous messaging |

---

### ✅ (e) Multiprogramming vs Multitasking + Process Information (with Explanation)

---

### 🔷 Multiprogramming vs Multitasking

| Feature               | **Multiprogramming**                                                                | **Multitasking**                                                                             |
| --------------------- | ----------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------- |
| **Definition**        | Allows **multiple programs** to reside in memory and **share CPU**.                 | Allows **multiple tasks (processes/threads)** to be executed **seemingly at the same time**. |
| **Focus**             | **Maximizing CPU utilization** by running another job while one is waiting for I/O. | **Providing responsiveness** and **user interactivity**.                                     |
| **Execution Type**    | Jobs take turns to use the CPU.                                                     | Context switching happens rapidly between tasks.                                             |
| **User Support**      | Usually **single-user systems**.                                                    | Usually **multi-user** and **interactive systems**.                                          |
| **Example**           | Batch processing (e.g., punch card jobs in early OS).                               | Modern OS (e.g., Windows, Linux) running browser, editor, and music player together.         |
| **Type of Switching** | Job switching (slower, based on I/O).                                               | Fast **context switching** between processes or threads.                                     |

---

### 🔷 Where Do You Get All the Information of a Process?

All process-related information is maintained by the **Operating System** in a special data structure called the **Process Control Block (PCB)**.

---

### 🔷 What is a PCB?

The **Process Control Block** is a **data structure in the OS kernel** that contains **all information about a particular process**.

---

### 🔷 Information Stored in the PCB

| Type of Information      | Description                                                                 |
| ------------------------ | --------------------------------------------------------------------------- |
| **Process ID (PID)**     | Unique identifier for the process.                                          |
| **Process State**        | Ready, Running, Waiting, etc.                                               |
| **Program Counter (PC)** | Address of the next instruction to execute.                                 |
| **CPU Registers**        | Contents of CPU registers when process is not running (for context switch). |
| **Memory Info**          | Base/limit registers, page tables, segment tables.                          |
| **Scheduling Info**      | Priority, scheduling queue pointers.                                        |
| **Accounting Info**      | CPU used, time limits, job/process number.                                  |
| **I/O Status Info**      | List of I/O devices allocated, open files, etc.                             |
| **Parent/Child Info**    | Relation to other processes (used in process trees).                        |

---

### 🔚 Summary:

* **Multiprogramming**: Multiple jobs in memory to keep the CPU busy.
* **Multitasking**: Multiple tasks running interactively and responsively.
* **PCB**: Holds **complete context and metadata** of a process (ID, state, CPU registers, memory, I/O, etc.).

---

### ✅ (2a) What is Deadlock?

A **deadlock** is a situation in an operating system where **a set of processes are blocked forever**, waiting for each other to release resources.

In simpler terms, **each process is holding a resource and waiting to acquire a resource held by another**, causing a **circular wait** and **none of them can proceed**.

---

### 🔒 Example of Deadlock:

Let’s say:

* Process **P1** holds **Resource R1** and waits for **R2**.
* Process **P2** holds **Resource R2** and waits for **R1**.
  Both processes keep waiting — **deadlock occurs**.

---

### 🔑 Necessary Conditions for Deadlock

There are **four Coffman conditions** that must all be true simultaneously for a deadlock to occur:

| No. | Condition            | Description                                                                                                    |
| --- | -------------------- | -------------------------------------------------------------------------------------------------------------- |
| 1️⃣ | **Mutual Exclusion** | At least one resource must be held in a **non-shareable mode**. Only one process can use it at a time.         |
| 2️⃣ | **Hold and Wait**    | A process is **holding at least one resource** and **waiting** to acquire additional resources held by others. |
| 3️⃣ | **No Preemption**    | Resources **cannot be forcibly removed** from the processes holding them.                                      |
| 4️⃣ | **Circular Wait**    | There exists a **circular chain** of processes, each waiting for a resource held by the next process.          |

---

### 🔁 Visual Summary:

```
P1 → R1 (held) — waiting for → R2 (held by P2)
P2 → R2 (held) — waiting for → R1 (held by P1)
```

This circular dependency, along with the above conditions, leads to **deadlock**.

---

(b) Consider the following snapshot of a system:

| Process | Allocation | Max | Available |
|---|---|---|---|
| | A B C D | A B C D | A B C D |
| P0 | 0 0 1 2 | 0 0 1 2 | 1 5 2 0 |
| P1 | 1 0 0 0 | 1 7 5 0 | |
| P2 | 1 3 5 4 | 2 3 5 6 | |
| P3 | 0 6 3 2 | 0 6 5 2 | |
| P4 | 0 0 1 4 | 0 6 5 6 | |

Answer the following questions using Banker's algorithm:
<br>
i) What is the content of "Need" matrix?
<br>
ii) Is the system in safe state?
If a request from process P1 arrives for (0, 4, 2, 0), can the request be granted immediately?

Sure! Here's a **complete and easy-to-understand** solution to your Banker's Algorithm question in **Markdown format**:

---

## 🏦 Banker's Algorithm Problem (Safe State & Request Check)

### Given:

| Process | Allocation | Max     |
| ------- | ---------- | ------- |
|         | A B C D    | A B C D |
| P0      | 0 0 1 2    | 0 0 1 2 |
| P1      | 1 0 0 0    | 1 7 5 0 |
| P2      | 1 3 5 4    | 2 3 5 6 |
| P3      | 0 6 3 2    | 0 6 5 2 |
| P4      | 0 0 1 4    | 0 6 5 6 |

### Available Resources:

```
A B C D
1 5 2 0
```

---

### ✅ i) **Need Matrix**

Formula:

```
Need = Max - Allocation  
```

| Process | Need (A B C D) |
| ------- | -------------- |
| P0      | 0 0 0 0        |
| P1      | 0 7 5 0        |
| P2      | 1 0 0 2        |
| P3      | 0 0 2 0        |
| P4      | 0 6 4 2        |

---

### ✅ ii) **Is the system in a safe state?**

We apply **Banker's Safety Algorithm**:

#### Initial Work = Available:

```
Work = [1, 5, 2, 0]  
Finish = [False, False, False, False, False]
```

---

#### 🟢 Step-by-step process:

✅ **P0** can finish (Need ≤ Work):

* Work = Work + Allocation of P0 = `[1+0, 5+0, 2+1, 0+2] = [1, 5, 3, 2]`
* Finish = `[✔, ✘, ✘, ✘, ✘]`

✅ **P2** can finish: Need `[1,0,0,2]` ≤ Work `[1,5,3,2]`

* Work = Work + Allocation of P2 = `[1+1, 5+3, 3+5, 2+4] = [2, 8, 8, 6]`
* Finish = `[✔, ✘, ✔, ✘, ✘]`

✅ **P1** can finish: Need `[0,7,5,0]` ≤ Work `[2,8,8,6]`

* Work = Work + Allocation of P1 = `[2+1, 8+0, 8+0, 6+0] = [3, 8, 8, 6]`
* Finish = `[✔, ✔, ✔, ✘, ✘]`

✅ **P3** can finish: Need `[0,0,2,0]` ≤ Work `[3,8,8,6]`

* Work = Work + Allocation of P3 = `[3+0, 8+6, 8+3, 6+2] = [3, 14, 11, 8]`
* Finish = `[✔, ✔, ✔, ✔, ✘]`

✅ **P4** can finish: Need `[0,6,4,2]` ≤ Work `[3,14,11,8]`

* Work = Work + Allocation of P4 = `[3+0, 14+0, 11+1, 8+4] = [3, 14, 12, 12]`
* Finish = `[✔, ✔, ✔, ✔, ✔]`

✅ All processes can finish → **Safe State**

---

### ✅ iii) **Can the request (0,4,2,0) from P1 be granted?**

#### Request by P1 = `[0, 4, 2, 0]`

#### Check 1: **Request ≤ Need of P1**

* So, **its Need** = Max − Allocation = `1 7 5 0 − 1 0 0 0` = `0 7 5 0`

Need of P1 = `[0, 7, 5, 0]` → ✅ Yes, request is within Need.

#### Check 2: **Request ≤ Available**

Available = `[1, 5, 2, 0]` →
Request = `[0, 4, 2, 0]` → ✅ Yes, request is within Available.

So the **request can be granted immediately**.

---

### ✅ Final Answers:

* **i) Need Matrix:** See table above.
* **ii) Safe State?** → ✅ **Yes**
* **iii) Can Request (0,4,2,0) be Granted to P1?** → ✅ **Yes**

Sure! Here's a clear explanation of **external and internal fragmentation**, along with how each can be removed, and easy examples for both.

---

## ✅ (c) How External and Internal Fragmentation Can Be Removed? With Examples

---

### 📦 What is Fragmentation?

When memory is allocated and deallocated, **free spaces get scattered**, which leads to **wasted memory**. This is called **fragmentation**, and it comes in two types:

---

## 🧩 1. Internal Fragmentation

### 🔹 What is it?

Occurs when a fixed-sized memory block is **allocated more than required**.

### 📘 Example:

Suppose we have memory blocks of **4 KB** each.

A process requests **2.5 KB** → it still gets a **4 KB block** →
➡️ **1.5 KB is wasted** inside the block.

This **unused space inside allocated memory** is called **internal fragmentation**.

### 🔧 How to Remove It?

| Method                                    | Description                                                                             |
| ----------------------------------------- | --------------------------------------------------------------------------------------- |
| ✅ Use **dynamic (variable) partitioning** | Allocate only the amount of memory that the process actually needs.                     |
| ✅ Use **paging or segmentation**          | Logical memory is divided into small chunks (pages), which helps reduce internal waste. |

---

## 🌐 2. External Fragmentation

### 🔹 What is it?

Happens when **enough total free memory exists**, but it's **not contiguous** (not side-by-side).

### 📘 Example:

Imagine this memory:

```
[2 KB Free] [3 KB Used] [4 KB Free] [5 KB Used] [2 KB Free]
```

A process needs **5 KB**, but we have:

* 2 KB + 4 KB + 2 KB = 8 KB total free memory
  ➡️ But **none of it is 5 KB in a single block**, so the process **cannot be allocated memory**.

This is called **external fragmentation** — the memory is scattered.

### 🔧 How to Remove It?

| Method                                     | Description                                                                                                                                            |
| ------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------ |
| ✅ **Compaction**                           | Move memory contents to make all free memory **contiguous** (side-by-side). <br> 🔁 Example: shift all used blocks to one side and combine free space. |
| ✅ Use **paging/segmentation**              | In paging, processes are divided into small fixed-size pages, so **no need for contiguous memory blocks**.                                             |
| ✅ Use **best-fit or worst-fit** strategies | Helps reduce leftover spaces during memory allocation.                                                                                                 |

---

## 📊 Quick Summary Table:

| Type                       | Cause                                    | Solution(s)                                            |
| -------------------------- | ---------------------------------------- | ------------------------------------------------------ |
| **Internal Fragmentation** | Fixed-size blocks waste memory inside    | Dynamic allocation, Paging, Segmentation               |
| **External Fragmentation** | Free memory is scattered, not continuous | Compaction, Paging/Segmentation, Allocation strategies |

---

### ✅ (d) What is PCB? Explain [2 Marks]

---

### 🧠 **PCB – Process Control Block**

A **Process Control Block (PCB)** is a **data structure** used by the **Operating System (OS)** to **store all information** about a **process**.

You can think of it as the **identity card or record file** for a process. Every time a process is created, the OS **creates a PCB** for it and uses it to **track and manage** the process.

---

### 🧾 **Contents of a PCB:**

| 🔢 Section                    | 📄 Description                                                                    |
| ----------------------------- | --------------------------------------------------------------------------------- |
| **1. Process ID (PID)**       | Unique ID to identify the process.                                                |
| **2. Process State**          | Current status of the process: Ready, Running, Waiting, etc.                      |
| **3. Program Counter**        | Holds the address of the **next instruction** to be executed.                     |
| **4. CPU Registers**          | Stores all CPU registers (like Accumulator, Stack Pointer) for context switching. |
| **5. Memory Management Info** | Info like page tables, memory limits, and segment tables.                         |
| **6. Accounting Info**        | Includes how much CPU time the process has used, process priority, etc.           |
| **7. I/O Status Info**        | List of I/O devices assigned to the process and files it has opened.              |

---

### 📘 **Why PCB is Important?**

* When the CPU switches from one process to another (**context switching**), it **saves the current process's PCB** and **loads the next process's PCB**.
* It helps the OS **keep track** of all running processes and manage their resources efficiently.

---

### 🧮 **Example (simplified):**

Let’s say Process P1 is paused, and Process P2 needs to run.
➡️ OS saves **P1’s current info** in its PCB.
➡️ Then loads **P2’s PCB** to continue its execution from where it left off.

---

### 📌 Summary:

> **PCB is like a folder** that stores all the important information about a process, allowing the operating system to control and manage the process properly.

---

Let's solve each scheduling algorithm step-by-step:

---

## ✅ Given:

| Process | Burst Time | Priority | Arrival Time |
| ------- | ---------- | -------- | ------------ |
| P1      | 10         | 3        | 0            |
| P2      | 1          | 1        | 1            |
| P3      | 2          | 3        | 2            |
| P4      | 1          | 4        | 3            |
| P5      | 5          | 2        | 4            |

---

# ✅ i) Gantt Charts for each scheduling algorithm

---

## 🔄 **Round Robin (Time Quantum = 3)**

### 💡 Arrival Time Considered

* RR picks from ready queue in **arrival order**.
* Each process gets **3 ms** time slice before rotating.

### ➕ Steps:

```
Time  | Action
------+-----------------------
0-3   | P1 (remaining = 7)
3-4   | P2 (done)
4-6   | P3 (done)
6-7   | P4 (done)
7-10  | P5 (remaining = 2)
10-13 | P1 (remaining = 4)
13-15 | P5 (done)
15-18 | P1 (remaining = 1)
18-19 | P1 (done)
```

### 📊 Gantt Chart:

```
| P1 | P2 | P3 | P4 | P5 | P1 | P5 | P1 | P1 |
0    3    4    6    7   10   13   15  18  19
```

---

## ⏩ **First-Come, First-Served (FCFS)**

### 🔠 Order: P1 → P2 → P3 → P4 → P5

Based on **arrival time**.

### 📊 Gantt Chart:

```
| P1 | P2 | P3 | P4 | P5 |
0   10   11   13   14   19
```

---

## 🔽 **Non-preemptive Priority** (Higher number = Higher priority)

### ✅ Order of Execution:

* Arrival based + priority:

  * P1 (3), P2 (1), P3 (3), P4 (4), P5 (2)
* At t = 0: P1
* At t = 1: P2 arrives (priority 1, lower than P1)
* At t = 2: P3 arrives (equal priority)
* At t = 3: P4 arrives (**highest**)
* At t = 4: P5 arrives

So:

* P1 starts at 0 and runs fully (non-preemptive)
* After P1 finishes (t=10), choose highest priority from ready queue → P4 (priority 4), then P3 (3), P5 (2), P2 (1)

### 📊 Gantt Chart:

```
| P1 | P4 | P3 | P5 | P2 |
0   10   11   13   18   19
```

---

# ✅ ii) Turnaround and Waiting Time Calculation

| Process | Arrival | Burst | Completion | Turnaround = C - A | Waiting = TAT - B |
| ------- | ------- | ----- | ---------- | ------------------ | ----------------- |

---

## 🔄 **Round Robin Results:**

| Process | Arrival | Burst | Completion | TAT | WT |
| ------- | ------- | ----- | ---------- | --- | -- |
| P1      | 0       | 10    | 19         | 19  | 9  |
| P2      | 1       | 1     | 4          | 3   | 2  |
| P3      | 2       | 2     | 6          | 4   | 2  |
| P4      | 3       | 1     | 7          | 4   | 3  |
| P5      | 4       | 5     | 15         | 11  | 6  |

👉 **Average TAT = (19+3+4+4+11)/5 = 8.2**
👉 **Average WT = (9+2+2+3+6)/5 = 4.4**

---

## ⏩ **FCFS Results:**

| Process | Arrival | Burst | Completion | TAT | WT |
| ------- | ------- | ----- | ---------- | --- | -- |
| P1      | 0       | 10    | 10         | 10  | 0  |
| P2      | 1       | 1     | 11         | 10  | 9  |
| P3      | 2       | 2     | 13         | 11  | 9  |
| P4      | 3       | 1     | 14         | 11  | 10 |
| P5      | 4       | 5     | 19         | 15  | 10 |

👉 **Average TAT = (10+10+11+11+15)/5 = 11.4**
👉 **Average WT = (0+9+9+10+10)/5 = 7.6**

---

## 🔽 **Non-preemptive Priority Results:**

| Process | Arrival | Burst | Completion | TAT | WT |
| ------- | ------- | ----- | ---------- | --- | -- |
| P1      | 0       | 10    | 10         | 10  | 0  |
| P4      | 3       | 1     | 11         | 8   | 7  |
| P3      | 2       | 2     | 13         | 11  | 9  |
| P5      | 4       | 5     | 18         | 14  | 9  |
| P2      | 1       | 1     | 19         | 18  | 17 |

👉 **Average TAT = (10+8+11+14+18)/5 = 12.2**
👉 **Average WT = (0+7+9+9+17)/5 = 8.4**

---

# 📌 Summary Table

| Algorithm               | Avg TAT | Avg WT |
| ----------------------- | ------- | ------ |
| Round Robin (Q=3)       | 8.2     | 4.4    |
| FCFS                    | 11.4    | 7.6    |
| Non-preemptive Priority | 12.2    | 8.4    |

---

Sure! Here's a simple and clear explanation for each part of your question:

---

## 🔄 **(b) Convoy Effect, Priority Scheduling, and Round Robin Limitation**

---

### 🛑 **Convoy Effect**

**Definition:**
The **convoy effect** occurs when a **long CPU-bound process** holds the CPU, and many **short I/O-bound processes** are stuck waiting. As a result, the overall system becomes inefficient — all other processes move slowly like a “convoy behind a slow truck.”

---

#### ✅ **Example of Convoy Effect:**

Let’s say we have 3 processes:

| Process | Type      | CPU Burst |
| ------- | --------- | --------- |
| P1      | CPU-bound | 10        |
| P2      | I/O-bound | 2         |
| P3      | I/O-bound | 2         |

In **FCFS (First Come First Serve)**:

* P1 arrives first and takes 10 units.
* P2 and P3 must **wait 10 units**, even though they only need 2 units each.

➡️ So, **short jobs get delayed**, and **CPU is underutilized** when I/O-bound processes finish fast but wait for CPU to be free.

---

### 🎯 **Solving the Convoy Effect in Priority Scheduling**

In **Priority Scheduling**, each process is given a priority. The CPU is given to the process with the **highest priority**.

#### 🔧 Problem with Priority Scheduling:

* **Starvation**: Low-priority processes might never get the CPU.

#### ✅ **Solution: Aging**

* **Aging** gradually **increases the priority** of waiting processes over time.
* This ensures **no process waits forever**.

📌 Example:

* If a low-priority process waits too long, we increase its priority.
* Eventually, it will reach a high enough priority to be scheduled.

---

### 🔄 **Does Round Robin Have Limitations?**

Yes, **Round Robin (RR)** has limitations.

#### 🔍 **Problem: Poor for Mixed Workloads**

Round Robin uses a **fixed time quantum** and switches between processes in order.

#### ❌ Limitation:

* If **quantum is too small**, too many context switches → overhead.
* If **quantum is too large**, it behaves like FCFS → longer waiting times for short jobs.

---

#### 🧪 **Example:**

| Process | Arrival | Burst |
| ------- | ------- | ----- |
| P1      | 0       | 20    |
| P2      | 1       | 3     |
| P3      | 2       | 3     |

With **Quantum = 4**:

* P1 runs for 4, then P2 for 3 (done), P3 for 3 (done), then back to P1.
* But P2 and P3 still **waited unnecessarily**.

✅ **Conclusion**:

* RR is **fair**, but not always **efficient** for real-time or short job-dominated systems.

---

### ✅ Summary

| Concept             | Problem                               | Solution                                   |
| ------------------- | ------------------------------------- | ------------------------------------------ |
| Convoy Effect       | Long process delays short ones        | Use better scheduling (e.g. SJF, Priority) |
| Priority Scheduling | Starvation of low-priority            | Use **aging**                              |
| Round Robin         | Context switch overhead or long waits | Carefully choose **time quantum**          |


---

## ✅ (d) **What is Deadlock?**

A **deadlock** is a situation in an operating system where **two or more processes are waiting for each other to release resources**, and **none of them can proceed**.

### 🔒 Example:

* **Process A** has a **printer** and wants a **scanner**.
* **Process B** has a **scanner** and wants a **printer**.
* Both are waiting for each other — and they’re **stuck forever**. That’s a **deadlock**!

---

## 🔁 **Four Conditions for Deadlock (Must Happen Together)**

| No. | Condition            | Explanation                                                                                     |
| --- | -------------------- | ----------------------------------------------------------------------------------------------- |
| 1️⃣ | **Mutual Exclusion** | Only one process can use a resource at a time.                                                  |
| 2️⃣ | **Hold and Wait**    | A process holds one resource and waits for another.                                             |
| 3️⃣ | **No Preemption**    | A resource can’t be taken back — it must be released voluntarily.                               |
| 4️⃣ | **Circular Wait**    | A group of processes are waiting in a circular chain (P1 waits for P2, P2 for P3, … Pn for P1). |

> ✅ **If even one of these conditions is broken**, deadlock can be **prevented**.

---

## 🛡️ **Deadlock Prevention (Breaking the Conditions)**

You can **prevent** deadlock by **not allowing one or more of the four conditions**:

| Method                         | How It Works                                                                                 |
| ------------------------------ | -------------------------------------------------------------------------------------------- |
| **Eliminate Mutual Exclusion** | Not possible for all resources (e.g., printers). So usually we allow this.                   |
| **Eliminate Hold and Wait**    | Make processes **request all resources at once**, and proceed only if all are available.     |
| **Allow Preemption**           | Take resources from processes forcefully (if safe to do so).                                 |
| **Avoid Circular Wait**        | Number the resources. Force processes to **request resources in a fixed order** (ascending). |

---

### ✅ (e) **What is a Resource Allocation Graph (RAG)?**

A **Resource Allocation Graph (RAG)** is a **visual tool** used in operating systems to represent the allocation of **resources to processes**. It helps in detecting the possibility of **deadlocks**.

---

### 📌 **Components of a Resource Allocation Graph:**

* **Processes**: Represented by **circles (e.g., P1, P2)**.
* **Resources**: Represented by **squares (e.g., R1, R2)**.
* **Edges**:

  * **Request edge** (→): From **process to resource** (means process is waiting for that resource).
  * **Assignment edge** (←): From **resource to process** (means resource is assigned to that process).

---

### 🧠 **How to Use It:**

* If the graph contains **no cycles**, there is **no deadlock**.
* If the graph **has a cycle**:

  * If **each resource has only one instance**, then **deadlock exists**.
  * If **resources have multiple instances**, a cycle **might** lead to a deadlock.

---

### 📊 **Example of Resource Allocation Graph:**

Imagine:

* **P1** is using **R1**
* **P2** is waiting for **R1**

```
   R1
  ↙   ↘
P1     P2
```

**Explanation**:

* R1 → P1 (assignment edge): R1 is assigned to P1
* P2 → R1 (request edge): P2 is requesting R1

➡️ In this case, there’s no cycle → **No deadlock**.

---

### 🪤 **Example with Deadlock (Cycle):**

* **P1** is holding **R1** and requesting **R2**
* **P2** is holding **R2** and requesting **R1**

```
P1 → R2 → P2 → R1 → P1
```

➡️ This is a **cycle** → **Deadlock exists**.

---


## ✅ Given:

* **Processes**: P0, P1, P2, P3, P4
* **Resources**: A = 10, B = 5, C = 7
* **Available**: A = 3, B = 3, C = 2

---

### 🔹 Step 1: **Construct the Allocation and Max Tables**

| Process | Allocation (A B C) | Max (A B C) | Need = Max - Allocation |
| ------- | ------------------ | ----------- | ----------------------- |
| P0      | 0 1 0              | 7 5 3       | 7 4 3                   |
| P1      | 2 0 0              | 3 2 2       | 1 2 2                   |
| P2      | 3 0 2              | 9 0 2       | 6 0 0                   |
| P3      | 2 1 1              | 2 2 2       | 0 1 1                   |
| P4      | 0 0 2              | 4 3 3       | 4 3 1                   |

---

## ✅ Part i) Is the system in **safe state**?

### 🔹 Step 2: **Available Resources**

* Initially: A = 3, B = 3, C = 2

We’ll check if all processes can finish one by one.

### 🔸 Try P1:

* **Need = (1 2 2)** ≤ Available (3 3 2) ✅
* → P1 can finish.
* Release its resources: (2 0 0)
* New Available: (3+2, 3+0, 2+0) = **(5 3 2)**

---

### 🔸 Try P3:

* Need = (0 1 1) ≤ (5 3 2) ✅
* → P3 can finish.
* Release: (2 1 1)
* Available = (5+2, 3+1, 2+1) = **(7 4 3)**

---

### 🔸 Try P0:

* Need = (7 4 3) ≤ (7 4 3) ✅
* → P0 can finish
* Release: (0 1 0)
* Available = (7, 5, 3)

---

### 🔸 Try P2:

* Need = (6 0 0) ≤ (7 5 3) ✅
* → P2 can finish
* Release: (3 0 2)
* Available = (10, 5, 5)

---

### 🔸 Try P4:

* Need = (4 3 1) ≤ (10 5 5) ✅
* → P4 can finish
* Release: (0 0 2)
* Available = (10, 5, 7)

---

### ✅ **Safe Sequence**:

```
P1 → P3 → P0 → P2 → P4
```

### ✔️ System is in a **Safe State**

---

## ✅ Part ii) Can **P0 request (0, 2, 0)**?

### P0’s current **Need** = (7 4 3)

So,

* Request (0, 2, 0) ≤ Need (7 4 3) ✅
* Request (0, 2, 0) ≤ Available (3, 3, 2) ✅

**Grant the request**:

* P0’s new Allocation: (0 1+2 0) → (0 3 0)
* P0’s new Need: (7 4-2 3) → (7 2 3)
* Available becomes: (3 3-2 2) → **(3 1 2)**

Now recheck **safe state** with updated state:

---

### New Available: (3 1 2)

### 🔸 Try P3:

* Need = (0 1 1) ≤ (3 1 2) ✅
* Finish → Release (2 1 1)
* New Available = (5 2 3)

---

### 🔸 Try P1:

* Need = (1 2 2) ≤ (5 2 3) ✅
* Finish → Release (2 0 0)
* New Available = (7 2 3)

---

### 🔸 Try P0:

* New Need = (7 2 3) ≤ (7 2 3) ✅
* Finish → Release (0 3 0)
* Available = (7 5 3)

---

### 🔸 Try P2:

* Need = (6 0 0) ≤ (7 5 3) ✅
* Finish → Release (3 0 2)
* Available = (10 5 5)

---

### 🔸 Try P4:

* Need = (4 3 1) ≤ (10 5 5) ✅
* Finish → Release (0 0 2)
* Final Available = (10 5 7)

---

✅ **Safe Sequence** after P0’s request:
**P3 → P1 → P0 → P2 → P4**

✔️ **Request by P0 for (0,2,0)** **can be granted.**

---

## ✅ Part iii) Can **P1 request (3,3,0)**?

* P1’s current **Need** = (1 2 2)
* Requested = (3,3,0) ❌

> This **exceeds its declared maximum**:

* Request (3 3 0) > Need (1 2 2) ❌

---

### ❌ **Request denied** — It **exceeds Max**.

---

## ✅ Final Answers:

| Question                 | Answer                                          |
| ------------------------ | ----------------------------------------------- |
| Is system in safe state? | ✅ Yes                                           |
| Safe Sequence            | `P1 → P3 → P0 → P2 → P4`                        |
| Can P0 request (0,2,0)?  | ✅ Yes — Safe sequence: `P3 → P1 → P0 → P2 → P4` |
| Can P1 request (3,3,0)?  | ❌ No — Request exceeds maximum                  |


---

![alt text](image.png) 


---

### 🔍 **Legend:**

* **Processes**: Circles (`P1`, `P2`, ..., `P5`)
* **Resources**: Squares (`R1`, `R2`, ..., `R4`)
* **Edges**:

  * Arrow from **process → resource**: **Request**
  * Arrow from **resource → process**: **Allocation**

---

### 🧠 Step-by-step Analysis:

#### 🔸 **List of Dependencies** (follow arrows):

1. **P1 → R1**
   → P1 **is requesting R1**

2. **R1 → P4**
   → R1 **is allocated to P4**

3. **P4 → R2**
   → P4 **is requesting R2**

4. **R2 → P1**
   → R2 **is allocated to P1**

➡️ **Cycle detected**:

```
P1 → R1 → P4 → R2 → P1
```

✅ **This is a circular wait**, meaning **P1, P4** are involved in a **deadlock**.

---

#### 🔸 Continue Checking Other Parts:

5. **P2 → R3**
   → P2 is requesting R3

6. **R3 → P2**
   → R3 is allocated to P2
   ✅ No cycle here

7. **P3 → R4**
   → P3 is requesting R4

8. **R4 → P2**
   → R4 is allocated to P2
   ✅ No cycle here either (R4 → P2 already holding, but no cycle with P3 unless P2 requests something else, which it doesn’t)

---

### ✅ **Final Conclusion**:

Yes, **deadlock exists**, involving:

```
P1 ↔ P4 ↔ R1 ↔ R2
```

---

### 🔒 **Deadlocked Processes**:

* **P1**
* **P4**

---



### (E) 🔒 What is an **Unsafe State**?

An **unsafe state** in operating systems refers to a situation where the **system does not have enough available resources** to safely guarantee that **all processes can complete**, even if **no deadlock has happened yet**.

> ⚠️ **Unsafe ≠ Deadlock**, but unsafe **can lead** to deadlock if further resource requests occur.

---

### ✅ Key Idea:

* In a **safe state**, the system can find a **sequence** (called **safe sequence**) where **all processes can finish** without getting stuck.
* In an **unsafe state**, **no such sequence exists**, and if processes continue requesting resources, a **deadlock may occur**.

---

### 🧠 Example:

Assume:

* **3 processes**: P1, P2, P3
* **10 total resources**
* Allocation & Max needs:

| Process | Allocated | Max |
| ------- | --------- | --- |
| P1      | 3         | 7   |
| P2      | 2         | 4   |
| P3      | 3         | 6   |

* **Available = 2**

#### 🔍 Let's try to find a safe sequence:

1. Check if any process can finish with `Available = 2`:

   * P1 needs `7 - 3 = 4` → ❌ can't finish
   * P2 needs `4 - 2 = 2` → ✅ can finish

2. If P2 finishes, it frees 2 more → Available = 4
   Now:

   * P1 needs 4 → ✅
   * P3 needs 3 → ✅
     ⏱️ Safe Sequence: `P2 → P1 → P3` ✅

> So, in this case, the system is **safe**.

---

Now suppose **Available = 1**.

1. Check again:

   * P1 needs 4 → ❌
   * P2 needs 2 → ❌
   * P3 needs 3 → ❌

> 😨 No process can complete → **Unsafe State**

Still **no deadlock yet**, but the system is **at risk** of one occurring.

---

### ✅ Summary

| Safe State                             | Unsafe State                | Deadlock                          |
| -------------------------------------- | --------------------------- | --------------------------------- |
| All processes can finish in some order | No guaranteed safe sequence | Processes are permanently blocked |
| Deadlock is impossible                 | Deadlock **might** occur    | Deadlock **has already** occurred |

---

Let me know if you want a visual diagram to understand unsafe states too!



---

## Chapter 5

---

### 🧠 Question 5.1:

**"A CPU-scheduling algorithm determines an order for the execution of its scheduled processes. Given `n` processes to be scheduled on one processor, how many different schedules are possible? Give a formula in terms of `n`."**

---

### ✅ **Answer:**

When we have `n` processes and want to schedule them **one after another** on a **single processor**, we are simply trying to find out how many **different sequences** (or permutations) we can arrange those `n` processes in.

---

### 🔢 **Formula:**

The number of different schedules (permutations) for `n` processes is:

$$
\boxed{n! \quad \text{(n factorial)}}
$$

---

### 🔍 **Explanation:**

* `n!` (read as "n factorial") means:

$$
n \times (n - 1) \times (n - 2) \times \dots \times 1
$$

* Each position in the schedule can be filled by a different process, and the order **matters** because scheduling **P1 → P2** is not the same as **P2 → P1**.

---

### 📘 **Example:**

If there are 3 processes: P1, P2, and P3

$$
\text{Number of schedules} = 3! = 3 × 2 × 1 = 6
$$

These possible schedules are:

1. P1 → P2 → P3
2. P1 → P3 → P2
3. P2 → P1 → P3
4. P2 → P3 → P1
5. P3 → P1 → P2
6. P3 → P2 → P1

---

### 📌 **Conclusion:**

If `n` processes are scheduled on one processor, the total number of different execution orders is:

$$
\boxed{n!}
$$

This formula helps us understand the complexity and variety of scheduling possibilities in an operating system.

---

### 🧠 Question 5.2:

**"Explain the difference between preemptive and non-preemptive scheduling."**

---

### ✅ **Answer:**

In CPU scheduling, **preemptive** and **non-preemptive** scheduling are two ways an operating system manages how processes get CPU time.

---

### 🔄 **1. Preemptive Scheduling**

* In **preemptive scheduling**, the CPU **can be taken away** from a process **even if it has not finished**.
* The operating system can **interrupt** a running process and give the CPU to another process that has higher priority or is ready to run.
* This approach is **more responsive** and suitable for **multitasking**.

#### 📌 Example:

Suppose Process P1 is running, and a higher-priority Process P2 arrives.
In **preemptive scheduling**, the OS will pause P1 and give the CPU to P2.

#### ✅ Examples of Preemptive Scheduling Algorithms:

* Round Robin (RR)
* Shortest Remaining Time First (SRTF)
* Priority Scheduling (Preemptive version)

---

### ⏳ **2. Non-Preemptive Scheduling**

* In **non-preemptive scheduling**, once a process starts executing, it **runs until it finishes or waits** (like for I/O).
* The CPU **cannot be taken** away until the process **voluntarily gives it up**.
* This method is simpler but may cause **longer waiting times** for some processes.

#### 📌 Example:

If Process P1 is running, and Process P2 (even if it's high priority) comes in,
P1 will continue until it finishes. Only then P2 can start.

#### ✅ Examples of Non-Preemptive Scheduling Algorithms:

* First-Come, First-Served (FCFS)
* Shortest Job First (SJF)
* Priority Scheduling (Non-preemptive version)

---

### 📊 **Comparison Table:**

| Feature              | Preemptive Scheduling | Non-Preemptive Scheduling   |
| -------------------- | --------------------- | --------------------------- |
| CPU taken during run | Yes (by force)        | No (process finishes first) |
| Responsiveness       | High                  | Low                         |
| Complexity           | More complex          | Simple                      |
| Risk of starvation   | Higher                | Lower                       |
| Multitasking support | Good                  | Not ideal                   |

---

### 📌 **Conclusion:**

* Use **preemptive scheduling** when you want better responsiveness and multitasking (like in modern OS).
* Use **non-preemptive scheduling** for simpler systems where context switching overhead must be minimized.

Absolutely! Here's the extended answer in **Markdown format** with **real OS-level examples** of both **Preemptive** and **Non-Preemptive** Scheduling:


---

# 🧠 **Real Case Example**


## 🌀 Preemptive Scheduling — **Real OS Examples**

### 📱 1. **Android OS (Linux Kernel)**

* **Scenario:** While you're downloading a file, you receive a phone call.
* **What Happens:** The OS **interrupts** the background downloading process and gives CPU control to the phone app.
* **Why:** Because handling a phone call is **time-sensitive**, the OS uses **preemptive scheduling** to respond quickly.

---

### 💻 2. **Windows OS**

* **Scenario:** You’re typing in MS Word while a software update is happening in the background.
* **What Happens:** Windows **preempts** the update process to give the CPU to MS Word because you’re actively interacting with it.
* **Why:** Interactive applications get priority, thanks to **preemptive multitasking**.

---

### 💽 3. **Unix/Linux OS**

* Uses **Round Robin** and **priority-based preemptive** scheduling.
* If a higher-priority process becomes ready, the current process is **preempted** even in the middle of its execution.

---

## 🧘 Non-Preemptive Scheduling — **Real OS Examples**

### 🖥️ 1. **Older versions of MS-DOS**

* **Scenario:** You run a program like a game or a file copier.
* **What Happens:** The program uses the CPU **until it finishes or waits** (e.g., for input).
* **Why:** MS-DOS uses **non-preemptive scheduling**, meaning it does not forcibly interrupt the CPU from running processes.

---

### 🧩 2. **Early Windows 3.x Systems**

* These used **cooperative multitasking**, where:

  * A running process had to **voluntarily yield** the CPU.
  * If a process **crashed** or **did not release** the CPU, the whole system could freeze.
* This is a **form of non-preemptive scheduling**.

---

### ⚙️ 3. **Embedded Systems**

* Many embedded systems (like washing machines or small IoT devices) use **non-preemptive scheduling**.
* Tasks run to completion to keep the system **simple and predictable**.

---

### 📊 Summary Table:

| Type           | Real OS Example                       | Behavior                                   |
| -------------- | ------------------------------------- | ------------------------------------------ |
| Preemptive     | Linux, Windows, Android               | CPU can be taken away mid-task for another |
| Non-Preemptive | MS-DOS, Windows 3.x, Embedded Systems | CPU runs task till it finishes or waits    |

---

### 📌 Conclusion:

* **Modern operating systems** like Linux, Windows, and Android use **preemptive scheduling** for better performance and user experience.
* **Older systems** or **simple embedded systems** often use **non-preemptive scheduling** to keep things straightforward and predictable.

---

Here’s the full answer to your question **in Markdown format**, with **easy step-by-step explanations** for all three parts (a, b, and c):

---

### 🧠 Question 5.3:

You are given 3 processes with their arrival and burst times:

| Process | Arrival Time | Burst Time |
| ------- | ------------ | ---------- |
| P1      | 0.0          | 8          |
| P2      | 0.4          | 4          |
| P3      | 1.0          | 1          |

Use **non-preemptive scheduling** to answer the following:

---

### 🧮 **a. FCFS (First Come First Serve) Scheduling**

> FCFS runs processes in the order they arrive.

#### 📋 Process Execution Order:

* P1 (arrives at 0.0)
* P2 (arrives at 0.4)
* P3 (arrives at 1.0)

#### ⏱️ Gantt Chart:

```
| P1 |      P2     | P3 |
0    8             12   13
```

#### 🧾 Turnaround Time Formula:

$$
\text{Turnaround Time} = \text{Completion Time} - \text{Arrival Time}
$$

| Process | Arrival | Burst | Completion | Turnaround      |
| ------- | ------- | ----- | ---------- | --------------- |
| P1      | 0.0     | 8     | 8          | 8 - 0 = 8       |
| P2      | 0.4     | 4     | 12         | 12 - 0.4 = 11.6 |
| P3      | 1.0     | 1     | 13         | 13 - 1 = 12     |

#### 🧮 **Average Turnaround Time:**

$$
\frac{8 + 11.6 + 12}{3} = \boxed{10.53 \text{ units (approx)}}
$$

---

### 🧮 **b. SJF (Shortest Job First) Non-Preemptive Scheduling**

> Always pick the **shortest job** that has **arrived so far**.

#### 🧭 Step-by-Step:

* At **time 0**, only **P1** has arrived → Start **P1** (burst 8).
* At **time 8**, both **P2** and **P3** have arrived. Pick the shorter burst → **P3** (burst 1).
* After P3 → Run **P2**.

#### ⏱️ Gantt Chart:

```
| P1 |    P3   |     P2     |
0    8         9            13
```

| Process | Arrival | Burst | Completion | Turnaround      |
| ------- | ------- | ----- | ---------- | --------------- |
| P1      | 0.0     | 8     | 8          | 8 - 0 = 8       |
| P2      | 0.4     | 4     | 13         | 13 - 0.4 = 12.6 |
| P3      | 1.0     | 1     | 9          | 9 - 1 = 8       |

#### 🧮 **Average Turnaround Time:**

$$
\frac{8 + 12.6 + 8}{3} = \boxed{9.53 \text{ units (approx)}}
$$

---

### 🧮 **c. "Future-Knowledge SJF" (CPU idle for 1 unit, then use SJF)**

> We wait **1 unit** so that all 3 processes have arrived, and then apply SJF.

#### 🧭 Process Order After Waiting:

* After waiting till **t = 1.0**, all processes have arrived:

  * P3 (1 unit)
  * P2 (4 units)
  * P1 (8 units)

→ Use **SJF order**: P3 → P2 → P1

#### ⏱️ Gantt Chart:

```
Idle |  P3  |   P2   |     P1     |
0    1      2        6            14
```

| Process | Arrival | Burst | Completion | Turnaround    |
| ------- | ------- | ----- | ---------- | ------------- |
| P1      | 0.0     | 8     | 14         | 14 - 0.0 = 14 |
| P2      | 0.4     | 4     | 6          | 6 - 0.4 = 5.6 |
| P3      | 1.0     | 1     | 2          | 2 - 1.0 = 1   |

#### 🧮 **Average Turnaround Time:**

$$
\frac{14 + 5.6 + 1}{3} = \boxed{6.87 \text{ units (approx)}}
$$

---

### 📌 **Conclusion Table:**

| Scheduling Method            | Average Turnaround Time |
| ---------------------------- | ----------------------- |
| FCFS                         | 10.53 units             |
| SJF (Normal, Non-Preemptive) | 9.53 units              |
| Future-Knowledge SJF         | 6.87 units              |

✅ As you can see, **future-knowledge SJF** gives the **best average turnaround time**, but in real-world scenarios, **we don’t usually know future arrivals**.

---


### 🧠 Question 5.4

You're given 5 processes with the following details:

| Process | Burst Time | Priority |
| ------- | ---------- | -------- |
| P1      | 2 ms       | 2        |
| P2      | 1 ms       | 1        |
| P3      | 8 ms       | 4        |
| P4      | 4 ms       | 2        |
| P5      | 5 ms       | 3        |

> All processes arrive at **time = 0**
> Higher **priority number = higher priority**

---

## 🔹 (a) Gantt Charts for Each Scheduling Algorithm

---

### 1. **First-Come, First-Served (FCFS)**

Order: P1 → P2 → P3 → P4 → P5

```
| P1 | P2 |     P3     |   P4   |   P5   |
0    2    3           11       15       20
```

---

### 2. **Shortest Job First (SJF) — Non-Preemptive**

Order: P2 (1) → P1 (2) → P4 (4) → P5 (5) → P3 (8)

```
| P2 | P1 |   P4   |   P5   |      P3      |
0    1    3       7       12            20
```

---

### 3. **Non-Preemptive Priority Scheduling**

> Higher number = higher priority
> Order: P3 (4) → P5 (3) → P1 (2) → P4 (2) → P2 (1)
> P1 and P4 have same priority → tie-breaker by arrival order.

```
|     P3     |   P5   | P1 |  P4  | P2 |
0           8       13   15   19   20
```

---

### 4. **Round Robin (RR), Quantum = 2**

We'll rotate each process in the order they arrived with 2ms time slices.

**Step-by-step Execution:**

* P1 (2) → done
* P2 (1) → done
* P3 (8-2=6)
* P4 (4-2=2)
* P5 (5-2=3)
* P3 (6-2=4)
* P4 (2) → done
* P5 (3-2=1)
* P3 (4-2=2)
* P5 (1) → done
* P3 (2) → done

```
| P1 | P2 | P3 | P4 | P5 | P3 | P4 | P5 | P3 | P5 | P3 |
0    2    3    5    7    9   11   13   14   16   17   19
```

---

## 🔹 (b) Turnaround Time for Each Algorithm

> **Turnaround Time = Completion Time - Arrival Time**

### 🔸 FCFS

| Process | Completion | Turnaround |
| ------- | ---------- | ---------- |
| P1      | 2          | 2          |
| P2      | 3          | 3          |
| P3      | 11         | 11         |
| P4      | 15         | 15         |
| P5      | 20         | 20         |

**Average Turnaround Time (FCFS):**

$$
\frac{2 + 3 + 11 + 15 + 20}{5} = \boxed{10.2 \text{ ms}}
$$

---

### 🔸 SJF

| Process | Completion | Turnaround |
| ------- | ---------- | ---------- |
| P2      | 1          | 1          |
| P1      | 3          | 3          |
| P4      | 7          | 7          |
| P5      | 12         | 12         |
| P3      | 20         | 20         |

**Average Turnaround Time (SJF):**

$$
\frac{1 + 3 + 7 + 12 + 20}{5} = \boxed{8.6 \text{ ms}}
$$

---

### 🔸 Priority Scheduling

| Process | Completion | Turnaround |
| ------- | ---------- | ---------- |
| P3      | 8          | 8          |
| P5      | 13         | 13         |
| P1      | 15         | 15         |
| P4      | 19         | 19         |
| P2      | 20         | 20         |

**Average Turnaround Time (Priority):**

$$
\frac{8 + 13 + 15 + 19 + 20}{5} = \boxed{15.0 \text{ ms}}
$$

---

### 🔸 Round Robin (Quantum = 2)

| Process | Completion | Turnaround |
| ------- | ---------- | ---------- |
| P1      | 2          | 2          |
| P2      | 3          | 3          |
| P3      | 19         | 19         |
| P4      | 11         | 11         |
| P5      | 17         | 17         |

**Average Turnaround Time (RR):**

$$
\frac{2 + 3 + 19 + 11 + 17}{5} = \boxed{10.4 \text{ ms}}
$$

---

## 🔹 (c) Waiting Time for Each Algorithm

> **Waiting Time = Turnaround Time - Burst Time**

---

### 🔸 FCFS

| Process | Turnaround | Burst | Waiting |
| ------- | ---------- | ----- | ------- |
| P1      | 2          | 2     | 0       |
| P2      | 3          | 1     | 2       |
| P3      | 11         | 8     | 3       |
| P4      | 15         | 4     | 11      |
| P5      | 20         | 5     | 15      |

**Average Waiting Time (FCFS):**

$$
\frac{0 + 2 + 3 + 11 + 15}{5} = \boxed{6.2 \text{ ms}}
$$

---

### 🔸 SJF

| Process | Turnaround | Burst | Waiting |
| ------- | ---------- | ----- | ------- |
| P2      | 1          | 1     | 0       |
| P1      | 3          | 2     | 1       |
| P4      | 7          | 4     | 3       |
| P5      | 12         | 5     | 7       |
| P3      | 20         | 8     | 12      |

**Average Waiting Time (SJF):**

$$
\frac{0 + 1 + 3 + 7 + 12}{5} = \boxed{4.6 \text{ ms}}
$$

---

### 🔸 Priority Scheduling

| Process | Turnaround | Burst | Waiting |
| ------- | ---------- | ----- | ------- |
| P3      | 8          | 8     | 0       |
| P5      | 13         | 5     | 8       |
| P1      | 15         | 2     | 13      |
| P4      | 19         | 4     | 15      |
| P2      | 20         | 1     | 19      |

**Average Waiting Time (Priority):**

$$
\frac{0 + 8 + 13 + 15 + 19}{5} = \boxed{11.0 \text{ ms}}
$$

---

### 🔸 Round Robin (Quantum = 2)

| Process | Turnaround | Burst | Waiting |
| ------- | ---------- | ----- | ------- |
| P1      | 2          | 2     | 0       |
| P2      | 3          | 1     | 2       |
| P3      | 19         | 8     | 11      |
| P4      | 11         | 4     | 7       |
| P5      | 17         | 5     | 12      |

**Average Waiting Time (RR):**

$$
\frac{0 + 2 + 11 + 7 + 12}{5} = \boxed{6.4 \text{ ms}}
$$

---

## 🔹 (d) Which Algorithm Has Minimum Average Waiting Time?

| Algorithm   | Avg Waiting Time |
| ----------- | ---------------- |
| FCFS        | 6.2 ms           |
| SJF         | **4.6 ms** ✅     |
| Priority    | 11.0 ms          |
| Round Robin | 6.4 ms           |

---

### ✅ **Conclusion:**

* The **Shortest Job First (SJF)** algorithm provides the **minimum average waiting time** among all.
* However, **SJF requires knowledge of future burst times**, which is not always possible in real-time systems.

---


## 🧠 Question 5.5: Priority-based Preemptive Round Robin (Quantum = 10)

| Process | Priority | Burst Time | Arrival Time |
| ------- | -------- | ---------- | ------------ |
| P1      | 40       | 20         | 0            |
| P2      | 30       | 25         | 25           |
| P3      | 30       | 25         | 30           |
| P4      | 35       | 15         | 60           |
| P5      | 5        | 10         | 100          |
| P6      | 10       | 10         | 105          |

* **Time Quantum:** 10 units
* **Preemption allowed by higher-priority processes**
* **Idle process (`Pidle`) is used when no other process is available (priority = 0)**

---

## 🔹 (a) Gantt Chart — Execution Order with Time Segments

Let’s simulate time step-by-step:

### 🕒 Time 0 to 100 (before P5 & P6 arrive):

* **Time 0:** Only P1 is present → executes
* **Time 0–10:** `P1` runs (remaining = 10)
* **Time 10–20:** `P1` continues (done at 20)
* **Time 20–25:** No new process → `Pidle`
* **Time 25:** `P2` arrives → runs
* **Time 25–30:** `P2` runs
* **Time 30:** `P3` arrives (same priority as `P2`)
  → RR continues with `P2`
* **Time 30–35:** `P2` continues (remaining = 5)
* **Time 35–45:** `P3` runs
* **Time 45–55:** `P3` continues (remaining = 5)
* **Time 55–60:** `P2` finishes its 5ms
* **Time 60:** `P4` arrives (priority 35 > P3) → P4 preempts
* **Time 60–70:** `P4` runs (10)
* **Time 70–75:** `P4` runs (5 more → done)
* **Time 75–80:** `P3` completes remaining 5ms

### 🕒 Time 80–100 (waiting for P5 & P6):

* **Time 80–100:** `Pidle` (no processes yet)

### 🕒 Time 100–120:

* **Time 100:** P5 arrives
* **Time 105:** P6 arrives (priority > P5)
* **Time 105–115:** `P6` runs → done
* **Time 115–125:** `P5` runs → done

---


### ✅ Final Gantt Chart (Tabular Format)

| Start Time | End Time | Executing Process |
| ---------- | -------- | ----------------- |
| 0          | 10       | P1                |
| 10         | 20       | P1                |
| 20         | 25       | Pidle             |
| 25         | 30       | P2                |
| 30         | 35       | P2                |
| 35         | 45       | P3                |
| 45         | 55       | P3                |
| 55         | 60       | P2                |
| 60         | 70       | P4                |
| 70         | 75       | P4                |
| 75         | 80       | P3                |
| 80         | 100      | Pidle             |
| 100        | 105      | P5 (waiting)      |
| 105        | 115      | P6                |
| 115        | 125      | P5                |

---


## 🔹 (b) Turnaround Time

> **Turnaround Time = Completion Time - Arrival Time**

| Process | Arrival | Completion | Turnaround Time |
| ------- | ------- | ---------- | --------------- |
| P1      | 0       | 20         | 20              |
| P2      | 25      | 60         | 35              |
| P3      | 30      | 75         | 45              |
| P4      | 60      | 75         | 15              |
| P5      | 100     | 125        | 25              |
| P6      | 105     | 115        | 10              |

---

## 🔹 (c) Waiting Time

> **Waiting Time = Turnaround Time - Burst Time**

| Process | Turnaround | Burst | Waiting Time |
| ------- | ---------- | ----- | ------------ |
| P1      | 20         | 20    | 0            |
| P2      | 35         | 25    | 10           |
| P3      | 45         | 25    | 20           |
| P4      | 15         | 15    | 0            |
| P5      | 25         | 10    | 15           |
| P6      | 10         | 10    | 0            |

---

## 🔹 (d) CPU Utilization

> **CPU Utilization = Time CPU was busy / Total Time × 100%**

* **Total Time:** From time 0 to 125 → 125 units
* **Idle Time:** 20–25 (5 units), 80–100 (20 units) → 25 units
* **Busy Time = 125 - 25 = 100 units**

$$
\text{CPU Utilization} = \frac{100}{125} \times 100 = \boxed{80\%}
$$

---

### ✅ Summary:

| Metric             | Value   |
| ------------------ | ------- |
| Average Turnaround | 25.0 ms |
| Average Waiting    | 7.5 ms  |
| CPU Utilization    | **80%** |

---


### 🔹 5.6 What advantage is there in having different time-quantum sizes at different levels of a multilevel queueing system?

#### ✅ Answer:

In a **Multilevel Queue Scheduling system**, processes are divided into multiple queues based on their **type or priority**. Each queue can have its **own scheduling algorithm** and **time-quantum size**.

#### 🔍 **Advantage of Having Different Time-Quantum Sizes:**

The main advantage is that it allows the system to:

* **Optimize response time** for interactive (shorter) tasks.
* **Provide fair CPU usage** for background or long-running tasks.

---

### 📊 Example Table:

| Queue Level | Type of Processes      | Time Quantum        | Benefit                            |
| ----------- | ---------------------- | ------------------- | ---------------------------------- |
| Level 1     | Interactive/Foreground | Small (e.g., 5ms)   | Faster response, less waiting time |
| Level 2     | System/Medium jobs     | Medium (e.g., 15ms) | Balanced performance               |
| Level 3     | Background/Batch jobs  | Large (e.g., 50ms)  | Fewer context switches, efficiency |

---

### 🎯 Summary:

Using **smaller time-quantum** for higher-priority queues gives **better responsiveness** for interactive tasks.
Using **larger time-quantum** for lower-priority queues reduces the **overhead of context switching** for long-running jobs.

Thus, **different time-quantums at each level** help balance **efficiency**, **responsiveness**, and **fairness** in the system.

---





