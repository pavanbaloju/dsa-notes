Here are the **full notes** on **Side Views of a Binary Tree** – including **left view**, **right view**, and their **BFS and DFS implementations** – with **time and space complexities** and real explanations.

---

## 🌲 What Are Side Views of a Binary Tree?

Side views are the **set of nodes visible when you view the binary tree from one side**.

---

### 📌 Types of Side Views:

|View|Description|
|---|---|
|**Left View**|First node you see at each level when viewing the tree from the left|
|**Right View**|Last node you see at each level when viewing the tree from the right|

---

## 🧠 Intuition

Each **level of the tree** may have multiple nodes, but:

- **Left view** keeps only the **first node from the left** at each level.
    
- **Right view** keeps only the **last node from the left** at each level.
    

This can be done using:

- **BFS** (Level-order traversal)
    
- **DFS** with level tracking
    

---

## ✅ Example

Consider the tree:

```
         1
       /   \
      2     3
       \   / \
        5 6   4
```

- **Left View**: `1 2 5`
    
- **Right View**: `1 3 4`
    

---

## ✅ BFS Approach (Level-Order Traversal)

### 🔧 Algorithm:

1. Use a queue to perform level-order traversal.
    
2. For each level:
    
    - For **left view**, add the first node (`i == 0`)
        
    - For **right view**, add the last node (`i == levelSize - 1`)
        

---

### ✅ Java Code: **Left View Using BFS**

```java
public List<Integer> leftView(TreeNode root) {
    List<Integer> result = new ArrayList<>();
    if (root == null) return result;

    Queue<TreeNode> queue = new LinkedList<>();
    queue.offer(root);

    while (!queue.isEmpty()) {
        int levelSize = queue.size();

        for (int i = 0; i < levelSize; i++) {
            TreeNode curr = queue.poll();

            if (i == 0) result.add(curr.val); // First node of each level

            if (curr.left != null) queue.offer(curr.left);
            if (curr.right != null) queue.offer(curr.right);
        }
    }

    return result;
}
```

---

### ✅ Java Code: **Right View Using BFS**

```java
public List<Integer> rightView(TreeNode root) {
    List<Integer> result = new ArrayList<>();
    if (root == null) return result;

    Queue<TreeNode> queue = new LinkedList<>();
    queue.offer(root);

    while (!queue.isEmpty()) {
        int levelSize = queue.size();

        for (int i = 0; i < levelSize; i++) {
            TreeNode curr = queue.poll();

            if (i == levelSize - 1) result.add(curr.val); // Last node of each level

            if (curr.left != null) queue.offer(curr.left);
            if (curr.right != null) queue.offer(curr.right);
        }
    }

    return result;
}
```

---

## ✅ DFS Approach (Recursive, Preorder with level tracking)

### 🔧 Key Insight:

- Use **preorder traversal**
    
- Track the **depth level** of recursion
    
- If `level == result.size()`, it’s the first node we’re visiting at that level
    

---

### ✅ Java Code: **Right View Using DFS**

```java
public List<Integer> rightView(TreeNode root) {
    List<Integer> result = new ArrayList<>();
    dfs(root, 0, result);
    return result;
}

private void dfs(TreeNode node, int level, List<Integer> result) {
    if (node == null) return;

    if (level == result.size()) {
        result.add(node.val);  // First node encountered at this level
    }

    dfs(node.right, level + 1, result); // right-first
    dfs(node.left, level + 1, result);
}
```

---

### ✅ Java Code: **Left View Using DFS**

```java
public List<Integer> leftView(TreeNode root) {
    List<Integer> result = new ArrayList<>();
    dfs(root, 0, result);
    return result;
}

private void dfs(TreeNode node, int level, List<Integer> result) {
    if (node == null) return;

    if (level == result.size()) {
        result.add(node.val);  // First node encountered at this level
    }

    dfs(node.left, level + 1, result); // left-first
    dfs(node.right, level + 1, result);
}
```

---

## 📊 Time & Space Complexity

|Approach|Time Complexity|Space Complexity|Notes|
|---|---|---|---|
|BFS|`O(N)`|`O(W)`|W = max width of tree (queue size)|
|DFS|`O(N)`|`O(H)`|H = height of tree (recursive call stack)|

Where `N` = number of nodes in the tree.

---

## 🧠 BFS vs DFS Tradeoffs

|Aspect|BFS|DFS|
|---|---|---|
|Side View|Easier to extract left/right node|Uses recursion + level tracking|
|Space|High if tree is wide (queue)|Low space if tree is narrow|
|Intuition|Level-by-level processing|Elegant control with recursion|

---

## 🔁 Summary Table

|Task|BFS Strategy|DFS Strategy|
|---|---|---|
|Left View|First node at each level|Left-first DFS|
|Right View|Last node at each level|Right-first DFS|

---

## 📌 Practice Problems

- Leetcode 199. **Binary Tree Right Side View**
    
- Leetcode 102. **Binary Tree Level Order Traversal**
    
- Leetcode 94. **Binary Tree Inorder Traversal**
    

---

Would you like similar notes on **Top View**, **Bottom View**, or **Vertical Order** next?