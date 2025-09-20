Here’s a full DSA note for the problem **“Find the Majority Element (appears more than ⌊n/2⌋ times)”**, with **multiple approaches**, **Java code**, **time/space analysis**, and **interview insights**.

---

# ✅ Majority Element (> n/2 times) – Full DSA Notes (Java)

---

## 🔹 Problem Statement

> Given an array `nums` of size `n`, find the element that appears more than `n/2` times.  
> You may assume that the majority element **always exists**.

**Example:**

```text
Input : [2, 2, 1, 1, 1, 2, 2]  
Output: 2
```

---

## 🔁 Pattern

- **Voting** (Boyer-Moore)
    
- **Hash Map Counting**
    
- **Sorting**
    

---

## 🧪 Test Case Expectations

|Input|Output|
|---|---|
|[3,3,4]|3|
|[1,1,1,2,3,4,1]|1|
|[5,5,5,5,5,5,1,2,3]|5|

---

# 🔻 Brute Force: Count Frequencies

### ✅ Java Code:

```java
public int majorityElement(int[] nums) {
    int n = nums.length;

    for (int i = 0; i < n; i++) {
        int count = 0;
        for (int j = 0; j < n; j++) {
            if (nums[j] == nums[i]) count++;
        }
        if (count > n / 2) return nums[i];
    }

    return -1; // Should never reach here as per problem constraint
}
```

### ⏱ Time & Space:

- Time: `O(n^2)`
    
- Space: `O(1)`
    

### ❌ Not suitable for interviews due to quadratic time.

---

# 🔸 Better: HashMap Frequency Count

### ✅ Java Code:

```java
public int majorityElement(int[] nums) {
    Map<Integer, Integer> map = new HashMap<>();
    int n = nums.length;

    for (int num : nums) {
        map.put(num, map.getOrDefault(num, 0) + 1);
        if (map.get(num) > n / 2) return num;
    }

    return -1;
}
```

### ⏱ Time & Space:

- Time: `O(n)`
    
- Space: `O(n)`
    

### ✅ Easy to implement

### ❌ Not optimal in terms of space

---

# ✅ Optimal: Boyer-Moore Voting Algorithm

### 🔸 Idea:

1. Maintain a `count` and a `candidate`.
    
2. If `count == 0`, set `candidate = current element`.
    
3. If current element == candidate, increment count.
    
4. Else, decrement count.
    
5. At the end, the candidate will be the majority element.
    

### ✅ Java Code:

```java
public int majorityElement(int[] nums) {
    int count = 0, candidate = 0;

    for (int num : nums) {
        if (count == 0) {
            candidate = num;
        }
        count += (num == candidate) ? 1 : -1;
    }

    return candidate;
}
```

### ⏱ Time & Space:

- Time: `O(n)`
    
- Space: `O(1)`
    

### ✅ Most optimal and interview-preferred

### ✅ Constant space, single pass

### 🧠 Elegant logic

---

## 🧠 Why Boyer-Moore Works

- Every time a non-majority element cancels out a majority vote,  
    the majority still stays ahead due to its higher count.
    
- When the loop ends, only the majority element can remain.
    

---

# 📊 Comparison Table

|Approach|Time|Space|Use in Interview|Notes|
|---|---|---|---|---|
|Brute Force|O(n²)|O(1)|❌ No|Only for learning|
|HashMap Counting|O(n)|O(n)|⚠️ Maybe|Easy but uses extra space|
|Boyer-Moore Voting|O(n)|O(1)|✅✅ Yes|Optimal, elegant, and scalable|

---

# 🔁 Variations

| Problem                 | Description                               |
| ----------------------- | ----------------------------------------- |
| Majority element > n/3  | Use two candidates (Leetcode 229)         |
| Find all elements > n/k | Generalized version using HashMap         |
| Voting + verification   | If not guaranteed to exist, verify at end |

---

## 🔎 Leetcode Links

- [Leetcode 169 – Majority Element](https://leetcode.com/problems/majority-element/)
    
- [Leetcode 229 – Majority Element II](https://leetcode.com/problems/majority-element-ii/)
    

---

## ✅ Summary

- Master the **Boyer-Moore Voting Algorithm**.
    
- For `> n/3`, extend to **two candidates**.
    
- Verify frequency if majority existence isn’t guaranteed.
    

---

Would you like:

- A side-by-side Java class with all 3 approaches?
    
- A visual explanation of Boyer-Moore with dry run?
    
- A follow-up problem set (like majority > n/3, majority in stream, etc.)?