Here’s the **Black Box Learning Breakdown for Graph Algorithms**, including **Java examples** and a structured approach.

---

# **Graph Algorithms – Black Box Learning Approach**

## **1. Input**

Graph algorithms work on **graphs**, which are represented as:

- **Adjacency List:** Best for sparse graphs (O(V + E) space).
- **Adjacency Matrix:** Best for dense graphs (O(V²) space).
- **Edge List:** Used in algorithms like Kruskal’s.

### **Example Input in Java (Graph Representation)**

```java
int[][] edges = {{0, 1}, {1, 2}, {2, 3}, {3, 0}};
```

---

## **2. Output**

- **Traversal order (BFS, DFS).**
- **Shortest path distances (Dijkstra, Bellman-Ford, Floyd-Warshall).**
- **Minimum Spanning Tree (Prim’s, Kruskal’s).**
- **Cycle detection in directed/undirected graphs.**

Example Output:

```java
System.out.println(shortestPath(graph, 0));  // Output: [0, 4, 7, 9]
```

---

## **3. Operations (Graph Algorithms Ranked by Complexity)**

|Algorithm|Example (Java)|Best Case|Average Case|Worst Case|Space Complexity|
|---|---|---|---|---|---|
|**Breadth-First Search (BFS)**|`bfs(graph, start);`|**O(1)**|**O(V + E)**|**O(V + E)**|**O(V)**|
|**Depth-First Search (DFS)**|`dfs(graph, start);`|**O(1)**|**O(V + E)**|**O(V + E)**|**O(V)**|
|**Dijkstra’s Algorithm**|`dijkstra(graph, src);`|**O(1)**|**O((V + E) log V)**|**O(V²)**|**O(V + E)**|
|**Bellman-Ford Algorithm**|`bellmanFord(graph, src);`|**O(1)**|**O(VE)**|**O(VE)**|**O(V)**|
|**Floyd-Warshall Algorithm**|`floydWarshall(graph);`|**O(1)**|**O(V³)**|**O(V³)**|**O(V²)**|
|**Kruskal’s Algorithm (MST)**|`kruskal(graph);`|**O(1)**|**O(E log E)**|**O(E log E)**|**O(V + E)**|
|**Prim’s Algorithm (MST)**|`prim(graph);`|**O(1)**|**O((V + E) log V)**|**O(V²)**|**O(V + E)**|

(_V = number of vertices, E = number of edges_)

---

## **4. Time and Space Complexities**

### **Time Complexity Summary**

|Algorithm|Best Case|Average Case|Worst Case|
|---|---|---|---|
|**BFS/DFS**|O(1)|O(V + E)|O(V + E)|
|**Dijkstra’s Algorithm**|O(1)|O((V + E) log V)|O(V²)|
|**Bellman-Ford Algorithm**|O(1)|O(VE)|O(VE)|
|**Floyd-Warshall Algorithm**|O(1)|O(V³)|O(V³)|
|**Kruskal’s Algorithm**|O(1)|O(E log E)|O(E log E)|
|**Prim’s Algorithm**|O(1)|O((V + E) log V)|O(V²)|

### **Space Complexity**

- **O(V + E) for BFS, DFS, Dijkstra (Adjacency List).**
- **O(V²) for Floyd-Warshall (Adjacency Matrix).**
- **O(V + E) for Kruskal’s (Union-Find).**

---

## **5. Use Cases (Problem Patterns)**

- **Graph Traversal:** BFS for shortest paths in unweighted graphs, DFS for cycle detection.
- **Shortest Path in Weighted Graphs:** Dijkstra for positive weights, Bellman-Ford for graphs with negative weights.
- **All-Pairs Shortest Paths:** Floyd-Warshall for small graphs.
- **Minimum Spanning Tree:** Kruskal and Prim for network design problems.
- **Cycle Detection:** DFS-based cycle detection for both directed and undirected graphs.

---

## **6. Problems in this Pattern**

### **Easy**

- BFS and DFS Traversal of a Graph
- Check if a Graph is Bipartite
- Find the Number of Connected Components

### **Medium**

- Shortest Path in a Weighted Graph (Dijkstra)
- Find a Minimum Spanning Tree (Kruskal’s or Prim’s)
- Detect a Cycle in a Directed Graph

### **Hard**

- Bellman-Ford Algorithm for Single Source Shortest Path
- Floyd-Warshall for All-Pairs Shortest Paths
- Traveling Salesman Problem (Graph DP)

---

## **7. Explore - Other Related Concepts**

- **Greedy Algorithms in Graphs:** Kruskal’s and Prim’s Algorithm.
- **Dynamic Programming on Graphs:** Floyd-Warshall, Bellman-Ford.
- **Graph Representation Trade-offs:** Adjacency List vs. Adjacency Matrix.
- **Flow Algorithms:** Ford-Fulkerson for maximum flow.
- **Topological Sorting:** Used for task scheduling in DAGs.

---

## **8. Code Implementations**

### **BFS (Graph Traversal)**

```java
import java.util.*;

class GraphBFS {
    static void bfs(Map<Integer, List<Integer>> graph, int start) {
        Queue<Integer> queue = new LinkedList<>();
        Set<Integer> visited = new HashSet<>();
        queue.offer(start);
        visited.add(start);

        while (!queue.isEmpty()) {
            int node = queue.poll();
            System.out.print(node + " ");
            for (int neighbor : graph.getOrDefault(node, new ArrayList<>())) {
                if (!visited.contains(neighbor)) {
                    queue.offer(neighbor);
                    visited.add(neighbor);
                }
            }
        }
    }

    public static void main(String[] args) {
        Map<Integer, List<Integer>> graph = new HashMap<>();
        graph.put(0, Arrays.asList(1, 2));
        graph.put(1, Arrays.asList(0, 3, 4));
        graph.put(2, Arrays.asList(0, 4));
        graph.put(3, Arrays.asList(1));
        graph.put(4, Arrays.asList(1, 2));

        bfs(graph, 0);  // Output: 0 1 2 3 4
    }
}
```

---

### **Dijkstra’s Algorithm (Shortest Path)**

```java
import java.util.*;

class Dijkstra {
    static int[] dijkstra(Map<Integer, List<int[]>> graph, int src, int V) {
        PriorityQueue<int[]> pq = new PriorityQueue<>(Comparator.comparingInt(a -> a[1]));
        int[] dist = new int[V];
        Arrays.fill(dist, Integer.MAX_VALUE);
        dist[src] = 0;
        pq.offer(new int[]{src, 0});

        while (!pq.isEmpty()) {
            int[] curr = pq.poll();
            int node = curr[0], cost = curr[1];

            if (cost > dist[node]) continue;

            for (int[] neighbor : graph.getOrDefault(node, new ArrayList<>())) {
                int nextNode = neighbor[0], edgeWeight = neighbor[1];
                if (dist[node] + edgeWeight < dist[nextNode]) {
                    dist[nextNode] = dist[node] + edgeWeight;
                    pq.offer(new int[]{nextNode, dist[nextNode]});
                }
            }
        }
        return dist;
    }

    public static void main(String[] args) {
        Map<Integer, List<int[]>> graph = new HashMap<>();
        graph.put(0, Arrays.asList(new int[]{1, 4}, new int[]{2, 7}));
        graph.put(1, Arrays.asList(new int[]{2, 1}, new int[]{3, 2}));
        graph.put(2, Arrays.asList(new int[]{3, 3}));

        System.out.println(Arrays.toString(dijkstra(graph, 0, 4)));  // Output: [0, 4, 5, 7]
    }
}
```

---

## **Conclusion**

By treating **Graph Algorithms as a black box**, we:  
✅ **Observed how input changes affect output.**  
✅ **Identified patterns in operations.**  
✅ **Implemented solutions before diving into deep theory.**

Would you like to continue with **Flow Algorithms (Ford-Fulkerson), Topological Sorting, or Graph DP next?**