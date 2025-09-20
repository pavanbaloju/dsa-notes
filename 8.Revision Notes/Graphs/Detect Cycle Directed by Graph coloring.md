### ✅ Cycle Detection Using Graph Coloring (Directed Graphs Only)

This method is **specifically for detecting cycles in **_Directed Graphs_** using a modified DFS traversal with coloring of nodes.

---

## 🧠 Core Idea

In this method, each node is assigned one of **three colors** during DFS:

|Color|Meaning|
|---|---|
|**0**|White: Node **not visited yet**|
|**1**|Gray: Node **is being visited** (in recursion stack)|
|**2**|Black: Node and its descendants are **fully processed**|

### 🔁 How It Detects Cycles:

- If during DFS you encounter a **gray node** again → you have a **back edge** → **cycle exists**.
    

---

## ✅ Example Scenario

```
Graph:
0 → 1 → 2
↑         ↓
←-------- 3

This has a cycle: 0 → 1 → 2 → 3 → 0
```

---

## ✅ Java Code with Comments

```java
public class CycleDetectionColoring {
    public boolean hasCycle(int[][] adjList) {
        int n = adjList.length;
        int[] color = new int[n]; // 0 = white, 1 = gray, 2 = black

        for (int i = 0; i < n; i++) {
            if (color[i] == 0) { // unvisited
                if (dfs(i, adjList, color)) return true;
            }
        }

        return false;
    }

    private boolean dfs(int node, int[][] adjList, int[] color) {
        color[node] = 1; // mark gray (visiting)

        for (int neighbor : adjList[node]) {
            if (color[neighbor] == 1) {
                // Found a back edge → cycle exists
                return true;
            }
            if (color[neighbor] == 0) {
                if (dfs(neighbor, adjList, color)) return true;
            }
        }

        color[node] = 2; // mark black (fully visited)
        return false;
    }
}
```

---

## ✅ Input Format

Each `adjList[i]` contains the list of nodes `i` points to:

```java
int[][] graph = {
    {1},     // 0 → 1
    {2},     // 1 → 2
    {3},     // 2 → 3
    {0}      // 3 → 0 → cycle!
};
```

---

## ⏱ Time and Space Complexity

- **Time:** `O(V + E)` — every node and edge is visited once.
    
- **Space:** `O(V)` for recursion + coloring array.
    

---

## ✅ Why Graph Coloring Works for Cycle Detection (Directed Only)?

- It tracks nodes **currently being visited**.
    
- A back edge (gray → gray) means you're visiting a node that’s already in the path → forms a **cycle**.
    
- Once fully explored, mark as black (can’t form a cycle anymore through that path).
    

---

## 🚫 Not for Undirected Graphs

In undirected graphs, **gray → gray** might just be the parent node, not a back edge. So this method gives false positives unless carefully handled. Instead, use:

- **DFS with parent tracking**, or
    
- **Union-Find** method for cycle detection in undirected graphs.
    

---

## ✅ Summary

| Graph Type | Works? | Better Method                  |
| ---------- | ------ | ------------------------------ |
| Directed   | ✅ Yes  | Graph Coloring via DFS         |
| Undirected | ❌ No   | Use DFS + parent or Union-Find |

---

Would you like a visualization of how the colors work during DFS?  
Or shall I give LeetCode/GeeksforGeeks practice problems for this pattern?