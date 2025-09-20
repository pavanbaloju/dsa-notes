Here are **full notes on the Edit Distance** problem, covering all approaches — Brute Force, Memoization, Tabulation, and Space Optimization — with clear explanations and Java code.

---

## ✅ Problem Statement

> Given two strings `s1` and `s2`, return the minimum number of operations required to convert `s1` to `s2`.  
> Operations allowed:
> 
> - **Insert** a character
>     
> - **Delete** a character
>     
> - **Replace** a character
>     

---

## 🔁 Pattern Recognition

This is a **variation of the LCS/DP on strings** pattern where:

- If characters match → move both indices.
    
- If not → try all 3 operations (Insert/Delete/Replace).
    

---

## 1. ✅ **Brute Force (Recursion)**

### Intuition:

Explore all 3 choices (insert, delete, replace) at each step where characters don't match.

### Recurrence Relation:

Let `f(i, j)` = edit distance between `s1[0...i]` and `s2[0...j]`

```
If s1[i] == s2[j]:
    f(i, j) = f(i-1, j-1)
Else:
    f(i, j) = 1 + min(
        f(i-1, j),     // delete
        f(i, j-1),     // insert
        f(i-1, j-1)    // replace
    )
```

### Base Case:

- If `i < 0`, return `j + 1` → insert remaining `j+1` characters of `s2`
    
- If `j < 0`, return `i + 1` → delete remaining `i+1` characters of `s1`
    

### Java Code:

```java
public static int editDistanceRecursive(String s1, String s2, int i, int j) {
    if (i < 0) return j + 1;
    if (j < 0) return i + 1;

    if (s1.charAt(i) == s2.charAt(j)) {
        return editDistanceRecursive(s1, s2, i - 1, j - 1);
    } else {
        return 1 + Math.min(
            editDistanceRecursive(s1, s2, i - 1, j),     // delete
            Math.min(
                editDistanceRecursive(s1, s2, i, j - 1), // insert
                editDistanceRecursive(s1, s2, i - 1, j - 1) // replace
            )
        );
    }
}
```

---

## 2. ✅ **Memoization (Top-Down DP)**

### Optimization:

Store intermediate results using a 2D `dp[i][j]` table.

### Java Code:

```java
public static int editDistanceMemo(String s1, String s2) {
    int m = s1.length(), n = s2.length();
    int[][] dp = new int[m][n];
    for (int[] row : dp) Arrays.fill(row, -1);
    return helper(s1, s2, m - 1, n - 1, dp);
}

private static int helper(String s1, String s2, int i, int j, int[][] dp) {
    if (i < 0) return j + 1;
    if (j < 0) return i + 1;

    if (dp[i][j] != -1) return dp[i][j];

    if (s1.charAt(i) == s2.charAt(j)) {
        dp[i][j] = helper(s1, s2, i - 1, j - 1, dp);
    } else {
        dp[i][j] = 1 + Math.min(
            helper(s1, s2, i - 1, j, dp),     // delete
            Math.min(
                helper(s1, s2, i, j - 1, dp), // insert
                helper(s1, s2, i - 1, j - 1, dp) // replace
            )
        );
    }

    return dp[i][j];
}
```

---

## 3. ✅ **Tabulation (Bottom-Up DP)**

### DP Table:

Let `dp[i][j]` = edit distance to convert `s1[0..i-1]` to `s2[0..j-1]`

### Base Cases:

- `dp[0][j] = j` → insert all of `s2[0..j-1]`
    
- `dp[i][0] = i` → delete all of `s1[0..i-1]`
    

### Java Code:

```java
public static int editDistanceTab(String s1, String s2) {
    int m = s1.length(), n = s2.length();
    int[][] dp = new int[m + 1][n + 1];

    // base cases
    for (int i = 0; i <= m; i++) dp[i][0] = i;
    for (int j = 0; j <= n; j++) dp[0][j] = j;

    for (int i = 1; i <= m; i++) {
        for (int j = 1; j <= n; j++) {
            if (s1.charAt(i - 1) == s2.charAt(j - 1)) {
                dp[i][j] = dp[i - 1][j - 1];
            } else {
                dp[i][j] = 1 + Math.min(
                    dp[i - 1][j],     // delete
                    Math.min(
                        dp[i][j - 1], // insert
                        dp[i - 1][j - 1]  // replace
                    )
                );
            }
        }
    }

    return dp[m][n];
}
```

---

## 4. ✅ **Space Optimized DP**

Only need the last and current row → 2 arrays

```java
public static int editDistanceSpaceOptimized(String s1, String s2) {
    int m = s1.length(), n = s2.length();
    int[] prev = new int[n + 1];
    int[] curr = new int[n + 1];

    for (int j = 0; j <= n; j++) prev[j] = j;

    for (int i = 1; i <= m; i++) {
        curr[0] = i;
        for (int j = 1; j <= n; j++) {
            if (s1.charAt(i - 1) == s2.charAt(j - 1)) {
                curr[j] = prev[j - 1];
            } else {
                curr[j] = 1 + Math.min(
                    prev[j],               // delete
                    Math.min(curr[j - 1],  // insert
                             prev[j - 1])  // replace
                );
            }
        }
        int[] temp = prev;
        prev = curr;
        curr = temp;
    }

    return prev[n];
}
```

---

## 🔍 Time and Space Complexity

|Approach|Time Complexity|Space Complexity|
|---|---|---|
|Brute Force|`O(3^n)`|`O(n)`|
|Memoization|`O(m * n)`|`O(m * n)`|
|Tabulation|`O(m * n)`|`O(m * n)`|
|Space Optimized|`O(m * n)`|`O(n)`|

---

## 🧠 Tips to Identify Edit Distance Pattern

- Two strings are involved
    
- Allowed operations: insert, delete, replace
    
- Asked for **minimum number of operations**
    

---

Let me know if you want the **DP table printed**, or **conversion path** traced as well.