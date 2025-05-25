
## **1(a) What tasks are performed in the front-end and back-end of a compiler, and why? How are the phases related to the passes?**

---

### 🔹 **Front-End of a Compiler**

The **front-end** checks the **correctness** of the source code.
It performs **analysis** and makes an **intermediate form** of the code.

#### ✅ Main Tasks:

* **Lexical Analysis**: Breaks the code into tokens (words, symbols).
* **Syntax Analysis**: Checks grammar rules (using a parser).
* **Semantic Analysis**: Checks meaning (e.g., correct variable use).
* **Intermediate Code Generation**: Creates a middle version of the code.
* **Error Detection**: Catches mistakes early.

#### 🎯 Why?

To make sure the code is correct and can be easily translated to machine code.

---

### 🔹 **Back-End of a Compiler**

The **back-end** focuses on **optimizing** the code and **generating machine code**.

#### ✅ Main Tasks:

* **Code Optimization**: Makes the code faster and smaller.
* **Code Generation**: Converts it to target machine code.
* **Error Handling**: Handles any leftover errors.

#### 🎯 Why?

To make the code **efficient** and **ready to run** on the computer.

---

### 🔁 **Phases and Passes**

* A **phase** is a single step in the compilation process (e.g., lexical analysis, syntax analysis).
* A **pass** is one **complete scan** over the source code (or intermediate code).

#### 📌 Key Point:

> Multiple **phases** can be done in a **single pass**, or spread across **multiple passes**.

#### Example:

* **One-pass compiler**: All phases done in one go.
* **Two-pass compiler**: Front-end in the first pass, back-end in the second.

---

Sure! Here's a clear and easy-to-understand answer to **1(b)** in **Markdown** format:

---

## **1(b) Given Grammar**

```
S → + S S | * S S | a
```

---

### **i. Left Factor the Grammar**

We observe that the first two productions start with common patterns (`+` and `*`), so we **factor** them:

```text
S → (+ | *) S S | a
```

Now introduce a new non-terminal `Op` for clarity:

```text
S  → Op S S | a  
Op → + | *
```

---

### **ii. Does left factoring make the grammar suitable for top-down parsing?**

✅ **Yes, partially.**

* **Left factoring removes ambiguity** in choosing between multiple productions that start the same way.
* However, for top-down parsing (like LL(1)), we also need to check for **left recursion** and **FIRST/FOLLOW** conflicts.
* In this grammar, there's **no left recursion** after factoring, and choices are clear, so **it helps in top-down parsing.**

---

### **iii. Eliminate Left Recursion (from the original grammar)**

**Original Grammar:**

```
S → + S S | * S S | a
```

Check if there's **left recursion**:

* There is **no direct left recursion** like `S → S α`, so we don't need to eliminate anything here.
* However, this grammar is **left recursive in structure** due to its recursive calls on the left side of the input (like prefix notation), which can still cause problems for **recursive descent parsers**.

Let’s try to **rewrite** it to avoid that prefix pattern and make it **non-left-recursive**:

We can convert it into a **right-recursive grammar**, like this:

Let’s define:

```text
S → a R
R → Op S R | ε
Op → + | *
```

This grammar accepts the same language and avoids prefix-style recursion.

---

### **iv. Is the resulting grammar suitable for top-down parsing?**

✅ **Yes.**

* It is **non-left-recursive**.
* It is **left factored**.
* It uses a **predictive structure** (good for LL(1) parsing).
* You can build a **parse table** without ambiguity.

So, **this grammar is suitable for top-down parsing** like **recursive descent parsers**.

---

Sure! Let's answer each part of Question 2 clearly and simply using **Markdown** formatting:

---

## **2. Given Grammar**

```
S → a S b S | b S a S | ε
```

---

## **(a) FIRST and FOLLOW Sets**

### 🔹 **FIRST(S)**

We compute what symbols can begin the strings derived from `S`.

* `S → a S b S` ⇒ starts with `a`
* `S → b S a S` ⇒ starts with `b`
* `S → ε` ⇒ includes `ε`

✅ So:

```text
FIRST(S) = { a, b, ε }
```

---

### 🔹 **FOLLOW(S)**

We compute what can come **after** `S`.

Let’s assume `S` is the **start symbol**, so **`$`** (end marker) is in FOLLOW(S).

Check all the places `S` appears on the right-hand side:

* In `a S b S`: after first `S`, we can have `b`, then another `S`, so `b` and `FIRST(S)` go into FOLLOW(S)
* In `b S a S`: similarly, we get `a`, and then again FIRST(S)
* Also include FOLLOW(S) wherever `S` appears at the **end** of a production

So:

```text
FOLLOW(S) = { a, b, $ }
```

---

## **(b) Predictive Parsing Table**

We use this rule:

* For each production `A → α`:

  * Add `A → α` to M\[A, x] for each `x ∈ FIRST(α)`
  * If `ε ∈ FIRST(α)`, then add `A → ε` to M\[A, y] for each `y ∈ FOLLOW(A)`

### 🔹 FIRST of each production

* `a S b S`: FIRST = `a`
* `b S a S`: FIRST = `b`
* `ε`: FIRST = `ε`

---

### 📊 Predictive Parse Table (M)

| Non-terminal | a           | b           | \$    |
| ------------ | ----------- | ----------- | ----- |
| **S**        | S → a S b S | S → b S a S | S → ε |

---

## **(c) Is the Grammar LL(1)?**

✅ **Yes.**

**Reason:**

* No multiple entries in any cell of the parse table
* FIRST and FOLLOW sets are disjoint where needed
* Left recursion is not present
* Grammar is suitable for **top-down (LL(1)) parsing**

---

Here is the answer to **Question 3(a)** in **Markdown** format with simplified explanations.

---

## **3(a) Given Grammar**

```
S → 0 S 1 | 0 1
```

We first add an augmented start symbol `S' → S` to help construct the LR(0) items.

---

### ✅ **i. Construct LR(0) Items**

We create **items** by placing a dot `•` in different positions in each production.

#### **Augmented Grammar:**

```
S' → • S
S  → • 0 S 1  
S  → • 0 1
```

---

### ✅ **ii. Compute LR(0) States**

We use **closure** and **goto** functions to compute the states.

---

### **🔹 I0: Start State (Closure of S' → • S)**

```
S' → • S  
S  → • 0 S 1  
S  → • 0 1
```

Transitions from I0:

* On `0` → go to **I1**
* On `S` → go to **I2**

---

### **🔹 I1: After reading `0`**

Advance the dot over `0` in all productions that start with it:

```
S → 0 • S 1  
S → 0 • 1
```

Now we need to include productions with `• S`, so:

```
S → 0 • S 1  
S → 0 • 1  
S → • 0 S 1  
S → • 0 1
```

Transitions from I1:

* On `0` → I1 (again)
* On `1` → I3
* On `S` → I4

---

### **🔹 I2: From I0 on `S`**

```
S' → S •
```

✅ This is a **final item** (accepting state).

---

### **🔹 I3: From I1 on `1`**

```
S → 0 1 •
```

✅ Item completed (reduction).

---

### **🔹 I4: From I1 on `S`**

```
S → 0 S • 1
```

On `1` → go to I5

---

### **🔹 I5: From I4 on `1`**

```
S → 0 S 1 •
```

✅ Item completed (reduction).

---

### 🧾 **Summary of States**

| State | Items                                                |
| ----- | ---------------------------------------------------- |
| I0    | S' → • S<br>S → • 0 S 1<br>S → • 0 1                 |
| I1    | S → 0 • S 1<br>S → 0 • 1<br>S → • 0 S 1<br>S → • 0 1 |
| I2    | S' → S •                                             |
| I3    | S → 0 1 •                                            |
| I4    | S → 0 S • 1                                          |
| I5    | S → 0 S 1 •                                          |

---

Here is the answer to **3(b)** in **Markdown** format with simplified language:

---

## **3(b) Difference Between Synthesized and Inherited Attributes**

| **Aspect**      | **Synthesized Attributes**                                | **Inherited Attributes**                                |
| --------------- | --------------------------------------------------------- | ------------------------------------------------------- |
| **Definition**  | Calculated **from children to parent** in the parse tree. | Passed **from parent to children** or between siblings. |
| **Direction**   | **Bottom-up**                                             | **Top-down or sideward**                                |
| **Usage**       | Common in **S-attributed** grammars                       | Used in **L-attributed** grammars                       |
| **Example**     | Evaluating an expression value from sub-expressions.      | Passing a type or scope from parent to a variable.      |
| **Ease of Use** | Easier to implement in **bottom-up parsing**              | More common in **top-down parsing**                     |

---

### ✅ **Simple Example**

Given a production:

```
E → E1 + T
```

* **Synthesized Attribute**:
  `E.val = E1.val + T.val`
  → `E.val` is computed from its children `E1` and `T`.

* **Inherited Attribute**:
  In a production like `A → B C`,
  if `B.in = A.in`
  → `B` inherits info from `A`.

---

Here’s the answer to **3(c)** in simplified **Markdown** format:

---

## **3(c) Role of Symbol Table in Compilers**

### 🔹 **What is a Symbol Table?**

A **symbol table** is a data structure used by the compiler to **store information about variables, functions, classes, etc.** used in the source code.

---

### 🔧 **Main Role**

* Stores **names** (identifiers) and their related **information**.
* Used during **semantic analysis**, **code generation**, and **optimization**.

---

### 📝 **What It Stores**

For each identifier (like a variable or function), it may store:

* Name
* Type (int, float, etc.)
* Scope (global/local)
* Memory location or address
* Parameters (for functions)

---

### ⚙️ **Key Technical Aspects**

| Aspect             | Description                                                               |
| ------------------ | ------------------------------------------------------------------------- |
| **Creation**       | Created during **syntax and semantic analysis** phases                    |
| **Insertion**      | When a new variable or function is declared                               |
| **Lookup**         | When a variable or function is used, the compiler checks its information  |
| **Scope Handling** | Maintains **separate entries** for same names in different scopes         |
| **Data Structure** | Usually implemented using **hash tables**, **trees**, or **linked lists** |
| **Efficiency**     | Should support **fast insertion and lookup** for large programs           |

---

### ✅ Example

When you write:

```c
int x = 10;
```

The symbol table stores:

```
Name: x, Type: int, Scope: local, Value: 10
```

---

Here is the answer to **4(a)** in **Markdown** format with simple and clear language:

---

## **4(a) Error Recovery Strategies in Syntax Analysis**

When a **syntax error** is found during parsing, the compiler must **recover** and continue checking the rest of the program. This helps in showing **more errors** in one run instead of stopping at the first one.

### 🔧 **Main Error Recovery Strategies:**

| **Strategy**                 | **Description**                                                                        |
| ---------------------------- | -------------------------------------------------------------------------------------- |
| **1. Panic Mode**            | Skips input symbols until a safe point (like `;` or `{`) is found to resume parsing.   |
| **2. Phrase-Level Recovery** | Tries to **fix the error locally** by inserting, deleting, or replacing a token.       |
| **3. Error Productions**     | Adds special rules to the grammar to **handle common mistakes** explicitly.            |
| **4. Global Correction**     | Tries to **minimize total changes** to make the input valid (complex and rarely used). |

---

### ✅ Example of Panic Mode:

If the parser expects `)` but finds `;`, it may skip ahead to the next `)` or `;` to continue parsing the program safely.

---

### 🔍 Summary:

* Syntax error recovery helps the parser **continue after errors**.
* Most common method: **panic mode** (simple and widely used).
* Helps provide **better user feedback** during compilation.

---





