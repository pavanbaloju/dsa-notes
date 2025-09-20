Here are **full notes** for the problem **"Longest Substring with At Most K Distinct Characters"**, a classic **Sliding Window + HashMap** pattern problem:

---

## 🔍 Problem Statement

Given a string `s` and an integer `k`, return the **length of the longest substring** that contains **at most `k` distinct characters**.

---

## ✅ 1. Example

```java
Input: s = "eceba", k = 2  
Output: 3  
Explanation: The substring is "ece" with 2 distinct characters.
```

---

## ✅ 2. Intuition

- We need to **maintain a window** of characters such that the number of **distinct characters** inside it is **at most `k`**.
    
- Every time we **add a new character**, if distinct count exceeds `k`, we **shrink the window** from the left until the condition is valid again.
    

---

## ✅ 3. Time and Space Complexity

|Operation|Complexity|
|---|---|
|Time|O(n)|
|Space|O(k) or O(26/128) depending on charset|

---

## ✅ 4. Java Code Using HashMap

```java
public int lengthOfLongestSubstringKDistinct(String s, int k) {
    if (s == null || s.length() == 0 || k == 0) return 0;

    Map<Character, Integer> map = new HashMap<>();
    int left = 0, right = 0;
    int maxLength = 0;

    while (right < s.length()) {
        char c = s.charAt(right);
        map.put(c, map.getOrDefault(c, 0) + 1);
        right++;

        // Shrink the window if more than k distinct characters
        while (map.size() > k) {
            char leftChar = s.charAt(left);
            map.put(leftChar, map.get(leftChar) - 1);
            if (map.get(leftChar) == 0) {
                map.remove(leftChar);
            }
            left++;
        }

        maxLength = Math.max(maxLength, right - left);
    }

    return maxLength;
}
```

---

## ✅ 5. Dry Run (s = "eceba", k = 2)

|Window|Distinct|Action|maxLength|
|---|---|---|---|
|"e"|1|Expand|1|
|"ec"|2|Expand|2|
|"ece"|2|Expand|3|
|"eceb"|3|Shrink → "ceb"|3|
|"ceba"|3|Shrink → "ba"|3|

Final answer: `3`

---

## ✅ 6. Edge Cases

- If `k == 0`: return `0`
    
- If `s.length() < k`: return `s.length()`
    
- If all characters are the same: return `s.length()`
    
- If `k >= 26` (or total unique chars in input), return full string
    

---

## ✅ 7. Alternative: Using Array for Fixed Character Set (lowercase)

```java
public int lengthOfLongestSubstringKDistinct(String s, int k) {
    int[] count = new int[128]; // ASCII
    int distinct = 0, left = 0, max = 0;

    for (int right = 0; right < s.length(); right++) {
        if (count[s.charAt(right)]++ == 0) distinct++;

        while (distinct > k) {
            if (--count[s.charAt(left++)] == 0) distinct--;
        }

        max = Math.max(max, right - left + 1);
    }

    return max;
}
```

---

## ✅ 8. Related Problems

|Problem|Pattern|
|---|---|
|Longest Substring Without Repeating Characters|Sliding Window + Set|
|Longest Substring With At Most Two Distinct|Sliding Window + HashMap|
|Minimum Window Substring|Sliding Window + Counter|
|Longest Repeating Character Replacement|Sliding Window + Frequency|

---

## ✅ 9. Interview Tip

This is a **classic FAANG sliding window** question that tests your understanding of:

- Maintaining a condition (distinct count)
    
- Dynamically shrinking/growing the window
    
- Using frequency maps
    

You can confidently expect this or a variation in interviews involving strings and window logic.

---

Would you like a visual dry run or Python version too?