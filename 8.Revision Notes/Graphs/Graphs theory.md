Here’s a **comprehensive Graph Theory Guide** for your interview preparation — covering **core concepts**, **patterns**, and **most asked problem types**, with a strong focus on intuition, visual understanding, and practical use in coding interviews.

---

## 🧭 GRAPH THEORY — INTERVIEW REVISION GUIDE

---

### 🔹 WHAT IS A GRAPH?

A **graph** is a collection of **nodes (vertices)** connected by **edges**.

- Can be **directed** or **undirected**
    
- Can be **weighted** or **unweighted**
    
- May contain **cycles** or be **acyclic**
    
- May be **connected** or **disconnected**
    

---

## 📦 GRAPH REPRESENTATIONS

|Representation|Use When...|Code (Adjacency List) Example|
|---|---|---|
|**Adjacency List**|Sparse graphs|`List<List<Integer>>` or `Map<Integer, List<Integer>>`|
|**Adjacency Matrix**|Dense graphs, fast edge lookup|`int[][] matrix`|
|**Edge List**|Useful for Kruskal’s, sorting edges|`List<int[]>` or `List<Edge>`|

---

## 🧰 CORE GRAPH ALGORITHMS (Must-Know)

|Algorithm|Use Case|
|---|---|
|**DFS**|Traverse graph/depth-first tasks|
|**BFS**|Shortest path in unweighted graph|
|**Topological Sort**|Order of tasks (DAGs)|
|**Union-Find (DSU)**|Connectivity checks, cycles, components|
|**Dijkstra**|Shortest path (weighted, no neg weights)|
|**Bellman-Ford**|Shortest path (with negative weights)|
|**Floyd-Warshall**|All-pairs shortest path|
|**Prim’s / Kruskal’s**|Minimum Spanning Tree (MST)|
|**Tarjan’s / Kosaraju**|SCC (Strongly Connected Components)|

---

## 🧠 MOST COMMON GRAPH PATTERNS (LEETCODE + INTERVIEWS)

---

### 1️⃣ **DFS & BFS Traversal**

- Graph/Tree Traversal
    
- Connected Components
    
- Cycle Detection
    
- Path Existence
    

🧠 Problems:

- Clone Graph
    
- Number of Islands
    
- Surrounded Regions
    
- Word Ladder
    
- Rotten Oranges
    

---

### 2️⃣ **Topological Sorting**

- Task Scheduling
    
- Detect Cycles in DAG
    
- Course Schedule
    

🧠 Problems:

- Course Schedule I & II
    
- Alien Dictionary
    
- Kahn’s Algorithm (BFS)
    
- DFS-based topo sort
    

---

### 3️⃣ **Shortest Path**

- Unweighted: BFS
    
- Weighted: Dijkstra (min-heap), Bellman-Ford, Floyd-Warshall
    

🧠 Problems:

- Dijkstra: Network Delay Time, Path with Min Effort
    
- Bellman-Ford: Cheapest Flights Within K Stops
    
- BFS: Word Ladder, Shortest Bridge
    

---

### 4️⃣ **Union Find (Disjoint Set)**

- Dynamic connectivity
    
- Kruskal’s MST
    
- Cycle detection
    

🧠 Problems:

- Redundant Connection
    
- Number of Connected Components
    
- Accounts Merge
    
- Satisfiability of Equality Equations
    

---

### 5️⃣ **Backtracking on Graphs**

- Hamiltonian Path/Cycle
    
- Coloring
    
- Knights Tour
    

🧠 Problems:

- Word Search
    
- Graph Coloring
    
- N-Queens (Tree, but similar ideas)
    

---

### 6️⃣ **Minimum Spanning Tree (MST)**

- Undirected weighted graph
    
- Minimum cost to connect all nodes
    

🧠 Problems:

- Kruskal’s: Connecting Cities, Min Cost to Supply Water
    
- Prim’s: Network Connection Cost
    

---

### 7️⃣ **Strongly Connected Components (SCC)**

- Tarjan’s Algorithm (Low-Link Values)
    
- Kosaraju’s (Two DFS passes)
    

🧠 Problems:

- Critical Connections (Bridges)
    
- Number of SCCs in a directed graph
    

---

## 🧩 GRAPH PROBLEM TYPES — WHAT TO ASK FIRST

1. Is the graph **directed** or **undirected**?
    
2. Is the graph **weighted** or **unweighted**?
    
3. Is it **cyclic** or **acyclic**?
    
4. Are you looking for **paths**, **connected components**, **shortest distance**, etc.?
    
5. Is it **dynamic** (edges/nodes added over time)?
    
6. Is the input **grid-based** or explicit graph?
    

---

## 🌐 GRIDS AS GRAPHS

Many 2D problems are disguised graphs:

- Each cell is a node
    
- Adjacent cells (up/down/left/right or diagonals) are edges
    

🧠 Classic Examples:

- Number of Islands
    
- Shortest Path in Binary Matrix
    
- Pacific Atlantic Water Flow
    
- Surrounded Regions
    

---

## 🛠 GRAPH PRACTICE ROADMAP (Ordered)

|Level|Focus|Key Problems|
|---|---|---|
|Easy|BFS/DFS, Connected Components|Number of Islands, Flood Fill, Clone Graph|
|Medium|Cycle Detection, Topo Sort|Course Schedule, Word Ladder, Accounts Merge|
|Medium|Union Find|Redundant Connection, DSU Variants|
|Medium|Shortest Path|Dijkstra, Bellman-Ford, Min Effort Path|
|Hard|MST, Bridges, SCC|Critical Connections, Tarjan, Kruskal|
|Hard|Grid + Backtracking|Word Search, Surrounded Regions, Maze Problems|

---

## 🔄 COMBINE GRAPH WITH:

- **Heaps + Graph** → Dijkstra, Prim’s
    
- **DSU + Sorting** → Kruskal’s MST
    
- **Graphs + DFS + Backtracking** → Word Search, Coloring
    
- **Graphs + Topo + Heap** → Lexicographically smallest order
    

---

Would you like:

- A full **Graph Cheat Sheet** PDF?
    
- Or a **Leetcode sheet by pattern** (curated + progressive)?
    

Let me know and I’ll prepare that next.


Here's a comprehensive but focused list of **graph problem patterns** often asked in coding interviews, along with example problems from each category. These patterns help you quickly identify what technique or algorithm is needed to solve a problem based on the structure and constraints.

---

## 🔁 **Graph Problem Patterns**

### 1. **Traversal Patterns**

> Breadth-First Search (BFS) / Depth-First Search (DFS)

|Pattern|Use Case|Example Problems|
|---|---|---|
|**BFS**|Shortest path in unweighted graphs, level-order traversal|- 01 Matrix (Leetcode 542) - Rotting Oranges (994)|
|**DFS**|Connected components, islands, flood fill|- Number of Islands (200) - Max Area of Island (695)|

---

### 2. **Connected Components**

> Count or detect separate graphs (components)

|Pattern|Use Case|Example Problems|
|---|---|---|
|**DFS/BFS/Union-Find**|Count clusters or connected groups|- Number of Provinces (547) - Graph Valid Tree (261) - Friend Circles|

---

### 3. **Cycle Detection**

> Detect whether a cycle exists in the graph

|Pattern|Use Case|Example Problems|
|---|---|---|
|**Undirected Graph (DFS/Union-Find)**|- Cycle detection in undirected graphs|- Detect Cycle in Undirected Graph (LC 684)|
|**Directed Graph (DFS with Rec Stack or Kahn's Algo)**|- Detect cycle in course scheduling|- Course Schedule (207)|

---

### 4. **Topological Sorting**

> Order of tasks/nodes respecting dependencies

|Pattern|Use Case|Example Problems|
|---|---|---|
|**Kahn’s Algorithm (BFS)** **DFS-based Ordering**|- Dependency resolution, course scheduling|- Course Schedule II (210) - Alien Dictionary (269)|

---

### 5. **Shortest Path Algorithms**

> Find the minimum distance or time to reach destination

|Pattern|Use Case|Example Problems|
|---|---|---|
|**BFS**|Unweighted Graphs|- Shortest Path in Binary Matrix (1091)|
|**Dijkstra’s Algorithm (Min Heap)**|Weighted Graphs, No negative weights|- Network Delay Time (743) - Path with Minimum Effort (1631)|
|**Bellman-Ford**|Handles negative weights|- Cheapest Flights Within K Stops (787)|
|**Floyd-Warshall**|All-pairs shortest path|- Minimum Time to Collect All Apples|

---

### 6. **Union-Find (Disjoint Set Union)**

> Grouping and checking connectivity

|Pattern|Use Case|Example Problems|
|---|---|---|
|**DSU with Path Compression**|- Merging sets, cycle detection, Kruskal's|- Accounts Merge (721) - Redundant Connection (684) - Most Stones Removed (947)|

---

### 7. **Minimum Spanning Tree (MST)**

> Build minimum cost tree that connects all nodes

|Pattern|Use Case|Example Problems|
|---|---|---|
|**Kruskal’s Algorithm** **Prim’s Algorithm**|- Optimize cost, connect components|- Connecting Cities With Minimum Cost (1135) - Min Cost to Connect All Points (1584)|

---

### 8. **2D Grid as Graph**

> Treat 2D matrices as graph problems (4 or 8 directions)

|Pattern|Use Case|Example Problems|
|---|---|---|
|**BFS/DFS on 2D grid**|- Search, fill, shortest path, flooding|- Number of Islands (200) - Pacific Atlantic Water Flow (417)|

---

### 9. **Backtracking with Graphs**

> Often used in traversal with constraints

|Pattern|Use Case|Example Problems|
|---|---|---|
|**DFS with visited set**|- All paths, cycles, constraints|- Word Search (79) - Reconstruct Itinerary (332)|

---

### 10. **Graph Coloring / Bipartite Check**

> Can the graph be colored using 2 colors?

|Pattern|Use Case|Example Problems|
|---|---|---|
|**BFS/DFS Coloring**|- Check bipartiteness|- Is Graph Bipartite? (785)|

---

## ✅ Optional Patterns (Advanced or Niche)

|Pattern|Use Case|Example Problems|
|---|---|---|
|**Eulerian Path/Circuit**|- Path that visits every edge exactly once|- Reconstruct Itinerary (332)|
|**Bridges and Articulation Points**|- Critical connections|- Critical Connections in a Network (1192)|

---

Would you like these structured into a **PDF quick revision sheet** or a **tagged problem list** next?