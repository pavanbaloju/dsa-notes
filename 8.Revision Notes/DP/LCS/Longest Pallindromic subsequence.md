Here are **all four approaches** to solve the **Longest Palindromic Subsequence (LPS)** using the **Longest Common Subsequence (LCS)** trick — with full explanations and Java code.

---

## 🔁 Problem Recap:

Given a string `s`, return the length of the longest subsequence of `s` that is a palindrome.

### 🔑 Key Insight:

LPS of `s` = LCS(`s`, `reverse(s)`)

---

## ✅ 1. Brute Force – Recursion without Memoization

### 🔍 Idea:

Try all subsequences from both ends and check which characters match.

### ⏱ Time Complexity:

- Exponential: `O(2^n)`
    

```java
public class LPS {
    public int longestPalindromeSubseq(String s) {
        String rev = new StringBuilder(s).reverse().toString();
        return lcsRecursive(s, rev, s.length(), rev.length());
    }

    private int lcsRecursive(String s1, String s2, int i, int j) {
        if (i == 0 || j == 0) return 0;

        if (s1.charAt(i - 1) == s2.charAt(j - 1)) {
            return 1 + lcsRecursive(s1, s2, i - 1, j - 1);
        } else {
            return Math.max(
                lcsRecursive(s1, s2, i - 1, j),
                lcsRecursive(s1, s2, i, j - 1)
            );
        }
    }
}
```

---

## ✅ 2. Memoization – Top-down DP

### 🔍 Idea:

Same as brute force, but use a 2D array to **memoize** overlapping subproblems.

### ⏱ Time and Space:

- Time: `O(n^2)`
    
- Space: `O(n^2)` for the DP array and recursion stack
    

```java
public class LPS {
    public int longestPalindromeSubseq(String s) {
        String rev = new StringBuilder(s).reverse().toString();
        int n = s.length();
        int[][] dp = new int[n + 1][n + 1];

        // Fill with -1 to indicate uncalculated states
        for (int[] row : dp)
            Arrays.fill(row, -1);

        return lcsMemo(s, rev, n, n, dp);
    }

    private int lcsMemo(String s1, String s2, int i, int j, int[][] dp) {
        if (i == 0 || j == 0) return 0;
        if (dp[i][j] != -1) return dp[i][j];

        if (s1.charAt(i - 1) == s2.charAt(j - 1)) {
            dp[i][j] = 1 + lcsMemo(s1, s2, i - 1, j - 1, dp);
        } else {
            dp[i][j] = Math.max(
                lcsMemo(s1, s2, i - 1, j, dp),
                lcsMemo(s1, s2, i, j - 1, dp)
            );
        }

        return dp[i][j];
    }
}
```

---

## ✅ 3. Tabulation – Bottom-up DP

### 🔍 Idea:

Iteratively build a 2D table where `dp[i][j]` is the LCS of first `i` chars of `s` and first `j` of `rev`.

### ⏱ Time: `O(n^2)`, Space: `O(n^2)`

```java
public class LPS {
    public int longestPalindromeSubseq(String s) {
        String rev = new StringBuilder(s).reverse().toString();
        int n = s.length();
        int[][] dp = new int[n + 1][n + 1];

        // Base case already 0-initialized
        for (int i = 1; i <= n; i++) {
            for (int j = 1; j <= n; j++) {
                if (s.charAt(i - 1) == rev.charAt(j - 1)) {
                    dp[i][j] = 1 + dp[i - 1][j - 1];
                } else {
                    dp[i][j] = Math.max(dp[i - 1][j], dp[i][j - 1]);
                }
            }
        }

        return dp[n][n];
    }
}
```

---

## ✅ 4. Space Optimized Tabulation – 1D Arrays

### 🔍 Idea:

Only two rows are needed at any time: `prev` and `curr`.

### ⏱ Time: `O(n^2)`, Space: `O(n)`

```java
public class LPS {
    public int longestPalindromeSubseq(String s) {
        String rev = new StringBuilder(s).reverse().toString();
        int n = s.length();
        int[] prev = new int[n + 1];
        int[] curr = new int[n + 1];

        for (int i = 1; i <= n; i++) {
            for (int j = 1; j <= n; j++) {
                if (s.charAt(i - 1) == rev.charAt(j - 1)) {
                    curr[j] = 1 + prev[j - 1];
                } else {
                    curr[j] = Math.max(prev[j], curr[j - 1]);
                }
            }
            // Copy current row to previous
            prev = curr.clone();
        }

        return prev[n];
    }
}
```

---

## 🔚 Summary Table

|Approach|Time|Space|Suitable For|
|---|---|---|---|
|Brute Force|O(2ⁿ)|O(1)|Concept building, not interviews|
|Memoization|O(n²)|O(n²)|Top-down recursion lovers|
|Tabulation|O(n²)|O(n²)|Easy to debug|
|Space Optimized|O(n²)|O(n)|Production code / memory-constrained|

---

Would you like the **print of LPS** as well (not just length)?