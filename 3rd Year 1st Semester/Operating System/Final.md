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





