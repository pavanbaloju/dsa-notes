'Here are the **full notes on the 0/1 Knapsack Problem**, including brute-force, top-down (memoization), bottom-up (tabulation), and space optimization with detailed **intuition**, **code**, and **comments**.

---

## ✅ Problem Statement (0/1 Knapsack)

You are given:

- `n` items, each with:
    
    - weight: `wt[i]`
        
    - value: `val[i]`
        
- A maximum weight capacity `W`
    

You can either **pick** or **not pick** an item. Return the **maximum total value** you can carry without exceeding capacity `W`.

This is called **0/1** because you can either include one item or not (no repetition or fraction).

---

## 🔍 Intuition

### Recurrence relation:

For every index `i` and current capacity `W`, we have two options:

- **Pick** the item (if its weight ≤ W):
    
    - Add its value to the result of solving the subproblem without it and with reduced capacity.
        
- **Skip** the item:
    
    - Just solve for the remaining items with the same capacity.
        

```text
f(i, W) = max(
    val[i] + f(i-1, W - wt[i]),  // pick
    f(i-1, W)                    // skip
)
```

---

## 🔁 Step 1: Simple Recursion (Exponential)

```java
int knapsackRec(int[] wt, int[] val, int W, int i) {
    if (i == 0) {
        if (wt[0] <= W) return val[0];
        return 0;
    }

    int notTake = knapsackRec(wt, val, W, i - 1);
    int take = Integer.MIN_VALUE;
    if (wt[i] <= W)
        take = val[i] + knapsackRec(wt, val, W - wt[i], i - 1);

    return Math.max(take, notTake);
}
```

⛔ **Time complexity:** O(2^n)

---

## 🧠 Step 2: Top-Down DP (Memoization)

```java
int knapsackMemo(int[] wt, int[] val, int W) {
    int n = wt.length;
    int[][] dp = new int[n][W + 1];
    for (int[] row : dp) Arrays.fill(row, -1);
    return helper(n - 1, W, wt, val, dp);
}

int helper(int i, int W, int[] wt, int[] val, int[][] dp) {
    if (i == 0) {
        return (wt[0] <= W) ? val[0] : 0;
    }

    if (dp[i][W] != -1) return dp[i][W];

    int notTake = helper(i - 1, W, wt, val, dp);
    int take = Integer.MIN_VALUE;
    if (wt[i] <= W)
        take = val[i] + helper(i - 1, W - wt[i], wt, val, dp);

    return dp[i][W] = Math.max(take, notTake);
}
```

✅ **Time & Space:** O(n * W), with memo table

---

## 🧱 Step 3: Bottom-Up DP (Tabulation)

```java
int knapsackTab(int[] wt, int[] val, int W) {
    int n = wt.length;
    int[][] dp = new int[n][W + 1];

    // Base case: first item
    for (int w = wt[0]; w <= W; w++) {
        dp[0][w] = val[0];
    }

    for (int i = 1; i < n; i++) {
        for (int w = 0; w <= W; w++) {
            int notTake = dp[i - 1][w];
            int take = Integer.MIN_VALUE;
            if (wt[i] <= w)
                take = val[i] + dp[i - 1][w - wt[i]];
            dp[i][w] = Math.max(take, notTake);
        }
    }

    return dp[n - 1][W];
}
```

📦 **Space complexity:** O(n * W)  
⏱ **Time complexity:** O(n * W)

---

## 💾 Step 4: Space Optimization (1D DP)

```java
int knapsackSpaceOpt(int[] wt, int[] val, int W) {
    int n = wt.length;
    int[] prev = new int[W + 1];

    // Base case
    for (int w = wt[0]; w <= W; w++) {
        prev[w] = val[0];
    }

    for (int i = 1; i < n; i++) {
        int[] curr = new int[W + 1];
        for (int w = 0; w <= W; w++) {
            int notTake = prev[w];
            int take = Integer.MIN_VALUE;
            if (wt[i] <= w)
                take = val[i] + prev[w - wt[i]];
            curr[w] = Math.max(take, notTake);
        }
        prev = curr;
    }

    return prev[W];
}
```

🧠 **Only two 1D arrays are needed**

---

## ✅ Summary of All Approaches

|Approach|Time Complexity|Space Complexity|
|---|---|---|
|Recursion|O(2^n)|O(n) (stack)|
|Memoization|O(n * W)|O(n * W)|
|Tabulation|O(n * W)|O(n * W)|
|Space Optimized|O(n * W)|O(W)|

---

## 🎯 Key Insights

- **Choice at every step**: Pick or not pick an item → ideal for DP
    
- State depends on **index** and **remaining capacity**
    
- Use **DP when overlapping subproblems** and **optimal substructure**
    
- Start from **basic recursion**, then build up
    

---

Let me know if you want the **0/1 Knapsack with item list (actual picked items)** or **bounded/unbounded knapsack** variants next.