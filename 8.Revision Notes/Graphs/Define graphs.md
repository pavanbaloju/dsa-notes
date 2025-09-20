Here’s a **complete summary of Graph Definitions and Properties** — essential for both interviews and building intuition for graph problems.

---

## 📘 GRAPH DEFINITIONS

---

### 🔹 1. **Graph**

A **graph** is a data structure consisting of:

- **Vertices (or Nodes)** — entities (e.g., people, cities, states).
    
- **Edges** — relationships between pairs of vertices.
    

Formally, a graph **G** is defined as:

```
G = (V, E)
where:
V = set of vertices
E = set of edges (pairs of vertices)
```

---

### 🔹 2. **Types of Graphs**

|Type|Description|
|---|---|
|**Directed Graph (Digraph)**|Edges have direction (u → v)|
|**Undirected Graph**|Edges are bidirectional (u — v)|
|**Weighted Graph**|Each edge has a weight or cost|
|**Unweighted Graph**|No weights; edges only represent connections|
|**Simple Graph**|No loops or multiple edges between the same pair of nodes|
|**Multigraph**|Multiple edges between same pair of nodes allowed|
|**Cyclic Graph**|Contains one or more cycles|
|**Acyclic Graph**|No cycles (e.g., DAG — Directed Acyclic Graph)|
|**Connected Graph**|All nodes reachable (for undirected graphs)|
|**Disconnected Graph**|Some nodes are isolated or unreachable|

---

## 📐 GRAPH TERMINOLOGY

---

### 1. **Vertex (Node)**

An individual entity in the graph.

### 2. **Edge**

A connection between two vertices. Can be directed (`(u → v)`) or undirected (`(u — v)`).

### 3. **Degree**

- **Undirected graph**: Number of edges connected to a node.
    
- **Directed graph**:
    
    - **In-degree**: Number of incoming edges.
        
    - **Out-degree**: Number of outgoing edges.
        

### 4. **Path**

A sequence of vertices connected by edges.

### 5. **Cycle**

A path that starts and ends at the same vertex without repeating edges or vertices.

### 6. **Connected Components**

A **connected component** is a subgraph where every node is reachable from every other node in that component.

### 7. **Tree**

A special type of graph that is:

- Connected
    
- Acyclic
    
- Has `n` nodes and `n - 1` edges
    

### 8. **Subgraph**

A graph formed from a subset of the vertices and edges of another graph.

### 9. **Bridge**

An edge that, if removed, increases the number of connected components (aka “cut-edge”).

### 10. **Articulation Point**

A node that, if removed, increases the number of connected components.

---

## 📊 GRAPH PROPERTIES

---

### ✅ 1. **Number of Edges**

- **Undirected Simple Graph:**  
    Max edges = `n * (n - 1) / 2`
    
- **Directed Graph:**  
    Max edges = `n * (n - 1)`
    

### ✅ 2. **Density**

Measures how full the graph is:

```
Density = actual_edges / max_possible_edges
```

Sparse graphs → few edges  
Dense graphs → edges close to maximum

### ✅ 3. **Adjacency**

Two nodes are **adjacent** if there is an edge between them.

---

## 🧮 GRAPH REPRESENTATION IN CODE

---

### 1. **Adjacency List**

- Space-efficient for sparse graphs.
    
- Example:
    

```java
Map<Integer, List<Integer>> graph = new HashMap<>();
```

### 2. **Adjacency Matrix**

- Easy edge lookup, O(1)
    
- Uses more space (O(n²))
    

```java
int[][] matrix = new int[n][n];
```

### 3. **Edge List**

- Stores all edges as pairs.
    
- Useful in Kruskal's algorithm
    

```java
List<int[]> edges = new ArrayList<>();
```

---

## 🧠 WHEN TO USE WHAT?

|Scenario|Use|
|---|---|
|Many nodes, few edges|Adjacency List|
|Small graphs or dense graphs|Adjacency Matrix|
|Sorting or filtering by edge weights|Edge List|
|Need fast neighbor lookup|Adjacency List or Matrix|
|Weighted Graph + Pathfinding|List with weight pairs (e.g., `(v, weight)`)|

---

## 🚀 NEXT STEP

Would you like me to continue with:

- Graph **traversal algorithms** (DFS, BFS)
    
- **Graph coding patterns**
    
- **Common interview questions** with visual intuition
    

Just say the word and we’ll build on this.