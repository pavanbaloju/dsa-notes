Here’s a complete guide on the **Types of Dynamic Programming (DP)** with explanations, patterns, examples, and when to use each type. This is a foundational topic for cracking many coding interviews.

---

## 🔶 What is Dynamic Programming?

Dynamic Programming is a technique for solving **optimization problems** by **breaking them down into overlapping subproblems** and **storing the results** to avoid redundant work (memoization/tabulation).

---

## 🔷 Core Characteristics of a DP Problem

1. **Overlapping Subproblems**: Subproblems are solved repeatedly.
    
2. **Optimal Substructure**: The solution to the problem can be built from the solutions of its subproblems.
    

---

## 🔷 Types of DP (by structure and technique)

### 1. **Memoization (Top-Down DP)**

- Use recursion.
    
- Store results of subproblems in a cache/map/array to avoid re-computation.
    

```java
Map<Integer, Integer> memo = new HashMap<>();
int dp(int n) {
    if (n <= 1) return n;
    if (memo.containsKey(n)) return memo.get(n);
    int ans = dp(n - 1) + dp(n - 2);
    memo.put(n, ans);
    return ans;
}
```

🔹 **Use when:** Recursion is intuitive and you need to avoid recalculating results.

---

### 2. **Tabulation (Bottom-Up DP)**

- Build up the solution iteratively using a table.
    
- No recursion.
    

```java
int fib(int n) {
    int[] dp = new int[n + 1];
    dp[0] = 0; dp[1] = 1;
    for (int i = 2; i <= n; i++)
        dp[i] = dp[i - 1] + dp[i - 2];
    return dp[n];
}
```

🔹 **Use when:** You want better control over time/space and avoid stack overflows.

---

### 3. **1D DP**

- One-dimensional array is enough to store the states.
    

✅ Examples:

- Fibonacci
    
- Climbing Stairs
    
- House Robber
    
- Jump Game
    

---

### 4. **2D DP**

- Use a 2D table to represent multiple variables/states.
    

✅ Examples:

- Longest Common Subsequence
    
- Edit Distance
    
- Matrix Chain Multiplication
    
- 0/1 Knapsack
    
- Wildcard Matching
    

---

### 5. **DP on Subsequences / Strings**

- Used when solving subsequence/subarray/substring problems.
    

✅ Examples:

- Longest Palindromic Subsequence
    
- Longest Common Subsequence
    
- Palindrome Partitioning
    
- Count of distinct subsequences
    

---

### 6. **DP on Grids / Matrix**

- Used in path-counting or cost-minimization over grids.
    

✅ Examples:

- Unique Paths
    
- Minimum Path Sum
    
- Maximal Square
    
- Cherry Pickup
    

---

### 7. **Bitmask DP**

- Use bitmask (integers) to represent subsets.
    
- Generally used when number of elements is ≤ 20.
    

✅ Examples:

- Traveling Salesman Problem
    
- Count of subsets with certain properties
    
- Partition to K Equal Sum Subsets
    

---

### 8. **DP with State Compression**

- Optimize space using fewer states.
    

✅ Examples:

- Optimize 2D DP to 1D
    
- Optimize LCS
    
- Bitmask + DP for small input sizes
    

---

### 9. **Digit DP**

- DP where the number is processed digit by digit.
    
- Usually used in counting problems involving numbers up to N.
    

✅ Examples:

- Count of numbers with some property from 1 to N
    
- Count of numbers with no repeated digits
    

---

### 10. **Tree DP**

- DP over a tree (post-order traversal).
    

✅ Examples:

- Diameter of a Tree
    
- House Robber III (Binary Tree)
    
- Subtree queries
    
- DP on rooted trees
    

---

### 11. **DP on Graphs (Topo Order)**

- Especially useful for DAGs (Directed Acyclic Graphs).
    
- Combine DP + Topological Sort.
    

✅ Examples:

- Longest path in DAG
    
- Counting paths in DAG
    
- Course Scheduling variations
    

---

### 12. **Interval DP**

- Solve problems based on partitioning or merging intervals.
    
- Usually used when you divide a range into two parts and recurse.
    

✅ Examples:

- Burst Balloons
    
- Matrix Chain Multiplication
    
- Palindrome Partitioning
    

---

### 13. **Knapsack DP**

- Classical DP pattern where choices are based on capacity and items.
    
- 0/1, Unbounded, Bounded variants.
    

✅ Examples:

- 0/1 Knapsack
    
- Coin Change (Minimum and Number of ways)
    
- Subset Sum
    

---

### 14. **Monotonic DP**

- Optimized using monotonicity properties and data structures like deque.
    

✅ Examples:

- Sliding Window Maximum
    
- Convex Hull Trick
    
- Line Container
    

---

## 🧭 How to Identify DP?

Ask these:

- Can I break the problem into **subproblems**?
    
- Do the subproblems **overlap**?
    
- Is there an **optimal substructure**?
    
- Can I **cache** or **build** the solution bottom-up?
    

---

## 🧠 How to Master Each Type?

|Step|Action|
|---|---|
|1|Study patterns under each type|
|2|Solve 3–5 problems per type|
|3|Write template code|
|4|Optimize time/space|
|5|Discuss and explain to others|

---

Would you like a **cheat sheet PDF**, **Java templates for each DP type**, or a **DP pattern-based roadmap** to practice?