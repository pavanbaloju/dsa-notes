Here’s your **complete notes on Longest Common Subsequence (LCS)** — one of the most important **Dynamic Programming** patterns asked in interviews at MAANG-level companies. It forms the base of many problems like Edit Distance, Longest Palindromic Subsequence, and more.

---

## 📌 Problem Statement

> Given two strings `text1` and `text2`, return the **length** of their **longest common subsequence**.

A **subsequence** is a sequence that appears in the same **relative order**, but not necessarily **contiguously**.

---

## 🧠 Intuition

You're comparing two strings character by character to find the longest possible _subsequence_ (not substring) that is common to both.

---

## ✅ Brute Force – Recursion

Try all possibilities by either:

- Matching characters
    
- Or skipping from one of the strings
    

### 🔁 Recurrence Relation:

Let `f(i, j)` be the LCS of `text1[0...i]` and `text2[0...j]`:

```
If text1[i] == text2[j]:
    f(i, j) = 1 + f(i-1, j-1)
Else:
    f(i, j) = max(f(i-1, j), f(i, j-1))
```

### 📦 Base Case:

```
f(-1, j) = 0 or f(i, -1) = 0
```

---

### ✅ Code (Recursive – Exponential)

```java
int lcs(String s1, String s2, int i, int j) {
    if (i < 0 || j < 0) return 0;
    if (s1.charAt(i) == s2.charAt(j))
        return 1 + lcs(s1, s2, i - 1, j - 1);
    else
        return Math.max(
            lcs(s1, s2, i - 1, j),
            lcs(s1, s2, i, j - 1)
        );
}
```

⛔ **Time Complexity**: `O(2^n)`  
⛔ **Space**: Recursive stack

---

## ✅ Top-Down DP (Memoization)

Just memoize the recursive solution.

### ✅ Code (Java)

```java
int[][] memo;
int lcs(String s1, String s2) {
    int m = s1.length(), n = s2.length();
    memo = new int[m][n];
    for (int[] row : memo) Arrays.fill(row, -1);
    return dp(s1, s2, m - 1, n - 1);
}

int dp(String s1, String s2, int i, int j) {
    if (i < 0 || j < 0) return 0;
    if (memo[i][j] != -1) return memo[i][j];
    if (s1.charAt(i) == s2.charAt(j))
        return memo[i][j] = 1 + dp(s1, s2, i - 1, j - 1);
    return memo[i][j] = Math.max(dp(s1, s2, i - 1, j), dp(s1, s2, i, j - 1));
}
```

✅ **Time Complexity**: `O(m * n)`  
✅ **Space Complexity**: `O(m * n)` for memo + stack

---

## ✅ Bottom-Up DP (Tabulation)

Build up a 2D DP table where `dp[i][j]` stores the length of LCS for `s1[0...i-1]` and `s2[0...j-1]`.

### ✅ Code:

```java
int longestCommonSubsequence(String text1, String text2) {
    int m = text1.length(), n = text2.length();
    int[][] dp = new int[m + 1][n + 1];

    // Explicit initialization
    for (int i = 0; i <= m; i++) {
        for (int j = 0; j <= n; j++) {
            dp[i][j] = 0;
        }
    }

    for (int i = 1; i <= m; i++) {
        for (int j = 1; j <= n; j++) {
            if (text1.charAt(i - 1) == text2.charAt(j - 1)) {
                dp[i][j] = 1 + dp[i - 1][j - 1];
            } else {
                dp[i][j] = Math.max(dp[i - 1][j], dp[i][j - 1]);
            }
        }
    }

    return dp[m][n];
}

```

✅ Time: `O(m * n)`  
✅ Space: `O(m * n)`

---

## ✅ Space-Optimized DP

Since we only use the current and previous rows, we can reduce space to `O(n)`.

```java
int longestCommonSubsequence(String text1, String text2) {
    int m = text1.length(), n = text2.length();
    int[] prev = new int[n + 1];
    int[] curr = new int[n + 1];

    // Explicit initialization
    for (int i = 0; i <= n; i++) {
        prev[i] = 0;
        curr[i] = 0;
    }

    for (int i = 1; i <= m; i++) {
        for (int j = 1; j <= n; j++) {
            if (text1.charAt(i - 1) == text2.charAt(j - 1)) {
                curr[j] = 1 + prev[j - 1];
            } else {
                curr[j] = Math.max(prev[j], curr[j - 1]);
            }
        }

        // Instead of swapping, just copy values
        for (int j = 0; j <= n; j++) {
            prev[j] = curr[j];
            curr[j] = 0; // reset for next row
        }
    }

    return prev[n];
}

```

✅ Space: `O(n)`

---

## ✅ To Reconstruct the Actual LCS (String)

If you want the actual **subsequence string**:

### Modify the bottom-up DP:

- Traverse back from `dp[m][n]`
    
- If chars match, add to result
    
- Else move to `max(dp[i-1][j], dp[i][j-1])`
    

```java
String getLCS(String s1, String s2) {
    int m = s1.length(), n = s2.length();
    int[][] dp = new int[m + 1][n + 1];

    // Fill dp table
    for (int i = 1; i <= m; i++) {
        for (int j = 1; j <= n; j++) {
            if (s1.charAt(i - 1) == s2.charAt(j - 1))
                dp[i][j] = 1 + dp[i - 1][j - 1];
            else
                dp[i][j] = Math.max(dp[i - 1][j], dp[i][j - 1]);
        }
    }

    // Reconstruct LCS
    StringBuilder lcs = new StringBuilder();
    int i = m, j = n;
    while (i > 0 && j > 0) {
        if (s1.charAt(i - 1) == s2.charAt(j - 1)) {
            lcs.append(s1.charAt(i - 1));
            i--; j--;
        } else if (dp[i - 1][j] > dp[i][j - 1]) {
            i--;
        } else {
            j--;
        }
    }

    return lcs.reverse().toString();
}
```

---

## 🧩 Problems Based on LCS

|Problem|Variation|
|---|---|
|🔸 Longest Common Subsequence|Base|
|🔸 Print LCS|Reconstruct path|
|🔸 Longest Palindromic Subsequence|LCS between `s` and `reverse(s)`|
|🔸 Shortest Common Supersequence|`len(s1) + len(s2) - LCS(s1, s2)`|
|🔸 Edit Distance|Extension|
|🔸 Min Insertions to Palindrome|`len(s) - LCS(s, reverse(s))`|
|🔸 Number of Distinct Subsequences|Advanced DP|

---

## 🧠 Interviewer Cues

- "Find common patterns between two strings"
    
- "Find the longest matching subsequence"
    
- "You can skip characters but not reorder"
    

If it involves **subsequences**, it's a signal to check if **LCS or DP on indices** applies.

---

Would you like this turned into a printable one-pager or used as Anki-style Q&A flashcards for review?