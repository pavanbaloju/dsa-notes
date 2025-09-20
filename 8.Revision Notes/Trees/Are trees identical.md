Here are **full notes** on the classic **“Identical Trees”** problem – how to check whether **two binary trees are the same**.

---

## 🌳 Problem: **Same Tree / Identical Trees**

### 📄 Problem Statement (LeetCode 100 - [Same Tree](https://leetcode.com/problems/same-tree/))

> Given two binary trees `p` and `q`, check if they are the **same**.

Two binary trees are considered **identical** if:

- They are structurally identical (same shape),
    
- The corresponding nodes have **equal values**.
    

---

## ✅ Input and Output

### 🔹 Input:

- Two binary tree roots: `TreeNode p`, `TreeNode q`
    

### 🔹 Output:

- Boolean: `true` if both trees are the same, else `false`
    

---

## 🔍 Intuition

To be identical:

- Both roots must be `null`, or both must be non-null with equal values.
    
- Left subtrees must be identical.
    
- Right subtrees must be identical.
    

So it’s a **recursive tree comparison**.

---

## ✅ Approach 1: Recursive DFS

### 💡 Idea:

Traverse both trees **simultaneously**:

- If both nodes are `null` → return `true`.
    
- If one is `null` and the other is not → return `false`.
    
- If values mismatch → return `false`.
    
- Recursively compare:
    
    - `left subtree` of both trees
        
    - `right subtree` of both trees
        

---

### ✅ Java Code:

```java
class TreeNode {
    int val;
    TreeNode left, right;
    TreeNode(int x) { val = x; }
}

public class IdenticalTrees {
    public boolean isSameTree(TreeNode p, TreeNode q) {
        if (p == null && q == null) return true;              // Both null → same
        if (p == null || q == null) return false;             // One is null → different
        if (p.val != q.val) return false;                     // Different values

        // Check left and right subtrees
        return isSameTree(p.left, q.left) && isSameTree(p.right, q.right);
    }
}
```

---

## ✅ Approach 2: Iterative (Using BFS Queue)

If you prefer a **non-recursive** solution:

### 🔁 Java Code:

```java
import java.util.*;

public class IdenticalTreesIterative {
    public boolean isSameTree(TreeNode p, TreeNode q) {
        Queue<TreeNode> queue1 = new LinkedList<>();
        Queue<TreeNode> queue2 = new LinkedList<>();

        queue1.offer(p);
        queue2.offer(q);

        while (!queue1.isEmpty() && !queue2.isEmpty()) {
            TreeNode n1 = queue1.poll();
            TreeNode n2 = queue2.poll();

            if (n1 == null && n2 == null) continue;
            if (n1 == null || n2 == null) return false;
            if (n1.val != n2.val) return false;

            queue1.offer(n1.left);
            queue1.offer(n1.right);

            queue2.offer(n2.left);
            queue2.offer(n2.right);
        }

        return queue1.isEmpty() && queue2.isEmpty();
    }
}
```

---

## 📊 Time and Space Complexity

|Metric|Complexity|
|---|---|
|Time|`O(n)` – each node once|
|Space|`O(h)` recursion stack (`h` = tree height) for recursive or `O(n)` for iterative BFS queue|

---

## 🔁 Example

```text
Tree 1:
    1
   / \
  2   3

Tree 2:
    1
   / \
  2   3

=> Output: true
```

```text
Tree 1:
    1
   /
  2

Tree 2:
    1
     \
      2

=> Output: false
```

---

## 🧠 Common Mistakes

- Only comparing root values without checking structure.
    
- Forgetting to check null on both sides.
    
- Thinking `null == non-null` is true in Java (it's not).
    

---

## 📌 Variations

- **Check if one tree is a subtree of another** (LeetCode 572)
    
- **Check if two trees are mirror images** (Symmetric Tree)
    

---

Would you like to see this visually with a dry run? Or do you want the **mirror tree** or **subtree** version next?