Here are **full notes for the "Coin Change 2"** problem, covering all approaches — from recursion to space-optimized dynamic programming.

---

## 🔍 Problem: Coin Change II

Given an integer array `coins` representing different denominations and an integer `amount`, return the **number of combinations** that make up that amount.  
You may assume that you have **infinite** number of each coin.

---

### 🧠 1. Identifying the Pattern

- **Unbounded Knapsack**: You can pick a coin multiple times.
    
- **Counting Ways**: You are asked **how many combinations**, not the minimum number of coins.
    
- **Order doesn't matter** → Treat as **combinations**, not permutations.
    

---

## 🧱 Problem Definition

**Input:** `coins = [1, 2, 5]`, `amount = 5`  
**Output:** `4`  
**Explanation:**  
The four combinations are:

- 1+1+1+1+1
    
- 1+1+1+2
    
- 1+2+2
    
- 5
    

---

## 🔨 Approach 1: Recursion (TLE)

```java
int countWays(int i, int amount, int[] coins) {
    if (i == 0) {
        return (amount % coins[0] == 0) ? 1 : 0;
    }

    int notTake = countWays(i - 1, amount, coins);
    int take = 0;
    if (coins[i] <= amount) {
        take = countWays(i, amount - coins[i], coins);
    }
    return take + notTake;
}
```

- **Time Complexity:** Exponential
    
- **Space Complexity:** O(amount) auxiliary stack space
    

---

## 🧠 Approach 2: Memoization (Top-Down DP)

```java
int[][] dp = new int[n][amount + 1];
for (int[] row : dp) Arrays.fill(row, -1);

int countWays(int i, int amount, int[] coins, int[][] dp) {
    if (i == 0) return (amount % coins[0] == 0) ? 1 : 0;
    if (dp[i][amount] != -1) return dp[i][amount];

    int notTake = countWays(i - 1, amount, coins, dp);
    int take = 0;
    if (coins[i] <= amount) {
        take = countWays(i, amount - coins[i], coins, dp);
    }

    return dp[i][amount] = take + notTake;
}
```

- **Time Complexity:** `O(n * amount)`
    
- **Space Complexity:** `O(n * amount)` for DP + O(amount) recursion stack
    

---

## 📊 Approach 3: Tabulation (Bottom-Up DP)

```java
int change(int amount, int[] coins) {
    int n = coins.length;
    int[][] dp = new int[n][amount + 1];

    // Base Case
    for (int t = 0; t <= amount; t++) {
        if (t % coins[0] == 0) dp[0][t] = 1;
    }

    for (int i = 1; i < n; i++) {
        for (int t = 0; t <= amount; t++) {
            int notTake = dp[i - 1][t];
            int take = 0;
            if (coins[i] <= t) take = dp[i][t - coins[i]];
            dp[i][t] = take + notTake;
        }
    }

    return dp[n - 1][amount];
}
```

- **Time Complexity:** `O(n * amount)`
    
- **Space Complexity:** `O(n * amount)`
    

---

## 💾 Approach 4: Space Optimized

We only need previous and current rows → use a 1D array.

```java
int change(int amount, int[] coins) {
    int n = coins.length;
    int[] dp = new int[amount + 1];

    dp[0] = 1;  // One way to make amount 0

    for (int i = 0; i < n; i++) {
        for (int t = coins[i]; t <= amount; t++) {
            dp[t] += dp[t - coins[i]];
        }
    }

    return dp[amount];
}
```

- **Time Complexity:** `O(n * amount)`
    
- **Space Complexity:** `O(amount)`
    

> 🚨 The loop over coins is **outer**, and the amount loop is **inner** so that we **do not double count permutations**.

---

## 🧠 Key Intuition:

- This is **unbounded knapsack**.
    
- **Inclusion (take)** doesn’t reduce the index.
    
- To **avoid permutations**, keep the **coin index as outer loop**.
    

---

## ✅ Summary of Approaches

|Approach|Time Complexity|Space Complexity|Notes|
|---|---|---|---|
|Recursion|Exponential|O(amount)|TLE for large inputs|
|Memoization|O(n * amount)|O(n * amount)|Top-down with caching|
|Tabulation|O(n * amount)|O(n * amount)|Bottom-up DP table|
|Space Optimized|O(n * amount)|O(amount)|Most efficient for interviews|

---

Let me know if you’d like the **minimum number of coins** version as well (`Coin Change 1`) — it's a similar problem but the objective is different.