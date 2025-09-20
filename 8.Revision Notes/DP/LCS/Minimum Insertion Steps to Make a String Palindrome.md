Here's the full explanation for **Leetcode 1312: Minimum Insertion Steps to Make a String Palindrome**, using the **Longest Palindromic Subsequence (LPS)** approach — with all variations: Brute Force, Memoization, Tabulation, and Space Optimized.

---

### 🔍 Problem Statement

You are given a string `s`. You need to return the **minimum number of insertions** required to make `s` a palindrome.

---

### 🔑 Key Insight

The **minimum number of insertions** needed to make a string a palindrome =  
👉 `length of string - length of longest palindromic subsequence`

Why?

Because:

- A **palindromic subsequence** is already in correct order.
    
- Only the remaining characters need to be inserted to balance and make the full string a palindrome.
    

---

### 🧠 Step-by-step Intuition

1. Reverse the string `s` → call it `revS`
    
2. Find **Longest Common Subsequence (LCS)** of `s` and `revS` → that gives the LPS.
    
3. Minimum insertions = `s.length() - LCS(s, revS)`
    

---

### 📦 Approaches

---

## ✅ Approach 1: Brute Force Recursion (LCS of s and revS)

```java
int lcsBrute(String s1, String s2, int i, int j) {
    if (i < 0 || j < 0) return 0;
    if (s1.charAt(i) == s2.charAt(j)) {
        return 1 + lcsBrute(s1, s2, i - 1, j - 1);
    } else {
        return Math.max(lcsBrute(s1, s2, i - 1, j), lcsBrute(s1, s2, i, j - 1));
    }
}

int minInsertions(String s) {
    String revS = new StringBuilder(s).reverse().toString();
    int lps = lcsBrute(s, revS, s.length() - 1, revS.length() - 1);
    return s.length() - lps;
}
```

**Time Complexity:** Exponential — T(n) = O(2^n)

---

## ✅ Approach 2: Memoization (Top-Down DP)

```java
int lcsMemo(String s1, String s2, int i, int j, int[][] dp) {
    if (i < 0 || j < 0) return 0;
    if (dp[i][j] != -1) return dp[i][j];

    if (s1.charAt(i) == s2.charAt(j)) {
        return dp[i][j] = 1 + lcsMemo(s1, s2, i - 1, j - 1, dp);
    } else {
        return dp[i][j] = Math.max(lcsMemo(s1, s2, i - 1, j, dp), lcsMemo(s1, s2, i, j - 1, dp));
    }
}

int minInsertions(String s) {
    String revS = new StringBuilder(s).reverse().toString();
    int n = s.length();
    int[][] dp = new int[n][n];
    for (int[] row : dp) Arrays.fill(row, -1);

    int lps = lcsMemo(s, revS, n - 1, n - 1, dp);
    return n - lps;
}
```

**Time Complexity:** `O(n^2)`, **Space:** `O(n^2)`

---

## ✅ Approach 3: Tabulation (Bottom-Up DP)

```java
int minInsertions(String s) {
    String revS = new StringBuilder(s).reverse().toString();
    int n = s.length();
    int[][] dp = new int[n + 1][n + 1];

    for (int i = 1; i <= n; i++) {
        for (int j = 1; j <= n; j++) {
            if (s.charAt(i - 1) == revS.charAt(j - 1)) {
                dp[i][j] = 1 + dp[i - 1][j - 1];
            } else {
                dp[i][j] = Math.max(dp[i - 1][j], dp[i][j - 1]);
            }
        }
    }

    int lps = dp[n][n];
    return n - lps;
}
```

**Time Complexity:** `O(n^2)`  
**Space Complexity:** `O(n^2)`

---

## ✅ Approach 4: Space Optimized DP

```java
int minInsertions(String s) {
    String revS = new StringBuilder(s).reverse().toString();
    int n = s.length();
    int[] prev = new int[n + 1];
    int[] curr = new int[n + 1];

    for (int i = 1; i <= n; i++) {
        for (int j = 1; j <= n; j++) {
            if (s.charAt(i - 1) == revS.charAt(j - 1)) {
                curr[j] = 1 + prev[j - 1];
            } else {
                curr[j] = Math.max(prev[j], curr[j - 1]);
            }
        }
        prev = curr.clone();  // Safe copy
    }

    int lps = prev[n];
    return n - lps;
}
```

**Time Complexity:** `O(n^2)`  
**Space Complexity:** `O(n)`

---

### 📌 Summary Table

|Approach|Time Complexity|Space Complexity|Comment|
|---|---|---|---|
|Brute Force|Exponential|O(1)|For understanding only|
|Memoization|O(n²)|O(n²)|Top-down DP|
|Tabulation|O(n²)|O(n²)|Bottom-up DP|
|Space Optimized|O(n²)|O(n)|Most efficient|

---

### ✅ Example

```text
Input: s = "mbadm"
Reverse = "mdabm"
LPS = "mam" or "mdm" → length = 3
Insertions = 5 - 3 = 2
```

---

Would you like me to generate an **Anki-style summary card** or **visual table** to revise LPS-based problems too?