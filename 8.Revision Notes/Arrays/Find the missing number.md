Here’s a **full DSA breakdown** of the classic problem: **“Find the Missing Number in an Array”**, including **all standard approaches**, **Java code**, **dry run explanation**, **time/space complexity**, and **interview insights**.

---

# ✅ Problem: Find the Missing Number in an Array

---

## 🔹 Problem Statement

> Given an array `nums` containing `n` distinct numbers in the range `[0, n]`, return the one number that is missing from the array.

📌 Exactly one number is missing.

### 🔸 Example:

```text
Input : nums = [3, 0, 1]  
Output: 2

Input : nums = [0, 1]  
Output: 2
```

---

## 🔁 Pattern: **Array / Math / XOR**

---

## ✅ Constraints

- Array contains **n** elements
    
- Numbers range from `0` to `n` inclusive
    
- No duplicates
    
- Only **one number is missing**
    

---

# 🔻 Approach 1: Sorting + Linear Scan

### ✅ Java Code:

```java
public int missingNumber(int[] nums) {
    Arrays.sort(nums);

    for (int i = 0; i < nums.length; i++) {
        if (nums[i] != i) {
            return i;
        }
    }

    return nums.length;
}
```

### ⏱ Time & Space:

- Time: `O(n log n)` (due to sorting)
    
- Space: `O(1)`
    

### ❌ Not optimal due to sorting

---

# 🔸 Approach 2: Use HashSet

### ✅ Java Code:

```java
public int missingNumber(int[] nums) {
    Set<Integer> set = new HashSet<>();
    for (int num : nums) {
        set.add(num);
    }

    for (int i = 0; i <= nums.length; i++) {
        if (!set.contains(i)) {
            return i;
        }
    }

    return -1; // Should not happen
}
```

### ⏱ Time & Space:

- Time: `O(n)`
    
- Space: `O(n)`
    

### ✅ Easy to understand

### ❌ Not space-optimal

---

# ✅ Approach 3: Sum Formula (Optimal – Math)

### 🔸 Idea:

- Total sum from 0 to n = `n * (n + 1) / 2`
    
- Subtract the sum of the array to find the missing number
    

### ✅ Java Code:

```java
public int missingNumber(int[] nums) {
    int n = nums.length;
    int total = n * (n + 1) / 2;

    int sum = 0;
    for (int num : nums) {
        sum += num;
    }

    return total - sum;
}
```

### ⏱ Time & Space:

- Time: `O(n)`
    
- Space: `O(1)`
    

### ✅ Very efficient

### ✅ Preferred in interviews

---

# ✅ Approach 4: XOR Trick (Optimal – Bit Manipulation)

### 🔸 Idea:

- XOR of all indices and all elements cancels out duplicates
    
- Only the missing number remains
    

### ✅ Java Code:

```java
public int missingNumber(int[] nums) {
    int n = nums.length;
    int xor = 0;

    for (int i = 0; i < n; i++) {
        xor ^= i ^ nums[i];
    }

    return xor ^ n;
}
```

### 🔁 Dry Run:

```text
nums = [3, 0, 1]
i     =  0 1 2
nums  =  3 0 1
xor = 0 ^ 0 ^ 3 = 3  
xor = 3 ^ 1 ^ 0 = 2  
xor = 2 ^ 2 ^ 1 = 1  
xor = 1 ^ 3 = 2  ✅
```

### ⏱ Time & Space:

- Time: `O(n)`
    
- Space: `O(1)`
    

### ✅ Elegant and interview-friendly

### ✅ Works when sum may overflow

---

## 📊 Comparison Table

|Approach|Time|Space|Notes|
|---|---|---|---|
|Sorting + Scan|O(n log n)|O(1)|Simple but not optimal|
|HashSet|O(n)|O(n)|Easy, not space-efficient|
|Sum Formula|O(n)|O(1)|Optimal, watch for overflow|
|XOR Trick|O(n)|O(1)|Best for binary/interview use|

---

## 🧠 Pattern Summary

- **Missing Number (0 to n)**: Use XOR or sum
    
- **Two elements missing?** → Use sum + sum of squares
    
- **Unsorted, duplicates?** → Use HashSet or HashMap
    

---

## ✅ Follow-up Variants

|Variant|Approach|
|---|---|
|Two numbers missing|Use set or math with 2 equations|
|Missing number in sorted array|Binary search|
|Missing + Duplicate|Use sum and sum of squares equations|
|Streaming array|XOR with expected range|

---

## 🔗 Leetcode Problem

- [Leetcode 268 – Missing Number](https://leetcode.com/problems/missing-number/)
    

---

Would you like:

- Visual diagrams or dry runs for each method?
    
- Practice set for missing/duplicate pattern?
    
- Problems where **sum approach fails but XOR works** (like overflows)?