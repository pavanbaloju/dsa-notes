Here are the **full notes** for the problem:

## 🔍 **Count Substrings Without Repeating Characters**

---

### ✅ 1. Problem Statement

Given a string `s`, return the **number of substrings** where all characters are **unique** (i.e., no repeating characters).

---

### ✅ 2. Input & Output

- **Input**:
    
    - `s = "abc"`
        
- **Output**:
    
    - `6`
        
    - Because the substrings are: `"a"`, `"b"`, `"c"`, `"ab"`, `"bc"`, `"abc"`
        

---

### ✅ 3. Intuition

We want to **count all substrings** (not just the longest one) that **don’t contain any duplicate characters**.

**Key ideas**:

- For every character, use a **sliding window** to extend the right pointer until a duplicate is found.
    
- Every time we extend the window ending at `right`, the number of valid substrings added is `right - left + 1`.
    

---

### ✅ 4. Time and Space Complexity

|Aspect|Value|
|---|---|
|Time|O(n)|
|Space|O(1) (O(128) for ASCII chars)|

---

### ✅ 5. Java Code (Sliding Window)

```java
public int countUniqueSubstrings(String s) {
    int left = 0, count = 0;
    Set<Character> seen = new HashSet<>();

    for (int right = 0; right < s.length(); right++) {
        while (seen.contains(s.charAt(right))) {
            seen.remove(s.charAt(left));
            left++;
        }

        seen.add(s.charAt(right));
        count += right - left + 1;
    }

    return count;
}
```

---

### ✅ 6. Dry Run: `"abc"`

|Left|Right|Window|New Count|Total Count|
|---|---|---|---|---|
|0|0|a|1|1|
|0|1|ab|2|3|
|0|2|abc|3|6|

Substrings counted: `"a"`, `"ab"`, `"abc"`, `"b"`, `"bc"`, `"c"`

---

### ✅ 7. Why does it work?

- Whenever we have a window of length `L` with unique characters, it contributes:
    
    - `L` substrings:
        
        - `[s[i]]` for all `i` in the window
            
        - `[s[i..j]]` for all `i <= j` in that window
            

Sliding window ensures **each substring is counted exactly once**, and duplicates are handled dynamically.

---

### ✅ 8. Alternate Brute Force Approach (TLE for large input)

```java
public int countUniqueSubstrings(String s) {
    int n = s.length(), count = 0;

    for (int i = 0; i < n; i++) {
        Set<Character> set = new HashSet<>();
        for (int j = i; j < n; j++) {
            if (set.contains(s.charAt(j))) break;
            set.add(s.charAt(j));
            count++;
        }
    }

    return count;
}
```

**Time Complexity**: O(n²)  
**Space Complexity**: O(n)

---

### ✅ 9. Patterns and Use Cases

- **Sliding Window with Set/Map** for counting substrings with constraints.
    
- Similar to:
    
    - Longest substring without repeating characters
        
    - Number of substrings with at most K distinct characters (more advanced)
        

---

### ✅ 10. LeetCode Variants

- [Longest Substring Without Repeating Characters](https://leetcode.com/problems/longest-substring-without-repeating-characters/)
    
- [Count Number of Nice Substrings](https://leetcode.com/problems/number-of-substrings-containing-all-three-characters/)
    

---

Let me know if you want:

- The version using frequency arrays instead of HashSet.
    
- The same logic in C++ or Python.
    
- Follow-up: Count substrings with **at most** or **exactly** `K` distinct characters.