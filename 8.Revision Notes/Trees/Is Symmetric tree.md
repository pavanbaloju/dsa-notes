Here are **full notes on the "Symmetric Tree" problem**, including:

- Definition and intuition
    
- Recursive and iterative solutions
    
- Java code
    
- Edge cases
    
- Time and space complexities
    
- Related problems
    

---

## ✅ Problem Definition

A **binary tree is symmetric** if the **left subtree is a mirror reflection of the right subtree**.

---

## 📌 Example

```
       1
     /   \
    2     2
   / \   / \
  3   4 4   3

=> Symmetric ✅
```

```
       1
     /   \
    2     2
     \     \
      3     3

=> Not Symmetric ❌
```

---

## 🧠 Intuition

A tree is symmetric if the **left and right subtrees are mirror images**. That means:

- Their root values must match
    
- The **left child of the left subtree** must equal the **right child of the right subtree**
    
- The **right child of the left subtree** must equal the **left child of the right subtree**
    

---

## ✅ Recursive Solution

### 🔧 Algorithm

1. Define a helper function `isMirror(t1, t2)`
    
2. Check base cases:
    
    - If both nodes are null → return true
        
    - If only one is null → return false
        
    - If values are different → return false
        
3. Recursively check:
    
    - `isMirror(t1.left, t2.right)`
        
    - `isMirror(t1.right, t2.left)`
        

---

### ✅ Java Code (Recursive)

```java
public boolean isSymmetric(TreeNode root) {
    if (root == null) return true;
    return isMirror(root.left, root.right);
}

private boolean isMirror(TreeNode t1, TreeNode t2) {
    if (t1 == null && t2 == null) return true;
    if (t1 == null || t2 == null) return false;
    if (t1.val != t2.val) return false;

    return isMirror(t1.left, t2.right) && isMirror(t1.right, t2.left);
}
```

---

## ✅ Iterative Solution (Using Queue)

### 🔧 Algorithm

1. Use a queue to store pairs of nodes `(t1, t2)`
    
2. Pop from queue:
    
    - If both null → continue
        
    - If one null or values don’t match → return false
        
3. Add `t1.left & t2.right`, `t1.right & t2.left` into the queue
    
4. If all matched, return true
    

---

### ✅ Java Code (Iterative)

```java
public boolean isSymmetric(TreeNode root) {
    if (root == null) return true;

    Queue<TreeNode> queue = new LinkedList<>();
    queue.offer(root.left);
    queue.offer(root.right);

    while (!queue.isEmpty()) {
        TreeNode t1 = queue.poll();
        TreeNode t2 = queue.poll();

        if (t1 == null && t2 == null) continue;
        if (t1 == null || t2 == null) return false;
        if (t1.val != t2.val) return false;

        queue.offer(t1.left);
        queue.offer(t2.right);
        queue.offer(t1.right);
        queue.offer(t2.left);
    }

    return true;
}
```

---

## 📊 Time & Space Complexity

|Approach|Time Complexity|Space Complexity|Notes|
|---|---|---|---|
|Recursive|`O(N)`|`O(H)`|H = height of tree (stack)|
|Iterative|`O(N)`|`O(N)`|queue holds up to N nodes|

---

## ⚠️ Edge Cases

1. **Empty tree** → Symmetric ✅
    
2. **Only root node** → Symmetric ✅
    
3. **One-sided tree** → Not symmetric ❌
    
4. **Same structure but mismatched values** → Not symmetric ❌
    

---

## 🧪 Test Cases

|Tree Structure|Output|
|---|---|
|`[]` (Empty)|`true`|
|`[1,2,2,3,4,4,3]`|`true`|
|`[1,2,2,null,3,null,3]`|`false`|
|`[1,2,2,2,null,2]`|`false`|

---

## 🔁 Related Problems

1. **Invert Binary Tree** (LC 226)
    
2. **Same Tree** (LC 100)
    
3. **Subtree of Another Tree** (LC 572)
    
4. **Check Mirror Trees** (custom problem)
    

---

## 🧠 Summary

|Concept|Key Point|
|---|---|
|Mirror definition|`left.val == right.val` and `left.left == right.right`|
|Recursive approach|Simple and elegant, good for interviews|
|Iterative approach|Space-efficient for shallow trees|
|Common mistake|Only checking values, not mirrored structure|

---
