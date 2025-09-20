Sure! Let’s go through **Ninja's Training Problem** from scratch, starting with problem understanding, moving to **simple recursion**, then **memoization**, **tabulation**, and **space optimization**. We'll also include explanations and code comments to help understand the flow.

---

## 🧠 Problem: Ninja’s Training

> A Ninja has to train for `N` days. Each day he can choose one of three activities (say A, B, C) with different points. He can't do the same activity on two consecutive days.  
> Return the **maximum total points** Ninja can earn in `N` days.

---

## 📥 Input

- `N` (number of days)
    
- `points[N][3]` → where `points[i][0]`, `points[i][1]`, and `points[i][2]` are the points on day `i` for task A, B, and C respectively.
    

---

## ✅ Constraints

- No two consecutive days with the same task.
    
- Choose one task per day.
    
- Maximize the total points.
    

---

## 🎯 Goal

Maximize the total points after N days, following the constraint.

---

## Step 1: Simple Recursion (Brute Force)

### 🔍 Intuition

- On each day, try all three tasks, but avoid repeating the task done on the previous day.
    
- Use recursion to try all options and return the max.
    

### 🧾 Parameters

Let’s define `f(day, lastTask)` → maximum points from `0...day` if you did `lastTask` yesterday.

- Base Case:
    
    - If day == 0, choose any task **except** `lastTask`
        
- Recurrence:
    
    - For each task `i` ≠ `lastTask`, call `f(day-1, i) + points[day][i]`
        

### 🧪 Code (Java)

```java
public class NinjaTraining {

    static int f(int day, int last, int[][] points) {
        if (day == 0) {
            int max = 0;
            for (int i = 0; i < 3; i++) {
                if (i != last) {
                    max = Math.max(max, points[0][i]);
                }
            }
            return max;
        }

        int max = 0;
        for (int i = 0; i < 3; i++) {
            if (i != last) {
                int val = points[day][i] + f(day - 1, i, points);
                max = Math.max(max, val);
            }
        }
        return max;
    }

    public static int ninjaTraining(int n, int[][] points) {
        return f(n - 1, 3, points); // 3 means no last task restriction
    }
}
```

### ⏱ Time Complexity:

`O(2^n)` → exponential (trying all paths)

---

## Step 2: Memoization (Top-down DP)

We add memoization using a 2D array: `dp[day][lastTask]`.

### 📦 Code

```java
public class NinjaTraining {

    static int f(int day, int last, int[][] points, int[][] dp) {
        if (dp[day][last] != -1) return dp[day][last];

        if (day == 0) {
            int max = 0;
            for (int i = 0; i < 3; i++) {
                if (i != last) {
                    max = Math.max(max, points[0][i]);
                }
            }
            return dp[day][last] = max;
        }

        int max = 0;
        for (int i = 0; i < 3; i++) {
            if (i != last) {
                int val = points[day][i] + f(day - 1, i, points, dp);
                max = Math.max(max, val);
            }
        }
        return dp[day][last] = max;
    }

    public static int ninjaTraining(int n, int[][] points) {
        int[][] dp = new int[n][4];
        for (int[] row : dp) Arrays.fill(row, -1);
        return f(n - 1, 3, points, dp);
    }
}
```

### ⏱ Time Complexity:

`O(n * 4)` → 4 = number of lastTasks (0 to 3)

---

## Step 3: Tabulation (Bottom-up)

We use a `dp[n][4]` table where `dp[day][lastTask]` stores the max points.

### 🧾 Base Case:

```java
dp[0][0] = max(points[0][1], points[0][2]); // if last was 0
dp[0][1] = max(points[0][0], points[0][2]); // if last was 1
dp[0][2] = max(points[0][0], points[0][1]); // if last was 2
dp[0][3] = max(points[0][0], points[0][1], points[0][2]); // no restriction
```

### 🔁 Transition:

```java
dp[day][last] = max(points[day][task] + dp[day-1][task]) for all task ≠ last
```

### 📦 Code

```java
public class NinjaTraining {

    public static int ninjaTraining(int n, int[][] points) {
        int[][] dp = new int[n][4];

        dp[0][0] = Math.max(points[0][1], points[0][2]);
        dp[0][1] = Math.max(points[0][0], points[0][2]);
        dp[0][2] = Math.max(points[0][0], points[0][1]);
        dp[0][3] = Math.max(points[0][0], Math.max(points[0][1], points[0][2]));

        for (int day = 1; day < n; day++) {
            for (int last = 0; last < 4; last++) {
                int max = 0;
                for (int task = 0; task < 3; task++) {
                    if (task != last) {
                        int point = points[day][task] + dp[day - 1][task];
                        max = Math.max(max, point);
                    }
                }
                dp[day][last] = max;
            }
        }

        return dp[n - 1][3]; // no task on day n-1
    }
}
```

---

## Step 4: Space Optimization

We only need the previous row.

### 📦 Code

```java
public class NinjaTraining {

    public static int ninjaTraining(int n, int[][] points) {
        int[] prev = new int[4];

        prev[0] = Math.max(points[0][1], points[0][2]);
        prev[1] = Math.max(points[0][0], points[0][2]);
        prev[2] = Math.max(points[0][0], points[0][1]);
        prev[3] = Math.max(points[0][0], Math.max(points[0][1], points[0][2]));

        for (int day = 1; day < n; day++) {
            int[] curr = new int[4];
            for (int last = 0; last < 4; last++) {
                int max = 0;
                for (int task = 0; task < 3; task++) {
                    if (task != last) {
                        max = Math.max(max, points[day][task] + prev[task]);
                    }
                }
                curr[last] = max;
            }
            prev = curr;
        }

        return prev[3];
    }
}
```

---

## 🔚 Summary

|Approach|Time|Space|
|---|---|---|
|Recursion|O(3^n)|O(n) stack|
|Memoization|O(n * 4)|O(n * 4)|
|Tabulation|O(n * 4)|O(n * 4)|
|Space Optimized|O(n * 4)|O(4)|

---

If you'd like, I can now help you move to the next 2D DP pattern or explain how to generalize this as a 2D DP template.