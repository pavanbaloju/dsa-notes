Here are the **full notes** for the classic **Subset Sum Equal to Target** problem, including explanations and code from brute force to space optimized tabulation:

---

## 🔍 Problem Statement

You are given an array of positive integers `arr[]` and a target sum `target`.  
Determine if there's **any subset** of the array whose **sum is exactly `target`**.

---

## 🧠 Intuition

This is a classic **0/1 Knapsack** problem:

- For every element, you have **2 choices**:
    
    1. **Pick it** (if it's not more than current target sum)
        
    2. **Skip it**
        

You want to explore all possibilities and check if **any subset** gives the required sum.

---

## ✅ Base Case Observations

- A `target sum = 0` is always possible by choosing the **empty subset**. So `dp[i][0] = true` for all `i`.
    
- If we have only the **first element** and its value is equal to the target, `dp[0][arr[0]] = true`.
    

---

## 1️⃣ Simple Recursion (Brute Force)

### 💡 Approach

At every index `i`, for a target `t`, check:

- If we **don't pick** current element → `f(i-1, t)`
    
- If we **pick it** (only if `arr[i] <= t`) → `f(i-1, t - arr[i])`
    

### 🧾 Code (Java)

```java
public boolean subsetSumRecursive(int[] arr, int target) {
    return isSubset(arr, arr.length - 1, target);
}

private boolean isSubset(int[] arr, int i, int target) {
    if (target == 0) return true;
    if (i == 0) return arr[0] == target;

    boolean notPick = isSubset(arr, i - 1, target);
    boolean pick = false;
    if (arr[i] <= target) {
        pick = isSubset(arr, i - 1, target - arr[i]);
    }
    return pick || notPick;
}
```

### 🕒 Time Complexity

- Exponential: `O(2^n)` – because we explore 2 choices at every step.
    

---

## 2️⃣ Top-Down DP (Memoization)

### 🔍 Memoization

Use a 2D array `dp[i][target]` to store already computed results.

### 🧾 Code (Java)

```java
public boolean subsetSumMemo(int[] arr, int target) {
    int n = arr.length;
    Boolean[][] dp = new Boolean[n][target + 1];
    return isSubset(arr, n - 1, target, dp);
}

private boolean isSubset(int[] arr, int i, int target, Boolean[][] dp) {
    if (target == 0) return true;
    if (i == 0) return arr[0] == target;

    if (dp[i][target] != null) return dp[i][target];

    boolean notPick = isSubset(arr, i - 1, target, dp);
    boolean pick = false;
    if (arr[i] <= target) {
        pick = isSubset(arr, i - 1, target - arr[i], dp);
    }
    return dp[i][target] = pick || notPick;
}
```

### 🕒 Time: `O(n * target)`

### 🛑 Space: `O(n * target)` (due to recursion stack + memo table)

---

## 3️⃣ Bottom-Up DP (Tabulation)

### 💡 Intuition

Build a DP table `dp[i][t]` → whether subset with first `i+1` elements can make sum `t`.

### ✅ Base cases:

- `dp[i][0] = true` for all `i`
    
- `dp[0][arr[0]] = true` if `arr[0] <= target`
    

### 🧾 Code (Java)

```java
public boolean subsetSumTabulation(int[] arr, int target) {
    int n = arr.length;
    boolean[][] dp = new boolean[n][target + 1];

    for (int i = 0; i < n; i++) dp[i][0] = true;
    if (arr[0] <= target) dp[0][arr[0]] = true;

    for (int i = 1; i < n; i++) {
        for (int t = 1; t <= target; t++) {
            boolean notPick = dp[i - 1][t];
            boolean pick = false;
            if (arr[i] <= t) {
                pick = dp[i - 1][t - arr[i]];
            }
            dp[i][t] = pick || notPick;
        }
    }
    return dp[n - 1][target];
}
```

---

## 4️⃣ Space Optimized Tabulation

### 💡 Why?

We only need values from `i-1`th row. So we can maintain 2 arrays: `prev` and `curr`

### 🧾 Code (Java)

```java
public boolean subsetSumSpaceOptimized(int[] arr, int target) {
    int n = arr.length;
    boolean[] prev = new boolean[target + 1];
    prev[0] = true;
    if (arr[0] <= target) prev[arr[0]] = true;

    for (int i = 1; i < n; i++) {
        boolean[] curr = new boolean[target + 1];
        curr[0] = true;
        for (int t = 1; t <= target; t++) {
            boolean notPick = prev[t];
            boolean pick = false;
            if (arr[i] <= t) pick = prev[t - arr[i]];
            curr[t] = pick || notPick;
        }
        prev = curr;
    }
    return prev[target];
}
```

### 🕒 Time: `O(n * target)`

### 💾 Space: `O(target)`

---

## 📌 Variations

1. **Count subsets** that sum to target → use integer DP to count ways instead of boolean.
    
2. **Subset sum equals K with negatives** → trickier due to offset handling.
    
3. **Print the subset** → backtrack using DP table.
    
4. **Partition Equal Subset Sum** → same as checking if `subsetSum(arr, totalSum / 2)` is possible.
    

---

## ✅ Takeaway

|Approach|Time|Space|
|---|---|---|
|Recursion|O(2^n)|O(n)|
|Memoization|O(n * sum)|O(n * sum)|
|Tabulation|O(n * sum)|O(n * sum)|
|Space Optimized|O(n * sum)|O(sum)|

---

Would you like the **count of subsets** or **printing all such subsets** as next steps?