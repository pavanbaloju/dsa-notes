Here are **full notes** for the classic DP problem:

## 🧗‍♂️ 746. Min Cost Climbing Stairs

---

### 📝 Problem Summary

You are given an array `cost[]`, where `cost[i]` is the cost of stepping on the `i`-th stair.  
You can start at **step 0 or step 1**, and at every step, you can move either **1 or 2 steps**.

Your goal is to reach the **top of the floor**, just **past the last stair**, with **minimum total cost**.

You **don’t need to step on the last stair**, just **pass it**.

---

### 📘 Example

```txt
Input: cost = [10, 15, 20]
Output: 15
Explanation: Start at index 1 → pay 15 → step to top.
```

```txt
Input: cost = [1, 100, 1, 1, 1, 100, 1, 1, 100, 1]
Output: 6
Explanation: 0 → 2 → 3 → 4 → 6 → 7 → 9 → top
```

---

### 🧠 Intuition

We can think of the goal as:

> “**What is the minimum cost to reach step `i`?**”  
> We use this to build the cost step-by-step using **Dynamic Programming**.

To reach step `i`, you can come from:

- `i-1` (pay `cost[i-1]`)
    
- `i-2` (pay `cost[i-2]`)
    

So, recurrence:

```
dp[i] = min(dp[i-1] + cost[i-1], dp[i-2] + cost[i-2])
```

We're trying to reach **just past the last step**, i.e., `n` (not `n-1`).

---

### ✅ Bottom-Up Tabulation

```java
public int minCostClimbingStairs(int[] cost) {
    int n = cost.length;
    int[] dp = new int[n + 1];  // dp[i] = min cost to reach step i

    dp[0] = 0; // before the first step
    dp[1] = 0; // before the second step

    for (int i = 2; i <= n; i++) {
        dp[i] = Math.min(dp[i - 1] + cost[i - 1],
                         dp[i - 2] + cost[i - 2]);
    }

    return dp[n]; // cost to reach the top
}
```

---

### ✅ Top-Down DP (Memoization)

```java
public int minCostClimbingStairs(int[] cost) {
    int n = cost.length;
    int[] memo = new int[n + 1];
    Arrays.fill(memo, -1);
    return dp(n, cost, memo);
}

int dp(int i, int[] cost, int[] memo) {
    if (i <= 1) return 0;
    if (memo[i] != -1) return memo[i];

    int oneStep = dp(i - 1, cost, memo) + cost[i - 1];
    int twoStep = dp(i - 2, cost, memo) + cost[i - 2];

    return memo[i] = Math.min(oneStep, twoStep);
}
```

---

### ✅ Space Optimized DP

```java
public int minCostClimbingStairs(int[] cost) {
    int n = cost.length;
    int prev2 = 0;  // dp[i - 2]
    int prev1 = 0;  // dp[i - 1]

    for (int i = 2; i <= n; i++) {
        int curr = Math.min(prev1 + cost[i - 1],
                            prev2 + cost[i - 2]);
        prev2 = prev1;
        prev1 = curr;
    }

    return prev1;
}
```

---

### 🧾 Time and Space Complexity

|Approach|Time|Space|
|---|---|---|
|Memoization|O(n)|O(n)|
|Tabulation|O(n)|O(n)|
|Space Optimized|O(n)|O(1)|

---

### 💡 Patterns & Problem Type

- Type: **Fibonacci-style DP**
    
- Subtype: **Min Cost Path / Climb with Skip**
    
- Decisions: At each step, jump 1 or 2 steps
    

---

### 🔗 Related Problems

|Problem|Notes|
|---|---|
|70. Climbing Stairs|Same structure, but count ways not min cost|
|198. House Robber|Maximize sum, skip adjacent|
|1137. N-th Tribonacci Number|Fibonacci variation|
|746. Min Cost Climbing Stairs|Current problem|

---

Would you like to move to **Climbing Stairs** (just count ways), or a **follow-up like Jump Game / House Robber II** next?