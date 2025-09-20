Here are **full notes** on the **“Maximum Sum of Non-Adjacent Elements”** problem, covering:

- Problem Understanding
    
- Recurrence Relation
    
- Memoization (Top-Down DP)
    
- Tabulation (Bottom-Up DP)
    
- Space Optimization
    
- Java Code with Comments
    
- Intuition & Edge Cases
    

---

### 🔸 Problem Statement

Given an array of integers, find the **maximum sum** of elements such that no two elements picked are adjacent.

**Input**: `nums = [2, 1, 4, 9]`  
**Output**: `11` (Pick 2 and 9)

---

### 🔸 Real World Analogy

Think of the array as houses on a street. Each number is the money inside. If you rob one house, you cannot rob the adjacent one.

This is a variation of the **House Robber** problem.

---

### 🔸 Step 1: Identify Choice

For every index `i`, you have two options:

- **Pick** it → add `nums[i]` and skip `i-1` → go to `i-2`
    
- **Not Pick** it → move to `i-1`
    

---

### 🔸 Step 2: Recurrence Relation

Let `f(i)` be the **maximum sum** from index `0...i`:

```
f(i) = max(f(i - 1), nums[i] + f(i - 2))
```

---

### 🔸 Step 3: Base Cases

- If `i == 0`, return `nums[0]`
    
- If `i < 0`, return `0` (no elements to pick)
    

---

## ✅ Top-Down DP (Memoization)

```java
int maxSum(int[] nums) {
    int n = nums.length;
    int[] dp = new int[n];
    Arrays.fill(dp, -1);
    return helper(n - 1, nums, dp);
}

int helper(int i, int[] nums, int[] dp) {
    if (i == 0) return nums[0];
    if (i < 0) return 0;

    if (dp[i] != -1) return dp[i];

    int pick = nums[i] + helper(i - 2, nums, dp);
    int notPick = helper(i - 1, nums, dp);

    return dp[i] = Math.max(pick, notPick);
}
```

---

## ✅ Bottom-Up DP (Tabulation)

```java
int maxSum(int[] nums) {
    int n = nums.length;
    if (n == 0) return 0;
    if (n == 1) return nums[0];

    int[] dp = new int[n];
    dp[0] = nums[0];
    dp[1] = Math.max(nums[0], nums[1]);

    for (int i = 2; i < n; i++) {
        int pick = nums[i] + dp[i - 2];
        int notPick = dp[i - 1];
        dp[i] = Math.max(pick, notPick);
    }

    return dp[n - 1];
}
```

---

## ✅ Space Optimized DP

Only `dp[i-1]` and `dp[i-2]` are used, so we can optimize space.

```java
int maxSum(int[] nums) {
    int n = nums.length;
    if (n == 0) return 0;
    if (n == 1) return nums[0];

    int prev2 = nums[0];
    int prev1 = Math.max(nums[0], nums[1]);

    for (int i = 2; i < n; i++) {
        int current = Math.max(prev1, nums[i] + prev2);
        prev2 = prev1;
        prev1 = current;
    }

    return prev1;
}
```

---

### 🔸 Time and Space Complexity

|Approach|Time|Space|
|---|---|---|
|Recursion|Exponential|O(1)|
|Memoization|O(n)|O(n)|
|Tabulation|O(n)|O(n)|
|Space Optimized|O(n)|O(1)|

---

### 🔸 Edge Cases

- Empty array → return `0`
    
- One element → return `nums[0]`
    
- All negative → You can allow negatives or restrict to non-negative sums depending on variation
    

---

### 🔸 Related Problems

- [198. House Robber](https://leetcode.com/problems/house-robber/)
    
- [213. House Robber II](https://leetcode.com/problems/house-robber-ii/)
    
- [740. Delete and Earn](https://leetcode.com/problems/delete-and-earn/)
    
- [House Robber III (Tree version)](https://leetcode.com/problems/house-robber-iii/)
    

---

Would you like a **visual trace of the DP table**, or should we move on to the **Frog Jump** problem next?