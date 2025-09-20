Here are **full notes** on calculating the **Height / Depth of a Binary Tree**, including definitions, recursive and iterative approaches, time complexities, and Java code.

---

## 🌳 Binary Tree: Height vs Depth

### 📌 Definitions

|Term|Meaning|
|---|---|
|**Height of a node**|The number of edges on the longest path from the node to a **leaf**.|
|**Height of the tree**|Height of the **root** node.|
|**Depth of a node**|The number of edges from the **root** to that node.|
|**Depth of tree**|Depth of the **deepest leaf** (same as height of tree).|

> ✅ So, **height of a tree = depth of the deepest node**

---

## ✅ Recursive Approach

### 🔧 Logic

The height of a node =  
`1 + max(height of left subtree, height of right subtree)`

For null nodes (base case), height is `0`.

### 💡 Tree Height Formula

```java
int height(TreeNode root) {
    if (root == null) return 0;
    return 1 + Math.max(height(root.left), height(root.right));
}
```

---

### ✅ Java Code (Recursive)

```java
class TreeNode {
    int val;
    TreeNode left, right;
    TreeNode(int val) {
        this.val = val;
    }
}

public class TreeHeight {
    public static int height(TreeNode root) {
        if (root == null) return 0;
        return 1 + Math.max(height(root.left), height(root.right));
    }
}
```

---

## ✅ Iterative (Level Order / BFS)

We can also use **Breadth-First Search** to calculate height.  
Each level processed in the queue increases the depth.

### ✅ Java Code (Iterative)

```java
public static int height(TreeNode root) {
    if (root == null) return 0;

    Queue<TreeNode> queue = new LinkedList<>();
    queue.offer(root);
    int height = 0;

    while (!queue.isEmpty()) {
        int size = queue.size(); // number of nodes in current level
        for (int i = 0; i < size; i++) {
            TreeNode curr = queue.poll();
            if (curr.left != null) queue.offer(curr.left);
            if (curr.right != null) queue.offer(curr.right);
        }
        height++; // completed one level
    }

    return height;
}
```

---

## ✅ Time and Space Complexity

|Approach|Time|Space|
|---|---|---|
|Recursive|`O(n)`|`O(h)` → height of the tree (call stack)|
|Iterative|`O(n)`|`O(w)` → width of the tree (queue)|

---

## 🧠 Practice Problems

|Problem|Difficulty|
|---|---|
|[Maximum Depth of Binary Tree – LeetCode #104](https://leetcode.com/problems/maximum-depth-of-binary-tree/)|Easy|
|[Minimum Depth of Binary Tree – LeetCode #111](https://leetcode.com/problems/minimum-depth-of-binary-tree/)|Easy|
|[Diameter of Binary Tree – LeetCode #543](https://leetcode.com/problems/diameter-of-binary-tree/)|Easy|
|[Balanced Binary Tree – LeetCode #110](https://leetcode.com/problems/balanced-binary-tree/)|Easy|

---

## 🧭 Notes

- **Height of leaf node** = 0
    
- **Depth of root** = 0
    
- In interview questions, when asked for **height**, assume **height of tree** (from root to deepest leaf).
    
- Use **level-order traversal** when you want shortest depth (e.g., for finding minimum depth).
    

---

Would you like a diagram explanation or examples with dry-run?