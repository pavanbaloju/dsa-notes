Here's a complete guide on **detecting a cycle in an undirected graph** using both **DFS** and **BFS** in Java, with full explanations and time complexity analysis.

---

## ✅ Problem Statement

Given an **undirected graph**, detect whether it contains **any cycle**.

---

## 🧠 Key Idea

- In **undirected graphs**, a cycle exists if we revisit a node **that is already visited and is not the parent** of the current node.
    
- This is different from directed graphs where the back edge itself indicates a cycle.
    

---

## ✅ DFS-Based Cycle Detection

### 🔍 Approach

- For every unvisited node, run DFS.
    
- Keep track of the parent node.
    
- If you encounter a visited node that’s **not the parent**, a cycle exists.
    

### ✅ Java Code – DFS

```java
import java.util.*;

public class CycleDetectionDFS {
    private final int V;
    private final List<List<Integer>> adj;

    public CycleDetectionDFS(int V) {
        this.V = V;
        adj = new ArrayList<>();
        for (int i = 0; i < V; i++)
            adj.add(new ArrayList<>());
    }

    public void addEdge(int u, int v) {
        adj.get(u).add(v);
        adj.get(v).add(u); // Undirected graph
    }

    public boolean hasCycle() {
        boolean[] visited = new boolean[V];

        for (int i = 0; i < V; i++) {
            if (!visited[i]) {
                if (dfs(i, -1, visited)) {
                    return true;
                }
            }
        }

        return false;
    }

    private boolean dfs(int node, int parent, boolean[] visited) {
        visited[node] = true;

        for (int neighbor : adj.get(node)) {
            if (!visited[neighbor]) {
                if (dfs(neighbor, node, visited)) return true;
            } else if (neighbor != parent) {
                // If visited and not the parent, it's a cycle
                return true;
            }
        }

        return false;
    }
}
```

---

## ✅ BFS-Based Cycle Detection

### 🔍 Approach

- For every unvisited node, run BFS.
    
- Store `(node, parent)` in queue.
    
- If a neighbor is visited and it's **not the parent**, then a cycle exists.
    

### ✅ Java Code – BFS

```java
import java.util.*;

public class CycleDetectionBFS {
    private final int V;
    private final List<List<Integer>> adj;

    public CycleDetectionBFS(int V) {
        this.V = V;
        adj = new ArrayList<>();
        for (int i = 0; i < V; i++)
            adj.add(new ArrayList<>());
    }

    public void addEdge(int u, int v) {
        adj.get(u).add(v);
        adj.get(v).add(u);
    }

    public boolean hasCycle() {
        boolean[] visited = new boolean[V];

        for (int i = 0; i < V; i++) {
            if (!visited[i]) {
                if (bfs(i, visited)) return true;
            }
        }

        return false;
    }

    private boolean bfs(int start, boolean[] visited) {
        Queue<int[]> queue = new LinkedList<>();
        queue.offer(new int[]{start, -1});
        visited[start] = true;

        while (!queue.isEmpty()) {
            int[] curr = queue.poll();
            int node = curr[0], parent = curr[1];

            for (int neighbor : adj.get(node)) {
                if (!visited[neighbor]) {
                    visited[neighbor] = true;
                    queue.offer(new int[]{neighbor, node});
                } else if (neighbor != parent) {
                    // Visited and not parent → cycle
                    return true;
                }
            }
        }

        return false;
    }
}
```

---

## ✅ Example Usage

```java
public class Main {
    public static void main(String[] args) {
        CycleDetectionDFS graphDFS = new CycleDetectionDFS(5);
        graphDFS.addEdge(0, 1);
        graphDFS.addEdge(1, 2);
        graphDFS.addEdge(2, 3);
        graphDFS.addEdge(3, 4);
        graphDFS.addEdge(4, 1); // cycle

        System.out.println("Cycle (DFS): " + graphDFS.hasCycle());

        CycleDetectionBFS graphBFS = new CycleDetectionBFS(5);
        graphBFS.addEdge(0, 1);
        graphBFS.addEdge(1, 2);
        graphBFS.addEdge(2, 3);
        graphBFS.addEdge(3, 4);
        graphBFS.addEdge(4, 1); // cycle

        System.out.println("Cycle (BFS): " + graphBFS.hasCycle());
    }
}
```

---

## ⏱️ Time and Space Complexity

Let `V` = number of vertices, `E` = number of edges

|Operation|DFS / BFS|
|---|---|
|Time Complexity|`O(V + E)`|
|Space Complexity|`O(V)` (for visited + call stack or queue)|

---

## 🧠 When to Use

- Use **DFS** when you’re okay with recursion and need quick detection.
    
- Use **BFS** when you prefer queue-based iterative control or need to process level-by-level (e.g., for shortest cycle).
    

---

Would you like cycle detection for **directed graphs**, or using **Disjoint Set (Union-Find)** as well?