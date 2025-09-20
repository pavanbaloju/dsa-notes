Here are **complete, structured notes on "Floor and Ceil in a Binary Search Tree (BST)"**, suitable for interviews and system design reasoning.

---

## ✅ 1. Problem Definitions

### 🔹 Floor in BST:

The **floor** of a given key `x` in a BST is the **largest value** in the tree **less than or equal to `x`**.

> `floor(x) = max(node.val | node.val ≤ x)`

### 🔹 Ceil in BST:

The **ceil** of a key `x` is the **smallest value** in the tree **greater than or equal to `x`**.

> `ceil(x) = min(node.val | node.val ≥ x)`

---

## ✅ 2. Real-World Applications

- Finding closest pricing lower/higher than a target
    
- Memory allocators for size-fit logic
    
- Time-stamped data systems (find nearest available entry)
    
- Scheduling systems (closest available slot before/after)
    

---

## ✅ 3. BST Property Used

For any node:

- Left subtree has all values < node.val
    
- Right subtree has all values > node.val
    

This helps us traverse efficiently while narrowing down the range.

---

## ✅ 4. Approach and Logic

### 🔹 Floor:

1. Start from the root.
    
2. If `node.val == key`, return it (exact match).
    
3. If `node.val > key`, discard right side → move left.
    
4. If `node.val < key`, it's a **candidate floor** → store it, move right (to find closer values).
    

### 🔹 Ceil:

1. Start from the root.
    
2. If `node.val == key`, return it.
    
3. If `node.val < key`, discard left → move right.
    
4. If `node.val > key`, it's a **candidate ceil** → store it, move left.
    

---

## ✅ 5. Java Code with Comments

### 🔸 Floor in BST (Iterative)

```java
public int findFloor(TreeNode root, int key) {
    int floor = -1;
    while (root != null) {
        if (root.val == key) {
            return key;
        } else if (root.val > key) {
            root = root.left;
        } else {
            floor = root.val;       // candidate floor
            root = root.right;
        }
    }
    return floor;
}
```

### 🔸 Ceil in BST (Iterative)

```java
public int findCeil(TreeNode root, int key) {
    int ceil = -1;
    while (root != null) {
        if (root.val == key) {
            return key;
        } else if (root.val < key) {
            root = root.right;
        } else {
            ceil = root.val;       // candidate ceil
            root = root.left;
        }
    }
    return ceil;
}
```

---

## ✅ 6. Recursive Versions

### 🔸 Floor

```java
public int findFloor(TreeNode root, int key) {
    if (root == null) return -1;

    if (root.val == key) return root.val;
    if (root.val > key) return findFloor(root.left, key);

    int rightFloor = findFloor(root.right, key);
    return rightFloor != -1 ? rightFloor : root.val;
}
```

### 🔸 Ceil

```java
public int findCeil(TreeNode root, int key) {
    if (root == null) return -1;

    if (root.val == key) return root.val;
    if (root.val < key) return findCeil(root.right, key);

    int leftCeil = findCeil(root.left, key);
    return leftCeil != -1 ? leftCeil : root.val;
}
```

---

## ✅ 7. Time and Space Complexity

|Operation|Time Complexity|Space Complexity|
|---|---|---|
|Best Case|`O(log n)` (Balanced BST)|`O(1)` (iterative), `O(h)` recursive|
|Worst Case|`O(n)` (Skewed BST)|`O(h)` (stack space for recursion)|

---

## ✅ 8. Edge Cases

- Tree is empty → return `-1`
    
- Key < all node values → Floor = -1
    
- Key > all node values → Ceil = -1
    
- Key = node value → Floor & Ceil = key
    

---

## ✅ 9. Dry Run Example

### BST:

```
       8
     /   \
    4    12
   / \   / \
  2   6 10 14
```

### For `key = 5`:

- Floor = 4 (largest ≤ 5)
    
- Ceil = 6 (smallest ≥ 5)
    

---

## ✅ 10. Practice Problems

- [Leetcode 270. Closest Binary Search Tree Value](https://leetcode.com/problems/closest-binary-search-tree-value/)
    
- [GFG: Floor in BST](https://www.geeksforgeeks.org/floor-in-a-sorted-array/)
    
- Implement lower/upper bound in BST
    

---

## ✅ 11. Extensions / Variants

- Implement floor/ceil in **sorted arrays** using binary search (time: O(log n))
    
- Find closest value rather than strict floor/ceil
    
- Find both floor and ceil in one traversal
    
- Return node instead of value
    
- Range queries using floor/ceil to bound the range
    

---

Would you like a visual explanation or want to include this in your tree notes structure as well?