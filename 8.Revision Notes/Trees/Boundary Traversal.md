Here are **full notes on Boundary Traversal** of a binary tree — a classic problem that tests your understanding of tree structure and traversal patterns.

---

## 🌳 Problem: **Boundary Traversal of Binary Tree**

### 📘 Statement:

You are given a binary tree. Print its boundary (anti-clockwise direction), i.e.,

1. **Left boundary** (excluding leaf nodes)
    
2. **All leaf nodes** (left to right)
    
3. **Right boundary** (excluding leaf nodes, printed bottom-up)
    

---

## 🔁 Example

Given:

```
        1
       / \
      2   3
     / \   \
    4   5   6
       / \
      7   8
```

### ✅ Output:

```
1 2 4 7 8 6 3
```

### ✅ Explanation:

- Left Boundary: `1 2 4`
    
- Leaf Nodes: `4 7 8 6`
    
- Right Boundary: `3` (bottom-up)
    

> We do **not** include duplicate nodes in the boundary.

---

## ✅ High-Level Steps

### 1. Add the **root**

- Always part of the boundary.
    

### 2. Add the **left boundary** (excluding leaves)

- Move left as much as possible
    
- Stop before leaf nodes
    

### 3. Add all **leaf nodes**

- From **left to right**
    
- Include leaves from both subtrees
    

### 4. Add the **right boundary** (excluding leaves)

- Move right as much as possible
    
- Stop before leaf nodes
    
- **Reverse** the order before adding to the result
    

---

## ✅ Java Code

```java
class TreeNode {
    int val;
    TreeNode left, right;
    TreeNode(int x) { val = x; }
}

public class BoundaryTraversal {

    public List<Integer> boundaryOfBinaryTree(TreeNode root) {
        List<Integer> result = new ArrayList<>();
        if (root == null) return result;

        if (!isLeaf(root)) result.add(root.val);

        addLeftBoundary(root.left, result);
        addLeaves(root, result);
        addRightBoundary(root.right, result);

        return result;
    }

    private boolean isLeaf(TreeNode node) {
        return node.left == null && node.right == null;
    }

    private void addLeftBoundary(TreeNode node, List<Integer> result) {
        while (node != null) {
            if (!isLeaf(node)) result.add(node.val);
            node = (node.left != null) ? node.left : node.right;
        }
    }

    private void addLeaves(TreeNode node, List<Integer> result) {
        if (node == null) return;

        if (isLeaf(node)) {
            result.add(node.val);
            return;
        }

        addLeaves(node.left, result);
        addLeaves(node.right, result);
    }

    private void addRightBoundary(TreeNode node, List<Integer> result) {
        Stack<Integer> temp = new Stack<>();
        while (node != null) {
            if (!isLeaf(node)) temp.push(node.val);
            node = (node.right != null) ? node.right : node.left;
        }

        while (!temp.isEmpty()) {
            result.add(temp.pop());
        }
    }
}
```

---

## 🧠 Dry Run (with Example Tree)

Given:

```
        1
       / \
      2   3
     / \   \
    4   5   6
       / \
      7   8
```

- **Left Boundary**: `2 → 4` (stop at 4 because it's a leaf)
    
- **Leaves**: `4 7 8 6`
    
- **Right Boundary** (reverse): `3`
    

Output: `1 2 4 7 8 6 3`

---

## 📊 Time and Space Complexity

|Metric|Value|
|---|---|
|Time|O(n) – visit each node once|
|Space|O(h) recursion stack for DFS on leaves (h = height)|

---

## 🔍 Edge Cases

- Tree with only one node → output is root
    
- All nodes only in left/right → linear traversal
    
- Don't include the **same leaf twice** in both boundaries and leaves
    

---

## 🧪 Test Cases

### Test 1

```java
Input: [1,null,2,3]
Output: [1,3,2]
```

### Test 2

```java
Input: [1]
Output: [1]
```

### Test 3

```java
Input: [1,2,3,4,5,6,null,null,null,7,8]
Output: [1,2,4,7,8,6,3]
```

---

## 🧾 Summary

- Root → Left Boundary → Leaves → Right Boundary (bottom-up)
    
- Handle corner cases (no left, no right, only root)
    
- Avoid adding leaves twice
    

---

Would you like a **diagram-based explanation**, or **code in Python/C++** too?