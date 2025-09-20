Absolutely. Here's a **comprehensive breakdown of multiple approaches** for the **Sort Colors** (Leetcode 75 / Dutch National Flag) problem, including code, trade-offs, and when to use each.

---

## ✅ Sort Colors – All Approaches (with Java Code + Notes)

---

### 🔹 Problem Recap

Sort an array with only three distinct values (0, 1, 2) **in-place**, and preferably in **one pass**.

---

## ✅ Approach 1: **Counting Sort (Two Passes)**

### 🔸 Idea:

- Count the number of 0s, 1s, and 2s.
    
- Then overwrite the original array with that many 0s, 1s, and 2s.
    

### ✅ Java Code:

```java
public void sortColors(int[] nums) {
    int count0 = 0, count1 = 0, count2 = 0;

    for (int num : nums) {
        if (num == 0) count0++;
        else if (num == 1) count1++;
        else count2++;
    }

    int i = 0;
    while (count0-- > 0) nums[i++] = 0;
    while (count1-- > 0) nums[i++] = 1;
    while (count2-- > 0) nums[i++] = 2;
}
```

### 🔹 Time & Space:

- Time: `O(n)`
    
- Space: `O(1)`
    
- Passes: 2
    

### 🔹 Pros:

- Simple and easy to write
    

### 🔹 Cons:

- Not truly one-pass
    
- Doesn't generalize to unknown range of elements
    

---

## ✅ Approach 2: **Dutch National Flag (One Pass, Optimal)**

### 🔸 Idea:

Use three pointers (`low`, `mid`, `high`) to place 0s to left, 2s to right, keep 1s in the middle.

### ✅ Java Code:

```java
public void sortColors(int[] nums) {
    int low = 0, mid = 0, high = nums.length - 1;

    while (mid <= high) {
        if (nums[mid] == 0) {
            swap(nums, low++, mid++);
        } else if (nums[mid] == 1) {
            mid++;
        } else { // nums[mid] == 2
            swap(nums, mid, high--);
        }
    }
}

private void swap(int[] arr, int i, int j) {
    int temp = arr[i];
    arr[i] = arr[j];
    arr[j] = temp;
}
```

### 🔹 Time & Space:

- Time: `O(n)`
    
- Space: `O(1)`
    
- Passes: 1
    

### 🔹 Pros:

- One pass, in-place, no extra space
    
- Optimal for interview setting
    

### 🔹 Cons:

- Slightly harder to code without bugs
    

---

## ✅ Approach 3: **Built-in Sort (Not Recommended in Interview)**

### ✅ Java Code:

```java
import java.util.Arrays;

public void sortColors(int[] nums) {
    Arrays.sort(nums);
}
```

### 🔹 Time & Space:

- Time: `O(n log n)`
    
- Space: `O(1)` (Java’s sort may use extra space depending on implementation)
    

### 🔹 Cons:

- Violates constraint of "without sort function"
    
- Not suitable for interviews
    

---

## ✅ Approach 4: **Custom Partitioning with Two Passes (Less Efficient than DNF)**

### 🔸 Idea:

- First, move all 0s to the front.
    
- Then move all 1s after 0s.
    

### ✅ Java Code:

```java
public void sortColors(int[] nums) {
    int index = 0;

    // First pass: move 0s
    for (int i = 0; i < nums.length; i++) {
        if (nums[i] == 0) {
            swap(nums, i, index++);
        }
    }

    // Second pass: move 1s
    for (int i = index; i < nums.length; i++) {
        if (nums[i] == 1) {
            swap(nums, i, index++);
        }
    }
}

private void swap(int[] arr, int i, int j) {
    int temp = arr[i];
    arr[i] = arr[j];
    arr[j] = temp;
}
```

### 🔹 Time & Space:

- Time: `O(n)`
    
- Space: `O(1)`
    
- Passes: 2
    

### 🔹 Pros:

- Simpler than full DNF if just learning
    

---

## ✅ Summary Table

|Approach|Time|Space|Passes|Interview Suitability|Notes|
|---|---|---|---|---|---|
|Counting Sort (2-pass)|O(n)|O(1)|2|✅ Good|Simple, safe choice|
|Dutch National Flag (Optimal)|O(n)|O(1)|1|✅✅ Best|Most efficient, one-pass|
|Built-in Sort|O(n log n)|O(1)|1|❌ Not allowed|Avoid in interviews|
|Custom Partitioning (2-pass)|O(n)|O(1)|2|✅ Fair|Simpler variant|

---

## 🔁 Follow-Up Variations

- **Sort Array by Parity** → Odd/Even separation
    
- **Wiggle Sort** → Even-indexed < odd-indexed values
    
- **Group Elements with Frequency Constraints**
    
- **Sort k distinct elements** → Extend DNF to k-way partitioning (bucket sort)
    

---

Would you like me to create:

- A **Java class template with all approaches**?
    
- A **flashcard-style summary** for interview revision?
    
- A **LeetCode practice sheet** with similar problems?