Here are the **full notes** on the classic sliding window problem:

---

# 🔍 Longest Substring Without Repeating Characters — Full Notes

### 🔹 Problem Statement:

Given a string `s`, find the length of the **longest substring without repeating characters**.

---

## 1. 🔧 Input & Output

- **Input**: A string `s` (e.g., `"abcabcbb"`)
    
- **Output**: An integer denoting the length of the longest substring without repeating characters  
    (e.g., `3` for `"abc"`)
    

---

## 2. ✅ Key Observations

- The order of characters **matters**.
    
- We need **contiguous substrings**.
    
- We must avoid **repeated characters**.
    
- This is a **Sliding Window** problem with a **HashSet** or **Map** for lookup.
    

---

## 3. ✅ Intuition

- Use a **window** (`start` to `end`) that expands as long as there are no duplicates.
    
- When a duplicate is found, **shrink** the window from the left until the duplicate is removed.
    
- Track the **maximum window size** found along the way.
    

---

## 4. ✅ Time and Space Complexity

|Operation|Complexity|
|---|---|
|Time|`O(n)`|
|Space|`O(n)`|

Why O(n)?  
Each character is visited at most twice (once by `end`, once by `start` when shrinking window).

---

## 5. ✅ Java Code (Using HashSet)

```java
public int lengthOfLongestSubstring(String s) {
    Set<Character> seen = new HashSet<>();
    int left = 0, right = 0, maxLen = 0;

    while (right < s.length()) {
        char ch = s.charAt(right);
        if (!seen.contains(ch)) {
            seen.add(ch);
            maxLen = Math.max(maxLen, right - left + 1);
            right++;
        } else {
            seen.remove(s.charAt(left));
            left++;
        }
    }

    return maxLen;
}
```

---

## 6. ✅ Java Code (Using HashMap — Better for Index Management)

```java
public int lengthOfLongestSubstring(String s) {
    Map<Character, Integer> map = new HashMap<>();
    int maxLen = 0;

    for (int right = 0, left = 0; right < s.length(); right++) {
        char ch = s.charAt(right);
        if (map.containsKey(ch)) {
            // Move left pointer to max of current or one after last occurrence
            left = Math.max(left, map.get(ch) + 1);
        }
        map.put(ch, right);
        maxLen = Math.max(maxLen, right - left + 1);
    }

    return maxLen;
}
```

---

## 7. 🧠 Sliding Window Pattern Breakdown

|Variable|Role|
|---|---|
|`left`|Start of the current window|
|`right`|End of the current window|
|`map` / `set`|Stores characters currently in the window|
|`maxLen`|Tracks max window size seen|

---

## 8. 🧪 Test Cases

|Input|Output|Explanation|
|---|---|---|
|`"abcabcbb"`|`3`|`"abc"`|
|`"bbbbb"`|`1`|`"b"`|
|`"pwwkew"`|`3`|`"wke"`|
|`""`|`0`|Empty string|
|`"au"`|`2`|`"au"`|

---

## 9. 🧠 Use Cases / Patterns

This problem is often used to:

- Teach **sliding window**.
    
- Optimize brute-force `O(n²)` to `O(n)`.
    

---

## 10. 🚫 Brute Force (For contrast)

```java
public int lengthOfLongestSubstring(String s) {
    int maxLen = 0;

    for (int i = 0; i < s.length(); i++) {
        Set<Character> set = new HashSet<>();
        for (int j = i; j < s.length(); j++) {
            if (set.contains(s.charAt(j))) break;
            set.add(s.charAt(j));
        }
        maxLen = Math.max(maxLen, set.size());
    }

    return maxLen;
}
```

**Time Complexity**: `O(n^2)`

---

## 11. Variants & Follow-ups

- Longest Substring With At Most K Distinct Characters.
    
- Longest Substring With At Most Two Distinct Characters.
    
- Longest Repeating Character Replacement.
    
- Minimum Window Substring.
    

---

Let me know if you want the **Leetcode links**, or want to **trace with an example** step-by-step.