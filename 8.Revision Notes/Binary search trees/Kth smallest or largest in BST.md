Here are **complete and structured notes on “Kth Smallest and Kth Largest Element in a BST”** — optimized for interviews, coding rounds, and system design discussions.

---

## ✅ 1. Problem Definition

### 🔹 Kth Smallest in BST:

> Return the **kth smallest** element in a Binary Search Tree.

### 🔹 Kth Largest in BST:

> Return the **kth largest** element in a Binary Search Tree.

---

## ✅ 2. Key Insight: Inorder Traversal

- **Inorder Traversal of BST** gives **sorted order** (ascending).
    
    - `Left → Root → Right`
        
- **Reverse Inorder Traversal** gives **descending order**.
    
    - `Right → Root → Left`
        

Hence:

- **Kth Smallest = kth element in inorder traversal**
    
- **Kth Largest = kth element in reverse inorder traversal**
    

---

## ✅ 3. Use Cases

- Find nth best/worst price, score, or timestamp
    
- Implement leaderboard or high-score tracking
    
- Efficient rank-based operations
    

---

## ✅ 4. Approaches

### 🟢 A. Inorder Traversal (Recursive)

#### 🔸 Kth Smallest

```java
int count = 0;
int result = -1;

public int kthSmallest(TreeNode root, int k) {
    inorder(root, k);
    return result;
}

private void inorder(TreeNode node, int k) {
    if (node == null) return;

    inorder(node.left, k);

    count++;
    if (count == k) {
        result = node.val;
        return;
    }

    inorder(node.right, k);
}
```

#### 🔸 Kth Largest

```java
int count = 0;
int result = -1;

public int kthLargest(TreeNode root, int k) {
    reverseInorder(root, k);
    return result;
}

private void reverseInorder(TreeNode node, int k) {
    if (node == null) return;

    reverseInorder(node.right, k);

    count++;
    if (count == k) {
        result = node.val;
        return;
    }

    reverseInorder(node.left, k);
}
```

---

### 🟡 B. Iterative Inorder Traversal (No Recursion)

#### Kth Smallest

```java
public int kthSmallest(TreeNode root, int k) {
    Stack<TreeNode> stack = new Stack<>();

    while (true) {
        while (root != null) {
            stack.push(root);
            root = root.left;
        }

        root = stack.pop();
        if (--k == 0) return root.val;
        root = root.right;
    }
}
```

---

### 🔴 C. Augmented BST (With Node Count) — Advanced

Use a modified BST where each node stores:

- `leftSubtreeSize`
    
- Enables `O(log n)` search for Kth element
    

```java
class TreeNode {
    int val;
    TreeNode left, right;
    int leftCount; // nodes in left subtree
}
```

Time Complexity: `O(log n)` for balanced BST  
Space Complexity: `O(1)`  
**Used in Order Statistic Tree or Treaps**

---

## ✅ 5. Time and Space Complexity

|Approach|Time|Space (Auxiliary)|
|---|---|---|
|Inorder Recursive|O(k + h)|O(h)|
|Inorder Iterative|O(k + h)|O(h)|
|Augmented BST|O(log n)|O(1)|

Where `h` is the height of the BST (`O(log n)` if balanced, `O(n)` if skewed)

---

## ✅ 6. Dry Run Example

### BST:

```
       5
     /   \
    3     8
   / \   / \
  2  4  6  10
```

**Inorder**: 2, 3, 4, 5, 6, 8, 10

- 1st smallest → 2
    
- 3rd smallest → 4
    
- 6th smallest → 8
    
- 2nd largest → 8
    
- 1st largest → 10
    

---

## ✅ 7. Edge Cases

- Tree is empty → return -1 or throw exception
    
- `k` is larger than total nodes → return -1 or error
    
- Duplicate values → still valid; BST allows duplicates on either side (if implemented)
    

---

## ✅ 8. Follow-up Questions

- Modify BST insert/delete to maintain subtree sizes
    
- Use self-balancing trees (e.g., AVL, Red-Black Trees) with order-statistics
    
- Find the **rank of a given node** (inverse problem)
    
- Stream of integers → find kth largest so far (Min Heap)
    

---

## ✅ 9. Related Problems

|Problem|Platform|
|---|---|
|[Kth Smallest in BST](https://leetcode.com/problems/kth-smallest-element-in-a-bst/)|LeetCode 230|
|[Kth Largest in BST](https://practice.geeksforgeeks.org/problems/kth-largest-element-in-bst/1)|GFG|
|[Kth Largest in Stream](https://leetcode.com/problems/kth-largest-element-in-a-stream/)|LeetCode 703|
|[Median in BST](https://www.geeksforgeeks.org/find-median-bst-time-o1-space/)|GFG|

---

## ✅ 10. System Design Insight

In large-scale systems:

- BST with augmented metadata (size, rank, frequency)
    
- May offload Kth queries to background cache or pre-compute top K
    
- Combine with **Segment Trees** or **Treaps** for faster dynamic updates
    

---

Would you like this added into your BST notes summary? Or do you want combined notes for all types of "Kth" element problems (arrays, heaps, trees)?