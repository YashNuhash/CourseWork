## 1 (a) Major Categories of Issues Addressed in the Theory of Computation

The **Theory of Computation** deals with the fundamental capabilities and limitations of computers. It is generally divided into **three major categories**:

---

#### 1. **Automata Theory**
- **Definition**: Studies abstract machines (automata) and the problems they can solve.
- **Examples**: Finite Automata, Pushdown Automata, Turing Machines.
- **Focus**: Models of computation, recognizing patterns and designing compilers.

**Significance**:
- Helps understand the working of language recognizers and parsers.
- Forms the foundation for designing programming languages and lexical analyzers.

---

#### 2. **Computability Theory**
- **Definition**: Deals with the question of what problems can be solved using algorithms.
- **Concepts**: Decidability, Turing machines, Halting problem.
- **Focus**: Determines whether a given problem is solvable or not.

**Significance**:
- Clarifies the limits of algorithmic computation.
- Prevents time and resource waste on unsolvable problems.

---

#### 3. **Complexity Theory**
- **Definition**: Studies the resources (time and space) needed to solve computational problems.
- **Classes**: P, NP, NP-Complete, NP-Hard.
- **Focus**: Efficiency of algorithms and classification of problems based on difficulty.

**Significance**:
- Helps in analyzing the performance of algorithms.
- Critical in fields like cryptography, optimization, and AI.

---

### Why Are These Categories Significant?

- **Foundation of Computer Science**: They define the theoretical limits of what computers can and cannot do.
- **Algorithm Design**: Provide tools to evaluate the feasibility and efficiency of algorithms.
- **Understanding Limitations**: Helps in distinguishing between solvable and unsolvable or intractable problems.
- **Practical Applications**: Useful in compiler construction, language processing, artificial intelligence, and software verification.

---

## (b) Formal Definitions: Alphabet, String, Language, Family of Languages

---

#### 1. **Alphabet (Σ)**

- **Definition**: A finite, non-empty set of symbols.
- **Notation**: Usually denoted by the Greek letter Σ (sigma).
- **Example**:  
  - Σ = {0, 1} → binary alphabet  
  - Σ = {a, b, c} → alphabet of lowercase letters

---

#### 2. **String**

- **Definition**: A finite sequence of symbols from an alphabet.
- **Notation**: If `w` is a string over alphabet Σ, then `w ∈ Σ*`.
- **Special Strings**:
  - **Empty string**: Denoted by ε (epsilon), has length 0.
- **Example**:  
  - For Σ = {0, 1}, possible strings: `0`, `10`, `1101`

---

#### 3. **Language**

- **Definition**: A set of strings formed from an alphabet.
- **Notation**: `L ⊆ Σ*`, where `Σ*` is the set of all possible strings over Σ.
- **Example**:  
  - Let Σ = {a, b}  
    Then L = {ε, a, ab, aab, abb} is a language over Σ.

---

#### 4. **Family of Languages**

- **Definition**: A group or collection of languages that share common characteristics, usually defined by a particular type of automaton or grammar.
- **Examples**:
  - **Regular Languages** → Recognized by Finite Automata
  - **Context-Free Languages** → Recognized by Pushdown Automata
  - **Recursive Languages** → Decidable by Turing Machines
  - **Recursively Enumerable Languages** → Recognized by Turing Machines (may not halt)

---

## (c) Proving: If L₁ and L₂ are regular, then L₁ \ L₂ is also regular

---

#### Given:
- L₁ and L₂ are **regular languages** over the same alphabet Σ.
- We want to prove that **L₁ \ L₂** is **regular**.

---

### Step-by-Step Proof:

#### 1. **Understanding Set Difference:**

The **difference** of two languages is defined as:

#### L₁ \ L₂ = { w ∈ Σ* | w ∈ L₁ and w ∉ L₂ }


This means the set of strings that are in L₁ but not in L₂.

---

#### 2. **Regular Languages are Closed Under Complement and Intersection**

Regular languages are closed under:
- **Complement**: If L is regular, then Σ* \ L is also regular.
- **Intersection**: If L₁ and L₂ are regular, then L₁ ∩ L₂ is also regular.

---

#### 3. **Rewriting L₁ \ L₂ Using Set Operations:**

We can express the difference as:

#### L₁ \ L₂ = L₁ ∩ (complement of L₂) = L₁ ∩ (Σ* \ L₂)



#### 4. **Use of Closure Properties:**

Since:
- L₂ is regular ⇒ its **complement** is regular
- L₁ is regular and complement of L₂ is regular ⇒ their **intersection** is regular

Therefore:
#### L₁ \ L₂ = L₁ ∩ (Σ* \ L₂) is regular


### ✅ Conclusion:

Since regular languages are closed under complement and intersection,  
**L₁ \ L₂ is regular** if both **L₁** and **L₂** are regular.

**Hence Proved.**

---

### (d) Comparison: NFA vs. DFA

---

| Feature | **DFA (Deterministic Finite Automaton)** | **NFA (Nondeterministic Finite Automaton)** |
|--------|-------------------------------------------|---------------------------------------------|
| **Definition** | Exactly one transition for each symbol from a state. | Can have zero, one, or multiple transitions for a symbol, including ε-transitions (no input). |
| **Transition Function** | δ: Q × Σ → Q | δ: Q × Σ → 2^Q |
| **Determinism** | Completely deterministic – no ambiguity in moves. | Nondeterministic – multiple choices possible. |
| **ε-transitions** | Not allowed. | Allowed. |
| **Computation** | Only one path of execution for each input string. | May have multiple paths (computation branches). |
| **Acceptance** | Input is accepted if a single path ends in an accepting state. | Accepted if **at least one path** leads to an accepting state. |
| **Ease of Construction** | More complex to construct in some cases. | Easier and more intuitive to construct. |
| **Speed of Simulation** | Faster (O(n), where n = input length). | May be slower (due to backtracking or parallelism simulation). |
| **Expressive Power** | Equal to NFA. | Equal to DFA. |
| **Conversion** | Not required. | Can be converted to equivalent DFA using **subset construction** (powerset method). |
| **Implementation** | Easier to implement in code/hardware. | More theoretical and useful for design/simplification. |

---

### ✅ Key Point:

> **DFA and NFA recognize the same class of languages: Regular Languages.**  
> That is, for every NFA, there exists an equivalent DFA that accepts the same language.

---

### Summary:

- NFAs are **easier to design** but **harder to simulate**.
- DFAs are **harder to design** but **easier to simulate**.
- **Both have the same computational power**.

---

### 2(a) Construct an NFA to recognize the language consisting of all strings over {0,1} containing a 0 in the third position from the end.

---

#### 💡 Language Definition:

Let L = { w ∈ {0,1}* | the third symbol from the end is 0 }

We want an NFA that **accepts** any string where:
- There are **at least 3 symbols**
- And the **third last** one is `0`

That means:
If w = `xabc` where `a`, `b`, `c ∈ {0,1}`, then:
- `a` must be `0`
- The rest `x` can be any string of any length (including empty)

![alt text](image.png)

#### 🧾 Transition Table Summary:

Let the NFA states be:

- `q0`: Start state, loops on `0` and `1`
- `q1`: On ε-transition from q0 — guess start of last 3 symbols
- `q2`: Reads `0` (third from end)
- `q3`: Reads any symbol (second from end)
- `q4`: Reads any symbol (last character) → **Final accepting state**

| Current | Input | Next    |
|---------|-------|---------|
| q0      | 0,1   | q0      |
| q0      | ε     | q1      |
| q1      | 0     | q2      |
| q2      | 0,1   | q3      |
| q3      | 0,1   | q4 (✔)  |

- `q4` is the accepting state.

---

#### ✅ Verbal Description:

The NFA accepts any string over `{0,1}` **whose third symbol from the end is `0`**.

Examples of accepted strings:
- `000`
- `1010`
- `11010`
- `10011`

Rejected examples:
- `001` → 3rd from end = `0`, ✔
- `011` → 3rd from end = `0`, ✔
- `111` → 3rd from end = `1`, ❌

---



### 2(b) Verbal Description of the Language Recognized by the DFA (Figure 1)

---

#### ✅ Description:

The DFA recognizes the language:

> **L = { w ∈ {0,1}* | w contains the substring `0010` }**

---

#### 🔍 Reasoning:

- The DFA transitions through the following states:
  - `q0` → Start state.
  - `q0 → q1` on input `0`
  - `q1 → q2` on input `0`
  - `q2 → q3` on input `1`
  - `q3 → q4` on input `0`

- Once the sequence `0010` is matched, the DFA enters the accepting state `q4`, which is **final** and **loops on both `0` and `1`**, meaning any extra symbols are accepted.

---

#### 🧪 Examples of Accepted Strings:
- `0010`
- `10010`
- `000010`
- `0010111`
- `1100100`

#### ❌ Examples of Rejected Strings:
- `0`
- `10`
- `011`
- `1101`
- `1110001`

---

#### 💡 Conclusion:

The DFA accepts all strings over `{0,1}` that **contain the substring `0010`** anywhere within them.

---

### 3(a) Suppose L₁ and L₂ are regular languages. Prove that L₁ ⋅ L₂ is also regular.

---

#### ✅ Statement:

If **L₁** and **L₂** are regular languages, then their **concatenation**  
L₁ ⋅ L₂ = { xy | x ∈ L₁ and y ∈ L₂ } is also a **regular language**.

---

#### 🧠 Proof Using Closure Properties:

Regular languages are **closed under concatenation**.  
This means:  
If L₁ and L₂ are regular, then L₁ ⋅ L₂ is also regular.

---

#### 🔧 Proof Sketch Using Automata:

Let:
- M₁ = (Q₁, Σ, δ₁, q₁₀, F₁) be a DFA/NFA that accepts L₁  
- M₂ = (Q₂, Σ, δ₂, q₂₀, F₂) be a DFA/NFA that accepts L₂  

We can construct an **NFA** M that accepts L₁ ⋅ L₂ as follows:

1. **States** of M = Q₁ ∪ Q₂  
2. **Start state** = q₁₀ (start of M₁)  
3. **Accepting states** = F₂ (accepting states of M₂)  
4. Add **ε-transitions** from each accepting state of M₁ (F₁) to the start state of M₂ (q₂₀)

This NFA first simulates M₁, and once M₁ accepts, it jumps to M₂ using an ε-move and continues to process the rest of the input.

---

#### 📌 Therefore:

Since we have constructed an NFA that accepts L₁ ⋅ L₂, and NFAs recognize regular languages,  
**L₁ ⋅ L₂ is regular**.

✅ **Q.E.D.**

### 🔍 Visual Representation of the Concatenation L₁ ⋅ L₂

Assume we have two NFAs:

#### 🌀 NFA for L₁:

 --> (q₁₀) --a--> (q₁₁) --b--> ((q₁₂))

- Start state: `q₁₀`
- Accepting state: `q₁₂`
- Accepts: "ab"

#### 🌀 NFA for L₂:

 --> (q₂₀) --c--> ((q₂₁))

- Start state: `q₂₀`
- Accepting state: `q₂₁`
- Accepts: "c"

---

### 🔗 Construction of NFA for L = L₁ ⋅ L₂

To construct the concatenation:

1. Take all states from both L₁ and L₂.
2. Add **ε-transition** from final state of L₁ (`q₁₂`) to start state of L₂ (`q₂₀`).

#### ✅ Combined NFA for L₁ ⋅ L₂:

 --> (q₁₀) --a--> (q₁₁) --b--> (q₁₂) --ε--> (q₂₀) --c--> ((q₂₁))


- Start state: `q₁₀`
- Accepting state: `q₂₁`
- Accepts: "abc"

---

### 🎯 Final Notes:

- The ε-transition allows the automaton to **seamlessly switch** from processing L₁ to L₂.
- This construction **does not require** the input to pause — it's handled by the NFA structure.
- Hence, L₁ ⋅ L₂ is regular.

✅ **This visual example proves that the concatenation of two regular languages results in another regular language.**

### 3(b) Convert the Regular Expression (ab ∪ a)\* to an Equivalent NFA

---

#### 📌 Given:

- Regular Expression: **(ab ∪ a)\***
- Alphabet: **Σ = {a, b}**

---

### 🔄 Step-by-Step Breakdown:

Let’s break down the regular expression:

1. **Sub-expression 1:** `ab` → a followed by b
2. **Sub-expression 2:** `a` → just a
3. **Union:** `ab ∪ a`
4. **Kleene Star:** `(ab ∪ a)*` → zero or more occurrences of either `ab` or `a`

---

### 🛠️ NFA Construction Strategy

We construct NFAs for basic parts, then combine:

![alt text](image-1.png)


---

### 💡 Conclusion:

This NFA accepts all strings formed by zero or more repetitions of either `a` or `ab`.  
Examples of strings accepted:
- ε
- a
- ab
- aa
- aba
- abab
- ababa
- etc.

✅ **Thus, the NFA correctly accepts the language described by the regular expression (ab ∪ a)\***

---

### 4(a) DFA Description

**Language L = { w ∣ w has exactly two a's and at least two b's }**

#### Verbal Description:

This DFA accepts all strings over the alphabet **Σ = {a, b}** such that:

- The string contains **exactly two occurrences of 'a'**, and  
- The string contains **at least two occurrences of 'b'** (i.e., two or more b's).

![alt text](image-2.png)

#### Explanation of DFA Behavior:

- The DFA uses **states to count** the number of a’s (up to exactly two) and the number of b’s (up to two, but allows more).
- Once two a’s are seen, **no further a's are allowed**; otherwise, the input is rejected.
- Once two or more b’s are seen, the DFA allows **any number of additional b’s**, remaining in an accepting state.
- The accepting state is reached **only** if the input has **exactly two 'a's and at least two 'b's**.

---

### 4(b) Prove that L = { aⁿbⁿ | n ≥ 0 } is **not regular** using the **Pumping Lemma**

---

#### 📌 Given:
- **Language**: L = { aⁿbⁿ | n ≥ 0 }
- **Alphabet**: Σ = { a, b }

---

### 🧠 Pumping Lemma Statement for Regular Languages

If **L is regular**, then there exists a **pumping length `p`** such that any string **s ∈ L** with **|s| ≥ p** can be split into three parts:  
**s = xyz**, satisfying:

1. |y| > 0  
2. |xy| ≤ p  
3. For all **i ≥ 0**, the string **xyⁱz ∈ L**

---

### 🚫 Assume L is Regular (for contradiction)

Let’s choose a string **s = aᵖbᵖ ∈ L**, where **p** is the pumping length.

- Clearly, **|s| = 2p ≥ p**
- By the lemma, we must split **s = xyz** such that:
  - **|xy| ≤ p** → so **x** and **y** consist of **only a’s**
  - **|y| > 0** → so **y** contains **at least one a**

Let:
- **x = aᵏ**
- **y = aᵐ**, where **m ≥ 1**
- **z = a^(p−k−m) bᵖ**

So the full string is: **xyz = aᵖbᵖ**

---

### 🧪 Now Pump: Choose i = 2  
New string: **xy²z = aᵏ (aᵐ)² a^(p−k−m) bᵖ = a^(p + m) bᵖ**

This means the number of **a’s > p**, but the number of **b’s = p**

➡️ So the pumped string is **not in L**  
Because it is **not of the form aⁿbⁿ** — the number of a’s and b’s are no longer equal.

---

### ❌ Contradiction

This contradicts the pumping lemma → Hence, **L is not regular**.

---

### ✅ Conclusion

**L = { aⁿbⁿ | n ≥ 0 } is NOT regular**, as it **fails** the conditions of the **Pumping Lemma**.








