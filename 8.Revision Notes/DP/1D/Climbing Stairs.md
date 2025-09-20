Here are the **full notes** for the classic **Climbing Stairs** problem, starting from problem identification to all solution approaches — **brute force**, **memoization**, **tabulation**, and **space optimization** — along with **intuition** and **Java code** for each.

---

## 🧩 Problem Statement: Climbing Stairs

> You are climbing a staircase. It takes `n` steps to reach the top.  
> Each time you can either climb **1 or 2 steps**.  
> In how many distinct ways can you climb to the top?

### 🎯 Input

- Integer `n` (number of stairs)
    

### 🎯 Output

- Integer (number of distinct ways to reach step `n`)
    

---

## ✅ Step 1: Recognize the Pattern

This is a classic **Dynamic Programming** problem.

At each step, you can:

- Jump **1 step**, or
    
- Jump **2 steps**
    

So to reach step `n`, you can come from:

- `n - 1` (1 step before)
    
- `n - 2` (2 steps before)
    

Which gives:

```text
ways(n) = ways(n - 1) + ways(n - 2)
```

This is exactly the **Fibonacci sequence**, just shifted by 1.

---

## ✅ Step 2: Define DP State

- Let `dp[i]` be the number of ways to reach step `i`.
    

---

## ✅ Step 3: Base Cases

- `dp[0] = 1` → 1 way to be on ground
    
- `dp[1] = 1` → 1 way to reach step 1 (1 step)
    

---

## ✅ Step 4: Recurrence (Transition)

```text
dp[i] = dp[i - 1] + dp[i - 2]
```

Because from `i-1` you take 1 step, from `i-2` you take 2 steps.

---

## ✅ Step 5: Approaches

---

### 🚫 Approach 1: Brute Force Recursion (TLE for n > 30)

```java
int climbStairs(int n) {
    if (n <= 1) return 1;
    return climbStairs(n - 1) + climbStairs(n - 2);
}
```

**Time Complexity:** `O(2^n)`  
**Space Complexity:** `O(n)` (recursive call stack)

---

### ✅ Approach 2: Top-Down with Memoization

```java
int[] memo;

int climbStairs(int n) {
    memo = new int[n + 1];
    Arrays.fill(memo, -1);
    return dp(n);
}

int dp(int n) {
    if (n <= 1) return 1;
    if (memo[n] != -1) return memo[n];
    return memo[n] = dp(n - 1) + dp(n - 2);
}
```

**Time:** `O(n)`  
**Space:** `O(n)` (memo + recursion stack)

---

### ✅ Approach 3: Bottom-Up DP (Tabulation)

```java
int climbStairs(int n) {
    if (n <= 1) return 1;
    int[] dp = new int[n + 1];
    dp[0] = dp[1] = 1;

    for (int i = 2; i <= n; i++) {
        dp[i] = dp[i - 1] + dp[i - 2];
    }

    return dp[n];
}
```

**Time:** `O(n)`  
**Space:** `O(n)` (array)

---

### ✅ Approach 4: Space Optimized (Only 2 variables)

Since only last 2 states are needed:

```java
int climbStairs(int n) {
    if (n <= 1) return 1;
    int prev1 = 1, prev2 = 1;

    for (int i = 2; i <= n; i++) {
        int curr = prev1 + prev2;
        prev2 = prev1;
        prev1 = curr;
    }

    return prev1;
}
```

**Time:** `O(n)`  
**Space:** `O(1)` ✅

---

## 🧠 Intuition Recap

|Step|Ways to Reach|
|---|---|
|0|1 (do nothing)|
|1|1 (1 step)|
|2|2 (`1+1`, `2`)|
|3|3 (`1+1+1`, `1+2`, `2+1`)|
|4|5 (`3 + 2`)|
|...|`ways[i] = ways[i-1] + ways[i-2]`|

---

## 🧪 Test Cases

```java
climbStairs(0) → 1  
climbStairs(1) → 1  
climbStairs(2) → 2  
climbStairs(3) → 3  
climbStairs(4) → 5  
climbStairs(5) → 8  
climbStairs(10) → 89
```

---

## 🔁 Variants and Follow-Ups

1. What if you can take 1, 3, or 5 steps?
    
    - Change recurrence to:
        
        ```java
        dp[i] = dp[i-1] + dp[i-3] + dp[i-5];
        ```
        
2. Count number of ways with constraints (like can't step on some stairs)
    
3. Count minimum cost to climb stairs (Leetcode 746)
    
4. Actual path printing (backtracking or DP with parent array)
    

---

## ✅ Summary

|Approach|Time|Space|Use When|
|---|---|---|---|
|Recursion|O(2^n)|O(n)|Never|
|Memoization|O(n)|O(n)|Easy to write|
|Tabulation|O(n)|O(n)|Better control|
|Space Optimized|O(n)|O(1)|Best|

---

Let me know if you want:

- The variant: [Min Cost Climbing Stairs – Leetcode 746]
    
- Or a **pattern** summary to generalize this type of DP problem.