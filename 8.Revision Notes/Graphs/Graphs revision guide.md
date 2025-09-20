Here’s a **comprehensive guide to Graph Patterns** for interview prep — structured to give you a strong mental model, with problem types and key techniques used across **DFS**, **BFS**, **Topological Sort**, **Union-Find**, **Shortest Path**, and more.

---

## 🌐 GRAPH PATTERNS – INTERVIEW REVISION GUIDE

---

### 1️⃣ **Graph Representations**

|Type|Description|Example|
|---|---|---|
|**Adjacency List**|`Map<Node, List<Node>>`|Space-efficient|
|**Adjacency Matrix**|2D `int[][]` matrix|Dense graphs|
|**Edge List**|List of edges (u, v)|Used in Kruskal's|

---

## 🔁 **TRAVERSAL PATTERNS**

---

### 2️⃣ **Depth-First Search (DFS)**

- **Recursive** or **explicit stack**
    
- Used in:
    
    - Cycle Detection
        
    - Connected Components
        
    - Topological Sort
        
    - Island Counting
        
    - Subgraph/Traversal problems
        

🧠 **Problems:**

- [Number of Islands](https://leetcode.com/problems/number-of-islands)
    
- [Clone Graph](https://leetcode.com/problems/clone-graph)
    
- [Max Area of Island](https://leetcode.com/problems/max-area-of-island)

---

### 3️⃣ **Breadth-First Search (BFS)**

- **Queue-based traversal**
    
- Used in:
    
    - Shortest path in **unweighted** graphs
        
    - Level-wise processing
        
    - Multi-source BFS (e.g., Rotten Oranges)
        

🧠 **Problems:**

- [Rotting Oranges](https://leetcode.com/problems/rotting-oranges)
    
- [01 Matrix](https://leetcode.com/problems/01-matrix/)
    
- [Word Ladder](https://leetcode.com/problems/word-ladder)
- [[Flood Fill]]

---

## 🔄 **GRAPH CONNECTIVITY PATTERNS**

---

### 4️⃣ **Union Find (Disjoint Set Union - DSU)**

- Detect cycles in undirected graphs
    
- Track connected components
    
- Kruskal's MST
    

🧠 **Problems:**

- [Graph Valid Tree](https://leetcode.com/problems/graph-valid-tree)
    
- [Number of Connected Components](https://leetcode.com/problems/number-of-connected-components-in-an-undirected-graph)
    
- [Accounts Merge](https://leetcode.com/problems/accounts-merge)
    

---

### 5️⃣ **Topological Sort (DAGs)**

- Used for ordering tasks with dependencies
    
- **Kahn’s Algorithm (BFS)** or **DFS with stack**
    
- Only works on **Directed Acyclic Graphs (DAGs)**
    

🧠 **Problems:**

- [Course Schedule](https://leetcode.com/problems/course-schedule)
    
- [Course Schedule II](https://leetcode.com/problems/course-schedule-ii)
    
- [Alien Dictionary](https://leetcode.com/problems/alien-dictionary)
    

---

### 6️⃣ **Cycle Detection**

- **Undirected Graph**: DFS or Union-Find
    
- **Directed Graph**: DFS with recursion stack
    

🧠 **Problems:**

- [Course Schedule](https://leetcode.com/problems/course-schedule)
    
- [Detect Cycle in Graph](https://practice.geeksforgeeks.org/problems/detect-cycle-in-a-directed-graph)
    

---

## 📏 **SHORTEST PATH ALGORITHMS**

---

### 7️⃣ **Dijkstra’s Algorithm**

- Graph with **non-negative weights**
    
- Use **PriorityQueue**
    
- Finds **shortest path from source to all nodes**
    

🧠 **Problems:**

- [Network Delay Time](https://leetcode.com/problems/network-delay-time)
    
- [Path With Minimum Effort](https://leetcode.com/problems/path-with-minimum-effort)
    
- [Cheapest Flights Within K Stops](https://leetcode.com/problems/cheapest-flights-within-k-stops)
    

---

### 8️⃣ **Bellman-Ford Algorithm**

- Handles **negative weights**
    
- Slower than Dijkstra
    
- Detects **negative cycles**
    

🧠 **Problems:**

- [Bellman-Ford Template](https://www.geeksforgeeks.org/bellman-ford-algorithm-dp-23/)
    

---

### 9️⃣ **Floyd-Warshall Algorithm**

- All-pairs shortest paths
    
- Good for dense graphs
    
- O(N³) Time
    

🧠 **Problems:**

- [Find the City With the Smallest Number of Neighbors at a Threshold Distance](https://leetcode.com/problems/find-the-city-with-the-smallest-number-of-neighbors-at-a-threshold-distance)
    

---

## 🌉 **MINIMUM SPANNING TREE (MST)**

---

### 🔹 **Prim’s Algorithm**

- Greedy
    
- Start from any node and grow MST
    
- Uses Min Heap (PQ)
    

### 🔹 **Kruskal’s Algorithm**

- Greedy
    
- Sort edges and pick if they don’t form a cycle
    
- Uses Union Find
    

🧠 **Problems:**

- [Min Cost to Connect All Points](https://leetcode.com/problems/min-cost-to-connect-all-points)
    
- [Connecting Cities With Minimum Cost](https://leetcode.com/problems/connecting-cities-with-minimum-cost)
    

---

## 🌊 **GRID & MAZE AS GRAPHS**

---

- Use BFS/DFS on grid
    
- Handle 4/8 direction movement
    
- Handle boundaries and visited
    

🧠 **Problems:**

- [Walls and Gates](https://leetcode.com/problems/walls-and-gates)
    
- [Surrounded Regions](https://leetcode.com/problems/surrounded-regions)
    
- [Shortest Path in Binary Matrix](https://leetcode.com/problems/shortest-path-in-binary-matrix)
    

---

## 🧠 **OTHER IMPORTANT PATTERNS**

---

### 🔁 **Backtracking in Graphs**

- Hamiltonian paths
    
- Coloring problems
    
- Knight’s tour, Sudoku
    

### 🔁 **Bridges and Articulation Points**

- Used to find critical connections in networks (Tarjan’s Algorithm)
    

🧠 **Problems:**

- [Critical Connections in a Network](https://leetcode.com/problems/critical-connections-in-a-network)
    

---

## 🔚 Want a pattern-wise Leetcode list or Graph cheatsheet?

Let me know and I can send a structured list to practice each category with 2–4 handpicked problems per pattern.