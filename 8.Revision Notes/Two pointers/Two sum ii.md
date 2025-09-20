Here are the **full notes for Two Sum II – Input Array is Sorted**, including intuition, multiple approaches, and Java code.

---

## ✅ Problem: Two Sum II – Input Array Is Sorted

**Leetcode #167**

> Given a **1-indexed** array of integers `numbers` that is **already sorted in non-decreasing order**, find two numbers such that they add up to a specific `target` number.

Return the indices of the two numbers (1-based index), as an integer array `answer[]` of size 2, where `1 <= answer[0] < answer[1] <= numbers.length`.

**You must use only constant extra space.**

---

## 🔸 Example

```java
Input: numbers = [2, 7, 11, 15], target = 9  
Output: [1, 2] // because numbers[0] + numbers[1] = 2 + 7 = 9
```

---

## 🧠 Intuition

Unlike regular Two Sum, here the input is **sorted**. So we can use the **Two Pointer** technique efficiently without a HashMap.

We maintain a `left` pointer at the start and a `right` pointer at the end and move them based on the sum compared to the target.

---

## ✅ Approach: Two Pointers (Optimal)

### 🔹 Logic

- Initialize two pointers: `left = 0` and `right = n - 1`
    
- While `left < right`:
    
    - Compute `sum = numbers[left] + numbers[right]`
        
    - If `sum == target`, return `[left+1, right+1]`
        
    - If `sum < target`, move `left++`
        
    - If `sum > target`, move `right--`
        

### 🔹 Code (Java)

```java
public int[] twoSum(int[] numbers, int target) {
    int left = 0, right = numbers.length - 1;

    while (left < right) {
        int sum = numbers[left] + numbers[right];
        
        if (sum == target) {
            return new int[] { left + 1, right + 1 }; // 1-indexed
        } else if (sum < target) {
            left++;
        } else {
            right--;
        }
    }
    
    return new int[] {}; // Guaranteed one solution
}
```

---

## ✅ Time and Space Complexity

|Metric|Complexity|
|---|---|
|Time|O(n)|
|Space|O(1)|

---

## ❓ Can it be done with Binary Search?

Yes, but it’s less efficient overall.

### Approach:

For each index `i`, do binary search on the subarray `(i+1 to n-1)` to find `target - numbers[i]`.

**Time**: O(n log n)  
**Space**: O(1)

---

## 🧪 Test Cases

```java
numbers = [2, 3, 4], target = 6        => [1, 3]
numbers = [-1, 0], target = -1         => [1, 2]
numbers = [1, 2, 3, 4, 4, 9, 56, 90], target = 8 => [4, 5]
```

---

## 🔄 Summary

|Condition|Best Approach|Time|Space|
|---|---|---|---|
|Sorted input|Two Pointers|O(n)|O(1)|
|Unsorted input|HashMap|O(n)|O(n)|
|Sorted input, no indices needed|Two Pointers or Binary Search|O(n) / O(n log n)|O(1)|

---

Would you like to continue with **Two Sum IV in BST** or **Three Sum** next?