To convert one string into another using **minimum insertions and deletions**, we can use the **Longest Common Subsequence (LCS)** technique.

---

## 🔍 Problem Statement

Given two strings `s1` and `s2`, find the **minimum number of insertions and deletions** required to convert `s1` into `s2`.

---

## 🧠 Core Idea

If we can find the **Longest Common Subsequence (LCS)** of `s1` and `s2`, then:

- Characters **not part of LCS in `s1`** must be **deleted**
    
- Characters **not part of LCS in `s2`** must be **inserted**
    

Let:

- `len1 = s1.length()`
    
- `len2 = s2.length()`
    
- `lcs = length of LCS(s1, s2)`
    

Then:

- **Deletions = len1 - lcs**
    
- **Insertions = len2 - lcs**
    
- **Total operations = deletions + insertions = len1 + len2 - 2 * lcs**
    

---

## 📘 Example

### Input:

```text
s1 = "heap"
s2 = "pea"
```

### LCS:

- LCS = `"ea"` (length = 2)
    

### Operations:

- Deletions = 4 - 2 = 2 (`h`, `p` at end)
    
- Insertions = 3 - 2 = 1 (`p` at start)
    
- Total = 3
    

---

## ✅ Steps to Solve

1. Compute `LCS(s1, s2)`
    
2. Return `(len1 - lcs) + (len2 - lcs)`
    

---

## 💻 Java Code

### Full DP Implementation

```java
public class MinInsertDeleteToConvert {
    
    public static int minOperations(String s1, String s2) {
        int lcs = longestCommonSubsequence(s1, s2);
        int deletions = s1.length() - lcs;
        int insertions = s2.length() - lcs;
        return deletions + insertions;
    }

    private static int longestCommonSubsequence(String s1, String s2) {
        int m = s1.length(), n = s2.length();
        int[][] dp = new int[m + 1][n + 1];

        // Initialize the table
        for (int i = 0; i <= m; i++) {
            for (int j = 0; j <= n; j++) {
                dp[i][j] = 0;
            }
        }

        // Bottom-up DP
        for (int i = 1; i <= m; i++) {
            for (int j = 1; j <= n; j++) {
                if (s1.charAt(i - 1) == s2.charAt(j - 1)) {
                    dp[i][j] = 1 + dp[i - 1][j - 1];
                } else {
                    dp[i][j] = Math.max(dp[i - 1][j], dp[i][j - 1]);
                }
            }
        }

        return dp[m][n];
    }

    public static void main(String[] args) {
        String s1 = "heap", s2 = "pea";
        System.out.println("Minimum operations: " + minOperations(s1, s2)); // Output: 3
    }
}
```

---

## 🧮 Time and Space Complexity

|Approach|Time Complexity|Space Complexity|
|---|---|---|
|Tabulation|`O(m*n)`|`O(m*n)`|
|Space Optimized|`O(m*n)`|`O(n)`|

---

## 🪄 Variation

- This is also known as:  
    **Minimum Insertions and Deletions to convert string A to string B**
    

---

Here is the **space-optimized version** of the problem:  
**Minimum Insertions and Deletions to Convert One String to Another**  
using **LCS with O(n) space**.

---

## ✅ Java Code – Space Optimized

```java
public class MinInsertDeleteToConvert {

    public static int minOperations(String s1, String s2) {
        int lcs = longestCommonSubsequence(s1, s2);
        int deletions = s1.length() - lcs;
        int insertions = s2.length() - lcs;
        return deletions + insertions;
    }

    private static int longestCommonSubsequence(String s1, String s2) {
        int m = s1.length(), n = s2.length();

        // Only two rows needed
        int[] prev = new int[n + 1];
        int[] curr = new int[n + 1];

        for (int i = 1; i <= m; i++) {
            for (int j = 1; j <= n; j++) {
                if (s1.charAt(i - 1) == s2.charAt(j - 1)) {
                    curr[j] = 1 + prev[j - 1];
                } else {
                    curr[j] = Math.max(prev[j], curr[j - 1]);
                }
            }
            // Move current to previous for next iteration
            int[] temp = prev;
            prev = curr;
            curr = temp; // Reuse the array, avoids creating new arrays
        }

        return prev[n]; // prev holds the last filled row
    }

    public static void main(String[] args) {
        String s1 = "heap", s2 = "pea";
        System.out.println("Minimum operations: " + minOperations(s1, s2)); // Output: 3
    }
}
```

---

## 🧮 Time & Space Complexity

|Metric|Value|
|---|---|
|Time Complexity|`O(m * n)`|
|Space Complexity|`O(n)`|

---

Let me know if you also want the **brute-force or memoization** version, or a **DP table printed** for visualization.