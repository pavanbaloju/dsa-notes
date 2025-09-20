Here are complete notes for the classic **“Count Subsets with Sum K”** problem, a direct extension of the **Subset Sum Problem** and part of the **0/1 Knapsack** family. The goal is not just to check if a subset exists, but to **count the total number of such subsets**.

---

## ✅ Problem Statement

**Given**: An array `nums` of non-negative integers, and an integer `target`.  
**Goal**: Count the number of subsets whose **sum equals `target`**.

---

## 🧠 Key Insight

Unlike `Partition Equal Subset Sum`, here we **need to count**, not return `true/false`.

This is a **counting variation** of the **Subset Sum** problem.

---

## 🔁 Step 1: Recursive Brute Force (TLE)

```java
int countSubsets(int[] nums, int index, int target) {
    if (target == 0) return 1;
    if (index < 0) return 0;

    int notTake = countSubsets(nums, index - 1, target);
    int take = 0;
    if (nums[index] <= target)
        take = countSubsets(nums, index - 1, target - nums[index]);

    return take + notTake;
}
```

Call:

```java
countSubsets(nums, nums.length - 1, k);
```

⛔ **Time:** O(2^n)

---

## 🧠 Step 2: Memoization (Top-Down DP)

```java
int countSubsets(int[] nums, int k) {
    int n = nums.length;
    Integer[][] dp = new Integer[n][k + 1];
    return count(n - 1, k, nums, dp);
}

int count(int i, int target, int[] nums, Integer[][] dp) {
    if (target == 0) return 1;
    if (i == 0) {
        if (nums[0] == 0 && target == 0) return 2; // include or exclude zero
        return (nums[0] == target) ? 1 : 0;
    }
    if (dp[i][target] != null) return dp[i][target];

    int notTake = count(i - 1, target, nums, dp);
    int take = 0;
    if (nums[i] <= target)
        take = count(i - 1, target - nums[i], nums, dp);

    return dp[i][target] = take + notTake;
}
```

✅ **Time & Space:** O(n * k)

---

## 🧱 Step 3: Tabulation (Bottom-Up DP)

```java
int countSubsetsTab(int[] nums, int k) {
    int n = nums.length;
    int[][] dp = new int[n][k + 1];

    // Base case
    for (int i = 0; i < n; i++) dp[i][0] = 1;  // sum 0 is always possible (empty set)

    if (nums[0] <= k) dp[0][nums[0]] += 1;

    for (int i = 1; i < n; i++) {
        for (int target = 0; target <= k; target++) {
            int notTake = dp[i - 1][target];
            int take = 0;
            if (nums[i] <= target)
                take = dp[i - 1][target - nums[i]];

            dp[i][target] = take + notTake;
        }
    }

    return dp[n - 1][k];
}
```

---

## 💾 Step 4: Space Optimization (1D DP)

```java
int countSubsetsSpaceOpt(int[] nums, int k) {
    int[] prev = new int[k + 1];
    prev[0] = 1;

    if (nums[0] <= k) prev[nums[0]] += 1;

    for (int i = 1; i < nums.length; i++) {
        int[] curr = new int[k + 1];
        curr[0] = 1;

        for (int target = 0; target <= k; target++) {
            int notTake = prev[target];
            int take = 0;
            if (nums[i] <= target)
                take = prev[target - nums[i]];

            curr[target] = take + notTake;
        }
        prev = curr;
    }

    return prev[k];
}
```

✅ **Time:** O(n * k)  
✅ **Space:** O(k)

---

## ⚠️ Special Case: Zeros in the Array

If there are `z` zeros in the array:

- Each zero can be **included or excluded** in every subset.
    
- So, **total count doubles for each zero**: `2^z` extra subsets that don't change the sum.
    

Already handled in memo/tabulation by:

```java
if (nums[0] == 0 && target == 0) return 2;
```

---

## 🧠 Pattern Type: 0/1 Knapsack (Count Variants)

---

## 🔄 Summary

|Approach|Time|Space|
|---|---|---|
|Recursion|O(2^n)|O(n)|
|Memoization|O(n * k)|O(n * k)|
|Tabulation|O(n * k)|O(n * k)|
|Space Optimized|O(n * k)|O(k)|

---

## 🎯 Similar Problems

1. **Target Sum (Leetcode 494)** – convert to count of subsets with a given difference.
    
2. **Subset Sum Equals K** – boolean version of this problem.
    
3. **Minimum Subset Sum Difference**
    
4. **Partition to K Equal Sum Subsets**
    
5. **Equal Sum Partition**
    

---

Let me know if you'd like:

- Target Sum notes
    
- A complete table of subset sum variations
    
- Or Anki card style breakdowns