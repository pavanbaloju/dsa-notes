Here are the **full revised notes on Inorder Traversal**, including intuitive explanation, all approaches (recursive, iterative, Morris), Java templates, dry run behavior, space/time complexity, use cases, and problem links.

---

# 🌿 Inorder Traversal – Full Notes (Java)

---

## ✅ What is Inorder Traversal?

> The traversal order is:

```
Left → Root → Right
```

---

## 🌳 Example Binary Tree

```
        1
       / \
      2   3
     / \
    4   5
```

### 📌 Inorder Output: `4 2 5 1 3`

---

## 🧠 Why Use Inorder?

- Used to get **sorted order** from **Binary Search Trees (BST)**
    
- Used for:
    
    - Validating BSTs
        
    - Reconstructing trees
        
    - Tree-to-list conversions
        

---

## 🔁 Approaches to Inorder Traversal

|Approach|Time|Space|Notes|
|---|---|---|---|
|1. Recursive|O(n)|O(h)|Simple, elegant|
|2. Iterative (Stack)|O(n)|O(h)|More control, interview-friendly|
|3. Morris Traversal|O(n)|O(1)|Tricky, threaded tree method|

---

## 🌿 1. Recursive Inorder Traversal

### ✅ Java Code

```java
void inorderRecursive(TreeNode root) {
    if (root == null) return;

    inorderRecursive(root.left);
    System.out.print(root.val + " ");
    inorderRecursive(root.right);
}
```

---

## 🌿 2. Iterative Inorder Traversal (Using Stack)

### ✅ Explanation

Simulate recursion using a stack:

- Go **left as far as possible**
    
- Print the node
    
- Then go **right**
    

### ✅ Java Code

```java
void inorderIterative(TreeNode root) {
    Stack<TreeNode> stack = new Stack<>();
    TreeNode current = root;

    while (current != null || !stack.isEmpty()) {
        while (current != null) {
            stack.push(current);
            current = current.left;
        }

        current = stack.pop();
        System.out.print(current.val + " ");
        current = current.right;
    }
}
```

---

## 🧪 Dry Run (Iterative)

Tree:

```
        1
       / \
      2   3
     / \
    4   5
```

Steps:

- Push 1, 2, 4
    
- Print 4 → back to 2
    
- Print 2 → go to 5
    
- Print 5 → back to 1
    
- Print 1 → go to 3 → Print 3
    

Output: `4 2 5 1 3`

---

## 🌿 3. Morris Inorder Traversal – O(1) Space

### ✅ Idea:

- No stack, no recursion
    
- Uses **threaded binary tree**:
    
    - Temporarily link rightmost of left subtree to current
        
    - Go back after printing left
        

### ✅ Java Code

```java
void morrisInorder(TreeNode root) {
    TreeNode current = root;

    while (current != null) {
        if (current.left == null) {
            System.out.print(current.val + " ");
            current = current.right;
        } else {
            TreeNode pred = current.left;
            while (pred.right != null && pred.right != current) {
                pred = pred.right;
            }

            if (pred.right == null) {
                pred.right = current; // create thread
                current = current.left;
            } else {
                pred.right = null; // remove thread
                System.out.print(current.val + " ");
                current = current.right;
            }
        }
    }
}
```

### ✅ When to Use Morris?

- Interview edge cases
    
- When recursion/stack is not allowed
    
- To traverse BSTs in-place
    

---

## ⏱ Time & Space Complexity

|Approach|Time|Space|
|---|---|---|
|Recursive|O(n)|O(h) (call stack)|
|Iterative|O(n)|O(h)|
|Morris|O(n)|O(1)|

> _h = tree height; worst case = O(n) if skewed_

---

## ⚠️ Edge Cases

|Case|Handling|
|---|---|
|`root == null`|Return early|
|Single node|Output single value|
|Skewed tree|Stack depth = O(n)|
|Cycles (Morris only)|Remove thread links properly|

---

## 🔗 Use Cases of Inorder Traversal

|Use Case|Why Inorder?|
|---|---|
|Printing sorted BST|Left-root-right gives sorted order|
|Validating a BST|Ensure sorted order without violations|
|Tree-to-list transformation|In-place or with array|
|Constructing BST from preorder/inorder|Use inorder as base|

---

## 🔗 Related Leetcode Problems

|Problem|Type|
|---|---|
|Leetcode 94 – Inorder Traversal|Recursion & Iterative|
|Leetcode 99 – Recover BST|Morris or inorder needed|
|Leetcode 230 – Kth Smallest in BST|Use inorder count|
|Leetcode 783 – Min Distance in BST|Use inorder tracking|

---

## ✅ Summary Table

|Feature|Value|
|---|---|
|Order|Left → Root → Right|
|Recursive|Simple and readable|
|Iterative|More control, good in interviews|
|Morris|Constant space, no stack|
|BST usage|Sorted order, kth smallest|

---

Would you like:

- A **practice sheet** with sorted problems by difficulty?
    
- A **step-by-step walkthrough with a tree visual**?
    
- **Follow-up: Zigzag, Vertical, Spiral, Morris postorder**?
    

Let me know and I’ll prepare those next.