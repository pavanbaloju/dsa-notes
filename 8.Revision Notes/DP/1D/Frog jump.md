Great — after Climbing Stairs, the next classic step is the **Frog Jump** problem. It builds on the same base (recurrence-style thinking) but adds **costs** and sometimes **k-jump generalization**.

---

# 🐸 Frog Jump – Full Notes

There are two main variations of Frog Jump:

---

## 🧩 **Frog Jump 1 (Leetcode-style)**

> A frog is on the 0th stair and wants to reach the `n-1`th stair.  
> Heights of stairs are given in an array `heights[]`.  
> Frog can jump **1 or 2** steps ahead.  
> **Cost to jump** from stair `i` to `j` is `abs(heights[i] - heights[j])`.  
> Find the **minimum total cost** to reach the `n-1`th stair.

---

### 🎯 Input

- `int[] heights` of size `n`
    

### 🎯 Output

- `int` minimum cost to reach the last stair
    

---

## ✅ Step 1: DP State

Let `dp[i]` = **minimum cost to reach** stair `i`.

---

## ✅ Step 2: Base Case

- `dp[0] = 0` (Frog starts here, no cost)
    

---

## ✅ Step 3: Recurrence (Transition)

From `i`, the frog can reach:

- `i+1` (cost: `abs(heights[i] - heights[i+1])`)
    
- `i+2` (cost: `abs(heights[i] - heights[i+2])`)
    

So:

```text
dp[i] = min(
  dp[i-1] + abs(heights[i] - heights[i-1]),
  dp[i-2] + abs(heights[i] - heights[i-2])
)
```

---

## ✅ Step 4: Approaches

---

### 🚫 Approach 1: Brute Force Recursion (TLE)

```java
int f(int i, int[] heights) {
    if (i == 0) return 0;
    int left = f(i - 1, heights) + Math.abs(heights[i] - heights[i - 1]);
    int right = Integer.MAX_VALUE;
    if (i > 1)
        right = f(i - 2, heights) + Math.abs(heights[i] - heights[i - 2]);
    return Math.min(left, right);
}
```

---

### ✅ Approach 2: Memoization (Top-Down)

```java
int[] dp;

int frogJump(int n, int[] heights) {
    dp = new int[n];
    Arrays.fill(dp, -1);
    return f(n - 1, heights);
}

int f(int i, int[] heights) {
    if (i == 0) return 0;
    if (dp[i] != -1) return dp[i];
    int left = f(i - 1, heights) + Math.abs(heights[i] - heights[i - 1]);
    int right = Integer.MAX_VALUE;
    if (i > 1)
        right = f(i - 2, heights) + Math.abs(heights[i] - heights[i - 2]);
    return dp[i] = Math.min(left, right);
}
```

**Time:** O(n)  
**Space:** O(n) + O(n) (memo + recursion stack)

---

### ✅ Approach 3: Tabulation (Bottom-Up)

```java
int frogJump(int n, int[] heights) {
    int[] dp = new int[n];
    dp[0] = 0;

    for (int i = 1; i < n; i++) {
        int jumpOne = dp[i - 1] + Math.abs(heights[i] - heights[i - 1]);
        int jumpTwo = Integer.MAX_VALUE;
        if (i > 1)
            jumpTwo = dp[i - 2] + Math.abs(heights[i] - heights[i - 2]);
        dp[i] = Math.min(jumpOne, jumpTwo);
    }

    return dp[n - 1];
}
```

**Time:** O(n)  
**Space:** O(n)

---

### ✅ Approach 4: Space Optimized

```java
int frogJump(int n, int[] heights) {
    int prev1 = 0, prev2 = 0;

    for (int i = 1; i < n; i++) {
        int jumpOne = prev1 + Math.abs(heights[i] - heights[i - 1]);
        int jumpTwo = Integer.MAX_VALUE;
        if (i > 1)
            jumpTwo = prev2 + Math.abs(heights[i] - heights[i - 2]);
        int curr = Math.min(jumpOne, jumpTwo);
        prev2 = prev1;
        prev1 = curr;
    }

    return prev1;
}
```

**Time:** O(n)  
**Space:** O(1) ✅

---

## 🧪 Example

```java
int[] heights = {10, 30, 40, 20};

// DP Table:
dp[0] = 0
dp[1] = abs(30 - 10) = 20
dp[2] = min(
    dp[1] + abs(40 - 30) = 20 + 10 = 30,
    dp[0] + abs(40 - 10) = 0 + 30 = 30
) = 30
dp[3] = min(
    dp[2] + abs(20 - 40) = 30 + 20 = 50,
    dp[1] + abs(20 - 30) = 20 + 10 = 30
) = 30

Answer = dp[3] = 30
```

---

## 🔁 Follow-Up: Frog Jump with K Distance

> Now the frog can jump to any stair `i-k` to `i-1` where `1 <= k <= K`.

### Transition:

```java
dp[i] = min over all j in [i-k, i-1] of: dp[j] + abs(heights[i] - heights[j])
```

### Java Code:

```java
int frogJump(int n, int[] heights, int k) {
    int[] dp = new int[n];
    dp[0] = 0;

    for (int i = 1; i < n; i++) {
        int minCost = Integer.MAX_VALUE;

        for (int j = 1; j <= k; j++) {
            if (i - j >= 0) {
                int jumpCost = dp[i - j] + Math.abs(heights[i] - heights[i - j]);
                minCost = Math.min(minCost, jumpCost);
            }
        }

        dp[i] = minCost;
    }

    return dp[n - 1];
}
```

**Time:** O(n*k)  
**Space:** O(n)

---

## ✅ Summary Table

|Approach|Time|Space|When to Use|
|---|---|---|---|
|Recursion|Exponential|O(n)|For intuition only|
|Memoization|O(n)|O(n)|Simple top-down|
|Tabulation|O(n)|O(n)|Control & clarity|
|Space Optimized|O(n)|O(1)|Best for basic version|
|K-Jump Version|O(n*k)|O(n)|Use nested loop|

---

Let me know if you want the **path reconstruction** version or want to **plot the full DP table for tracing**.