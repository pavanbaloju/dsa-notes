Here’s a complete DSA breakdown of **Leetcode 229 – Majority Element II**, with **multiple approaches, Java code, dry run logic, pattern, and variations**. This is an **extension of the Boyer-Moore Voting Algorithm** for elements appearing more than ⌊n/3⌋ times.

---

# ✅ Leetcode 229 – Majority Element II (Full Notes in Java)

---

## 🔹 Problem Statement

> Given an integer array `nums`, return **all elements** that appear **more than ⌊n/3⌋ times**.

📌 At most **two elements** can satisfy this condition.

**Example:**

```text
Input : [3,2,3]  
Output: [3]

Input : [1,1,1,3,3,2,2,2]  
Output: [1,2]
```

---

## 🔍 Key Observations

- An element that appears more than `n/3` times can be **at most 2 elements**:
    
    - If you divide `n` into 3 parts, at most two elements can dominate more than one-third each.
        

---

# 🔻 Brute Force: HashMap Count

### ✅ Java Code:

```java
public List<Integer> majorityElement(int[] nums) {
    Map<Integer, Integer> map = new HashMap<>();
    int n = nums.length;

    for (int num : nums) {
        map.put(num, map.getOrDefault(num, 0) + 1);
    }

    List<Integer> result = new ArrayList<>();
    for (Map.Entry<Integer, Integer> entry : map.entrySet()) {
        if (entry.getValue() > n / 3) {
            result.add(entry.getKey());
        }
    }

    return result;
}
```

### ⏱ Time & Space:

- Time: `O(n)`
    
- Space: `O(n)` (HashMap)
    

### ✅ Easy but uses extra space

### ❌ Not optimal

---

# ✅ Optimal: Extended Boyer-Moore Voting Algorithm

### 🔸 Idea:

Maintain **two candidates and two counters**:

- At most 2 elements can appear more than ⌊n/3⌋ times.
    
- First pass: Find possible candidates.
    
- Second pass: Count actual frequencies to verify.
    

---

### ✅ Java Code:

```java
public List<Integer> majorityElement(int[] nums) {
    int count1 = 0, count2 = 0;
    Integer candidate1 = null, candidate2 = null;

    // Step 1: Find potential candidates
    for (int num : nums) {
        if (candidate1 != null && num == candidate1) {
            count1++;
        } else if (candidate2 != null && num == candidate2) {
            count2++;
        } else if (count1 == 0) {
            candidate1 = num;
            count1 = 1;
        } else if (count2 == 0) {
            candidate2 = num;
            count2 = 1;
        } else {
            count1--;
            count2--;
        }
    }

    // Step 2: Verify candidates
    count1 = count2 = 0;
    for (int num : nums) {
        if (num == candidate1) count1++;
        else if (num == candidate2) count2++;
    }

    List<Integer> result = new ArrayList<>();
    int n = nums.length;
    if (count1 > n / 3) result.add(candidate1);
    if (count2 > n / 3) result.add(candidate2);

    return result;
}
```

---

### ⏱ Time & Space:

- Time: `O(n)`
    
- Space: `O(1)` – no extra space except output
    

### ✅ Most optimal

### ✅ Constant space

### ✅ Very common in interviews (Google, Amazon)

---

## 🔁 Dry Run Example

**Input:** `[1,1,1,3,3,2,2,2]`  
**Candidates After Pass 1:** candidate1 = 1, candidate2 = 2  
**Verification Pass:**

- 1 → appears 3 times
    
- 2 → appears 3 times  
    ✅ Both > n/3 (8/3 ≈ 2.66)
    

---

## 🧠 Summary – Boyer-Moore (n/3)

|Step|Action|
|---|---|
|Pass 1|Identify at most 2 candidates|
|Pass 2|Verify if they appear > n/3|
|Why 2 only?|⌊n/3⌋ implies max 2 elements|

---

## 📊 Comparison Table

|Approach|Time|Space|Interview Friendly|Notes|
|---|---|---|---|---|
|HashMap|O(n)|O(n)|⚠️ Okay|Easy, not space optimal|
|Extended Boyer-Moore|O(n)|O(1)|✅ Best|Two passes, elegant logic|

---

## 🧩 Variations

|Problem|How to Solve|
|---|---|
|Majority Element > n/2 (LC 169)|Boyer-Moore with 1 candidate|
|Majority Elements > n/k|Generalized Boyer-Moore (k-1 candidates)|
|Majority in streaming array|Use Voting with verification on batch|

---

## ✅ Leetcode Link

- [Leetcode 229 – Majority Element II](https://leetcode.com/problems/majority-element-ii/)
    

---

Would you like a:

- Generalized version for majority > n/k?
    
- Visual explanation of the voting process?
    
- Practice set with similar frequency-based questions?