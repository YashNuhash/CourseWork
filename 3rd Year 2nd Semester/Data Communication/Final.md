## 3. Digital & Analog Techniques 

### 3.1 [Read This First : line coding schemes: NRZ, RZ, Manchester,Differential Manchester, AMI. ](https://www.geeksforgeeks.org/digital-logic/difference-between-unipolar-polar-and-bipolar-line-coding-schemes/)

### 3.2 [Digital Modulation Techniques](https://www.tutorialspoint.com/principles_of_communication/principles_of_communication_digital_modulation_techniques.htm)

### 3.3 [GFG: Digital Modulation Techniques ](https://www.geeksforgeeks.org/electronics-engineering/digital-modulation-techniques/)

### 3.4 [PCM and Delta Modulation](https://www.geeksforgeeks.org/computer-networks/difference-between-pulse-code-modulation-pcm-and-delta-modulation-dm/)

### 3.5 Calculative Examples of 3.4 will be added below

--- 

## 4 Multiplexing & Spread Spectrum

### 4.1 [Types of Multiplexing in Data Communications](https://www.geeksforgeeks.org/computer-networks/types-of-multiplexing-in-data-communications/)

### 4.1.1 Comparison 


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