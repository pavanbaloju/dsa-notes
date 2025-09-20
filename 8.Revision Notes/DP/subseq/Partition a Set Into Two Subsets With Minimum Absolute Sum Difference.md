

---

## ✅ 1. **Brute Force Recursive Subset Generation**

### Idea:

- Try every subset by including or excluding each element.
    
- Calculate the sum of the subset (`s1`), and derive the other (`s2 = totalSum - s1`).
    
- Return the minimum difference `|s1 - s2|`.
    

### Code (Recursive):

```java
public int minSubsetSumDiff(int[] nums) {
    return helper(nums, 0, 0, Arrays.stream(nums).sum());
}

private int helper(int[] nums, int i, int s1, int totalSum) {
    if (i == nums.length) {
        int s2 = totalSum - s1;
        return Math.abs(s2 - s1);
    }

    int include = helper(nums, i + 1, s1 + nums[i], totalSum);
    int exclude = helper(nums, i + 1, s1, totalSum);

    return Math.min(include, exclude);
}
```

### Time:

- `O(2^n)`
    

### Space:

- `O(n)` (stack space)
    

**🔴 Not suitable for large `n > 20`**

---

## ✅ 2. **Top-Down DP (Memoization)**

### Idea:

Use memoization to store intermediate results of (index, currentSum).

### Code:

```java
public int minSubsetSumDiff(int[] nums) {
    int totalSum = Arrays.stream(nums).sum();
    Integer[][] dp = new Integer[nums.length][totalSum + 1];
    return helper(nums, 0, 0, totalSum, dp);
}

private int helper(int[] nums, int i, int s1, int totalSum, Integer[][] dp) {
    if (i == nums.length) {
        int s2 = totalSum - s1;
        return Math.abs(s2 - s1);
    }

    if (dp[i][s1] != null) return dp[i][s1];

    int include = helper(nums, i + 1, s1 + nums[i], totalSum, dp);
    int exclude = helper(nums, i + 1, s1, totalSum, dp);

    return dp[i][s1] = Math.min(include, exclude);
}
```

### Time:

- `O(n * totalSum)`
### Space:

- `O(n * totalSum)` + recursion stack

**🟡 Still limited if `totalSum` is large (e.g., 10^5+)**

---

## ✅ 3. **Bottom-Up DP (Tabulation)**

### Idea:

Use a boolean DP table `dp[i][j]` where `j` is a possible subset sum with first `i` elements.

Once the table is built, loop through all possible subset sums `s1` from `0` to `totalSum / 2`, and find minimum `|totalSum - 2 * s1|`.

### Code:

```java
public int minSubsetSumDiff(int[] nums) {
    int n = nums.length;
    int totalSum = Arrays.stream(nums).sum();
    int half = totalSum / 2;

    boolean[][] dp = new boolean[n][half + 1];
    for (int i = 0; i < n; i++) dp[i][0] = true;
    if (nums[0] <= half) dp[0][nums[0]] = true;

    for (int i = 1; i < n; i++) {
        for (int s = 1; s <= half; s++) {
            boolean notTake = dp[i - 1][s];
            boolean take = (nums[i] <= s) ? dp[i - 1][s - nums[i]] : false;
            dp[i][s] = take || notTake;
        }
    }

    int minDiff = Integer.MAX_VALUE;
    for (int s1 = 0; s1 <= half; s1++) {
        if (dp[n - 1][s1]) {
            int s2 = totalSum - s1;
            minDiff = Math.min(minDiff, Math.abs(s2 - s1));
        }
    }

    return minDiff;
}
```

### Time:

- `O(n * totalSum)`
    

### Space:

- `O(n * totalSum)`
    

**🟢 Good for moderate `totalSum` (up to 10^4–10^5)**

---

## ✅ 4. **Bottom-Up DP (Space Optimized 1D Array)**

### Idea:

Since `dp[i][j]` only depends on `dp[i-1][j]`, we can use a 1D array instead.

### Code:

```java
public int minSubsetSumDiff(int[] nums) {
    int totalSum = Arrays.stream(nums).sum();
    int half = totalSum / 2;
    boolean[] dp = new boolean[half + 1];
    dp[0] = true;

    if (nums[0] <= half) dp[nums[0]] = true;

    for (int i = 1; i < nums.length; i++) {
        boolean[] next = new boolean[half + 1];
        next[0] = true;

        for (int s = 1; s <= half; s++) {
            boolean notTake = dp[s];
            boolean take = (nums[i] <= s) ? dp[s - nums[i]] : false;
            next[s] = take || notTake;
        }
        dp = next;
    }

    int minDiff = Integer.MAX_VALUE;
    for (int s1 = 0; s1 <= half; s1++) {
        if (dp[s1]) {
            int s2 = totalSum - s1;
            minDiff = Math.min(minDiff, Math.abs(s2 - s1));
        }
    }

    return minDiff;
}
```

### Time:

- `O(n * totalSum)`
    

### Space:

- `O(totalSum)`
    

**🟢 Most optimal approach among DP variants**

---

## ✅ 5. **Meet in the Middle (Advanced)**

### Idea:

- For large `n` (e.g., `n ~ 40`), divide into two halves.
    
- Generate all subset sums of both halves.
    
- For each sum from left half, use binary search in right half to find the best `s1` such that `|totalSum - 2*s1|` is minimized.
    

### Time:

- `O(2^(n/2) * log(2^(n/2)))`
    

**🟢 Great when `n` is large but totalSum is huge**

---

## Summary Table

|Approach|Time Complexity|Space|Notes|
|---|---|---|---|
|Brute Force Recursion|`O(2^n)`|`O(n)`|Slow, only for tiny inputs|
|Top-Down DP (Memo)|`O(n * totalSum)`|`O(n * totalSum)`|Easier to write|
|Bottom-Up DP (2D)|`O(n * totalSum)`|`O(n * totalSum)`|Classic Knapsack|
|Bottom-Up DP (1D Optimized)|`O(n * totalSum)`|`O(totalSum)`|Best practical choice|
|Meet in the Middle|`O(2^(n/2) * log N)`|`O(2^(n/2))`|For large `n` (e.g., 40)|

---

## Want to Learn With Patterns?

This problem belongs to the **Subset Sum + Optimization** category.  
To build mastery, learn in the following order:

1. Subset Sum (whether possible)
    
2. Count Subsets with Sum
    
3. Equal Subset Partition
    
4. Target Sum (Leetcode 494)
    
5. Minimum Subset Sum Difference (**this one**)
    
6. K-partition into equal sum subsets
    
7. 0/1 Knapsack
    

Let me know if you want **Anki cards**, **problem links**, or **variation drills**.