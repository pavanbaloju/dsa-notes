Here are the **full notes for the “Minimum Coins”** problem — a classic variation of the **Unbounded Knapsack**. These notes include **brute force, memoization, tabulation, and space optimization**, as well as key **intuition** and **code templates**.

---

### 🔍 Problem Statement

> You are given an integer array `coins` representing different denominations and an integer `amount`. Return the **minimum number of coins** needed to make up that amount.  
> If it's not possible to make that amount, return `-1`.

---

## 🧠 Intuition

- At every coin index, we can **pick the coin multiple times** (unbounded), or **skip** to the next coin.
    
- We want the **minimum number of coins** needed to reach the `amount`.
    

---

## 🧪 Test Cases

```java
coins = [1, 2, 5], amount = 11 ➝ Output: 3 (5+5+1)
coins = [2], amount = 3         ➝ Output: -1
coins = [1], amount = 0         ➝ Output: 0
```

---

## ✅ Choice Diagram

At every step (index `i` and target sum `t`), you have two choices:

1. **Take** the current coin `coins[i]` (stay at `i` because unbounded).
    
2. **Not take** → move to next index `i+1`.
    

---

## 🧮 Approach 1: Recursion (Brute Force)

```java
int helper(int i, int amount, int[] coins) {
    if (i == 0) {
        if (amount % coins[0] == 0) return amount / coins[0];
        return (int)1e9;
    }

    int notTake = helper(i - 1, amount, coins);
    int take = (int)1e9;
    if (coins[i] <= amount)
        take = 1 + helper(i, amount - coins[i], coins); // unbounded

    return Math.min(take, notTake);
}
```

**Time Complexity:** Exponential  
**Space:** O(amount)

---

## 🧠 Edge Condition in Base Case

```java
if (i == 0) {
    if (amount % coins[0] == 0)
        return amount / coins[0];
    else
        return INF; // cannot be formed
}
```

---

## 🧠 Approach 2: Memoization (Top-Down DP)

```java
int helper(int i, int amount, int[] coins, int[][] dp) {
    if (i == 0) {
        if (amount % coins[0] == 0) return amount / coins[0];
        return (int)1e9;
    }

    if (dp[i][amount] != -1) return dp[i][amount];

    int notTake = helper(i - 1, amount, coins, dp);
    int take = (int)1e9;
    if (coins[i] <= amount)
        take = 1 + helper(i, amount - coins[i], coins, dp);

    return dp[i][amount] = Math.min(take, notTake);
}
```

**Time Complexity:** O(n * amount)  
**Space:** O(n * amount) + recursion stack

---

## 🧮 Approach 3: Tabulation (Bottom-Up DP)

```java
int coinChange(int[] coins, int amount) {
    int n = coins.length;
    int[][] dp = new int[n][amount + 1];

    for (int t = 0; t <= amount; t++) {
        if (t % coins[0] == 0) dp[0][t] = t / coins[0];
        else dp[0][t] = (int)1e9;
    }

    for (int i = 1; i < n; i++) {
        for (int t = 0; t <= amount; t++) {
            int notTake = dp[i - 1][t];
            int take = (int)1e9;
            if (coins[i] <= t) take = 1 + dp[i][t - coins[i]];
            dp[i][t] = Math.min(take, notTake);
        }
    }

    int res = dp[n - 1][amount];
    return res >= (int)1e9 ? -1 : res;
}
```

---

## 💾 Approach 4: Space Optimization

Since we're only using `dp[i-1]` and `dp[i]`, we can optimize space:

```java
int coinChange(int[] coins, int amount) {
    int n = coins.length;
    int[] prev = new int[amount + 1];

    for (int t = 0; t <= amount; t++) {
        if (t % coins[0] == 0) prev[t] = t / coins[0];
        else prev[t] = (int)1e9;
    }

    for (int i = 1; i < n; i++) {
        int[] curr = new int[amount + 1];
        for (int t = 0; t <= amount; t++) {
            int notTake = prev[t];
            int take = (int)1e9;
            if (coins[i] <= t) take = 1 + curr[t - coins[i]];
            curr[t] = Math.min(take, notTake);
        }
        prev = curr;
    }

    int res = prev[amount];
    return res >= (int)1e9 ? -1 : res;
}
```

---

## 🧠 Key Observations

- It’s a variation of **Unbounded Knapsack** with goal: **min number of items (coins)**.
    
- If no valid combination exists, return `-1`. So we use `Integer.MAX_VALUE` or large number `1e9` to detect impossible cases.
    
- Don’t forget to **initialize base case properly**, especially `t % coins[0] == 0`.
    

---

## 🧮 Summary Table

|Approach|Time Complexity|Space Complexity|
|---|---|---|
|Recursion|Exponential|O(target)|
|Memoization|O(n * target)|O(n * target)|
|Tabulation|O(n * target)|O(n * target)|
|Space Optimized|O(n * target)|O(target)|

---

If you'd like the same pattern applied to variations like **Coin Change II (count ways)** or **Minimum Coins to reach amount using exact k coins**, let me know.



In the **"Minimum Coins"** problem (also called **Coin Change - Minimum Coins**), the usual dynamic programming table `dp[i][j]` has this meaning:

---

### ✅ **Definition:**

`dp[i][j]` = Minimum number of coins required to make sum `j` using the **first `i + 1` coins** (i.e., coins from index `0` to `i`).

> You can also define it in a 1D or space-optimized form where:
> 
> `dp[j] = Minimum number of coins to make amount j`

---

### 🧠 **Intuition:**

At each cell `dp[i][j]`, we decide:

- **Not to take the coin `i`** → Then `dp[i][j] = dp[i-1][j]`
    
- **To take coin `i`** (if `coins[i] <= j`) → Then `dp[i][j] = 1 + dp[i][j - coins[i]]` (because we can reuse coin `i`)
    

---

### 🔁 **Transition:**

```java
if (coins[i] <= j)
    dp[i][j] = Math.min(dp[i-1][j], 1 + dp[i][j - coins[i]]);
else
    dp[i][j] = dp[i-1][j];
```

---

### 🧱 **Base Case:**

- For `j == 0`, `dp[i][0] = 0` for all `i`, because **0 coins needed to make sum 0**
    
- For `i == 0`, `dp[0][j] = j / coins[0]` if `j % coins[0] == 0`, else `INF`
    

---

### 🧪 Example:

Let `coins = [1, 2, 3]` and `target = 5`

You build `dp[3][6]` table (with 0-indexed `i` from 0 to 2, and `j` from 0 to 5).

---

Would you like the full solution again for **all approaches** (recursion, memoization, tabulation, space-optimized) with explanations and code?