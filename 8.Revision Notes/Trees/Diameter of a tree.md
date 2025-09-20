Here are **full notes** for **LeetCode 543 – Diameter of Binary Tree**, including definitions, approaches, Java code, and edge cases.

---

## 🌳 Problem: Diameter of Binary Tree

[LeetCode 543](https://leetcode.com/problems/diameter-of-binary-tree/)

### 🧾 Problem Statement

> Given the `root` of a binary tree, return the **length of the diameter** of the tree.
> 
> The **diameter** of a binary tree is the **length of the longest path between any two nodes**, measured in **number of edges**.

---

## ✅ Input and Output

### 🔹 Input:

A binary tree (root node)

### 🔹 Output:

An integer representing the **diameter** (number of **edges** on the longest path between any two nodes)

---

## 🔍 Key Observations

- The **diameter** does **not necessarily pass through the root**.
    
- At every node, the **diameter passing through it** is:
    
    ```
    left height + right height
    ```
    
- The answer is the **maximum** of all such diameters for each node.
    

---

## ✅ Approach: Post-order DFS (Recursive)

### 💡 Idea

At each node:

- Compute left height and right height recursively.
    
- Update the global maximum of `left + right` (current diameter).
    
- Return `1 + max(left, right)` for parent node’s height calculation.
    

---

## ✅ Java Code

```java
class TreeNode {
    int val;
    TreeNode left, right;
    TreeNode(int val) { this.val = val; }
}

public class DiameterBinaryTree {
    private int maxDiameter = 0;

    public int diameterOfBinaryTree(TreeNode root) {
        height(root);
        return maxDiameter;
    }

    private int height(TreeNode node) {
        if (node == null) return 0;

        int left = height(node.left);
        int right = height(node.right);

        // Update the maximum diameter
        maxDiameter = Math.max(maxDiameter, left + right);

        return 1 + Math.max(left, right);
    }
}
```

---

## 📊 Time and Space Complexity

|Metric|Complexity|
|---|---|
|Time|`O(n)` – each node is visited once|
|Space|`O(h)` – recursion stack (`h` = height of tree)|

---

## 🔁 Example

```text
Input:
       1
      / \
     2   3
    / \
   4   5

Longest path: 4 → 2 → 5 → 1 → 3  
Number of edges: 4

Output: 4
```

---

## 🧠 Intuition

- Every node contributes to:
    
    - A possible height to its parent
        
    - A candidate diameter: left height + right height
        
- We find all such candidate diameters and track the maximum.
    

---

## ⚠️ Common Mistakes

- **Returning the number of nodes instead of edges**: Remember, diameter is in **edges**.
    
- **Not updating diameter correctly**: Update only at current node as `left + right`, not `left + right + 1`.
    
- **Confusing depth and diameter**: Depth is from root to a leaf; diameter is the longest path between any two **nodes**.
    

---

## 🔄 Related Problems

|Problem|Description|
|---|---|
|[Maximum Depth of Binary Tree](https://leetcode.com/problems/maximum-depth-of-binary-tree/)|Return depth|
|[Balanced Binary Tree](https://leetcode.com/problems/balanced-binary-tree/)|Use height to check balance|
|[Longest Univalue Path](https://leetcode.com/problems/longest-univalue-path/)|Similar logic, with value check|
|[Diameter of N-ary Tree](https://leetcode.com/problems/diameter-of-n-ary-tree/)|Generalized for n children per node|

---

Would you like a **dry-run walkthrough** with visuals or a **variation with edge weights**?