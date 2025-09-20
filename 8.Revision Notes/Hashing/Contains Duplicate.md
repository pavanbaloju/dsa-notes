Here’s a full DSA breakdown of the classic problem **“Contains Duplicate”** – starting from brute force to optimal, with **Java code**, edge cases, and interview guidance.

---

# ✅ Problem: Contains Duplicate

(Leetcode 217)

---

## 🔹 Problem Statement

> Given an integer array `nums`, return `true` if any value appears **at least twice** in the array, and `false` if every element is distinct.

---

### 🔸 Examples:

```text
Input:  [1,2,3,1]   → Output: true  
Input:  [1,2,3,4]   → Output: false  
Input:  [1,1,1,3,3,4,3,2,4,2] → Output: true
```

---

## 🔁 Pattern

- **Hashing for fast lookup**
    
- Optional: **sorting if you want to avoid extra space**
    

---

# 🔻 Approach 1: Brute Force (Compare all pairs)

### ✅ Java Code

```java
public boolean containsDuplicate(int[] nums) {
    for (int i = 0; i < nums.length; i++) {
        for (int j = i + 1; j < nums.length; j++) {
            if (nums[i] == nums[j]) return true;
        }
    }
    return false;
}
```

---

### ⏱ Time & Space:

- Time: `O(n^2)`
    
- Space: `O(1)`
    
- ❌ Very slow, not suitable for large input
    

---

# ✅ Approach 2: Sort and Check Adjacent

### 🔸 Idea:

- Sort the array
    
- Check if any adjacent elements are equal
    

---

### ✅ Java Code

```java
public boolean containsDuplicate(int[] nums) {
    Arrays.sort(nums);
    for (int i = 1; i < nums.length; i++) {
        if (nums[i] == nums[i - 1]) return true;
    }
    return false;
}
```

---

### ⏱ Time & Space:

- Time: `O(n log n)`
    
- Space: `O(1)` (in-place sort if allowed)
    

### ✅ Efficient if space is a constraint

### ❌ Modifies original array

---

# ✅ Approach 3: HashSet (Optimal for Unordered Input)

### 🔸 Idea:

- Store all elements in a `Set`
    
- If an element already exists → duplicate found
    

---

### ✅ Java Code

```java
public boolean containsDuplicate(int[] nums) {
    Set<Integer> seen = new HashSet<>();
    for (int num : nums) {
        if (seen.contains(num)) return true;
        seen.add(num);
    }
    return false;
}
```

---

### ⏱ Time & Space:

- Time: `O(n)`
    
- Space: `O(n)`
    
- ✅ Best for interviews
    
- ✅ No need to modify input
    

---

## 📊 Comparison Table

|Approach|Time|Space|Notes|
|---|---|---|---|
|Brute Force|O(n²)|O(1)|❌ Slow|
|Sort + Scan|O(n log n)|O(1)|✅ Good when space constrained|
|✅ HashSet|O(n)|O(n)|✅ Best all-round approach|

---

## 🧠 Edge Cases

- Empty array → `false`
    
- Single element → `false`
    
- Very large numbers or negative values → works fine
    

---

## 🔗 Leetcode Link

- [Leetcode 217 – Contains Duplicate](https://leetcode.com/problems/contains-duplicate/)
    

---

## ✅ Summary

- Use **HashSet** for optimal time and clean logic.
    
- Use **sort + adjacent scan** if space is tight and mutation is allowed.
    
- Learn this well — it’s a building block for problems like:
    
    - **Longest consecutive sequence**
        
    - **Duplicate detection in subarrays**
        
    - **Sliding window uniqueness checks**
        

---

Would you like:

- Follow-up version: “Contains Duplicate II” (check within `k` distance)?
    
- Practice set on problems using `HashSet` or `HashMap` pattern?