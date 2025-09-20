Here are the **full notes for the Two Sum problem**, including intuition, multiple approaches, trade-offs, and code in Java.

---

## ✅ Problem: Two Sum

**Leetcode #1**

> Given an array of integers `nums` and an integer `target`, return the **indices** of the two numbers such that they add up to `target`.

You may assume that each input would have **exactly one solution**, and you may not use the same element twice.

---

## 🔸 Example

```java
Input: nums = [2, 7, 11, 15], target = 9  
Output: [0, 1]  // Because nums[0] + nums[1] = 2 + 7 = 9
```

---

## 🧠 Intuition

We want to find two indices `i` and `j` such that:

```java
nums[i] + nums[j] == target
```

---

## ✅ Approach 1: Brute Force

- Use two nested loops.
    
- Check every pair `(i, j)` whether their sum is equal to target.
    

### 🔹 Code

```java
public int[] twoSum(int[] nums, int target) {
    for (int i = 0; i < nums.length; i++) {
        for (int j = i + 1; j < nums.length; j++) {
            if (nums[i] + nums[j] == target) {
                return new int[] { i, j };
            }
        }
    }
    return new int[] {}; // Should not reach here if one solution is guaranteed
}
```

### ✅ Time and Space

|Metric|Complexity|
|---|---|
|Time|O(n²)|
|Space|O(1)|

---

## ✅ Approach 2: HashMap Lookup (Optimal)

Use a **HashMap** to store the number and its index as we iterate.

### 🔹 Idea

For each number `num`, check if `target - num` exists in the map.  
If it does, we have a solution.

### 🔹 Code

```java
public int[] twoSum(int[] nums, int target) {
    Map<Integer, Integer> map = new HashMap<>();
    
    for (int i = 0; i < nums.length; i++) {
        int complement = target - nums[i];
        if (map.containsKey(complement)) {
            return new int[] { map.get(complement), i };
        }
        map.put(nums[i], i);
    }
    
    return new int[] {}; // Should never happen if one solution is guaranteed
}
```

### ✅ Time and Space

|Metric|Complexity|
|---|---|
|Time|O(n)|
|Space|O(n)|

---

## 🔁 Variants of Two Sum

|Variant|Description|
|---|---|
|**Two Sum II**|Input array is sorted → use Two Pointer technique|
|**Two Sum IV**|Check if a BST contains two elements that sum to target|
|**Three Sum**|Find triplets that sum to 0|
|**Four Sum**|Find quadruplets that sum to a target|

---

## ✅ Approach 3: Two Pointers (Only if Sorted)

If array is sorted and **you want indices**, use a map or store original indices first.

Otherwise:

```java
public boolean hasTwoSum(int[] nums, int target) {
    Arrays.sort(nums);
    int left = 0, right = nums.length - 1;
    
    while (left < right) {
        int sum = nums[left] + nums[right];
        if (sum == target) return true;
        else if (sum < target) left++;
        else right--;
    }
    return false;
}
```

---

## 🔄 Follow-Up

> What if the array is **very large** and cannot fit into memory?

**Solution:** Use external storage techniques or a streaming approach with a **Set** of previously seen elements.

---

## ✅ Summary Table

|Approach|Time|Space|Use When|
|---|---|---|---|
|Brute Force|O(n²)|O(1)|Very small input size|
|HashMap|O(n)|O(n)|Best for random access arrays|
|Two Pointers|O(n log n) (sort) + O(n)|O(1)|Only when array is sorted or can be sorted|

---

Would you like to practice follow-up variants like “Two Sum in BST” or “Three Sum”?