Here are the **full notes on Preorder Traversal** (with both recursive and iterative approaches), including:

- ✅ Definition and traversal order
    
- 🔁 Java implementations
    
- 🧠 Visual dry run
    
- ⏱ Time & space complexity
    
- ⚠️ Edge cases
    
- 🔗 Real-world use cases & related problems
    

---

# 🌲 Preorder Traversal – Full Notes

---

## ✅ What is Preorder Traversal?

In **Preorder traversal**, we visit nodes in the following order:

> **Root → Left → Right**

### Example Tree:

```
        1
       / \
      2   3
     / \
    4   5
```

**Preorder Traversal:** `1 2 4 5 3`

---

## 🧠 Intuition

Preorder traversal is used when:

- You want to **process the root before its children**
    
- You want to **clone or serialize a tree**
    

---

## 🔁 Recursive Preorder Traversal – Java

```java
void preorder(TreeNode root) {
    if (root == null) return;
    System.out.print(root.val + " ");
    preorder(root.left);
    preorder(root.right);
}
```

**Output (on sample tree):** `1 2 4 5 3`

---

## 🔁 Iterative Preorder Traversal – Java (Using Stack)

```java
void preorderIterative(TreeNode root) {
    if (root == null) return;

    Stack<TreeNode> stack = new Stack<>();
    stack.push(root);

    while (!stack.isEmpty()) {
        TreeNode node = stack.pop();
        System.out.print(node.val + " ");

        // Push right first so left is processed first
        if (node.right != null) stack.push(node.right);
        if (node.left != null) stack.push(node.left);
    }
}
```

---

## 🧪 Dry Run (Iterative)

Stack state during traversal on:

```
        1
       / \
      2   3
     / \
    4   5
```

|Step|Stack|Output|
|---|---|---|
|1|[1]||
|2|[] → pop 1|1|
|3|[3, 2]||
|4|[3] → pop 2|1 2|
|5|[3, 5, 4]||
|6|[3, 5] → pop 4|1 2 4|
|7|[3] → pop 5|1 2 4 5|
|8|[] → pop 3|1 2 4 5 3|

---

## ⏱ Time and Space Complexity

|Operation|Value|
|---|---|
|Time Complexity|O(n)|
|Space Complexity|O(h) avg, O(n) worst (due to stack or recursion)|

---

## ⚠️ Edge Cases

|Case|What to Do|
|---|---|
|Empty tree (null root)|Return immediately|
|Tree with one node|Output: single root value|
|Skewed tree (linked list)|Stack space = O(n)|

---

## 🛠️ TreeNode Definition (Leetcode-style)

```java
class TreeNode {
    int val;
    TreeNode left, right;
    TreeNode(int val) {
        this.val = val;
    }
}
```

---

## 🔗 Use Cases of Preorder

|Use Case|Why Preorder?|
|---|---|
|Clone or Copy a Tree|Process root first|
|Serialize/Deserialize Trees|Maintain structure from top|
|Evaluate Expression Trees|Prefix evaluation|
|Flatten Tree to Linked List|Traverse root-first|

---

## 🔗 Related Problems

|Problem|Description|
|---|---|
|Leetcode 144 – Preorder Traversal|Recursive + Iterative|
|Leetcode 100 – Same Tree|Use preorder comparison|
|Leetcode 114 – Flatten Binary Tree|Preorder + modification|
|Leetcode 297 – Serialize/Deserialize Binary Tree|Based on preorder|

---

## ✅ Summary

|Feature|Preorder Traversal|
|---|---|
|Visit Order|Root → Left → Right|
|Tools Used|Stack (iterative) or recursion|
|Time Complexity|O(n)|
|Space|O(h) average, O(n) worst|
|Use Cases|Cloning, serialization, evaluation|

---

Would you like:

- **Morris Traversal version** (O(1) space)?
    
- **Preorder with color marking / unified iterative framework**?
    
- A **problem sheet** focused on preorder-based problems?
    

Let me know!