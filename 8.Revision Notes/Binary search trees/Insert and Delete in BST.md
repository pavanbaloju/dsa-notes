Here are **complete notes on Insert and Delete operations in a Binary Search Tree (BST)**, including Java code, step-by-step logic, edge cases, and time/space complexities.

---

## ✅ 1. INSERT in BST

### 🔹 Problem Statement

Given the root of a BST and a value `val`, insert the value into the BST such that the resulting tree remains a valid BST. Return the root of the BST after insertion.

---

### 🔹 Intuition

- Use **BST property**:
    
    - If `val < root.val`: go left.
        
    - If `val > root.val`: go right.
        
- Insert when you hit `null`.
    

---

### ✅ Java Code – Recursive

```java
public TreeNode insertIntoBST(TreeNode root, int val) {
    if (root == null) {
        return new TreeNode(val);
    }
    if (val < root.val) {
        root.left = insertIntoBST(root.left, val);
    } else {
        root.right = insertIntoBST(root.right, val);
    }
    return root;
}
```

---

### ✅ Java Code – Iterative

```java
public TreeNode insertIntoBST(TreeNode root, int val) {
    if (root == null) return new TreeNode(val);

    TreeNode curr = root;
    while (true) {
        if (val < curr.val) {
            if (curr.left == null) {
                curr.left = new TreeNode(val);
                break;
            }
            curr = curr.left;
        } else {
            if (curr.right == null) {
                curr.right = new TreeNode(val);
                break;
            }
            curr = curr.right;
        }
    }
    return root;
}
```

---

### 🔹 Time and Space Complexity

- **Time:** O(h) → height of the tree
    
- **Space:**
    
    - Recursive → O(h) (stack)
        
    - Iterative → O(1)
        

---

## ✅ 2. DELETE from BST

### 🔹 Problem Statement

Given the root of a BST and a key, delete the node with that value and return the new root.

---

### 🔹 Deletion Cases

There are **3 cases** when deleting a node:

1. **No children (leaf)** → Just remove the node.
    
2. **One child** → Replace the node with its child.
    
3. **Two children** →
    
    - Find **inorder successor** (smallest node in right subtree)
        
    - Replace current node's value with successor's value
        
    - Recursively delete the successor node
        

---

### ✅ Java Code

```java
public TreeNode deleteNode(TreeNode root, int key) {
    if (root == null) return null;

    if (key < root.val) {
        root.left = deleteNode(root.left, key);
    } else if (key > root.val) {
        root.right = deleteNode(root.right, key);
    } else {
        // Case 1 & 2: node with 0 or 1 child
        if (root.left == null) return root.right;
        if (root.right == null) return root.left;

        // Case 3: node with 2 children
        TreeNode minNode = findMin(root.right); // Inorder successor
        root.val = minNode.val;                 // Replace with successor
        root.right = deleteNode(root.right, minNode.val); // Delete successor
    }
    return root;
}

private TreeNode findMin(TreeNode node) {
    while (node.left != null) node = node.left;
    return node;
}
```

---

### 🔹 Time and Space Complexity

- **Time:** O(h)
    
- **Space:**
    
    - Recursive → O(h)
        
    - Iterative → possible, but more complex
        

---

## 🧠 Summary

|Operation|Time Complexity|Space Complexity|Notes|
|---|---|---|---|
|Insert|O(h)|O(h) or O(1)|Tail recursion or loop|
|Delete|O(h)|O(h)|3-case logic, use successor|
|Search|O(h)|O(1) or O(h)|Covered in earlier notes|

In a **balanced BST**, `h = log N`, so operations are efficient. But in a skewed tree, it becomes O(N).

---

Would you like notes on **Balancing a BST (like AVL or Red-Black Trees)** next?