**Here are **full notes** on the classic **198. House Robber** problem — one of the best starter problems in **Dynamic Programming**. This builds naturally on the “Maximum Sum of Non-Adjacent Elements” problem you just reviewed.

---

## 🏠 Problem: House Robber (Leetcode 198)

**You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed.**  
However, adjacent houses have security systems connected — if two adjacent houses are robbed on the same night, the system will alert the police.

**Goal**: Return the **maximum amount of money** you can rob **without robbing two adjacent houses**.

---

### 🔸 Example

```txt
Input: nums = [2, 7, 9, 3, 1]
Output: 12
Explanation: Rob house 1 (2) + house 3 (9) + house 5 (1) = 12
```

---

## 🎯 Step-by-Step Intuition

This is a classic **DP with two choices**:

At each index `i`, we decide:

- **Pick** house `i` → add `nums[i]` and go to `i-2`
    
- **Skip** house `i` → go to `i-1`
    

We want to **maximize total money** from `0` to `n-1`.

---

## 🔁 Recurrence Relation

Let `f(i)` = max money you can rob from house `0...i`

```
f(i) = max(f(i - 1), nums[i] + f(i - 2))
```

---

## 🧾 Base Cases

- `f(0) = nums[0]`
    
- `f(1) = max(nums[0], nums[1])`
    

---

## ✅ Top-Down DP (Memoization)

```java
int rob(int[] nums) {
    int n = nums.length;
    int[] dp = new int[n];
    Arrays.fill(dp, -1);
    return solve(n - 1, nums, dp);
}

int solve(int i, int[] nums, int[] dp) {
    if (i == 0) return nums[0];
    if (i < 0) return 0;
    if (dp[i] != -1) return dp[i];

    int pick = nums[i] + solve(i - 2, nums, dp);
    int skip = solve(i - 1, nums, dp);

    return dp[i] = Math.max(pick, skip);
}
```

---

## ✅ Bottom-Up DP (Tabulation)

```java
int rob(int[] nums) {
    int n = nums.length;
    if (n == 0) return 0;
    if (n == 1) return nums[0];

    int[] dp = new int[n];
    dp[0] = nums[0];
    dp[1] = Math.max(nums[0], nums[1]);

    for (int i = 2; i < n; i++) {
        int pick = nums[i] + dp[i - 2];
        int skip = dp[i - 1];
        dp[i] = Math.max(pick, skip);
    }

    return dp[n - 1];
}
```

---

## ✅ Space Optimized DP

Only `dp[i-1]` and `dp[i-2]` are needed.

```java
int rob(int[] nums) {
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

## 🧠 Time and Space Complexity

|Approach|Time|Space|
|---|---|---|
|Memoization|O(n)|O(n)|
|Tabulation|O(n)|O(n)|
|Space Optimized|O(n)|O(1)|

---

## 🔍 Edge Cases

- `[]` → return `0`
    
- `[5]` → return `5`
    
- `[2, 1, 1, 2]` → return `4` (pick 1st and 4th house)
    

---

## 🔗 Related Problems

- [213. House Robber II (circular)](https://leetcode.com/problems/house-robber-ii/)
    
- [337. House Robber III (tree)](https://leetcode.com/problems/house-robber-iii/)
    
- [740. Delete and Earn (value adjacency instead of index)](https://leetcode.com/problems/delete-and-earn/)
    

---

Would you like to move on to **House Robber II** (circular version) or a different DP pattern like **Frog Jump** or **Partition DP**?**