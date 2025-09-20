Here are **full notes for the 3Sum problem**, including intuition, brute force, optimized approach with two pointers, and Java code.

---

## ✅ Problem: 3Sum (Leetcode #15)

> Given an integer array `nums`, return all the **unique triplets** `[nums[i], nums[j], nums[k]]` such that:
> 
> - `i != j != k`, and
>     
> - `nums[i] + nums[j] + nums[k] == 0`.
>     

The solution set must **not contain duplicate** triplets.

---

## 🔸 Example

```java
Input: nums = [-1, 0, 1, 2, -1, -4]
Output: [[-1, -1, 2], [-1, 0, 1]]
```

---

## 🧠 Intuition

The brute force way would be to try every combination of three elements. But that’s O(n³) time. We can do better.

The key idea:

- Sort the array.
    
- Fix one element, and use the **Two Pointers** technique to find the other two that sum to `-fixed`.
    

---

## ✅ Optimal Approach: Sorting + Two Pointers

### 🔹 Steps:

1. **Sort** the array → so we can skip duplicates and use two pointers.
    
2. Loop `i` from 0 to n-2:
    
    - Skip duplicates for `i`.
        
    - Set two pointers: `left = i+1`, `right = n-1`.
        
    - While `left < right`, calculate `sum = nums[i] + nums[left] + nums[right]`
        
        - If sum == 0 → add to result, skip duplicates, move both pointers.
            
        - If sum < 0 → move `left++`
            
        - If sum > 0 → move `right--`
            

---

### 🔹 Code (Java)

```java
public List<List<Integer>> threeSum(int[] nums) {
    List<List<Integer>> res = new ArrayList<>();
    Arrays.sort(nums); // Step 1: Sort the array
    
    for (int i = 0; i < nums.length - 2; i++) {
        if (i > 0 && nums[i] == nums[i - 1]) continue; // Skip duplicate `i`
        
        int left = i + 1;
        int right = nums.length - 1;
        
        while (left < right) {
            int sum = nums[i] + nums[left] + nums[right];
            
            if (sum == 0) {
                res.add(Arrays.asList(nums[i], nums[left], nums[right]));
                left++;
                right--;
                
                // Skip duplicates
                while (left < right && nums[left] == nums[left - 1]) left++;
                while (left < right && nums[right] == nums[right + 1]) right--;
            }
            else if (sum < 0) {
                left++;
            }
            else {
                right--;
            }
        }
    }
    
    return res;
}
```

---

## ✅ Time and Space Complexity

|Metric|Complexity|
|---|---|
|Time|O(n²)|
|Space|O(1) (excluding output)|

- Sorting takes O(n log n), outer loop O(n), inner loop O(n) → total O(n²)
    
- Uses no extra data structures for lookup → constant space (apart from output list)
    

---

## 🔄 Summary Table

|Approach|Time Complexity|Space Complexity|Notes|
|---|---|---|---|
|Brute Force (3 loops)|O(n³)|O(1)|Too slow for large inputs|
|HashSet (for 2Sum)|O(n²)|O(n)|Requires care for duplicates|
|Two Pointers (optimal)|✅ O(n²)|✅ O(1)|Clean, efficient, no extra space|

---

## 🧪 Test Cases

```java
Input: [-1, 0, 1, 2, -1, -4]
Output: [[-1, -1, 2], [-1, 0, 1]]

Input: [0, 0, 0]
Output: [[0, 0, 0]]

Input: []
Output: []

Input: [1, 2, -2, -1]
Output: []
```

---

## 📌 Variants

- **3Sum Closest** – Find triplet whose sum is closest to a given target.
    
- **3Sum Smaller** – Count triplets with sum less than a target.
    
- **4Sum** – Generalization of the problem (can also be solved with 2 pointers + loop).
    
- **kSum** – Recursive generalization.
    

---

Would you like to continue with **3Sum Closest** or move on to **4Sum**?