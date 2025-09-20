Here are the **full notes on Breadth-First Search (BFS) using Queue**, structured for clarity and practical use:

---

# 📘 BFS Using Queue – Full Notes (Java)

---

## ✅ What is BFS?

> **Breadth-First Search** (BFS) is a graph/tree traversal algorithm that explores all **neighbors** before going deeper.

- Traverses **level by level**
    
- Uses a **Queue** (FIFO) to manage the traversal
    
- Can be used on both **trees** and **graphs**
    

---

## 🧠 Intuition

Imagine you’re at a root node and want to visit everyone one step away from you before going further.  
This is exactly what BFS does: visit all nodes at **distance 1**, then **distance 2**, and so on.

---

## 🔁 Key Data Structure: Queue

- Queue ensures that **nodes are visited in the order they are discovered**
    
- In graphs, also maintain a **visited set** to avoid revisiting nodes
    

---

# ✅ BFS on a Binary Tree

### 📌 Java Code

```java
public void bfsBinaryTree(TreeNode root) {
    if (root == null) return;

    Queue<TreeNode> queue = new LinkedList<>();
    queue.offer(root);

    while (!queue.isEmpty()) {
        TreeNode current = queue.poll();
        System.out.print(current.val + " ");

        if (current.left != null) queue.offer(current.left);
        if (current.right != null) queue.offer(current.right);
    }
}
```

### 🧪 Sample Input

```text
        1
       / \
      2   3
     / \
    4   5
```

**Output:** `1 2 3 4 5`

---

# ✅ BFS on a Graph

### 📌 Java Code (Adjacency List)

```java
public void bfsGraph(int start, Map<Integer, List<Integer>> graph) {
    Set<Integer> visited = new HashSet<>();
    Queue<Integer> queue = new LinkedList<>();

    queue.offer(start);
    visited.add(start);

    while (!queue.isEmpty()) {
        int node = queue.poll();
        System.out.print(node + " ");

        for (int neighbor : graph.getOrDefault(node, new ArrayList<>())) {
            if (!visited.contains(neighbor)) {
                visited.add(neighbor);
                queue.offer(neighbor);
            }
        }
    }
}
```

### 🧪 Input Graph (Adjacency List)

```java
0: [1, 2]
1: [0, 3]
2: [0, 4]
3: [1]
4: [2]
```

Start from `0`, Output: `0 1 2 3 4`

---

## 📌 Level Order BFS (Tree/Graph with Levels)

```java
public List<List<Integer>> levelOrder(TreeNode root) {
    List<List<Integer>> result = new ArrayList<>();
    if (root == null) return result;

    Queue<TreeNode> queue = new LinkedList<>();
    queue.offer(root);

    while (!queue.isEmpty()) {
        int levelSize = queue.size();
        List<Integer> level = new ArrayList<>();

        for (int i = 0; i < levelSize; i++) {
            TreeNode node = queue.poll();
            level.add(node.val);

            if (node.left != null) queue.offer(node.left);
            if (node.right != null) queue.offer(node.right);
        }

        result.add(level);
    }

    return result;
}
```

---

## ⏱ Time & Space Complexity

|Operation|Time|Space|
|---|---|---|
|Tree BFS|O(n)|O(n)|
|Graph BFS|O(V + E)|O(V)|
|Level-order BFS|O(n)|O(n)|

---

## ⚠️ Edge Cases

|Scenario|What to handle|
|---|---|
|Disconnected Graph|Use BFS for each component|
|Cycles in Graph|Use `visited` to avoid infinite loop|
|Null Root (Tree)|Handle with null check|
|Empty Adjacency List|Default to empty list in `getOrDefault`|

---

## 🧠 BFS vs DFS

|Feature|BFS (Queue)|DFS (Stack / Recursion)|
|---|---|---|
|Traversal|Level-wise|Depth-wise|
|Space|May use more (queue)|May use less (stack)|
|Use Cases|Shortest path (unweighted), level-order|Cycle detection, Topo sort|

---

## 🔗 Common Problems Using BFS

|Problem|Type|
|---|---|
|Leetcode 102 – Binary Tree Level Order|BFS on Tree|
|Leetcode 994 – Rotting Oranges|BFS on Grid|
|Leetcode 200 – Number of Islands|BFS/DFS|
|Leetcode 752 – Open the Lock|BFS with states|
|Leetcode 286 – Walls and Gates|Multi-source BFS|

---

## ✅ Summary

|Concept|Key Point|
|---|---|
|Queue|Used for order-preserving traversal|
|Tree BFS|No visited set needed|
|Graph BFS|Always track visited nodes|
|Level Order|Track size of current level using loop|
|Complexity|Linear with respect to nodes/edges|

---

Would you like:

- A **grid BFS template** (for matrix-based problems)?
    
- A **multi-source BFS** template?
    
- A **BFS shortest path finder**?
    

Let me know and I’ll add those for you.