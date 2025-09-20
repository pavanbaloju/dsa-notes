Here's a complete breakdown of the **"Remove Duplicates from Sorted Array"** problem — including all approaches, Java code, dry run, edge cases, and follow-ups.

---

## ✅ Problem: Remove Duplicates from Sorted Array

---

### 🔸 Statement

Given an **integer array `nums` sorted in non-decreasing order**, remove the duplicates **in-place** such that each unique element appears only once.  
Return the number of unique elements (`k`), and modify `nums` such that the first `k` elements of `nums` contain the unique elements.

---

### 📥 Input:

```java
nums = [0,0,1,1,1,2,2,3,3,4]
```

### 📤 Output:

```java
k = 5, nums = [0,1,2,3,4,_,_,_,_,_]
```

---

## 🔍 Constraints

- Do not use extra space (O(1) space).
    
- Maintain the original relative order.
    
- You can modify the input array in-place.
    

---

## ✅ Approach: Two Pointer Technique

### 🔧 Idea:

- Use two pointers:
    
    - `i` for placing unique elements.
        
    - `j` to iterate over the array.
        
- For every new unique value (`nums[j] != nums[i]`), increment `i` and assign `nums[i] = nums[j]`.
    

---

### ✅ Java Code:

```java
public int removeDuplicates(int[] nums) {
    if (nums.length == 0) return 0;

    int i = 0;  // slow pointer

    for (int j = 1; j < nums.length; j++) {
        if (nums[j] != nums[i]) {
            i++;
            nums[i] = nums[j];
        }
    }

    return i + 1;  // length of unique elements
}
```

---

### ⏱️ Time and Space Complexity:

|Metric|Value|
|---|---|
|Time|O(n)|
|Space|O(1)|

---

## 🔄 Dry Run:

For `nums = [0,0,1,1,1,2,2,3,3,4]`

|Step|i|j|nums|
|---|---|---|---|
|Init|0|1|[0,0,...]|
|j=2|1|2|[0,1,...]|
|j=5|2|5|[0,1,2,...]|
|j=7|3|7|[0,1,2,3,...]|
|j=9|4|9|[0,1,2,3,4...]|

Returns `5`

---

## ⚠️ Edge Cases

1. **Empty Array**: `[]` → return `0`
    
2. **All unique elements**: `[1,2,3,4]` → return length of array
    
3. **All same elements**: `[1,1,1]` → return `1`
    

---

## 🧠 Intuition

- The array is **already sorted**, so duplicates are adjacent.
    
- We can safely overwrite the next slot with the next unique value.
    

---

## 🔁 Follow-Up

### 🔹 What if duplicates are allowed **at most twice**?

Use a variant of the two-pointer where you allow two entries before skipping duplicates.

```java
public int removeDuplicates(int[] nums) {
    int i = 0;
    for (int n : nums) {
        if (i < 2 || n > nums[i - 2]) {
            nums[i++] = n;
        }
    }
    return i;
}
```

---

## 🧪 Test Cases

|Input|Output|
|---|---|
|`[1,1,2]`|`2` + `[1,2,_]`|
|`[0,0,1,1,1,2,2,3,3,4]`|`5` + `[0,1,2,3,4,...]`|
|`[]`|`0`|
|`[1,2,3]`|`3`|

---

## ✅ Summary

- Use **two pointers** for in-place modification.
    
- Increment slow pointer `i` only when new unique value is found.
    
- Return `i + 1` for the count of unique elements.
    

---

Would you like notes for the follow-up: **Remove Duplicates from Sorted Array II** (where at most 2 occurrences are allowed)?