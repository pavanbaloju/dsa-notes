Here are **full notes on detecting a cycle in a **directed graph**, using both the **DFS with recursion stack** and **BFS (Kahn’s Algorithm)** approaches. Each method includes a detailed explanation followed by **well-commented Java code**.

---

# ✅ **Cycle Detection in a Directed Graph**

---

## 🔹 Problem Definition

> Given a **directed graph**, determine whether it contains a **cycle**. A cycle exists if we can **start from a node and return to the same node** by following the **direction of the edges**.

---

# 🔸 Approach 1: **DFS with Recursion Stack**

---

## ✅ Intuition

In a **directed graph**, a cycle can be detected using **Depth-First Search (DFS)** by tracking:

- Nodes that are **currently in the recursive call stack** (i.e., part of the current path).
    
- Nodes that have been **completely visited** and finished processing.
    

If during DFS, we reach a node that is already in the **recursion stack**, it means we've found a cycle.

To detect a cycle in an **directed graph**, the **visited array is not enough** on its own.
#### Why?

Because when you traverse an undirected graph using DFS or BFS, you can come back to the same node via its parent. That **back edge to the parent is not a cycle**.  
So, to distinguish between a **legitimate backtrack to parent** and an **actual cycle**, you must **track the parent** node.

---

## 🧠 Algorithm Steps

1. Create two boolean arrays:
    
    - `visited[]` – to track if a node has been visited.
        
    - `recStack[]` – to track the current path of recursion.
        
2. For each unvisited node, perform DFS:
    
    - Mark the node as visited and add it to the recursion stack.
        
    - Recur for all its neighbors.
        
        - If a neighbor is unvisited, recursively DFS on it.
            
        - If a neighbor is already in the recursion stack → **Cycle detected**.
            
    - Remove the node from the recursion stack on backtrack.
        

---

## ✅ Java Code (DFS + Recursion Stack)

```java
import java.util.*;

public class DirectedGraphCycleDFS {
    private final int V; // Number of vertices
    private final List<List<Integer>> adj; // Adjacency list

    public DirectedGraphCycleDFS(int V) {
        this.V = V;
        adj = new ArrayList<>();
        for (int i = 0; i < V; i++)
            adj.add(new ArrayList<>());
    }

    // Add a directed edge from u -> v
    public void addEdge(int u, int v) {
        adj.get(u).add(v);
    }

    // Main function to detect cycle
    public boolean hasCycle() {
        boolean[] visited = new boolean[V];
        boolean[] recStack = new boolean[V];

        // Check for every node (handles disconnected components)
        for (int i = 0; i < V; i++) {
            if (!visited[i]) {
                if (dfs(i, visited, recStack))
                    return true;
            }
        }
        return false;
    }

    // Helper function for DFS traversal
    private boolean dfs(int node, boolean[] visited, boolean[] recStack) {
        visited[node] = true;
        recStack[node] = true;

        // Explore all neighbors
        for (int neighbor : adj.get(node)) {
            if (!visited[neighbor]) {
                if (dfs(neighbor, visited, recStack))
                    return true;
            } else if (recStack[neighbor]) {
                // Node already in current path => cycle
                return true;
            }
        }

        // Backtrack: remove from recursion stack
        recStack[node] = false;
        return false;
    }
}
```

---

## ✅ Time & Space Complexity

|Metric|Value|
|---|---|
|Time Complexity|O(V + E)|
|Space Complexity|O(V)|

---

# 🔸 Approach 2: **Kahn’s Algorithm (BFS for Topological Sort)**

---

### 💡 Why Normal BFS Fails in Directed Graphs

In **undirected graphs**, BFS can detect a cycle by checking if a visited node is encountered again **that is not the parent**.

But in **directed graphs**, edges have a direction, and simply revisiting a node does **not always mean a cycle** — unless that node is still **active in the current traversal path**.

However, **BFS has no natural concept of a recursion path**, unlike DFS.

So just using a `visited[]` array in BFS doesn't help you know whether you returned to a node **through a back edge** (which forms a cycle) or through a **legitimate forward edge**.

## ✅ Intuition

- In a **Directed Acyclic Graph (DAG)**, topological sort is always possible.
    
- If there is a **cycle**, at least one node will always have a non-zero indegree → topological sort **cannot include all nodes**.
    

---

## 🧠 Algorithm Steps

1. Compute the **indegree** of each node.
    
2. Add all nodes with indegree = 0 to a queue.
    
3. Repeatedly dequeue a node, and for each of its neighbors:
    
    - Reduce their indegree by 1.
        
    - If any neighbor’s indegree becomes 0, add it to the queue.
        
4. If **all nodes** are processed, the graph is **acyclic**.
    
5. If **some nodes remain**, a **cycle exists**.
    

---

## ✅ Java Code (Kahn’s Algorithm – BFS)

```java
import java.util.*;

public class DirectedGraphCycleBFS {
    private final int V;
    private final List<List<Integer>> adj;

    public DirectedGraphCycleBFS(int V) {
        this.V = V;
        adj = new ArrayList<>();
        for (int i = 0; i < V; i++)
            adj.add(new ArrayList<>());
    }

    // Add a directed edge from u -> v
    public void addEdge(int u, int v) {
        adj.get(u).add(v);
    }

    public boolean hasCycle() {
        int[] indegree = new int[V];

        // Step 1: Calculate indegree for each node
        for (int i = 0; i < V; i++) {
            for (int neighbor : adj.get(i)) {
                indegree[neighbor]++;
            }
        }

        // Step 2: Add all nodes with indegree 0 to queue
        Queue<Integer> queue = new LinkedList<>();
        for (int i = 0; i < V; i++) {
            if (indegree[i] == 0)
                queue.offer(i);
        }

        int count = 0;

        // Step 3: Process nodes with BFS
        while (!queue.isEmpty()) {
            int node = queue.poll();
            count++;

            for (int neighbor : adj.get(node)) {
                indegree[neighbor]--;
                if (indegree[neighbor] == 0)
                    queue.offer(neighbor);
            }
        }

        // Step 4: If not all nodes were processed → Cycle exists
        return count != V;
    }
}
```

---

## ✅ Time & Space Complexity

|Metric|Value|
|---|---|
|Time Complexity|O(V + E)|
|Space Complexity|O(V)|

---

# ✅ Example Usage for Both

```java
public class Main {
    public static void main(String[] args) {
        // DFS-based detection
        DirectedGraphCycleDFS dfsGraph = new DirectedGraphCycleDFS(4);
        dfsGraph.addEdge(0, 1);
        dfsGraph.addEdge(1, 2);
        dfsGraph.addEdge(2, 3);
        dfsGraph.addEdge(3, 1); // cycle

        System.out.println("Cycle (DFS)? " + dfsGraph.hasCycle());

        // Kahn's Algorithm
        DirectedGraphCycleBFS bfsGraph = new DirectedGraphCycleBFS(4);
        bfsGraph.addEdge(0, 1);
        bfsGraph.addEdge(1, 2);
        bfsGraph.addEdge(2, 3);
        bfsGraph.addEdge(3, 1); // cycle

        System.out.println("Cycle (BFS)? " + bfsGraph.hasCycle());
    }
}
```

---

# ✅ Summary Table

|Feature|DFS with Rec Stack|Kahn’s Algorithm (BFS)|
|---|---|---|
|Can detect cycle|✅|✅|
|Detect cycle path|✅ (trace with stack)|❌|
|Easy to implement|Moderate|Slightly more setup|
|Handles disconnected graphs|✅|✅|
|Topological sort required|❌|✅ (core to logic)|

---

Would you like me to add a **trace of an example input** or **convert this to an interview-style explanation** next?