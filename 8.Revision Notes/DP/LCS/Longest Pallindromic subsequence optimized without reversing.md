Here are the **full notes for the Longest Palindromic Subsequence (LPS)** problem, including all standard approaches — Brute Force, Memoization, Tabulation, and Space Optimization — and how it connects to **Longest Common Subsequence (LCS)**.

---

### 🔍 Problem Statement:

Given a string `s`, return the **length** of the **longest palindromic subsequence** in `s`.

A **subsequence** is a sequence derived from the string by deleting some or no elements **without changing the order** of the remaining characters.

---

### ✅ Intuition:

If we reverse the string and find the **LCS between the original string and the reversed string**, it will give the longest palindromic subsequence.  
This is because a palindromic subsequence reads the same forward and backward.

So,

- Let `s1 = s`
    
- Let `s2 = reverse(s)`
    
- Then LPS(s) = LCS(s1, s2)
    

---

### 💡 Brute Force Approach (Recursive)

Try all subsequences and pick the longest one that is a palindrome.

```java
public int longestPalindromeSubseq(String s) {
    return helper(s, 0, s.length() - 1);
}

private int helper(String s, int i, int j) {
    if (i > j) return 0;
    if (i == j) return 1;

    if (s.charAt(i) == s.charAt(j)) {
        return 2 + helper(s, i + 1, j - 1);
    } else {
        return Math.max(helper(s, i + 1, j), helper(s, i, j - 1));
    }
}
```

**Time Complexity:** Exponential — O(2^n)  
**Space Complexity:** O(n) (implicit recursion stack)

---

### 🧠 Memoization (Top-Down DP)

Cache results for overlapping subproblems using a 2D array.

```java
public int longestPalindromeSubseq(String s) {
    int n = s.length();
    Integer[][] dp = new Integer[n][n];
    return helper(s, 0, n - 1, dp);
}

private int helper(String s, int i, int j, Integer[][] dp) {
    if (i > j) return 0;
    if (i == j) return 1;
    if (dp[i][j] != null) return dp[i][j];

    if (s.charAt(i) == s.charAt(j)) {
        dp[i][j] = 2 + helper(s, i + 1, j - 1, dp);
    } else {
        dp[i][j] = Math.max(helper(s, i + 1, j, dp), helper(s, i, j - 1, dp));
    }

    return dp[i][j];
}
```

**Time:** O(n²)  
**Space:** O(n²) (for dp table and recursion)

---

### 📋 Tabulation (Bottom-Up DP)

```java
public int longestPalindromeSubseq(String s) {
    int n = s.length();
    int[][] dp = new int[n][n];

    // every single character is a palindrome of length 1
    for (int i = 0; i < n; i++) {
        dp[i][i] = 1;
    }

    for (int len = 2; len <= n; len++) {
        for (int i = 0; i <= n - len; i++) {
            int j = i + len - 1;

            if (s.charAt(i) == s.charAt(j)) {
                dp[i][j] = 2 + ((i + 1 <= j - 1) ? dp[i + 1][j - 1] : 0);
            } else {
                dp[i][j] = Math.max(dp[i + 1][j], dp[i][j - 1]);
            }
        }
    }

    return dp[0][n - 1];
}
```

**Time:** O(n²)  
**Space:** O(n²)

---

### 💾 Space Optimization (2 Rows)

Since we only need previous and current rows, we can reduce space to O(n)

```java
public int longestPalindromeSubseq(String s) {
    int n = s.length();
    int[] prev = new int[n];
    int[] curr = new int[n];

    for (int i = n - 1; i >= 0; i--) {
        curr[i] = 1;  // single char is a palindrome
        for (int j = i + 1; j < n; j++) {
            if (s.charAt(i) == s.charAt(j)) {
                curr[j] = 2 + prev[j - 1];
            } else {
                curr[j] = Math.max(prev[j], curr[j - 1]);
            }
        }
        prev = curr.clone();  // safe copy
    }

    return prev[n - 1];
}
```

**Time:** O(n²)  
**Space:** O(n)

---

### ✅ LCS-Based Method (Alternate)

You can also solve LPS by reducing it to LCS:

```java
public int longestPalindromeSubseq(String s) {
    String rev = new StringBuilder(s).reverse().toString();
    return longestCommonSubsequence(s, rev);
}

private int longestCommonSubsequence(String s1, String s2) {
    int n = s1.length();
    int[][] dp = new int[n + 1][n + 1];

    for (int i = 1; i <= n; i++) {
        for (int j = 1; j <= n; j++) {
            if (s1.charAt(i - 1) == s2.charAt(j - 1))
                dp[i][j] = 1 + dp[i - 1][j - 1];
            else
                dp[i][j] = Math.max(dp[i - 1][j], dp[i][j - 1]);
        }
    }

    return dp[n][n];
}
```

---

### 🧪 Example:

```text
Input: s = "bbbab"
Reversed: "babbb"

LCS = "bbbb" → Length = 4 → Output = 4
```

---

### 🔑 Takeaways:

- LPS is **not the same as longest palindrome substring**.
    
- Subsequence is **non-contiguous**, unlike substrings.
    
- Reducing LPS to LCS is an **elegant trick** and often asked in interviews.
    
- For production-quality code, prefer **tabulation with 2D DP** or **space-optimized 1D DP**.
    

---

Would you like me to add LPS printing or backtracking reconstruction?