Here are the **full notes** on **Longest Increasing Subsequence (LIS)**, including brute force, memoization, tabulation, binary search optimization, intuition, and use-cases.

## NOT SO Intuitive - practice often
---

## 🔍 Problem Statement

Given an integer array `nums`, return the length of the **longest strictly increasing subsequence**.

### Example:

```
Input: nums = [10,9,2,5,3,7,101,18]
Output: 4
Explanation: LIS is [2,3,7,101]
```

---

## 🧠 Intuition

We want to find a subsequence (not subarray) where elements are strictly increasing, and the length is maximized.

This is a classic DP problem where at each index, we have two choices:

- Pick the number (only if it increases the sequence)
    
- Don’t pick and move ahead
    

---

## 🟠 Brute Force (Recursion)

Try all increasing subsequences and return the longest.

### ✅ Approach:

- For each index, either pick or skip.
    
- Only pick if `nums[i] > prev`.
    

```java
int lengthOfLIS(int[] nums) {
    return helper(0, -1, nums);
}

int helper(int index, int prevIndex, int[] nums) {
    if (index == nums.length) return 0;
    
    int notTake = helper(index + 1, prevIndex, nums);
    int take = 0;
    if (prevIndex == -1 || nums[index] > nums[prevIndex]) {
        take = 1 + helper(index + 1, index, nums);
    }
    
    return Math.max(take, notTake);
}
```

### ⏱ Time: `O(2^n)`

### ⏳ Space: `O(n)`

---

## 🟡 Memoization (Top Down)

We memoize the function on `(index, prevIndex)`.

```java
int lengthOfLIS(int[] nums) {
    int[][] dp = new int[nums.length][nums.length + 1];
    for (int[] row : dp) Arrays.fill(row, -1);
    return helper(0, -1, nums, dp);
}

int helper(int index, int prevIndex, int[] nums, int[][] dp) {
    if (index == nums.length) return 0;
    if (dp[index][prevIndex + 1] != -1) return dp[index][prevIndex + 1];

    int notTake = helper(index + 1, prevIndex, nums, dp);
    int take = 0;
    if (prevIndex == -1 || nums[index] > nums[prevIndex]) {
        take = 1 + helper(index + 1, index, nums, dp);
    }

    return dp[index][prevIndex + 1] = Math.max(take, notTake);
}
```

### ⏱ Time: `O(n^2)`

### ⏳ Space: `O(n^2)` (due to recursion stack + dp)

---

## 🟢 Tabulation (Bottom-Up DP)

```java
int lengthOfLIS(int[] nums) {
    int n = nums.length;
    int[][] dp = new int[n+1][n+1];

    for (int index = n - 1; index >= 0; index--) {
        for (int prev = index - 1; prev >= -1; prev--) {
            int notTake = dp[index + 1][prev + 1];
            int take = 0;
            if (prev == -1 || nums[index] > nums[prev]) {
                take = 1 + dp[index + 1][index + 1];
            }
            dp[index][prev + 1] = Math.max(take, notTake);
        }
    }
    return dp[0][0];
}
```

### ⏱ Time: `O(n^2)`

### ⏳ Space: `O(n^2)`

---

## ✅ Space Optimization

We only need two rows (`curr`, `next`).

```java
int lengthOfLIS(int[] nums) {
    int n = nums.length;
    int[] curr = new int[n + 1];
    int[] next = new int[n + 1];

    for (int index = n - 1; index >= 0; index--) {
        for (int prev = index - 1; prev >= -1; prev--) {
            int notTake = next[prev + 1];
            int take = 0;
            if (prev == -1 || nums[index] > nums[prev]) {
                take = 1 + next[index + 1];
            }
            curr[prev + 1] = Math.max(take, notTake);
        }
        next = curr.clone();
    }

    return next[0];
}
```

### ⏱ Time: `O(n^2)`

### ⏳ Space: `O(n)`

---

## 🔥 Binary Search Optimized DP (Patience Sorting)

Maintain an array `tails`, where `tails[i]` is the **smallest tail of all increasing subsequences of length `i+1`**.

```java
int lengthOfLIS(int[] nums) {
    List<Integer> tails = new ArrayList<>();
    for (int num : nums) {
        int idx = Collections.binarySearch(tails, num);
        if (idx < 0) idx = -(idx + 1);
        if (idx == tails.size()) tails.add(num);
        else tails.set(idx, num);
    }
    return tails.size();
}
```

### ⏱ Time: `O(n log n)`

### ⏳ Space: `O(n)`

---

## 📌 dp[i] Definition

`dp[i]` = Length of LIS ending at index `i`.

```java
int lengthOfLIS(int[] nums) {
    int n = nums.length;
    int[] dp = new int[n];
    Arrays.fill(dp, 1);

    int max = 1;
    for (int i = 1; i < n; i++) {
        for (int j = 0; j < i; j++) {
            if (nums[i] > nums[j]) {
                dp[i] = Math.max(dp[i], dp[j] + 1);
            }
        }
        max = Math.max(max, dp[i]);
    }

    return max;
}
```

---

## 🧪 Test Cases

```java
[10,9,2,5,3,7,101,18] => 4
[0,1,0,3,2,3] => 4
[7,7,7,7,7] => 1
```

---

## 📚 Variations

1. Print the actual LIS
    
2. Count the number of LIS (`#673`)
    
3. Longest Bitonic Subsequence
    
4. Maximum Sum Increasing Subsequence
    

---

## 🧭 Pattern Recognition

- Keywords: **"subsequence"**, **"increasing"**
    
- Usually can’t be solved by sliding window (not continuous)
    
- Greedy + Binary search may optimize
    

---

Let me know if you want to add _printing LIS_, _variations_, or a _visual walkthrough_.