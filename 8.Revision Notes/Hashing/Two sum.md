Here is the complete DSA breakdown of the classic and most fundamental array problem: **Two Sum** — with **multiple approaches**, **Java code**, and **interview-level reasoning**.

---

# ✅ Problem: Two Sum

(Leetcode 1)

---

## 🔹 Problem Statement

> Given an array of integers `nums` and an integer `target`, return **indices** of the two numbers such that they **add up to target**.  
> You may assume that each input has **exactly one solution**, and you may **not use the same element twice**.

---

### 🔸 Example

```text
Input:  nums = [2,7,11,15], target = 9  
Output: [0,1]  // because nums[0] + nums[1] = 2 + 7 = 9
```

---

## 🔁 Pattern

- Hashing for complements
    
- Two-pointer (if array is sorted)
    

---

# 🔻 Approach 1: Brute Force (Check all pairs)

### ✅ Java Code

```java
public int[] twoSum(int[] nums, int target) {
    int n = nums.length;
    for (int i = 0; i < n; i++) {
        for (int j = i + 1; j < n; j++) {
            if (nums[i] + nums[j] == target) {
                return new int[]{i, j};
            }
        }
    }
    return new int[]{-1, -1}; // shouldn't happen if input is valid
}
```

---

### ⏱ Time & Space:

- Time: `O(n^2)`
    
- Space: `O(1)`
    
- ❌ Inefficient for large input
    

---

# ✅ Approach 2: HashMap for Complements (Optimal for Unsorted)

### 🔸 Idea:

- Store `value → index` in a HashMap
    
- For each `num`, check if `target - num` exists in the map
    

---

### ✅ Java Code

```java
public int[] twoSum(int[] nums, int target) {
    Map<Integer, Integer> map = new HashMap<>();

    for (int i = 0; i < nums.length; i++) {
        int complement = target - nums[i];
        if (map.containsKey(complement)) {
            return new int[]{map.get(complement), i};
        }
        map.put(nums[i], i);
    }

    return new int[]{-1, -1}; // shouldn't happen
}
```

---

### ⏱ Time & Space:

- Time: `O(n)`
    
- Space: `O(n)`
    
- ✅ Best for unsorted input
    
- ✅ Most commonly accepted in interviews
    

---

# 🔄 Optional: If array is **sorted**, use Two Pointers

### ✅ Java Code

```java
public int[] twoSumSorted(int[] nums, int target) {
    int left = 0, right = nums.length - 1;

    while (left < right) {
        int sum = nums[left] + nums[right];
        if (sum == target) return new int[]{left, right};
        else if (sum < target) left++;
        else right--;
    }

    return new int[]{-1, -1};
}
```

---

### ⏱ Time & Space:

- Time: `O(n)`
    
- Space: `O(1)`
    
- ✅ Best when input is sorted
    
- ❌ Returns **indices in sorted array**, not original
    

---

## 📊 Comparison Table

|Approach|Time|Space|Input|Notes|
|---|---|---|---|---|
|Brute Force|O(n²)|O(1)|Unsorted|Basic and slow|
|HashMap (Optimal)|O(n)|O(n)|Unsorted|✅ Best for general input|
|Two Pointers|O(n)|O(1)|Sorted|✅ Best when sorted|

---

## 🧠 Edge Cases

- Negative numbers (works fine)
    
- Multiple answers? (Leetcode guarantees one)
    
- Same number used twice? (Disallowed unless appears twice in array)
    

---

## 🔗 Leetcode Link

- [Leetcode 1 – Two Sum](https://leetcode.com/problems/two-sum/)
    

---

## 📦 Variants to Practice

|Problem|Description|
|---|---|
|LC 167|Two Sum II – Input array is sorted|
|LC 653|Two Sum IV – BST version|
|LC 560|Subarray sum equals K|
|LC 18|4Sum|
|LC 15|3Sum|

---

## ✅ Summary

- Use **HashMap** to store complements and indices → O(n)
    
- Two-pointer only if array is **sorted**
    
- Know how to extend to **3Sum**, **4Sum**, **Two Sum BST**, and **k-sum** problems
    

---

Would you like:

- A dry run of the hashmap approach with example?
    
- A reusable Java utility for variants like 2Sum/3Sum?
    
- Top problems in the **2-pointer and hashing** category?