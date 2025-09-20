Here is the **updated Java code** for an **undirected, unweighted graph using Adjacency Matrix** with both **BFS** and **DFS** traversal methods added.

---

### ✅ `GraphMatrix` with BFS and DFS

```java
import java.util.*;

public class GraphMatrix {
    private final int[][] adjMatrix;
    private final int V;

    public GraphMatrix(int V) {
        this.V = V;
        adjMatrix = new int[V][V];
    }

    // Add an undirected edge
    public void addEdge(int u, int v) {
        adjMatrix[u][v] = 1;
        adjMatrix[v][u] = 1;
    }

    // Remove an undirected edge
    public void removeEdge(int u, int v) {
        adjMatrix[u][v] = 0;
        adjMatrix[v][u] = 0;
    }

    public boolean isEdge(int u, int v) {
        return adjMatrix[u][v] == 1;
    }

    // Print all neighbors of each node
    public void printGraph() {
        System.out.println("Adjacency Matrix:");
        for (int i = 0; i < V; i++) {
            System.out.print(i + ": ");
            for (int j = 0; j < V; j++) {
                if (adjMatrix[i][j] == 1) {
                    System.out.print(j + " ");
                }
            }
            System.out.println();
        }
    }

    // ✅ Breadth-First Search (BFS)
    public void bfs(int start) {
        boolean[] visited = new boolean[V];
        Queue<Integer> queue = new LinkedList<>();

        visited[start] = true;
        queue.offer(start);

        System.out.print("BFS: ");
        while (!queue.isEmpty()) {
            int current = queue.poll();
            System.out.print(current + " ");

            for (int neighbor = 0; neighbor < V; neighbor++) {
                if (adjMatrix[current][neighbor] == 1 && !visited[neighbor]) {
                    visited[neighbor] = true;
                    queue.offer(neighbor);
                }
            }
        }
        System.out.println();
    }

    // ✅ Depth-First Search (DFS)
    public void dfs(int start) {
        boolean[] visited = new boolean[V];
        System.out.print("DFS: ");
        dfsHelper(start, visited);
        System.out.println();
    }

    private void dfsHelper(int current, boolean[] visited) {
        visited[current] = true;
        System.out.print(current + " ");

        for (int neighbor = 0; neighbor < V; neighbor++) {
            if (adjMatrix[current][neighbor] == 1 && !visited[neighbor]) {
                dfsHelper(neighbor, visited);
            }
        }
    }
}
```

---

### ✅ Example Usage:

```java
public class Main {
    public static void main(String[] args) {
        GraphMatrix g = new GraphMatrix(5);
        g.addEdge(0, 1);
        g.addEdge(0, 4);
        g.addEdge(1, 2);
        g.addEdge(1, 3);
        g.addEdge(2, 3);
        g.addEdge(3, 4);

        g.printGraph();

        g.bfs(0); // Output: BFS: 0 1 4 2 3
        g.dfs(0); // Output: DFS: 0 1 2 3 4
    }
}
```

---

### 📌 Notes:

- BFS uses a **queue** and visits all nodes level by level.
    
- DFS uses **recursion (stack)** and goes deep before backtracking.
    
- Both traverse **O(V + E)** in general, but since this is an adjacency matrix, checking neighbors is **O(V)** per node, so worst case is **O(V²)**.
    

Would you like the same implemented for **directed or weighted graphs** too?