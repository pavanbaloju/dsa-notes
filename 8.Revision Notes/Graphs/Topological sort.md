Here are **full notes on Topological Sort** including explanation, approaches (DFS and BFS), implementation in Java with comments, and time/space complexity:

---

## ✅ What is Topological Sort?

Topological sort of a **Directed Acyclic Graph (DAG)** is a linear ordering of its vertices such that for every directed edge `u → v`, vertex `u` comes before `v` in the ordering.

> **Applies only to DAGs**.  
> Used in scheduling, build systems, course prerequisite resolution, etc.

---

## ✅ Properties

- Only valid for **Directed Acyclic Graphs (DAGs)**
    
- A graph can have **multiple valid topological orderings**
    
- If a cycle exists → **no valid topological sort**
    

---

## ✅ Use Cases

- Build system dependencies (build module A before B)
    
- Course scheduling
    
- Task scheduling with precedence
    
- Compilation order
    

---

## ✅ Approaches

### 🔹 1. **DFS-based Topological Sort**

**Intuition**: Do a DFS from each node. Once a node has finished visiting all its neighbors, add it to a stack. Reverse the stack to get the topological order.

#### 📌 Key Idea:

- When DFS finishes for a node, all nodes depending on it are already added.
    
- So you can safely place it later in the order.
    

#### ✅ Java Code (DFS-based):

```java
import java.util.*;

public class TopoSortDFS {
    public List<Integer> topoSort(int V, List<List<Integer>> adj) {
        boolean[] visited = new boolean[V];
        Stack<Integer> stack = new Stack<>();

        for (int i = 0; i < V; i++) {
            if (!visited[i]) {
                dfs(i, visited, stack, adj);
            }
        }

        List<Integer> result = new ArrayList<>();
        while (!stack.isEmpty()) {
            result.add(stack.pop()); // reverse order
        }

        return result;
    }

    private void dfs(int node, boolean[] visited, Stack<Integer> stack, List<List<Integer>> adj) {
        visited[node] = true;

        for (int neighbor : adj.get(node)) {
            if (!visited[neighbor]) {
                dfs(neighbor, visited, stack, adj);
            }
        }

        stack.push(node); // add to stack after all descendants are visited
    }
}
```

#### ⏱️ Time Complexity:

- `O(V + E)`
    

#### 🧠 Space Complexity:

- `O(V)` for visited + stack
    

---

### 🔹 2. **BFS-based (Kahn's Algorithm)**

**Intuition**: In topological order, always place a node with `indegree == 0` (i.e., no dependencies left).

#### 📌 Steps:

1. Compute indegree of each node
    
2. Add all nodes with `indegree = 0` to a queue
    
3. While queue is not empty:
    
    - Remove node, add it to result
        
    - For each neighbor, reduce indegree
        
    - If any neighbor’s indegree becomes 0, add to queue
        
4. If result contains all nodes → valid topological sort
    
    - Else → cycle exists
        

#### ✅ Java Code (Kahn's Algorithm):

```java
import java.util.*;

public class TopoSortKahn {
    public List<Integer> topoSort(int V, List<List<Integer>> adj) {
        int[] indegree = new int[V];

        // Compute indegrees
        for (int u = 0; u < V; u++) {
            for (int v : adj.get(u)) {
                indegree[v]++;
            }
        }

        Queue<Integer> queue = new LinkedList<>();
        for (int i = 0; i < V; i++) {
            if (indegree[i] == 0) {
                queue.add(i);
            }
        }

        List<Integer> result = new ArrayList<>();

        while (!queue.isEmpty()) {
            int node = queue.poll();
            result.add(node);

            for (int neighbor : adj.get(node)) {
                indegree[neighbor]--;
                if (indegree[neighbor] == 0) {
                    queue.add(neighbor);
                }
            }
        }

        // Check for cycle
        if (result.size() != V) {
            throw new RuntimeException("Cycle detected — topological sort not possible.");
        }

        return result;
    }
}
```

#### ⏱️ Time Complexity:

- `O(V + E)`
    

#### 🧠 Space Complexity:

- `O(V)` for indegree array and queue
    

---

## 🔄 DFS vs BFS (Kahn’s Algorithm)

|Feature|DFS-Based|BFS-Based (Kahn's)|
|---|---|---|
|Order Mechanism|Post-order stack|Indegree + queue|
|Detects cycle|❌ (need extra logic)|✅ Easily (via count check)|
|Recursive|✅|❌ Iterative|
|Space|Stack + visited|Indegree array + queue|

---

## 🧠 When to Use What?

- Use **DFS** when recursion is more intuitive, or you already have a recursive framework.
    
- Use **Kahn’s Algorithm** when:
    
    - You want to **detect cycle** while sorting.
        
    - You prefer **iterative solutions**.
        

---

## ✅ Sample Input Graph

```
Vertices: 6
Edges:
0 → 1  
0 → 2  
1 → 3  
2 → 3  
4 → 5
```

Possible topological sorts:

- `0 2 1 3 4 5`
    
- `0 1 2 3 4 5`
    
- `4 5 0 2 1 3` etc.
    

---

## ❗Edge Case

- If the graph contains a **cycle**, no topological order exists.
    
    - Kahn’s algorithm will detect it.
        
    - DFS must be extended with a `recStack[]` to detect cycles.
        

---

Let me know if you'd like:

- Cycle detection added to DFS version
    
- Visual diagrams or dry run
    
- Practice problems or LeetCode links