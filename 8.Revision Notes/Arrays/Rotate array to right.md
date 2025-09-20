Here's a **comprehensive DSA note on "Rotate Array to the Right"**, including **Brute Force to Optimal Approaches** in a clear progression, along with **Java code, diagrams (conceptually), time/space complexity**, and **interview notes**.

---

# ✅ Rotate Array to the Right – Full Notes (Brute Force to Optimal in Java)

---

### 🔹 Problem Statement

> Rotate the array `nums` to the right by `k` steps, where `k >= 0`.

**Example:**

```text
Input : nums = [1,2,3,4,5,6,7], k = 3  
Output: [5,6,7,1,2,3,4]
```

---

## 🧠 Key Insight

Rotating right by `k` means:  
Each element at index `i` moves to `(i + k) % n`.

---

## ⚠️ Constraints

- Must handle **large k** (e.g., `k > nums.length`)
    
- **In-place** preferred (`O(1)` space)
    
- Efficient for large input sizes (`O(n)` time)
    

---

# 🔻 Approach 1: Brute Force (Rotate One-by-One)

### 🔸 Idea:

Repeat the following `k` times:

1. Store the last element
    
2. Shift all elements one step to the right
    
3. Put the last element at index 0
    

### ✅ Java Code:

```java
public void rotate(int[] nums, int k) {
    int n = nums.length;
    k = k % n;

    for (int i = 0; i < k; i++) {
        int last = nums[n - 1];
        for (int j = n - 1; j > 0; j--) {
            nums[j] = nums[j - 1];
        }
        nums[0] = last;
    }
}
```

### ⏱ Time & Space:

- Time: `O(k * n)`
    
- Space: `O(1)`
    

### 📝 Notes:

- ❌ Inefficient, fails on large arrays or big `k`
    
- ✅ Only for conceptual clarity
    
- ❌ Not suitable for interviews
    

---

# 🔸 Approach 2: Extra Array (Modular Indexing)

### 🔸 Idea:

Create a new array.  
For each index `i` in original array, move it to index `(i + k) % n` in the new array.

### ✅ Java Code:

```java
public void rotate(int[] nums, int k) {
    int n = nums.length;
    int[] result = new int[n];

    for (int i = 0; i < n; i++) {
        result[(i + k) % n] = nums[i];
    }

    for (int i = 0; i < n; i++) {
        nums[i] = result[i];
    }
}
```

### ⏱ Time & Space:

- Time: `O(n)`
    
- Space: `O(n)` – not in-place
    

### 📝 Notes:

- ✅ Correct and simple
    
- ❌ Not space-efficient
    
- ✅ Use in real-world code if space is allowed
    
- ⚠️ Not preferred in interviews due to space usage
    

---

# ✅ Approach 3: Optimal – Reverse Array In-Place

### 🔸 Idea:

Rotate in 3 steps:

1. Reverse entire array
    
2. Reverse first `k` elements
    
3. Reverse the remaining `n - k` elements
    

#### Conceptual Diagram:

```
Original:    [1, 2, 3, 4, 5, 6, 7]
Step 1:      [7, 6, 5, 4, 3, 2, 1]
Step 2 (k=3):[5, 6, 7, 4, 3, 2, 1]
Step 3:      [5, 6, 7, 1, 2, 3, 4]
```

### ✅ Java Code:

```java
public void rotate(int[] nums, int k) {
    int n = nums.length;
    k = k % n;

    reverse(nums, 0, n - 1);   // Step 1
    reverse(nums, 0, k - 1);   // Step 2
    reverse(nums, k, n - 1);   // Step 3
}

private void reverse(int[] arr, int start, int end) {
    while (start < end) {
        int temp = arr[start];
        arr[start++] = arr[end];
        arr[end--] = temp;
    }
}
```

### ⏱ Time & Space:

- Time: `O(n)`
    
- Space: `O(1)` – in-place
    

### 📝 Notes:

- ✅ Most optimal
    
- ✅ In-place
    
- ✅ One of the best array manipulation patterns to master
    
- ✅ Preferred in interviews (Amazon, Google, etc.)
    

---

## 📊 Comparison Table

|Approach|Time|Space|In-Place|Interview Worthy|Notes|
|---|---|---|---|---|---|
|Rotate One-by-One|O(k * n)|O(1)|✅|❌ No|Too slow, only good for small inputs|
|Extra Array|O(n)|O(n)|❌|⚠️ Maybe|Good for real apps but not interviews|
|Reverse In-Place|O(n)|O(1)|✅|✅ Yes|Most efficient & elegant|

---
