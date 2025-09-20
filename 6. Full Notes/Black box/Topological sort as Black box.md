Here’s the **Black Box Learning Breakdown for Topological Sorting**, including **Java examples** and a structured approach.

---

# **Topological Sorting – Black Box Learning Approach**

## **1. Input**

Topological Sorting is a **linear ordering of vertices** in a **Directed Acyclic Graph (DAG)** such that **for every directed edge (u → v), u appears before v in the ordering**.

- **Input:** A **DAG (Directed Acyclic Graph)** represented using an **Adjacency List** or **Adjacency Matrix**.
- **Condition:** **Graph must be acyclic (no cycles).**
- **Output:** A **linear order** of vertices that respects dependencies.

### **Example Input in Java (Graph Representation)**

```java
int[][] edges = {{5, 0}, {5, 2}, {4, 0}, {4, 1}, {2, 3}, {3, 1}};
```

---

## **2. Output**

- **A valid order of tasks respecting dependencies.**
- **One possible valid ordering; multiple valid orderings may exist.**

Example Output:

```java
[5, 4, 2, 3, 1, 0]  // One valid topological order
```

---

## **3. Operations (Topological Sorting Techniques Ranked by Complexity)**

|Algorithm|Example (Java)|Best Case|Average Case|Worst Case|Space Complexity|
|---|---|---|---|---|---|
|**DFS-Based Topological Sort**|`topoSortDFS(graph);`|**O(1)**|**O(V + E)**|**O(V + E)**|**O(V + E)**|
|**Kahn’s Algorithm (BFS-Based)**|`topoSortBFS(graph);`|**O(1)**|**O(V + E)**|**O(V + E)**|**O(V + E)**|

(_V = number of vertices, E = number of edges_)

---

## **4. Time and Space Complexities**

### **Time Complexity Summary**

|Algorithm|Best Case|Average Case|Worst Case|
|---|---|---|---|
|**DFS-Based Topological Sort**|O(1)|O(V + E)|O(V + E)|
|**Kahn’s Algorithm (BFS-Based)**|O(1)|O(V + E)|O(V + E)|

### **Space Complexity**

- **O(V + E) for storing the graph in an adjacency list.**
- **O(V) for storing the topological order.**

---

## **5. Use Cases (Problem Patterns)**

- **Task Scheduling:** Dependencies between jobs, courses, or manufacturing steps.
- **Compilation Order of Modules:** Ensuring all dependencies are compiled before the dependent module.
- **Dependency Resolution:** Package management (e.g., resolving dependencies in a build system).
- **Order of Execution in Circuits:** Determining the sequence of steps in hardware logic gates.

---

## **6. Problems in this Pattern**

### **Easy**

- Find a Valid Topological Ordering of a DAG
- Check if a Graph is a DAG (Detect Cycles in a Directed Graph)

### **Medium**

- Course Schedule (Finding a Valid Course Order)
- Task Scheduling with Dependencies
- Minimum Time to Finish All Jobs (DAG with Weights)

### **Hard**

- Parallel Job Scheduling (Finding the Longest Path in a DAG)
- Order of Compilation in a Large Codebase
- Detecting Cyclic Dependencies in a Build System

---

## **7. Explore - Other Related Concepts**

- **Cycle Detection in Directed Graphs:** If a cycle exists, topological sorting is not possible.
- **Strongly Connected Components (SCCs):** Kosaraju’s and Tarjan’s Algorithm for component-based sorting.
- **Longest Path in a DAG:** Uses topological order for efficient computation.
- **Shortest Path in a DAG:** Faster than Dijkstra’s Algorithm using topological order.
- **Critical Path Method (CPM):** Project scheduling using DAGs.

---

## **8. Code Implementations**

### **DFS-Based Topological Sort**

```java
import java.util.*;

class TopoSortDFS {
    static void dfs(int node, Map<Integer, List<Integer>> graph, Set<Integer> visited, Stack<Integer> stack) {
        visited.add(node);
        for (int neighbor : graph.getOrDefault(node, new ArrayList<>())) {
            if (!visited.contains(neighbor)) {
                dfs(neighbor, graph, visited, stack);
            }
        }
        stack.push(node);  // Add to stack after visiting all neighbors
    }

    static List<Integer> topoSortDFS(Map<Integer, List<Integer>> graph, int V) {
        Stack<Integer> stack = new Stack<>();
        Set<Integer> visited = new HashSet<>();

        for (int i = 0; i < V; i++) {
            if (!visited.contains(i)) {
                dfs(i, graph, visited, stack);
            }
        }

        List<Integer> result = new ArrayList<>();
        while (!stack.isEmpty()) {
            result.add(stack.pop());
        }
        return result;
    }

    public static void main(String[] args) {
        Map<Integer, List<Integer>> graph = new HashMap<>();
        graph.put(5, Arrays.asList(0, 2));
        graph.put(4, Arrays.asList(0, 1));
        graph.put(2, Arrays.asList(3));
        graph.put(3, Arrays.asList(1));

        List<Integer> topoOrder = topoSortDFS(graph, 6);
        System.out.println(topoOrder); // Output: [5, 4, 2, 3, 1, 0] (or another valid order)
    }
}
```

---

### **Kahn’s Algorithm (BFS-Based Topological Sort)**

```java
import java.util.*;

class TopoSortBFS {
    static List<Integer> topoSortBFS(Map<Integer, List<Integer>> graph, int V) {
        int[] inDegree = new int[V];
        for (List<Integer> neighbors : graph.values()) {
            for (int neighbor : neighbors) {
                inDegree[neighbor]++;
            }
        }

        Queue<Integer> queue = new LinkedList<>();
        for (int i = 0; i < V; i++) {
            if (inDegree[i] == 0) {
                queue.offer(i);
            }
        }

        List<Integer> result = new ArrayList<>();
        while (!queue.isEmpty()) {
            int node = queue.poll();
            result.add(node);

            for (int neighbor : graph.getOrDefault(node, new ArrayList<>())) {
                if (--inDegree[neighbor] == 0) {
                    queue.offer(neighbor);
                }
            }
        }

        return result.size() == V ? result : new ArrayList<>(); // Return empty list if cycle exists
    }

    public static void main(String[] args) {
        Map<Integer, List<Integer>> graph = new HashMap<>();
        graph.put(5, Arrays.asList(0, 2));
        graph.put(4, Arrays.asList(0, 1));
        graph.put(2, Arrays.asList(3));
        graph.put(3, Arrays.asList(1));

        List<Integer> topoOrder = topoSortBFS(graph, 6);
        System.out.println(topoOrder); // Output: [5, 4, 2, 3, 1, 0] (or another valid order)
    }
}
```

---

## **Conclusion**

By treating **Topological Sorting as a black box**, we:  
✅ **Observed how input changes affect output.**  
✅ **Identified patterns in operations.**  
✅ **Implemented solutions before diving into deep theory.**

Would you like to continue with **Cycle Detection in Directed Graphs, Strongly Connected Components (SCCs), or DAG Shortest Path next?**