Here are **full notes on the Partition Equal Subset Sum problem**, including brute-force intuition, dynamic programming solutions (memoization, tabulation), space optimization, and key patterns. This is a classic variation of **Subset Sum** and a fundamental **0/1 Knapsack** problem.

---

## ✅ Problem Statement

**Given**: An array `nums` of positive integers.  
**Goal**: Return `true` if the array can be **partitioned into two subsets with equal sum**.

---

## 🧠 Key Insight

If total sum of the array is **odd**, it's impossible to split equally.

If total sum is **even**, we just need to find if there exists a **subset** whose sum = `totalSum / 2`.

This reduces to:

> Can we pick some elements from `nums` such that their sum = `target = totalSum / 2`?

This is a **subset sum** problem — a variation of **0/1 Knapsack**.

---

## 🔁 Step 1: Recursive Solution (TLE for large input)

```java
boolean canPartitionRec(int[] nums) {
    int sum = Arrays.stream(nums).sum();
    if (sum % 2 != 0) return false;

    return isSubsetSum(nums, nums.length - 1, sum / 2);
}

boolean isSubsetSum(int[] nums, int i, int target) {
    if (target == 0) return true;
    if (i == 0) return nums[0] == target;

    boolean notTake = isSubsetSum(nums, i - 1, target);
    boolean take = false;
    if (nums[i] <= target)
        take = isSubsetSum(nums, i - 1, target - nums[i]);

    return take || notTake;
}
```

⛔ **Time Complexity:** Exponential

---

## 🧠 Step 2: Top-Down Memoization (DP + Recursion)

```java
boolean canPartitionMemo(int[] nums) {
    int sum = Arrays.stream(nums).sum();
    if (sum % 2 != 0) return false;
    int target = sum / 2;
    int n = nums.length;
    Boolean[][] dp = new Boolean[n][target + 1];
    return isSubsetSum(n - 1, target, nums, dp);
}

boolean isSubsetSum(int i, int target, int[] nums, Boolean[][] dp) {
    if (target == 0) return true;
    if (i == 0) return nums[0] == target;
    if (dp[i][target] != null) return dp[i][target];

    boolean notTake = isSubsetSum(i - 1, target, nums, dp);
    boolean take = false;
    if (nums[i] <= target)
        take = isSubsetSum(i - 1, target - nums[i], nums, dp);

    return dp[i][target] = take || notTake;
}
```

✅ **Time & Space**: O(n * target)

---

## 🧱 Step 3: Bottom-Up Tabulation (Classic DP Table)

```java
boolean canPartitionTab(int[] nums) {
    int sum = Arrays.stream(nums).sum();
    if (sum % 2 != 0) return false;
    int target = sum / 2;
    int n = nums.length;
    boolean[][] dp = new boolean[n][target + 1];

    // Base cases
    for (int i = 0; i < n; i++) dp[i][0] = true;
    if (nums[0] <= target) dp[0][nums[0]] = true;

    for (int i = 1; i < n; i++) {
        for (int t = 1; t <= target; t++) {
            boolean notTake = dp[i - 1][t];
            boolean take = false;
            if (nums[i] <= t)
                take = dp[i - 1][t - nums[i]];
            dp[i][t] = take || notTake;
        }
    }

    return dp[n - 1][target];
}
```

✅ **Time:** O(n * target)  
✅ **Space:** O(n * target)

---

## 💾 Step 4: Space Optimization (1D DP)

```java
boolean canPartitionSpaceOpt(int[] nums) {
    int sum = Arrays.stream(nums).sum();
    if (sum % 2 != 0) return false;
    int target = sum / 2;
    boolean[] prev = new boolean[target + 1];
    prev[0] = true;

    if (nums[0] <= target) prev[nums[0]] = true;

    for (int i = 1; i < nums.length; i++) {
        boolean[] curr = new boolean[target + 1];
        curr[0] = true;
        for (int t = 1; t <= target; t++) {
            boolean notTake = prev[t];
            boolean take = false;
            if (nums[i] <= t)
                take = prev[t - nums[i]];
            curr[t] = take || notTake;
        }
        prev = curr;
    }

    return prev[target];
}
```

✅ **Time:** O(n * target)  
✅ **Space:** O(target)

---

## 🔄 Summary Table

|Approach|Time Complexity|Space Complexity|
|---|---|---|
|Recursion|O(2^n)|O(n) (stack)|
|Memoization|O(n * target)|O(n * target)|
|Tabulation|O(n * target)|O(n * target)|
|Space Optimized|O(n * target)|O(target)|

---

## 🎯 Use Cases & Pattern Matching

This problem teaches:

- Converting "partition" problems to **subset sum**.
    
- Recognizing when to use **0/1 Knapsack** structure.
    
- Transition from recursion → memo → tabulation → space optimized.
    

---

## 🧠 Follow-up Problems (Practice These)

1. **Subset Sum Equals K**
    
2. **Count of Subsets with Sum K**
    
3. **Target Sum (Leetcode 494)**
    
4. **Minimum Subset Sum Difference**
    
5. **Can Partition into K Equal Subsets**
    
6. **Equal Sum Partition (GeeksforGeeks)**
    

---

Let me know if you'd like the **Subset Sum Variants deck** or **Count Subsets** next.