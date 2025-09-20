Here are **full notes** on the **Unbounded Knapsack problem**, including brute force, memoization, tabulation, space optimization, and real-world variations like **Coin Change**, **Rod Cutting**, and **Integer Break**.

---

## 🧭 Problem Statement (Unbounded Knapsack)

You're given:

- `n` items, each with:
    
    - `weight[i]`
        
    - `value[i]`
        
- A **maximum capacity** `W`
    

**Objective:**  
Maximize total value by selecting items such that total weight ≤ `W`.  
You can take **unlimited instances** of each item.

---

## 🧠 Key Idea

Unlike 0/1 knapsack, where each item is picked **at most once**,  
in **unbounded knapsack**, each item can be **picked any number of times**.

---

## ✅ Variations

|Problem|Base Idea|
|---|---|
|**Unbounded Knapsack**|Maximize total value|
|**Coin Change 1**|Min number of coins|
|**Coin Change 2**|Count combinations|
|**Rod Cutting**|Max profit|
|**Integer Break**|Max product|

---

## 🧮 Brute Force (Recursion)

```java
int unboundedKnapsack(int idx, int W, int[] wt, int[] val) {
    if (idx == 0) {
        return (W / wt[0]) * val[0];
    }

    int notPick = unboundedKnapsack(idx - 1, W, wt, val);
    int pick = Integer.MIN_VALUE;

    if (wt[idx] <= W) {
        pick = val[idx] + unboundedKnapsack(idx, W - wt[idx], wt, val);
    }

    return Math.max(pick, notPick);
}
```

- **Time:** Exponential `O(2^W)`
    
- **Space:** `O(W)` (recursive stack)
    

---

## 🧵 Memoization

```java
int[][] dp = new int[n][W + 1];

for (int[] row : dp) Arrays.fill(row, -1);

int unboundedKnapsack(int idx, int W, int[] wt, int[] val, int[][] dp) {
    if (idx == 0) return (W / wt[0]) * val[0];
    if (dp[idx][W] != -1) return dp[idx][W];

    int notPick = unboundedKnapsack(idx - 1, W, wt, val, dp);
    int pick = Integer.MIN_VALUE;
    if (wt[idx] <= W) {
        pick = val[idx] + unboundedKnapsack(idx, W - wt[idx], wt, val, dp);
    }

    return dp[idx][W] = Math.max(pick, notPick);
}
```

- **Time:** `O(n * W)`
    
- **Space:** `O(n * W)` + recursion stack
    

---

## 📊 Tabulation (Bottom-Up)

```java
int unboundedKnapsack(int n, int W, int[] wt, int[] val) {
    int[][] dp = new int[n][W + 1];

    // Base case
    for (int w = 0; w <= W; w++) {
        dp[0][w] = (w / wt[0]) * val[0];
    }

    for (int i = 1; i < n; i++) {
        for (int w = 0; w <= W; w++) {
            int notPick = dp[i - 1][w];
            int pick = (wt[i] <= w) ? val[i] + dp[i][w - wt[i]] : Integer.MIN_VALUE;
            dp[i][w] = Math.max(pick, notPick);
        }
    }

    return dp[n - 1][W];
}
```

- **Time:** `O(n * W)`
    
- **Space:** `O(n * W)`
    

---

## ♻️ Space Optimized

```java
int unboundedKnapsack(int n, int W, int[] wt, int[] val) {
    int[] prev = new int[W + 1];

    for (int w = 0; w <= W; w++) {
        prev[w] = (w / wt[0]) * val[0];
    }

    for (int i = 1; i < n; i++) {
        for (int w = 0; w <= W; w++) {
            int notPick = prev[w];
            int pick = (wt[i] <= w) ? val[i] + prev[w - wt[i]] : Integer.MIN_VALUE;
            prev[w] = Math.max(pick, notPick);
        }
    }

    return prev[W];
}
```

- **Time:** `O(n * W)`
    
- **Space:** `O(W)`
    

---

## 💡 Tricks to Identify Unbounded Knapsack:

Look for these cues in the problem statement:

- “You may pick unlimited number of each item”
    
- “Infinite supply of coins/rods/integers”
    
- “Use a number/coin/length multiple times”
    
- Ask: _Is repetition of items allowed?_
    

---

## 🧠 Examples of Problems using Unbounded Knapsack

|Problem|Goal|DP Relation|
|---|---|---|
|**Coin Change 1**|Min number of coins|Minimize|
|**Coin Change 2**|Count combinations|Count ways|
|**Rod Cutting**|Maximize cut profit|Maximize|
|**Integer Break**|Max product of split|Maximize|

---

## 🔁 Compare: 0/1 vs Unbounded

|Feature|0/1 Knapsack|Unbounded Knapsack|
|---|---|---|
|Use item multiple?|❌ No|✅ Yes|
|DP transition|`dp[i-1][j-wt]`|`dp[i][j-wt]`|

---

Would you like me to create **code templates for Coin Change, Rod Cutting, Integer Break**, etc., too?