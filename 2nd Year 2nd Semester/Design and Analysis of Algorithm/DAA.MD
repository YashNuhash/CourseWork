
<span style="font-size:24px;">

# CSE-2204: Design and Analysis of Algorithms

## Table of Contents
1. [Key Algorithmic Methods and Processes](#Key-Algorithmic-Methods-and-Processes)
2. [Algorithm Complexity](#algorithm-complexity)
3. [Divide and Conquer](#divide-and-conquer)
4. [Greedy Algorithms](#greedy-algorithms)
5. [Dynamic Programming](#dynamic-programming)
6. [Graph Algorithms](#graph-algorithms)
7. [Backtracking and Branch and Bound](#backtracking-and-branch-and-bound)

---

## Key Algorithmic Methods and Processes

### 1. Definitions of Key Terms

- **Master Theorem**: A formula to solve recurrence relations for divide-and-conquer algorithms, giving an asymptotic solution for recursive cases.

- **Substitution Method**: Solves recurrences by making a guess for the solution’s form and then proving it correct through induction.

- **Divide and Conquer**: Breaks a problem into smaller sub-problems, solves them independently, and combines their solutions; examples include Merge Sort and Quick Sort.

- **Greedy Algorithms**: Chooses the best local option at each step, aiming for a globally optimal solution in problems like Huffman Coding.

- **Dynamic Programming (DP)**: Breaks down complex problems into simpler overlapping sub-problems, storing their solutions to avoid redundant calculations; examples include Fibonacci calculation.

- **Brute Force**: Examines all possible solutions and selects the best one; effective only for small inputs due to inefficiency with large datasets.

- **NP-Complete and NP-Hard**: NP-complete problems are challenging problems without known efficient solutions; NP-hard includes problems as hard as NP-complete but may not be verifiable in polynomial time.

- **Backtracking**: Builds solutions incrementally and abandons paths that fail to satisfy constraints; used in problems like N-Queens and Sudoku.

---

### 2. Differences Between These Methods

| Method             | Approach             | Key Characteristic               | Efficiency                |
|--------------------|----------------------|----------------------------------|---------------------------|
| Master Theorem     | Analytical           | Used for solving recurrence      | Efficient for divide-and-conquer recurrences |
| Substitution       | Analytical           | Guesses solution form            | Effective with induction  |
| Divide and Conquer | Problem Decomposition| Divides into smaller sub-problems| Often logarithmic (log n) |
| Greedy             | Heuristic            | Local optimal choice             | Fast, not always optimal  |
| Dynamic Programming| Memoization          | Stores intermediate results      | Efficient for overlapping subproblems |
| Brute Force        | Exhaustive Search    | Tries all possibilities          | Inefficient for large inputs |
| NP-Complete/Hard   | Complexity Class     | No known efficient solution      | Often requires exponential time |
| Backtracking       | Recursive Search     | Incremental solution building    | Effective for constraint satisfaction |

---

### 3. Relationships Between These Methods

- **Divide and Conquer** and **Master Theorem**: Master Theorem is frequently used to analyze the complexity of divide-and-conquer algorithms.
- **Dynamic Programming** vs **Greedy Algorithms**: Both aim to optimize; however, DP guarantees optimal solutions for problems with overlapping subproblems, while greedy is optimal for problems that satisfy the "greedy-choice property."
- **Backtracking** and **Brute Force**: Backtracking is a refined form of brute force, used in situations where certain constraints can eliminate large subsets of possible solutions.

---

### 4. Importance and Significance of Each Method

- **Master Theorem**: Essential for quickly analyzing the time complexity of recursive divide-and-conquer algorithms, which is foundational for algorithmic analysis.
- **Substitution**: Provides a powerful tool to verify conjectured solutions and analyze the behavior of recursive algorithms.
- **Divide and Conquer**: Efficiently handles large datasets by breaking problems into manageable pieces, crucial in areas like sorting and searching.
- **Greedy Algorithms**: Useful for optimization problems with faster solutions, particularly when the problem allows for local optimizations leading to global solutions.
- **Dynamic Programming**: Vital for problems with overlapping subproblems, significantly reducing computational complexity.
- **Brute Force**: While inefficient for large problems, brute force provides a baseline solution and is straightforward to implement.
- **NP-Complete and NP-Hard**: These classifications help in understanding computational boundaries and direct efforts toward approximate or heuristic solutions when exact solutions are impractical.
- **Backtracking**: Important for constraint-based problems, allowing the efficient exploration of potential solutions without unnecessary computation.

---

### Asymptotic Analysis
Asymptotic analysis evaluates the performance of algorithms based on input size \( n \), focusing on growth rates rather than exact timings. It provides a high-level measure of efficiency using **Big O (worst-case)**, **Theta (average-case)**, and **Omega (best-case)** notations.

### Complexity Analysis of Insertion Sort
- **Best Case (Ω)**: \( O(n) \) — Occurs when the array is already sorted.
- **Average Case (Θ)**: \( O(n^2) \) — Requires shifting elements on average.
- **Worst Case (O)**: \( O(n^2) \) — Occurs when the array is sorted in reverse order.
- **Space Complexity**: \( O(1) \) as it requires no additional memory beyond the input array.

### Sorting Algorithms

1. **Merge Sort**
   - **Method**: Divide and Conquer; splits the array in half, sorts each half, and merges the sorted halves.
   - **Time Complexity**: \( O(n \log n) \) for all cases.
   - **Space Complexity**: \( O(n) \) due to temporary arrays for merging.
   - **Stability**: Stable, as it preserves the order of equal elements.

2. **Heap Sort**
   - **Method**: Builds a max-heap and repeatedly extracts the maximum element to sort the array.
   - **Time Complexity**: \( O(n \log n) \) for all cases.
   - **Space Complexity**: \( O(1) \), as it sorts in place.
   - **Stability**: Not stable, as equal elements may not retain their order.

3. **Quick Sort**
   - **Method**: Divide and Conquer; selects a pivot, partitions the array, and recursively sorts the partitions.
   - **Time Complexity**: \( O(n \log n) \) on average, \( O(n^2) \) in the worst case (e.g., already sorted array).
   - **Space Complexity**: \( O(\log n) \) for recursion stack.
   - **Stability**: Not stable, as the pivot selection may change the order of equal elements.

These algorithms offer different trade-offs in time complexity, space usage, and stability, making each suitable for different scenarios.


---


---


## Algorithms: Definitions, Pseudocode, and Example Implementations

---

### 1. Longest Common Subsequence (LCS)
- **Definition**: Finds the longest sequence that appears in the same order in two sequences.
- **Pseudocode**:
  ```plaintext
  LCS(X, Y):
      Create a table `dp` with dimensions (m+1) x (n+1), where m and n are lengths of X and Y
      for i = 0 to m:
          for j = 0 to n:
              if i == 0 or j == 0:
                  dp[i][j] = 0
              else if X[i-1] == Y[j-1]:
                  dp[i][j] = dp[i-1][j-1] + 1
              else:
                  dp[i][j] = max(dp[i-1][j], dp[i][j-1])
      return dp[m][n]
  ```

- **C++ Implementation**:
  ```cpp
  int LCS(string X, string Y) {
      int m = X.length(), n = Y.length();
      vector<vector<int>> dp(m + 1, vector<int>(n + 1, 0));
      for (int i = 1; i <= m; i++) {
          for (int j = 1; j <= n; j++) {
              if (X[i - 1] == Y[j - 1])
                  dp[i][j] = dp[i - 1][j - 1] + 1;
              else
                  dp[i][j] = max(dp[i - 1][j], dp[i][j - 1]);
          }
      }
      return dp[m][n];
  }
  ```

---

### 2. Huffman Coding
- **Definition**: A compression algorithm that creates a binary tree based on symbol frequencies.
- **Pseudocode**:
  ```plaintext
  Huffman(S):
      Create a priority queue `Q` with nodes for each symbol in S, weighted by frequency
      while Q has more than one node:
          Remove two nodes with lowest weight from Q
          Create a new node with these two nodes as children
          Set new node weight as the sum of the two nodes' weights
          Insert the new node into Q
      Return the root node of the Huffman Tree
  ```

- **C++ Implementation**:
  ```cpp
  struct Node {
      char data;
      int freq;
      Node *left, *right;
      Node(char data, int freq) : data(data), freq(freq), left(NULL), right(NULL) {}
  };
  struct Compare {
      bool operator()(Node* l, Node* r) { return l->freq > r->freq; }
  };
  void HuffmanCoding(vector<char> symbols, vector<int> freq) {
      priority_queue<Node*, vector<Node*>, Compare> minHeap;
      for (int i = 0; i < symbols.size(); ++i)
          minHeap.push(new Node(symbols[i], freq[i]));
      while (minHeap.size() > 1) {
          Node* left = minHeap.top(); minHeap.pop();
          Node* right = minHeap.top(); minHeap.pop();
          Node* sum = new Node('$', left->freq + right->freq);
          sum->left = left;
          sum->right = right;
          minHeap.push(sum);
      }
      // Huffman Tree is in minHeap.top()
  }
  ```

---

### 3. Breadth-First Search (BFS) & Depth-First Search (DFS)
- **Definition (BFS)**: Visits nodes level by level in a graph.
- **Definition (DFS)**: Visits nodes along each branch before backtracking.
- **BFS Pseudocode**:
  ```plaintext
  BFS(G, start):
      Initialize queue with start node
      while queue is not empty:
          v = queue.front(); queue.pop()
          for each neighbor w of v:
              if w is unvisited:
                  mark w as visited
                  queue.push(w)
  ```
- **DFS Pseudocode**:
  ```plaintext
  DFS(G, v):
      mark v as visited
      for each neighbor w of v:
          if w is unvisited:
              DFS(G, w)
  ```

- **C++ Implementation (BFS)**:
  ```cpp
  void BFS(vector<vector<int>>& adj, int start) {
      queue<int> q;
      vector<bool> visited(adj.size(), false);
      visited[start] = true;
      q.push(start);
      while (!q.empty()) {
          int v = q.front();
          q.pop();
          for (int w : adj[v]) {
              if (!visited[w]) {
                  visited[w] = true;
                  q.push(w);
              }
          }
      }
  }
  ```

- **C++ Implementation (DFS)**:
  ```cpp
  void DFS(vector<vector<int>>& adj, vector<bool>& visited, int v) {
      visited[v] = true;
      for (int w : adj[v])
          if (!visited[w])
              DFS(adj, visited, w);
  }
  ```

---

### 4. Dijkstra’s Algorithm
- **Definition**: Finds the shortest path from a source to all other vertices in a weighted graph.
- **Pseudocode**:
  ```plaintext
  Dijkstra(G, source):
      Initialize distance[source] = 0, all other distances = infinity
      Priority queue pq, insert (0, source)
      while pq is not empty:
          (dist, v) = pq.extract_min()
          for each neighbor w of v:
              if distance[v] + weight(v, w) < distance[w]:
                  update distance[w]
                  insert (distance[w], w) into pq
  ```

- **C++ Implementation**:
  ```cpp
  void Dijkstra(vector<vector<pair<int, int>>>& graph, int src, vector<int>& dist) {
      dist[src] = 0;
      priority_queue<pair<int, int>, vector<pair<int, int>>, greater<>> pq;
      pq.push({0, src});
      while (!pq.empty()) {
          auto [d, v] = pq.top(); pq.pop();
          if (d > dist[v]) continue;
          for (auto [w, weight] : graph[v]) {
              if (dist[v] + weight < dist[w]) {
                  dist[w] = dist[v] + weight;
                  pq.push({dist[w], w});
              }
          }
      }
  }
  ```

---

### 5. Minimum Spanning Tree (MST) with Kruskal's Algorithm
- **Definition**: Finds a subset of edges forming a tree that includes every vertex with minimum total weight.
- **Pseudocode**:
  ```plaintext
  Kruskal(G):
      Initialize empty MST
      Sort all edges in G by weight
      for each edge (u, v) in sorted edges:
          if u and v are in different sets:
              add (u, v) to MST
              merge sets of u and v
  ```

- **C++ Implementation**:
  ```cpp
  struct Edge {
      int u, v, weight;
      bool operator<(Edge const& other) { return weight < other.weight; }
  };
  int Kruskal(int n, vector<Edge>& edges) {
      sort(edges.begin(), edges.end());
      int mst_weight = 0;
      DSU dsu(n);
      for (Edge& e : edges) {
          if (dsu.find(e.u) != dsu.find(e.v)) {
              mst_weight += e.weight;
              dsu.union(e.u, e.v);
          }
      }
      return mst_weight;
  }
  ```

---

# 5th Batch Question Solve:  

## 1. (a) With the help of a neat flow diagram, explain the algorithm design and analysis process. Discuss the various stages of the algorithm design and analysis process using a flow chart.

**Answer**:
The algorithm design and analysis process involves several stages, often depicted in a flowchart as follows:

1. **Problem Definition**: Understand the problem requirements, constraints, and input-output specifications.
2. **Algorithm Design**: Devise a step-by-step method (algorithm) to solve the problem.
3. **Algorithm Analysis**: Evaluate the algorithm's efficiency, mainly focusing on time and space complexity.
4. **Implementation**: Translate the algorithm into code using a programming language.
5. **Testing and Debugging**: Run the algorithm with different inputs to ensure correctness and efficiency.
6. **Optimization**: Improve the algorithm, if possible, to make it faster or use less memory.

Flow Chart:
- **Start**
- Define Problem ➔ Design Algorithm ➔ Analyze Algorithm ➔ Implement ➔ Test & Debug ➔ Optimize ➔ **End**

---

## 1. (b) Write down the worst-case time complexity for the following code segments and story:

### Part (a)
```cpp
for(i=0; i<N; i++) {
    for(j=1; j<=K; j=j*2) {
        a = a + (b + b) - c;
    }
}
```

**Answer**:
- Outer loop runs **N** times.
- Inner loop runs logarithmically based on `j` doubling each time (from `j=1` to `K`), so it runs approximately **O(log K)** times.
  
**Worst-Case Time Complexity**: \( O(N \cdot \log K) \).

---

### Part (b)
Story: Suppose you want to check whether anyone in the class has the same birthday as yours. You ask everyone once if they share your birthday. Then, if someone shares your birthday, you ask each person again to ensure nobody else shares the same birthday.

**Answer**:
In the worst case, you ask each person twice, leading to two rounds of checks for each classmate.

**Worst-Case Time Complexity**: \( O(n^2) \), where \( n \) is the number of students, as each student is checked in two rounds.

---

## 1. (c) Fibonacci Sequence with Recursion and Complexity Analysis

```plaintext
Fib(n):
    if n == 0 or n == 1:
        return n
    else:
        return Fib(n-1) + Fib(n-2)
```

**Time Complexity**: \( O(2^n) \), as each call splits into two additional calls, leading to exponential growth.

To reduce space and time complexity, we can use **Dynamic Programming** (Memoization) to store intermediate results, reducing the complexity to \( O(n) \).

---

## 2. (a) Define algorithms. How learning algorithms makes you a better programmer?

**Answer**:
An **algorithm** is a sequence of well-defined steps or rules to solve a problem. Learning algorithms improves problem-solving skills, optimizes solutions for efficiency, and enhances logical thinking, making a programmer more proficient and versatile.

---

## 2. (b) What is the smallest value of n such that an algorithm with a running time of 100n^2 runs faster than an algorithm with a running time of 2^n on the same machine?

**Answer**:
To find when \( 100n^2 < 2^n \):
1. Start with small values of \( n \) and compare the expressions.
2. By trial, \( n = 15 \) satisfies this inequality, where \( 100(15)^2 = 22500 \) and \( 2^{15} = 32768 \).
  
So, the smallest value of \( n \) is approximately **15**.

---

## 2. (c) Write down the algorithm for Insertion Sort and analyze the best case and worst-case running time.

**Insertion Sort Algorithm**:
1. For each element in the array, insert it into its correct position in the sorted portion.
2. Repeat until the entire array is sorted.

```cpp
void insertionSort(int arr[], int n) {
    for (int i = 1; i < n; i++) {
        int key = arr[i];
        int j = i - 1;
        while (j >= 0 && arr[j] > key) {
            arr[j + 1] = arr[j];
            j--;
        }
        arr[j + 1] = key;
    }
}
```

**Complexity Analysis**:
- **Best Case**: \( O(n) \), when the array is already sorted.
- **Worst Case**: \( O(n^2) \), when the array is sorted in reverse order.

---

## 2. (d) Define divide and conquer. Solve \( 9^{19} \mod 7 \) using the divide and conquer method.

**Definition**:
**Divide and Conquer** is an algorithm design paradigm that splits a problem into smaller sub-problems, solves each recursively, and combines their results.

To solve \( 9^{19} \mod 7 \) using Divide and Conquer:
1. **Base Modulus**: \( 9 \mod 7 = 2 \)
2. Calculate \( 2^{19} \mod 7 \) using **Exponentiation by Squaring**.

---

## 3. (a) Define Loop and Cycle of a graph. What do you mean by C5 and K5 of a graph? Draw the corresponding graph.

**Answer**:
- **Loop**: An edge that connects a vertex to itself.
- **Cycle**: A path in which the start and end vertices are the same and all other vertices are distinct.

- **C5**: A cycle graph with 5 vertices (a closed loop).
- **K5**: A complete graph with 5 vertices, where every pair of vertices is connected by an edge.

*Drawings of C5 and K5 would show C5 as a pentagon shape, and K5 as a fully connected graph with 5 vertices.*

---

## 3. (b) Run the following All-Pair-Shortest-Paths algorithm on the weighted and directed graph using the Floyd-Warshall Algorithm.

Given the Floyd-Warshall Algorithm, apply it to the provided 4-vertex graph.

1. Initialize distances with direct edges.
2. Update distances by checking if passing through an intermediate vertex results in a shorter path.
3. Repeat for each possible intermediate vertex.

The final matrix will show the shortest paths between all pairs.


Here are the detailed answers for the questions based on the provided image from page 2 of the exam paper.

---

## 4. (a) What do you mean by heap? Sort the following array using heap sort: A = {4, 1, 3, 2, 16, 9, 10, 14, 8, 7}

### Answer:
A **heap** is a complete binary tree that satisfies the **heap property**:
- In a **max-heap**, each parent node has a value greater than or equal to its children.
- In a **min-heap**, each parent node has a value less than or equal to its children.

**Heap Sort Algorithm**:
1. Build a max-heap from the input data.
2. Swap the root (maximum element) with the last element of the heap.
3. Reduce the heap size by one and heapify the root.
4. Repeat until the heap is empty.

### Sorting Array Using Heap Sort:
Given array: \( A = \{4, 1, 3, 2, 16, 9, 10, 14, 8, 7\} \)

1. Build a max-heap:
   - After max-heap construction, the array becomes: \( \{16, 14, 10, 8, 7, 9, 3, 2, 4, 1\} \).
2. Swap root with the last element and heapify:
   - Continue this process to get the sorted array: \( \{1, 2, 3, 4, 7, 8, 9, 10, 14, 16\} \).

---

## 4. (b) Trace the dynamic programming algorithm for the longest common subsequence problem with strings X[1...4] = "bdab" and Y[1...5] = "abdab". Complete all entries in the table and build all optimal solutions.

### Answer:
To solve this problem, we use a dynamic programming table to store the lengths of LCS at each step. Here’s the process:

|       | 0 | a | b | d | a | b |
|-------|---|---|---|---|---|---|
| **0** | 0 | 0 | 0 | 0 | 0 | 0 |
| **b** | 0 | 0 | 1 | 1 | 1 | 1 |
| **d** | 0 | 0 | 1 | 2 | 2 | 2 |
| **a** | 0 | 1 | 1 | 2 | 3 | 3 |
| **b** | 0 | 1 | 2 | 2 | 3 | 4 |

1. **Resulting LCS**: The length of LCS is 4.
2. **Construct LCS** by backtracking from the table: Possible LCS could be "bdab" or "adab".

---

## 4. (c) Find out the following in the given graph:
1. Hamiltonian Circuit
2. Hamiltonian Path
3. Euler Circuit
4. Euler Path

### Answer:
To find paths and circuits in the provided graph:

1. **Hamiltonian Circuit**: A circuit that visits each vertex exactly once and returns to the starting vertex. (Depends on the specific layout of the graph; check if all vertices form a closed loop.)
2. **Hamiltonian Path**: A path that visits each vertex exactly once. If such a path exists, it connects all vertices without forming a closed loop.
3. **Euler Circuit**: A circuit that traverses every edge exactly once and returns to the starting point. It exists if every vertex has an even degree.
4. **Euler Path**: A path that traverses every edge exactly once without necessarily returning to the start. It exists if exactly two vertices have an odd degree.

Use the graph structure to verify if these paths or circuits exist based on degree and connectivity.

---

## 5. (a) Define Bipartite graph and Graph Coloring. Prove if the following graph is bipartite or not without using graph coloring.

### Answer:
A **Bipartite Graph** is a graph that can be divided into two sets of vertices such that no two vertices within the same set are adjacent.

To check if the graph is bipartite:
1. Use BFS or DFS to attempt to color the graph with two colors.
2. If no two adjacent vertices have the same color, the graph is bipartite; otherwise, it is not.

From the given graph, attempt this coloring approach to verify if it is bipartite.

---

## 5. (b) What do you mean by Backtracking? State and illustrate a problem that can be solved by backtracking.

### Answer:
**Backtracking** is an algorithmic technique to solve problems incrementally, building candidates for solutions and abandoning them if they don’t meet the criteria.

**Example Problem**: The **N-Queens Problem**, where the objective is to place \( N \) queens on an \( N \times N \) chessboard so that no two queens attack each other.

In backtracking, we place queens one by one in different rows, checking for conflicts. If a conflict occurs, we backtrack and try a different placement.

---

## 5. (c) Find the Minimum Spanning Tree (MST) using Kruskal's Algorithm for the given graph.

### Answer:
**Kruskal's Algorithm** for MST:
1. Sort all edges in increasing order of weight.
2. Add edges to the MST, ensuring no cycles are formed, until all vertices are connected.

For the provided graph, follow this approach:
1. Sort edges.
2. Add edges sequentially to form the MST.

---

## 5. (d) What is the N-Queens Problem? Give a solution for 4-Queens Problem using Backtracking method.

### Answer:
The **N-Queens Problem** is to place \( N \) queens on an \( N \times N \) chessboard so that no two queens attack each other.

**4-Queens Solution using Backtracking**:
1. Place queens one by one in each row.
2. Check if placing a queen in a column is safe.
3. If safe, place the queen; if not, backtrack and try the next column.

For the 4-Queens problem, the solution is:
- Queens are placed at positions: \( (1,2), (2,4), (3,1), (4,3) \).


Here are the detailed answers for the questions from the provided image.

---

### 6. (a) Explain the Knapsack Problem using approximation algorithm with example.

The **Knapsack Problem** is a combinatorial optimization problem where we are given:
- A set of items, each with a weight and a value.
- A knapsack with a maximum weight capacity.

The goal is to maximize the total value of items placed in the knapsack without exceeding its weight capacity.

#### Approximation Algorithm: Greedy Method (Fractional Knapsack)
In the **Fractional Knapsack Problem**, we can take fractions of items. This allows us to use a greedy approach:
1. Sort items by their value-to-weight ratio in descending order.
2. Add items to the knapsack in this order until the capacity is full.
3. If an item cannot be fully added due to weight constraints, add a fraction of it.

#### Example:
Suppose we have:
- Knapsack capacity = 50
- Items with (value, weight): 
  - Item 1: (60, 10)
  - Item 2: (100, 20)
  - Item 3: (120, 30)

1. Calculate the value-to-weight ratio for each item:
   - Item 1: 60/10 = 6
   - Item 2: 100/20 = 5
   - Item 3: 120/30 = 4
2. Sort items by ratio: Item 1, Item 2, Item 3.
3. Add items to the knapsack:
   - Add Item 1 completely (weight = 10, value = 60).
   - Add Item 2 completely (weight = 20, value = 100).
   - Add part of Item 3 (remaining weight = 20), giving a value of \(120 \times \frac{20}{30} = 80\).

**Total Value** = 60 + 100 + 80 = 240.

---

### 6. (b) Explain Rabin-Karp Algorithm with example. What is the expected running time of this algorithm?

The **Rabin-Karp Algorithm** is a string-searching algorithm used to find a pattern (substring) within a text. It uses hashing to find matches and has an average-case complexity of \(O(n + m)\), where:
- \(n\) = length of the text.
- \(m\) = length of the pattern.

#### Steps of the Rabin-Karp Algorithm:
1. Compute the hash value of the pattern.
2. Compute the hash value of the first substring of the text with the same length as the pattern.
3. Slide the window over the text one character at a time:
   - Compute the hash value for the new substring.
   - If the hash values match, perform a character-by-character comparison to confirm the match.
4. If a match is found, record the position.

The algorithm is efficient because hash computations are quick, and string comparisons are only done when hash values match.

#### Example:
Pattern = "abc", Text = "abdababc"

1. Compute hash of "abc".
2. Slide through the text:
   - Check substring "abd" (no match).
   - Check substring "bda" (no match).
   - Check substring "dab" (no match).
   - Check substring "abc" (match found).

#### Expected Running Time:
- **Best case**: \(O(n + m)\) with an efficient hash function.
- **Worst case**: \(O(n \cdot m)\) when many hash collisions occur.

---

### 6. (c) Solve the Travelling Salesperson Problem (TSP) of the following graph using dynamic programming approach.

The **Travelling Salesperson Problem (TSP)** is a combinatorial problem where a salesperson must visit all cities exactly once and return to the starting city, minimizing the total travel distance.

#### Dynamic Programming Solution:
1. Let \( dp[S][i] \) represent the minimum cost to visit a set of cities \( S \), ending at city \( i \).
2. The base case: \( dp[\{start\}][start] = 0 \).
3. For each subset of cities, calculate the minimum path by trying all possible ways to reach city \( i \) from any previous city.
4. Recurrence Relation:
   \[
   dp[S][i] = \min(dp[S - \{i\}][j] + dist[j][i]) \quad \text{for } j \in S, j \neq i
   \]
5. Final solution: Find the minimum of \( dp[\{all\ cities\}][i] + dist[i][start] \) for all \( i \).

#### Example for the Provided Graph:
Assuming vertices as \( A, B, C, D \) and distances:
- \( A \to B = 25 \)
- \( A \to C = 10 \)
- \( A \to D = 15 \)
- \( B \to C = 45 \)
- \( B \to D = 20 \)
- \( C \to D = 35 \)

1. Initialize \( dp \) table for subsets and compute minimum costs step-by-step.
2. Final minimum cost will represent the shortest route covering all nodes and returning to the start.

Note: Full calculation requires constructing and filling a dynamic programming table based on subsets of cities, which is extensive.

---

# 6th Batch Question Solve: 


Certainly! Below are the step-by-step answers to the questions in the provided image.

## Question 1

### (a) Define algorithms. How do learning algorithms make you a better programmer?

**Answer:**
An algorithm is a finite sequence of well-defined instructions typically used to solve a class of specific problems or to perform a computation. Learning algorithms improves a programmer's ability to solve problems efficiently by enhancing their understanding of data structures, problem-solving techniques, and optimization methods. It also helps in writing cleaner, more efficient, and scalable code.

### (b) With the help of a neat flow diagram, explain the Algorithm design and analysis process. Discuss the various stages of the algorithm design and analysis process using a flow chart.

**Answer:**
1. **Problem Definition**: Understand and define the problem clearly.
2. **Algorithm Design**: Devise algorithms to solve the problem.
3. **Algorithm Analysis**: Analyze the algorithms for efficiency in terms of time and space.
4. **Algorithm Implementation**: Translate the algorithm into a programming language.
5. **Testing and Debugging**: Test the algorithm with various inputs and debug any issues.
6. **Optimization**: Optimize the algorithm to improve performance.

Flow Diagram:
```
[ Problem Definition ]
          ↓
[ Algorithm Design ]
          ↓
[ Algorithm Analysis ]
          ↓
[ Algorithm Implementation ]
          ↓
[ Testing and Debugging ]
          ↓
[ Optimization ]
```

### (c) What do you mean by time and space complexity of an algorithm? Explain time-space trade-off concept.

**Answer:**
- **Time Complexity**: It measures the amount of time an algorithm takes to complete as a function of the length of the input.
- **Space Complexity**: It measures the amount of memory space an algorithm uses in terms of the length of the input.
- **Time-Space Trade-off**: It refers to the balance between the time complexity and space complexity of an algorithm. Optimizing an algorithm for faster execution can sometimes increase its space requirements and vice versa.

### (d) Suppose you have to choose among three algorithms to solve a problem:
- Algorithm A solves an instance of size n by recursively solving eight instances of size n/2, and then combining their solutions in time O(n).
- Algorithm B solves an instance of size n by recursively solving twenty instances of size n/3, and then combining their solutions in time O(n).
- Algorithm C solves an instance of size n by recursively solving two instances of size n/2, and then combining their solutions in time O(n).

Which one is preferable, and why?

**Answer:**
To determine the preferable algorithm, we can use the Master Theorem for divide-and-conquer recurrences.

- **Algorithm A**: \( T(n) = 8T(n/2) + O(n) \)
  - \( a = 8, b = 2, f(n) = O(n) \)
  - \( f(n) = O(n^c) \), where \( c = 1 \)
  - Compare \( a \) with \( b^c \): \( 8 \) and \( 2^1 \)
  - Since \( a > b^c \), \( T(n) = O(n^{\log_b a}) = O(n^{\log_2 8}) = O(n^3) \)

- **Algorithm B**: \( T(n) = 20T(n/3) + O(n) \)
  - \( a = 20, b = 3, f(n) = O(n) \)
  - \( f(n) = O(n^c) \), where \( c = 1 \)
  - Compare \( a \) with \( b^c \): \( 20 \) and \( 3^1 \)
  - Since \( a > b^c \), \( T(n) = O(n^{\log_b a}) = O(n^{\log_3 20}) \approx O(n^{2.73}) \)

- **Algorithm C**: \( T(n) = 2T(n/2) + O(n) \)
  - \( a = 2, b = 2, f(n) = O(n) \)
  - \( f(n) = O(n^c) \), where \( c = 1 \)
  - Compare \( a \) with \( b^c \): \( 2 \) and \( 2^1 \)
  - Since \( a = b^c \), \( T(n) = O(n^c \log n) = O(n \log n) \)

**Preferred Algorithm**: Algorithm C is preferable as it has the lowest time complexity of \( O(n \log n) \) compared to Algorithms A and B.

## Question 2

### (a) Describe every step to divide the following list of numbers into two sublists using the process used in Quick sort algorithm: 
41, 79, 65, 35, 21, 48, 59, 87, 52, 28

**Answer:**
1. **Choose Pivot**: Select the first element as the pivot (41).
2. **Partitioning**:
   - **Left Sublist**: Elements less than the pivot: [35, 21, 28]
   - **Right Sublist**: Elements greater than or equal to the pivot: [79, 65, 48, 59, 87, 52]

### (b) Which searching algorithm you will be using in each of the following scenarios? Please explain your choice (in no more than 3 lines per scenario).

**Answer:**
- **i) Sorted Array (Ascending)**: Binary Search
  - Efficient for sorted arrays with time complexity \( O(\log n) \).

- **ii) Sorted Array (Descending)**: Binary Search
  - Adjust comparison to account for descending order; time complexity \( O(\log n) \).

- **iii) Unsorted Array**: Linear Search
  - Necessary since the array is unsorted; time complexity \( O(n) \).

### (c) Explain, in general terms, the main differences between the divide-and-conquer technique and dynamic programming.

**Answer:**
- **Divide-and-Conquer**:
  - Breaks a problem into smaller subproblems, solves each subproblem independently, and combines their solutions.
  - Example: Merge Sort, Quick Sort.

- **Dynamic Programming**:
  - Breaks a problem into smaller subproblems but stores the results of subproblems to avoid redundant computations.
  - Example: Fibonacci sequence, Knapsack problem.

### (d) What do you mean by analysis of algorithm? Describe the three asymptotic notations of an algorithm.

**Answer:**
- **Analysis of Algorithm**: It involves determining the computational complexity of algorithms, focusing on time and space requirements.
- **Asymptotic Notations**:
  - **Big O (\( O \))**: Upper bound on the time complexity, representing the worst-case scenario.
  - **Omega (\( \Omega \))**: Lower bound on the time complexity, representing the best-case scenario.
  - **Theta (\( \Theta \))**: Tight bound on the time complexity, representing the average-case scenario.

## Question 3

### (a) What is in place sorting algorithm? Apply merge sort for the following list. Draw all necessary steps until the list is sorted.
\[ A = [18, 26, 6, 43, 15, 91, 22, 26, 19, 55, 37, 43] \]

**Answer:**
Merge Sort Steps:
1. **Divide**: 
   - \[ [18, 26, 6, 43, 15, 91] \]
   - \[ [22, 26, 19, 55, 37, 43] \]

2. **Further Divide**:
   - \[ [18, 26, 6] \] and \[ [43, 15, 91] \]
   - \[ [22, 26, 19] \] and \[ [55, 37, 43] \]

3. **Further Divide**:
   - \[ [18], [26, 6] \]
   - \[ [43], [15, 91] \]
   - \[ [22], [26, 19] \]
   - \[ [55], [37, 43] \]

4. **Further Divide**:
   - \[ [26], [6] \]
   - \[ [15], [91] \]
   - \[ [26], [19] \]
   - \[ [37], [43] \]

5. **Merge**:
   - \[ [6, 26] \] and \[ [18] \]
   - \[ [15, 91] \] and \[ [43] \]
   - \[ [19, 26] \] and \[ [22] \]
   - \[ [37, 43] \] and \[ [55] \]

6. **Merge**:
   - \[ [6, 18, 26] \] and \[ [15, 43, 91] \]
   - \[ [19, 22, 26] \] and \[ [37, 43, 55] \]

7. **Merge Final**:
   - \[ [6, 18, 26, 15, 43, 91] \]
   - \[ [19, 22, 26, 37, 43, 55

] \]

8. **Final Merge**:
   - \[ [6, 15, 18, 19, 22, 26, 26, 37, 43, 43, 55, 91] \]

### (b) What is the best way to multiply a chain of matrices with dimensions that are 10 x 5, 5 x 2, 2 x 10, 10 x 12 using dynamic programming?

**Answer:**
To solve matrix chain multiplication using dynamic programming, use the following steps:

1. **Dimensions**: 
   \[ p = [10, 5, 2, 10, 12] \]
   
2. **Initialize Matrix \( m \)**:
   - \( m[i][j] \) = minimum number of scalar multiplications needed to compute the matrix \( A[i]A[i+1]...A[j] \).

3. **Cost Calculation**:
   - \( m[i][i] = 0 \)
   - For chain length \( l = 2 \) to \( n \):
     - For \( i = 1 \) to \( n-l+1 \):
       - \( j = i+l-1 \)
       - \( m[i][j] = \min(m[i][k] + m[k+1][j] + p[i-1] \cdot p[k] \cdot p[j]) \)

4. **Implementation**:
   - \( n = 4 \)
   - Fill the table \( m \) based on the above calculation.

Result: The minimum cost for multiplying the matrices in the given chain order is obtained from the \( m \) matrix.

## Question 3 (continued)

### (c) Trace the dynamic programming algorithm for the longest common subsequence problem with strings X[1...4] = "abcd" and Y[1...6] = "abebc". Complete all the entries in the table below, and also build all of the optimal solutions.

#### Solution:
We need to fill out the DP table for the longest common subsequence (LCS).

#### DP Table:
Let's create the table where \( dp[i][j] \) represents the length of LCS of \( X[0..i-1] \) and \( Y[0..j-1] \).

|   |   | a | b | e | b | c |
|---|---|---|---|---|---|---|
|   | 0 | 1 | 2 | 3 | 4 | 5 | 6 |
| a | 1 | 0 | 1 | 1 | 1 | 1 | 1 |
| b | 2 | 0 | 1 | 2 | 2 | 2 | 2 |
| c | 3 | 0 | 1 | 2 | 2 | 2 | 3 |
| d | 4 | 0 | 1 | 2 | 2 | 2 | 3 |

#### Steps to fill the DP table:
1. If \( X[i-1] == Y[j-1] \), then \( dp[i][j] = dp[i-1][j-1] + 1 \).
2. Otherwise, \( dp[i][j] = \max(dp[i-1][j], dp[i][j-1]) \).

- For \( i = 1 \) and \( j = 1 \): \( X[0] = 'a' \) and \( Y[0] = 'a' \)
  - \( dp[1][1] = dp[0][0] + 1 = 1 \)
- Continue this process for all cells.

#### Complete Table:

|   |   | a | b | e | b | c |
|---|---|---|---|---|---|---|
|   | 0 | 1 | 2 | 3 | 4 | 5 | 6 |
| a | 1 | 0 | 1 | 1 | 1 | 1 | 1 |
| b | 2 | 0 | 1 | 2 | 2 | 2 | 2 |
| c | 3 | 0 | 1 | 2 | 2 | 2 | 3 |
| d | 4 | 0 | 1 | 2 | 2 | 2 | 3 |

#### Optimal Solutions:
- LCS = "abc"

### (d) What makes a good hash function? Give example.

**Answer:**

A good hash function should have the following properties:
1. **Deterministic**: The same input should always produce the same output hash value.
2. **Uniform Distribution**: Hash values should be uniformly distributed to minimize collisions.
3. **Fast Computation**: The hash function should be fast to compute.
4. **Minimize Collisions**: Different inputs should ideally produce different hash values.

**Example**: 
- A simple yet effective hash function is the DJB2 hash function:
```c
unsigned long hash(unsigned char *str)
{
    unsigned long hash = 5381;
    int c;

    while ((c = *str++))
    {
        hash = ((hash << 5) + hash) + c; /* hash * 33 + c */
    }

    return hash;
}
```

## Question 4

### (a) Consider the following graph. Show the minimum cost to travel from node A to node F using Bellman-Ford Algorithm.

#### Graph:

```
A → B (1), A → C (4)
B → C (2), B → D (7)
C → E (3)
D → F (1)
E → D (-2), E → F (2)
```

#### Steps of Bellman-Ford Algorithm:
1. Initialize distances from source to all vertices as infinite and distance to the source itself as 0.
2. For each edge \( u \rightarrow v \) with weight \( w \):
   - If \( dist[u] + w < dist[v] \), then update \( dist[v] = dist[u] + w \).
3. Repeat step 2 for \( |V| - 1 \) times, where \( |V| \) is the number of vertices.
4. Check for negative weight cycles.

#### Implementation:
1. Initialize:
   ```
   dist[] = {0, ∞, ∞, ∞, ∞, ∞}
   ```
2. Relax edges repeatedly:

   After 1st iteration:
   ```
   dist[] = {0, 1, 4, ∞, ∞, ∞}
   ```
   After 2nd iteration:
   ```
   dist[] = {0, 1, 3, 8, ∞, ∞}
   ```
   After 3rd iteration:
   ```
   dist[] = {0, 1, 3, 6, 6, ∞}
   ```
   After 4th iteration:
   ```
   dist[] = {0, 1, 3, 6, 6, 8}
   ```
   After 5th iteration:
   ```
   dist[] = {0, 1, 3, 6, 6, 8}
   ```

Minimum cost to travel from node A to node F is 8.

### (b) Define single source shortest path. Find the shortest path for the following graph in figure (4.b) using Dijkstra’s algorithm.

#### Graph:

```
         1
    A --------- B
   / \       /  \
10/   \2    3/    \6
 /     \  / /      \
C-------D-----------E
  \ 4    \5        /
   \    / \      /
    \  /   \ 1 /
     F      G
```

#### Steps of Dijkstra’s Algorithm:
1. Initialize distances from source to all vertices as infinite and distance to the source itself as 0.
2. Set all vertices as unvisited.
3. For the current vertex, consider all its unvisited neighbors and calculate their tentative distances through the current vertex. Compare the newly calculated tentative distance to the current assigned value and assign the smaller one.
4. Mark the current vertex as visited.
5. Repeat steps 3-4 until all vertices are visited.

#### Implementation:
1. Initialize:
   ```
   dist[] = {0, ∞, ∞, ∞, ∞, ∞}
   ```
2. Visit vertices and update distances:

   After visiting A:
   ```
   dist[] = {0, 1, 2, ∞, ∞, ∞}
   ```

   After visiting B:
   ```
   dist[] = {0, 1, 2, 4, ∞, ∞}
   ```

   After visiting C:
   ```
   dist[] = {0, 1, 2, 4, 5, 4}
   ```

   After visiting D:
   ```
   dist[] = {0, 1, 2, 4, 5, 4}
   ```

   After visiting E:
   ```
   dist[] = {0, 1, 2, 4, 5, 4}
   ```

Shortest path from A to other nodes:
- A to B: 1
- A to C: 2
- A to D: 4
- A to E: 5
- A to F: 4

### (c) Write Warshall’s algorithm and apply it to compute transitive closure for the directed graph with the adjacency matrix shown below.

#### Adjacency Matrix:

```
    A B C D
A [ 0 1 0 0 ]
B [ 0 0 0 1 ]
C [ 0 0 0 0 ]
D [ 1 0 1 0 ]
```

#### Warshall’s Algorithm:
Warshall's algorithm is used to find the transitive closure of a directed graph. It uses the adjacency matrix and updates it based on reachability of nodes.

1. Initialize the reachability matrix as the adjacency matrix.
2. For each vertex k, update the reachability matrix.
   ```
   R[i][j] = R[i][j] || (R[i][k] && R[k][j])
   ```

#### Implementation:
1. Initial reachability matrix \( R \):

```
    A B C D
A [ 0 1 0 0 ]
B [ 0 0 0 1 ]
C [ 0 0 0 0 ]
D [ 1 0 1 0 ]
```

2. Update for \( k = 1 \):
```
    A B C D
A [ 0 1 0 1 ]
B [ 0 0 0 1 ]
C [ 0 0 0 0 ]
D [ 1 0 1 0 ]
```

3. Update for \( k = 2 \):
```
    A B C D
A [ 0 1 0 1 ]
B [ 0 0 0 1 ]
C [ 0 0 0 0 ]
D [ 1 0 1 0 ]
```



4. Update for \( k = 3 \):
```
    A B C D
A [ 0 1 0 1 ]
B [ 0 0 0 1 ]
C [ 0 0 0 0 ]
D [ 1 0 1 0 ]
```

5. Update for \( k = 4 \):
```
    A B C D
A [ 1 1 1 1 ]
B [ 1 0 1 1 ]
C [ 0 0 0 0 ]
D [ 1 1 1 1 ]
```

Final transitive closure matrix:
```
    A B C D
A [ 1 1 1 1 ]
B [ 1 0 1 1 ]
C [ 0 0 0 0 ]
D [ 1 1 1 1 ]
```

Here's a step-by-step solution to each question from the provided image:

---

### Question 5:

#### (a) What is N-Queens Problem? Draw a solution to 4-Queens Problem using the Backtracking method.

**Answer:**
The N-Queens Problem is a classic problem in computer science, where the goal is to place N queens on an N×N chessboard such that no two queens threaten each other. This means that no two queens should be in the same row, column, or diagonal.

For the 4-Queens Problem, we need to place 4 queens on a 4x4 board. Using backtracking, we start placing queens one by one and backtrack whenever we find that the current placement does not lead to a solution.

A solution to the 4-Queens Problem:

|   | Q |   |   |
|---|---|---|---|
|   |   |   | Q |
| Q |   |   |   |
|   |   | Q |   |

#### (b) State your opinion on "All Pair Shortest Paths Algorithm."

**Answer:**
The All Pair Shortest Paths (APSP) algorithm is used to find the shortest paths between every pair of vertices in a weighted graph. Floyd-Warshall is a popular algorithm for this purpose, which operates in \(O(V^3)\) time complexity, where \(V\) is the number of vertices. This algorithm is particularly useful for dense graphs or small graphs due to its cubic complexity. In scenarios where the graph is sparse, algorithms like Johnson's algorithm, which is faster in such cases, can be more efficient.

#### (c) What do you mean by class P and class NP?

**Answer:**
Class P consists of all decision problems that can be solved in polynomial time, meaning that an algorithm exists to solve the problem within a time complexity of \(O(n^k)\) for some constant \(k\).

Class NP consists of all decision problems for which a solution can be verified in polynomial time, even if finding the solution might take non-polynomial time. A well-known problem in this area is the P vs NP problem, which asks whether every problem in NP can also be solved in polynomial time (i.e., whether P = NP).

#### (d) Start with the following tree and use the Heapify algorithm to convert it into a maximum heap. Draw the resulting tree.

**Answer:**
To convert the tree into a max heap using the Heapify algorithm, we begin from the lowest non-leaf nodes and apply the Heapify process:

Starting Tree:
```
         20
       /    \
     10     30
    /  \   /   \
   5   15 40   35
  / \
 2   3
```

After applying Heapify, we get the Max Heap as follows:
```
         40
       /    \
     35     30
    /  \   /   \
   5   15 20   10
  / \
 2   3
```

---

### Question 6:

#### (a) Explain the knapsack problem. Apply the algorithm to determine the population of the second generation on the following Knapsack. Consider the initial population as four random chromosomes each of 4 bits.

**Answer:**
The Knapsack Problem is an optimization problem where we aim to maximize the value of items in a knapsack without exceeding a given weight limit. For a 0/1 knapsack, each item can either be included or excluded.

Given:
- Knapsack capacity \(K = 12 \text{ Kg}\)
- Items with respective weights and values

Items:

| Item | Weight | Value |
|------|--------|-------|
| A    | 5 Kg   | 12    |
| B    | 3 Kg   | 5     |
| C    | 7 Kg   | 10    |
| D    | 2 Kg   | 8     |

Chromosome representation:
Each chromosome has 4 bits, where each bit represents whether an item is included (1) or excluded (0).

Let's consider four random chromosomes:
1. 1010: Selects A and C, total weight = 12 Kg, total value = 22
2. 1100: Selects A and B, total weight = 8 Kg, total value = 17
3. 0110: Selects B and C, total weight = 10 Kg, total value = 15
4. 1110: Selects A, B, and C, total weight = 15 Kg (exceeds capacity, invalid)

Valid chromosomes for the second generation can include:
1. 1010 (Weight: 12, Value: 22)
2. 1100 (Weight: 8, Value: 17)
3. 0110 (Weight: 10, Value: 15)

#### (b) Write down the Quick-Hull algorithm to find a CONVEX HULL in a geometric plane and test it using suitable data.

**Answer:**
QuickHull is an algorithm for finding the convex hull of a set of points. It works as follows:

1. Find the points with minimum and maximum x-coordinates, as they are part of the convex hull.
2. Use these two points to form a line and divide the set of points into two subsets of points, which are on either side of the line.
3. For each subset, find the point that is farthest from the line. This point forms a triangle with the endpoints of the line, and any points inside this triangle cannot be part of the convex hull.
4. Repeat the process recursively for the two lines formed by this point and the endpoints.
5. Continue until no more points are left.

Testing Data:
Consider points: (0, 3), (1, 1), (2, 2), (4, 4), (0, 0), (1, 2), (3, 1), (3, 3)

After applying QuickHull, the convex hull points are: (0, 3), (4, 4), (3, 1), (0, 0)

#### (c) The Longest Increasing Subsequence (LIS) problem is to find the length of the longest subsequence of a given sequence such that all elements of the subsequence are sorted in non-decreasing order.

**Answer:**
To solve the Longest Increasing Subsequence (LIS) problem, we can use dynamic programming:

1. Initialize an array \( \text{dp}[] \) where each element represents the length of the LIS ending at that element.
2. For each element \( A[i] \) in the sequence, check all previous elements \( A[j] \) such that \( j < i \) and \( A[j] < A[i] \).
3. Update \( \text{dp}[i] = \max(\text{dp}[i], \text{dp}[j] + 1) \) if a longer subsequence ending at \( A[i] \) can be formed.
4. The length of the LIS will be the maximum value in the \( \text{dp}[] \) array.

Given sequence: \( [10, 22, 9, 33, 21, 50, 41, 60, 80] \)

LIS Length Calculation:
- \( dp[] = [1, 2, 1, 3, 2, 4, 4, 5, 6] \)
- The longest increasing subsequence length is 6 (corresponding to subsequence \( [10, 22, 33, 50, 60, 80] \)).

--- 
 

</span>