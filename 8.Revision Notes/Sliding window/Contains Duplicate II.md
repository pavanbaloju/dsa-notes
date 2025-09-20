Here’s a complete breakdown of the **“Contains Duplicate II”** problem — a common interview question that combines **HashMap** and **Sliding Window** techniques.

---

## 🔶 Problem: Contains Duplicate II

### ✅ Problem Statement:

Given an integer array `nums` and an integer `k`, return `true` if there are two **distinct indices** `i` and `j` in the array such that:

- `nums[i] == nums[j]`
    
- `abs(i - j) <= k`
    

---

## 🔍 Example:

```java
Input: nums = [1,2,3,1], k = 3  
Output: true   // 1 is repeated within distance 3

Input: nums = [1,0,1,1], k = 1  
Output: true   // 1 is repeated at indices 2 and 3

Input: nums = [1,2,3,1,2,3], k = 2  
Output: false  // duplicates exist, but not within distance 2
```

---

## 🔧 Approach 1: HashMap

### 🔹 Idea:

Store the last index of each element in a HashMap. When the same element is seen again, check if the **distance** between indices is less than or equal to `k`.

### ✅ Java Code:

```java
public boolean containsNearbyDuplicate(int[] nums, int k) {
    Map<Integer, Integer> map = new HashMap<>();  // value -> index
    for (int i = 0; i < nums.length; i++) {
        if (map.containsKey(nums[i])) {
            if (i - map.get(nums[i]) <= k) {
                return true;
            }
        }
        map.put(nums[i], i);  // update the index
    }
    return false;
}
```

---

## ⏱ Time and Space Complexity

|Type|Complexity|
|---|---|
|Time|O(n)|
|Space|O(min(n, k))|

---

## 🔧 Approach 2: Sliding Window with HashSet

### 🔹 Idea:

Maintain a sliding window of size `k`. If any duplicate is found **within the window**, return true.

### ✅ Java Code:

```java
public boolean containsNearbyDuplicate(int[] nums, int k) {
    Set<Integer> window = new HashSet<>();
    for (int i = 0; i < nums.length; i++) {
        if (window.contains(nums[i])) return true;
        window.add(nums[i]);
        if (window.size() > k) {
            window.remove(nums[i - k]);  // shrink window from left
        }
    }
    return false;
}
```

### 💡 Why this works?

- This maintains only the **last k elements** in the set (i.e., sliding window of size `k`).
    
- Ensures we only check for duplicates in the required range.
    

---

## 📌 When to Use Which?

|Approach|Use Case|
|---|---|
|HashMap|Need to track exact last index of every number|
|HashSet|Want to keep only recent `k` elements in memory|

---

## 🧠 Related Patterns

- HashMap / HashSet problems
    
- Sliding Window
    
- Distance-based constraints
    

---

## 🔗 Follow-Up Questions

- What if `k` can be very large? (Memory optimization)
    
- What if the elements are floating-point or objects? (Custom hash/equality)
    
- What if you're allowed only **O(1)** extra space?
    

---

Would you like me to convert this into a **Java template with dry-run comments** for better understanding or include a **visual sliding window demo**?