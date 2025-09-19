## 3. Digital & Analog Techniques 

### 3.1 [Read This First : line coding schemes: NRZ, RZ, Manchester,Differential Manchester, AMI. ](https://www.geeksforgeeks.org/digital-logic/difference-between-unipolar-polar-and-bipolar-line-coding-schemes/)


In data communication, both data and the signals that represent it can be either **digital or analog**. **Line coding** is the process of converting **digital data into digital signals**. This technique transforms a sequence of bits into a digital signal that can be transmitted over a communication channel. The process is a two-way street: at the sender's end, digital data is **encoded** into a digital signal; at the receiver's end, the digital data is **recreated by decoding** the incoming digital signal.

***

### **Categories of Line Coding Schemes**

Line coding schemes can be broadly categorized into five main types:

* **Unipolar**: Signals are either entirely above or entirely below the horizontal axis (e.g., Non-Return-to-Zero or NRZ).
* **Polar**: Signals use both positive and negative voltage levels (e.g., NRZ-L, NRZ-I, Return-to-Zero or RZ, and Biphase schemes like Manchester and Differential Manchester).
* **Bipolar**: Signals use three voltage levels—positive, negative, and zero—with the zero level often representing a specific bit and the positive and negative levels alternating for another bit (e.g., Alternate Mark Inversion or AMI and Pseudoternary).
* **Multilevel**: These schemes use more than two voltage levels to represent more than one bit per signal element.
* **Multitransition**: These schemes use transitions to represent data.

***

### **Key Characteristics of Line Coding Techniques**

Before diving into the differences between these schemes, it's crucial to understand the characteristics that make a good line coding technique:

* **Self-synchronization**: The receiver and sender clocks must be synchronized to correctly interpret the bit stream.
* **Error-detecting capability**: The scheme should have a built-in ability to detect errors in the received signal.
* **Immunity to noise and interference**: A robust scheme is resistant to noise and external interference.
* **Low complexity**: The encoding and decoding processes should be simple and easy to implement.
* **No low-frequency component (DC-component)**: Low-frequency signals cannot be transmitted over long distances, so the ideal scheme should have a zero average voltage.
* **Less baseline wandering**: The average voltage of the signal should not drift over time.

***


#### **Non-Return-to-Zero (NRZ)**

**Non-Return-to-Zero (NRZ)** is a unipolar line coding scheme where a positive voltage represents a bit `1` and a zero voltage represents a bit `0`. The signal level does not return to zero in the middle of a bit interval, which is why it's called NRZ. This can lead to issues with synchronization and baseline wandering, especially with long strings of `1`s or `0`s.

          
  **For example: For Data =10110**

  ![alt text](image-2.png)

But this scheme uses more power as compared to polar scheme to send one bit per unit line resistance. Moreover for continuous set of zeros or ones there will be self-synchronization and base line wandering problem.

---

#### **Return to Zero (RZ)**

![alt text](image-3.png)

**Return to Zero (RZ)** is a line coding scheme that addresses the synchronization problems of NRZ by having the signal return to a zero voltage level in the middle of each bit. This creates a transition that the receiver can use for synchronization. In a common RZ variant, a positive voltage (+V) is used for the first half of a bit `1` and a negative voltage (-V) for the first half of a bit `0`, with both returning to zero for the second half of the bit.


The main **disadvantage** of RZ is that it requires a greater bandwidth compared to NRZ because it uses a transition in every bit. It is also more complex due to its three voltage levels. For these reasons, it has been largely replaced by more efficient schemes like Manchester.

---

#### **Biphase (Manchester and Differential Manchester)**

![alt text](image-4.png)

The **Biphase** family of schemes solves the issues of RZ while maintaining its benefits.

* **Manchester Encoding**: This scheme combines aspects of RZ and NRZ-L. The bit duration is divided into two halves. The voltage level remains constant during the first half and transitions to the opposite level in the second half. This mid-bit transition provides a reliable synchronization mechanism. In one common convention, a transition from low to high (`-V` to `+V`) represents a bit `1`, and a high-to-low (`+V` to `-V`) transition represents a bit `0`. 

* **Differential Manchester Encoding**: This scheme combines elements of RZ and NRZ-I. A transition always occurs in the middle of each bit for synchronization. However, the bit's value is determined by whether a transition occurs at the beginning of the bit. If the next bit is a `0`, a transition occurs at the start; if it's a `1`, there is no transition. This makes it more robust to polarity inversions. 

The primary advantages of both Manchester and Differential Manchester are that they **eliminate baseline wandering** and have **no DC component** because each bit has both a positive and negative voltage contribution. The main **limitation** is that their minimum bandwidth is twice that of NRZ.

---

### **Bipolar Schemes**

**Bipolar schemes** use three voltage levels: positive, negative, and zero. The voltage level for one data element is always zero, while the other element alternates between positive and negative voltages. This provides the benefits of transitions without a significant increase in bandwidth.

 **Alternate Mark Inversion (AMI)**: 

  ![alt text](image-5.png)

In AMI, a neutral zero voltage represents a binary `0`, while binary `1`s are represented by alternating positive and negative voltages. This prevents a long string of `1`s from causing a DC component. 


---
### 3.2 [Digital Modulation Techniques](https://www.tutorialspoint.com/principles_of_communication/principles_of_communication_digital_modulation_techniques.htm)

### 3.3 [GFG: Digital Modulation Techniques ](https://www.geeksforgeeks.org/electronics-engineering/digital-modulation-techniques/)

### 3.4 [PCM and Delta Modulation](https://www.geeksforgeeks.org/computer-networks/difference-between-pulse-code-modulation-pcm-and-delta-modulation-dm/)

### 3.5 Calculative Examples of 3.4 will be added below

--- 

## 4 Multiplexing & Spread Spectrum

### 4.1 [Types of Multiplexing in Data Communications](https://www.geeksforgeeks.org/computer-networks/types-of-multiplexing-in-data-communications/)

### **Multiplexing in Communication Systems**

**Multiplexing** is a method that combines multiple signals or data streams into a single signal over a shared communication medium. It is the process of sharing a single medium or its bandwidth, allowing multiple signals from various sources to be transmitted over a single physical line. This process enhances the **efficient use of resources** and significantly increases the amount of data that can be sent over a network.

***

### **Uses of Multiplexing**

Multiplexing is used in various communication systems to improve network efficiency and capacity:

* **Efficient Utilization of Resources**: It maximizes the use of available bandwidth by allowing multiple signals to share the same channel.
* **Telecommunications**: In telephone networks, it enables simultaneous phone calls over a single line.
* **Internet and Data Networks**: It's used to transmit data from multiple users over a single network line, improving speed and efficiency.
* **Satellite Communications**: It helps efficiently utilize the limited bandwidth on satellite transponders.

***

### **Types of Multiplexing**

There are several types of multiplexing techniques, each designed for different communication needs.

![alt text](image-6.png)

#### **Frequency Division Multiplexing (FDM)**

![alt text](image-7.png)

**Frequency Division Multiplexing (FDM)** divides the bandwidth of a single physical medium into a number of smaller, independent frequency channels. Each signal is transmitted on a different frequency. FDM is commonly used in **radio and television transmission**. To prevent **inter-channel cross-talk**, FDM uses **guard bands**, which are unused strips of bandwidth placed between each channel.

![alt text](image-8.png)

#### **Time Division Multiplexing (TDM)**

![alt text](image-9.png)

**Time Division Multiplexing (TDM)** divides the shared medium's time instead of its frequency. Each connection occupies a portion of time on the link, and all signals share the same frequency but at different times. There are two main types of TDM:

1.  **Synchronous TDM**: 

![alt text](image-10.png)

In this type, a time slot is always allocated to an input frame in the output frame, regardless of whether there is data to send. This can be inefficient if a slot remains empty, wasting bandwidth.
2.  **Statistical (or Asynchronous) TDM**: 

![alt text](image-11.png)

This is a more efficient type where the output frame only collects data from input frames that have data to send. This fully utilizes the channel capacity, but it requires addressing information to be included with each data slot.


### **Advantages and Disadvantages of Multiplexing**

#### **Advantages**

* **Efficient Use of Bandwidth**: Allows more than one signal to be sent over a single channel.
* **Increased Data Transmission**: Significantly boosts the total amount of data that can be sent at one time.
* **Scalability**: Allows networks to easily expand without major infrastructure changes.
* **Flexibility**: Different multiplexing types can be chosen based on specific communication needs.

#### **Disadvantages**

* **Synchronization Issues**: Ensuring that multiple data streams remain synchronized can be challenging and may lead to errors.
* **Latency**: Combining and separating signals can introduce delays.
* **Signal Degradation**: Over long distances, multiplexed signals can degrade, requiring repeaters or signal boosters.
* **Resource Management**: Managing and allocating resources for multiplexed systems can be complex.

### 4.1.1 **Comparison**


---

### **Comparison of FDM, TDM, and Statistical TDM**

| Aspect                 | **FDM (Frequency Division Multiplexing)**           | **TDM (Time Division Multiplexing)**                                    | **Statistical TDM (STDM)**                                   |
| ---------------------- | --------------------------------------------------- | ----------------------------------------------------------------------- | ------------------------------------------------------------ |
| **Basic Idea**         | Each user gets a separate frequency band.           | Each user gets a fixed time slot in rotation.                           | Time slots are assigned dynamically based on demand.         |
| **Efficiency**         | Less efficient (unused frequency bands are wasted). | More efficient than FDM, but unused slots are wasted if a user is idle. | Most efficient: slots allocated only when users have data.   |
| **Complexity**         | Simpler hardware (filters, modulators).             | Moderate complexity (precise timing needed).                            | Higher complexity (needs buffering + slot assignment logic). |
| **Delay**              | Low (continuous channel).                           | Small fixed delay (waiting for slot).                                   | Variable delay (depends on demand and buffer).               |
| **Standards/Examples** | FM radio, Cable TV, DSL.                            | T1 (1.544 Mbps, 24 channels), E1 (2.048 Mbps, 32 channels).             | Packet-based networks (e.g., X.25, Frame Relay, ATM).        |
| **Best Use**           | Analog signals, continuous streams.                 | Digital telephony, synchronous data streams.                            | Data networks with bursty traffic.                           |

---

👉 Quick Hacks:

* **FDM = Frequencies split**
* **TDM = Time split (fixed turns)**
* **STDM = Smart time split (only when needed)**

---

### 4.2.1 [Frequency-Hopping Spread Spectrum in Wireless Networks](https://www.geeksforgeeks.org/ethical-hacking/frequency-hopping-spread-spectrum-in-wireless-networks/)

### 4.2.2 [Direct Sequence Spread Spectrum in Wireless Networks](https://www.geeksforgeeks.org/ethical-hacking/direct-sequence-spread-spectrum-in-wireless-networks/)

### 4.2.3 [Code Division Multiple Access](https://www.geeksforgeeks.org/computer-networks/cdma-full-form/)

---

## 5. Data Link Layer

### 5.1 [Error Detection in Computer Networks](https://www.geeksforgeeks.org/computer-networks/error-detection-in-computer-networks/)

### 5.2 **[Hamming Code in Computer Network](https://www.geeksforgeeks.org/computer-networks/hamming-code-in-computer-network/)**

### 5.3 **Linear block codes**


---

### **Linear Block Codes (LBC) in Data Communication**

**Definition:**
Linear block codes are **error control codes** where a block of $k$ information bits is encoded into a larger block of $n$ bits (called a *codeword*). The extra $(n-k)$ bits are **redundant parity bits**, added for error detection/correction.

---

### **Key Features**

* **Block structure:** Groups of $k$ bits processed together.
* **Linearity:** Any **linear combination** of valid codewords is also a valid codeword.
* **Error handling:** Can **detect** and sometimes **correct** errors depending on code design.
* **Notation:** Represented as $(n, k)$ code.

  * $n$ = length of codeword
  * $k$ = number of message bits
  * Redundancy = $n - k$

---

### **Encoding & Decoding**

* Encoding uses a **generator matrix (G):**

  $$
  \mathbf{c} = \mathbf{m} \cdot G
  $$

  ($\mathbf{m}$: message vector, $\mathbf{c}$: codeword).

* Decoding uses a **parity-check matrix (H):**

  $$
  H \cdot \mathbf{c}^T = 0
  $$

  If result ≠ 0, error is detected.

---

### **Standards / Examples**

* **Hamming Codes** → single-error correction, double-error detection.
* **Cyclic Redundancy Check (CRC)** → widely used in Ethernet, 4G/5G.
* **Reed-Solomon Codes** → CDs, DVDs, QR codes.

---

👉 **Hacks :**

* **Linear** = algebra rules apply.
* **Block** = fixed-size groups.
* **Code** = adds redundancy to fight errors.

---

### 5.4 Practice simple error detection/correction problems will be added later

### 5.5.1 [Flow Control](https://www.geeksforgeeks.org/computer-networks/flow-control-in-data-link-layer/)

### 5.5.2 [Error Control in Data Link Layer](https://www.geeksforgeeks.org/computer-networks/error-control-in-data-link-layer/)

### 5.5.3.1 [Stop and Wait ARQ](https://www.geeksforgeeks.org/computer-networks/stop-and-wait-arq/)

### 5.5.3.2 Sliding window

### 5.5.3.1 [Selective Repeat](https://www.geeksforgeeks.org/computer-networks/sliding-window-protocol-set-3-selective-repeat/)

### 5.5.2 [HDLC frame format.](https://www.geeksforgeeks.org/computer-networks/basic-frame-structure-of-hdlc/)