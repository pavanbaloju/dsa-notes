
---

## ✅ Graph Using Adjacency List (Pre-initialized)

```java
import java.util.*;

public class GraphAdjList {

    private Map<Integer, List<Integer>> adjList;
    private int vertices;

    public GraphAdjList(int vertices) {
        this.vertices = vertices;
        adjList = new HashMap<>();

        // Initialize each node with an empty list
        for (int i = 0; i < vertices; i++) {
            adjList.put(i, new ArrayList<>());
        }
    }

    public void addEdge(int u, int v) {
        adjList.get(u).add(v);
        adjList.get(v).add(u); // Remove for directed graph
    }

    public void printGraph() {
        for (int node : adjList.keySet()) {
            System.out.print(node + " -> ");
            for (int neighbor : adjList.get(node)) {
                System.out.print(neighbor + " ");
            }
            System.out.println();
        }
    }

    public void bfs(int start) {
        Set<Integer> visited = new HashSet<>();
        Queue<Integer> queue = new LinkedList<>();
        queue.offer(start);
        visited.add(start);

        System.out.print("BFS: ");
        while (!queue.isEmpty()) {
            int node = queue.poll();
            System.out.print(node + " ");

            for (int neighbor : adjList.get(node)) {
                if (!visited.contains(neighbor)) {
                    queue.offer(neighbor);
                    visited.add(neighbor);
                }
            }
        }
        System.out.println();
    }

    public void dfs(int start) {
        Set<Integer> visited = new HashSet<>();
        System.out.print("DFS: ");
        dfsHelper(start, visited);
        System.out.println();
    }

    private void dfsHelper(int node, Set<Integer> visited) {
        visited.add(node);
        System.out.print(node + " ");

        for (int neighbor : adjList.get(node)) {
            if (!visited.contains(neighbor)) {
                dfsHelper(neighbor, visited);
            }
        }
    }

    public static void main(String[] args) {
        GraphAdjList graph = new GraphAdjList(5);

        graph.addEdge(0, 1);
        graph.addEdge(0, 2);
        graph.addEdge(1, 3);
        graph.addEdge(2, 4);

        graph.printGraph();
        graph.bfs(0);
        graph.dfs(0);
    }
}
```

---

### ✅ Benefits of Pre-initialization:

- Avoids repeated checks like `putIfAbsent()`.
    
- Clearer separation of **initialization** vs **mutation** logic.
    
- Fewer runtime errors when using `get(node)` directly.
    

Would you like a version with **directed** or **weighted** edges next?