### ✅ Print the **Longest Increasing Subsequence (LIS)** – Full Notes

We’ll first discuss how to **compute the length of LIS**, then how to **print the actual sequence**, and we’ll provide:

- Intuition
    
- Code for DP with backtracking
    
- Optimized version with binary search
    

---

### 🧠 Problem

Given an array of integers, return the **longest increasing subsequence (LIS)**.

**Example**  
Input: `nums = [10, 9, 2, 5, 3, 7, 101, 18]`  
Output: `[2, 3, 7, 18]` (or any other valid LIS)

---

### ✅ Basic Intuition – Bottom-Up DP

- Define `dp[i]` as the length of the LIS ending at index `i`.
    
- For each `i`, look at all `j < i`, and if `nums[j] < nums[i]`, try extending the subsequence.
    

```java
int[] dp = new int[n];
Arrays.fill(dp, 1);

for (int i = 0; i < n; i++) {
    for (int j = 0; j < i; j++) {
        if (nums[j] < nums[i]) {
            dp[i] = Math.max(dp[i], 1 + dp[j]);
        }
    }
}
```

But to **print LIS**, we also need to **track predecessors**.

---

### ✅ Step-by-Step to **Print LIS using DP**

#### Idea:

- Keep a `dp[i]` = LIS ending at `i`
    
- Keep a `prev[i]` = index of previous element in the LIS ending at `i`
    
- Reconstruct by backtracking using `prev[]`
    

---

### ✅ Code – Print LIS Using O(n²) DP

```java
public List<Integer> longestIncreasingSubsequence(int[] nums) {
    int n = nums.length;
    int[] dp = new int[n];         // Length of LIS ending at i
    int[] prev = new int[n];       // Previous index in LIS
    Arrays.fill(dp, 1);
    Arrays.fill(prev, -1);

    int maxLen = 1;
    int lastIndex = 0;

    for (int i = 0; i < n; i++) {
        for (int j = 0; j < i; j++) {
            if (nums[j] < nums[i] && dp[j] + 1 > dp[i]) {
                dp[i] = dp[j] + 1;
                prev[i] = j;
            }
        }
        if (dp[i] > maxLen) {
            maxLen = dp[i];
            lastIndex = i;
        }
    }

    // Backtrack the LIS
    List<Integer> lis = new ArrayList<>();
    while (lastIndex != -1) {
        lis.add(nums[lastIndex]);
        lastIndex = prev[lastIndex];
    }

    Collections.reverse(lis);
    return lis;
}
```

---

### 🧠 Space Optimized or Binary Search Approach (O(n log n))

We can find **LIS length** in O(n log n) using a **tail array** (Patience Sorting), but it doesn’t give the actual sequence easily.  
If we want to print LIS in O(n log n), we must maintain an **index tracking array**.

But for interview purposes, the **O(n²) method above** is easier to implement and accepted.

---

### 🔍 Example Dry Run

```text
nums = [10, 22, 9, 33, 21, 50, 41, 60]

dp   = [1, 2, 1, 3, 2, 4, 4, 5]
prev = [-1, 0, -1, 1, 0, 3, 3, 5]

Max length = 5, lastIndex = 7
Backtracking from 7 → 5 → 3 → 1 → 0
Sequence = [10, 22, 33, 50, 60]
```

---

### 🧠 Key Concepts

- You can **backtrack** using a `prev[]` array to print LIS
    
- You can even store **paths** in a `List<List<Integer>>` if needed (more memory)
    
- Avoid using HashMaps here for order-sensitive sequences
    

---

### 📌 Summary

|Approach|Time|Space|Prints LIS|
|---|---|---|---|
|DP with backtrack|O(n²)|O(n)|✅ Yes|
|Binary search|O(n log n)|O(n)|❌ No (only length)|
|Optimized w/ index|O(n log n)|O(n)|✅ (Complex)|

Let me know if you want the binary search LIS printing approach as well.