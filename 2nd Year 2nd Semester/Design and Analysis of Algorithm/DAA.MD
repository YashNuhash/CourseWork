
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


</span>