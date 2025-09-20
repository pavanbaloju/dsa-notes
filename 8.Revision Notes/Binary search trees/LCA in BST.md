Here are **complete notes on Lowest Common Ancestor (LCA) in a Binary Search Tree (BST)** – ideal for coding interviews, DSA prep, and system design applications.

---

## ✅ 1. Problem Definition

**Given:** A Binary Search Tree (BST) and two nodes `p` and `q`.

**Goal:** Find the **lowest common ancestor (LCA)** of the two nodes.  
The LCA is the **deepest node** that is an **ancestor of both `p` and `q`**.

---

## ✅ 2. BST Properties to Leverage

- Left Subtree < Root < Right Subtree
    
- This order allows **directional search** using values.
    

---

## ✅ 3. Intuition

- **If both p and q < root** → LCA lies in left subtree
    
- **If both p and q > root** → LCA lies in right subtree
    
- **Else** (split happens) → `root` is the LCA
    

> The split point where `p` and `q` go into different branches (or one matches root) is the LCA.

---

## ✅ 4. Approach 1: Recursive (Optimal for BST)

```java
public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
    if (root == null) return null;

    if (p.val < root.val && q.val < root.val)
        return lowestCommonAncestor(root.left, p, q);
    else if (p.val > root.val && q.val > root.val)
        return lowestCommonAncestor(root.right, p, q);
    else
        return root;
}
```

### Time: O(h)

Where `h` is the height of the tree.

- `O(log n)` for balanced BST
    
- `O(n)` for skewed BST
    

### Space: O(h)

Due to recursion stack

---

## ✅ 5. Approach 2: Iterative

```java
public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
    while (root != null) {
        if (p.val < root.val && q.val < root.val)
            root = root.left;
        else if (p.val > root.val && q.val > root.val)
            root = root.right;
        else
            return root;
    }
    return null;
}
```

### Time: O(h)

### Space: O(1)

> **Preferred in system design or iterative-only environments.**

---

## ✅ 6. Dry Run Example

### BST:

```
        6
      /   \
     2     8
    / \   / \
   0   4 7   9
      / \
     3   5
```

**Input:** `p = 2`, `q = 8`  
**Output:** `6`

**Input:** `p = 2`, `q = 4`  
**Output:** `2`

---

## ✅ 7. Edge Cases

- One node is ancestor of the other → return ancestor
    
- One or both nodes not present → depends on contract (often assume always present)
    
- BST is skewed → still works
    

---

## ✅ 8. Difference from LCA in Binary Tree

|Feature|LCA in **BST**|LCA in **Binary Tree**|
|---|---|---|
|Leverages order?|✅ Yes|❌ No|
|Time (best case)|O(log n)|O(n)|
|Approach|Traverse using values|DFS both subtrees|
|Simpler logic|✅|❌|

---

## ✅ 9. Follow-up Variants

- Find LCA of multiple nodes
    
- Find distance between `p` and `q` in BST
    
- Count nodes between `p` and `q` using LCA
    
- Convert logic to support **non-BST** trees
    

---

## ✅ 10. Related Problems

|Problem|Platform|
|---|---|
|[LCA in BST](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-search-tree/)|LeetCode 235|
|[LCA in Binary Tree](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree/)|LeetCode 236|
|[LCA for Deepest Leaves](https://leetcode.com/problems/lowest-common-ancestor-of-deepest-leaves/)|LeetCode 1123|
|[Distance Between Two Nodes](https://www.geeksforgeeks.org/find-distance-between-two-nodes-of-a-binary-tree/)|GFG|

---

## ✅ 11. System Design Insight

In distributed systems:

- LCA logic is used to compute nearest common supervisor / manager in org trees
    
- Hierarchical memory cache or directory tree conflict resolution
    
- Used in **ACL / Permission Trees** (e.g., Git file trees)
    

---

Would you like the **LCA in Binary Tree** notes next, or a **visual reference** diagram for this one?