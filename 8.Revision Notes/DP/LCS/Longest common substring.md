Here are **all approaches to solve "Length of Longest Common Substring"**—with detailed explanations, Java code, time & space complexities, and the core logic behind each.

---

## ✅ Problem Statement

Given two strings `s1` and `s2`, return the **length of the longest common substring** (contiguous characters) present in both strings.

---

## 🧠 Key Concept

- Unlike **Longest Common Subsequence (LCS)**, substrings must be **continuous**.
    
- If `s1[i-1] == s2[j-1]`, we can **extend** the current matching substring:  
    `dp[i][j] = dp[i-1][j-1] + 1`
    
- Otherwise, break and reset:  
    `dp[i][j] = 0`
    

---

## 📘 1. Brute Force (TLE)

### 🔹 Idea:

- Try **every substring** of `s1` and check if it exists in `s2`.
    
- Time-consuming due to many substring checks.
    

### 💡 Complexity:

- **Time:** O(N³)
    
- **Space:** O(1)
    

### ✅ Java Code:

```java
public int longestCommonSubstring(String s1, String s2) {
    int maxLen = 0;
    for (int i = 0; i < s1.length(); i++) {
        for (int j = i; j < s1.length(); j++) {
            String sub = s1.substring(i, j + 1);
            if (s2.contains(sub)) {
                maxLen = Math.max(maxLen, sub.length());
            }
        }
    }
    return maxLen;
}
```

---

## 🧵 2. Memoization (Top-Down DP)

### 🔹 Idea:

- Define `dp[i][j]` as length of longest common substring **ending at** `s1[i]` and `s2[j]`.
    
- If characters match: `dp[i][j] = 1 + dp[i-1][j-1]`
    
- Otherwise: `dp[i][j] = 0`
    
- We maintain a global variable `maxLen` to store the maximum length across all recursive calls.
    

### 💡 Complexity:

- **Time:** O(N × M)
    
- **Space:** O(N × M) + recursion stack
    

### ✅ Java Code:

```java
public class Solution {
    int[][] dp;
    int maxLen = 0;

    public int longestCommonSubstring(String s1, String s2) {
        int n = s1.length(), m = s2.length();
        dp = new int[n][m];
        for (int[] row : dp)
            Arrays.fill(row, -1);

        for (int i = 0; i < n; i++) {
            for (int j = 0; j < m; j++) {
                solve(s1, s2, i, j);
            }
        }
        return maxLen;
    }

    private int solve(String s1, String s2, int i, int j) {
        if (i < 0 || j < 0) return 0;
        if (dp[i][j] != -1) return dp[i][j];

        if (s1.charAt(i) == s2.charAt(j)) {
            dp[i][j] = 1 + solve(s1, s2, i - 1, j - 1);
            maxLen = Math.max(maxLen, dp[i][j]);
        } else {
            dp[i][j] = 0;
        }
        return dp[i][j];
    }
}
```

---

## 📚 3. Tabulation (Bottom-Up DP)

### 🔹 Idea:

- Build a 2D table where `dp[i][j]` stores the length of the longest common substring ending at `s1[i-1]` and `s2[j-1]`.
    
- Track the `maxLen` as we go.
    

### 💡 Complexity:

- **Time:** O(N × M)
    
- **Space:** O(N × M)
    

### ✅ Java Code:

```java
public int longestCommonSubstring(String s1, String s2) {
    int n = s1.length(), m = s2.length();
    int[][] dp = new int[n + 1][m + 1]; // initialized to 0
    int maxLen = 0;

    for (int i = 1; i <= n; i++) {
        for (int j = 1; j <= m; j++) {
            if (s1.charAt(i - 1) == s2.charAt(j - 1)) {
                dp[i][j] = 1 + dp[i - 1][j - 1];
                maxLen = Math.max(maxLen, dp[i][j]);
            } else {
                dp[i][j] = 0;
            }
        }
    }
    return maxLen;
}
```

---

## 💾 4. Space Optimized Tabulation

### 🔹 Idea:

- You only need the **previous row** at any time.
    
- Use two 1D arrays: `prev[]` and `curr[]`.
    

### 💡 Complexity:

- **Time:** O(N × M)
    
- **Space:** O(M)
    

### ✅ Java Code:

```java
public int longestCommonSubstring(String s1, String s2) {
    int n = s1.length(), m = s2.length();
    int[] prev = new int[m + 1];
    int[] curr = new int[m + 1];
    int maxLen = 0;

    for (int i = 1; i <= n; i++) {
        Arrays.fill(curr, 0);
        for (int j = 1; j <= m; j++) {
            if (s1.charAt(i - 1) == s2.charAt(j - 1)) {
                curr[j] = 1 + prev[j - 1];
                maxLen = Math.max(maxLen, curr[j]);
            } else {
                curr[j] = 0;
            }
        }
        int[] temp = prev;
        prev = curr;
        curr = temp; // reuse arrays
    }
    return maxLen;
}
```

---

## 📊 Comparison Table

|Approach|Time Complexity|Space Complexity|Notes|
|---|---|---|---|
|Brute Force|O(N³)|O(1)|Very slow; only for understanding|
|Memoization (Top-down)|O(N × M)|O(N × M + stack)|Elegant recursion, but stack overhead|
|Tabulation|O(N × M)|O(N × M)|Best for clarity and debugging|
|Space Optimized|O(N × M)|O(M)|Ideal for large inputs|

---

## 🔍 Pattern Recognition Tips

- Keywords like:  
    **"longest common substring"**, **"contiguous match"**, or  
    **"maximum length of matching section"** point to this problem.
    
- Not to be confused with **Longest Common Subsequence** (non-contiguous).
    

---

Would you like a **LeetCode-style template** or **Anki-ready format** to practice this one further?