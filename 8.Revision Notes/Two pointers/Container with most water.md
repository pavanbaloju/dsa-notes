Here’s the **complete explanation and notes** for the classic problem:

# **Container With Most Water**

---

## ✅ Problem Statement

Given `n` non-negative integers `height[0], height[1], ..., height[n-1]` where each represents a vertical line on the x-axis at index `i` with height `height[i]`, find two lines that together with the x-axis **form a container** such that the container **holds the most water**.

Return the **maximum area** of water that the container can store.

---

## 🔸 Input / Output

### Input:

```java
int[] height = {1, 8, 6, 2, 5, 4, 8, 3, 7};
```

### Output:

```
49
```

(Explanation: Choose lines at index 1 and 8 → min(8, 7) = 7 → width = 8 - 1 = 7 → Area = 7 × 7 = **49**)

---

## 🔍 Key Insight

Area between two lines =

```
min(height[i], height[j]) * (j - i)
```

We need to **maximize this value**.

---

## 🔵 Optimal Approach – Two Pointers

### ✅ Intuition

- The container area depends on **width** and **height** (shorter line).
    
- Start with **maximum width** (`left = 0`, `right = n-1`) and move pointers inward.
    
- Always move the **shorter line’s pointer**, because increasing height is the only way to potentially increase area.
    

### ✅ Java Code

```java
public int maxArea(int[] height) {
    int maxArea = 0;
    int left = 0, right = height.length - 1;

    while (left < right) {
        int h = Math.min(height[left], height[right]);
        int w = right - left;
        int area = h * w;
        maxArea = Math.max(maxArea, area);

        if (height[left] < height[right])
            left++;
        else
            right--;
    }
    return maxArea;
}
```

---

## ⏱ Time and Space Complexity

- **Time:** `O(n)`
    
- **Space:** `O(1)`
    

---

## 🧠 Dry Run Example

For `height = {1,8,6,2,5,4,8,3,7}`

|left|right|min(height)|width|area|maxArea|
|---|---|---|---|---|---|
|0|8|1|8|8|8|
|1|8|7|7|49|49|
|1|7|3|6|18|49|
|...|...|...|...|...|...|

Final answer: **49**

---

## ❌ Brute Force (For Understanding Only)

Try all pairs and compute area.

```java
public int maxArea(int[] height) {
    int max = 0;
    for (int i = 0; i < height.length; i++) {
        for (int j = i + 1; j < height.length; j++) {
            int area = Math.min(height[i], height[j]) * (j - i);
            max = Math.max(max, area);
        }
    }
    return max;
}
```

- Time: `O(n^2)`
    
- Space: `O(1)`
    

---

## 📌 Notes

- This is a classic **Two Pointers** problem.
    
- Do **not** use stack here – it’s not useful for this pattern.
    
- Can appear in both DSA and System Design interviews to assess **optimization ability**.
    

---

## ✅ Key Takeaway

Always consider **shrinking window** techniques when:

- You are dealing with a **range (i to j)**.
    
- You need to **maximize or minimize** something across that range.
    
- The decision depends on **comparison of values at two ends**.
    

---

Let me know if you'd like visual illustrations, dry runs, or LeetCode variations like "Max Area Between K Lines" or "Trapping Rain Water".