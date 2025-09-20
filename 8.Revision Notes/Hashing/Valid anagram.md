Here’s the complete DSA breakdown for the string problem **“Valid Anagram”**, including multiple approaches, Java code, and interview-level reasoning.

---

# ✅ Problem: Valid Anagram (Leetcode 242)

---

## 🔹 Problem Statement

> Given two strings `s` and `t`, return `true` if `t` is an anagram of `s`, and `false` otherwise.

📌 An **anagram** is formed by rearranging the letters of a word, using all original letters exactly once.

---

### 🔸 Examples:

```text
Input: s = "anagram", t = "nagaram"
Output: true

Input: s = "rat", t = "car"
Output: false
```

---

## 🔁 Pattern

- **Character frequency counting**
    
- **Hashing or fixed-size array for alphabets**
    
- **Sorting comparison**
    

---

# 🔻 Approach 1: Sort Both Strings

### ✅ Java Code:

```java
public boolean isAnagram(String s, String t) {
    if (s.length() != t.length()) return false;

    char[] a = s.toCharArray();
    char[] b = t.toCharArray();
    Arrays.sort(a);
    Arrays.sort(b);

    return Arrays.equals(a, b);
}
```

---

### ⏱ Time & Space:

- Time: `O(n log n)`
    
- Space: `O(n)` for character arrays
    

### ✅ Simple to implement

### ❌ Sorting is slower than counting

---

# ✅ Approach 2: Count Frequencies Using Array (Optimal for lowercase letters)

### 🔸 Assumption: Only lowercase English letters (a–z)

### ✅ Java Code:

```java
public boolean isAnagram(String s, String t) {
    if (s.length() != t.length()) return false;

    int[] count = new int[26];

    for (int i = 0; i < s.length(); i++) {
        count[s.charAt(i) - 'a']++;
        count[t.charAt(i) - 'a']--;
    }

    for (int freq : count) {
        if (freq != 0) return false;
    }

    return true;
}
```

---

### ⏱ Time & Space:

- Time: `O(n)`
    
- Space: `O(1)` (fixed array of 26 characters)
    

### ✅ Best choice for lowercase-only strings

### ✅ Fastest and most memory-efficient

---

# 🔸 Approach 3: HashMap Count (Handles Unicode too)

### ✅ Java Code:

```java
public boolean isAnagram(String s, String t) {
    if (s.length() != t.length()) return false;

    Map<Character, Integer> map = new HashMap<>();

    for (char c : s.toCharArray()) {
        map.put(c, map.getOrDefault(c, 0) + 1);
    }

    for (char c : t.toCharArray()) {
        if (!map.containsKey(c)) return false;

        map.put(c, map.get(c) - 1);
        if (map.get(c) == 0) map.remove(c);
    }

    return map.isEmpty();
}
```

---

### ⏱ Time & Space:

- Time: `O(n)`
    
- Space: `O(k)` for unique characters (k ≤ n)
    

### ✅ Best for Unicode, multilingual input

### ❌ Slightly slower than array for fixed character sets

---

## 📊 Comparison Table

|Approach|Time|Space|Notes|
|---|---|---|---|
|Sort both strings|O(n log n)|O(n)|Easy, but not optimal|
|Count with array (26)|O(n)|O(1)|✅ Best for lowercase a–z|
|HashMap count|O(n)|O(k)|✅ Best for general Unicode input|

---

## 🧠 Edge Cases

- Unequal lengths → false immediately
    
- Empty strings → return true
    
- Case sensitivity: `"A"` ≠ `"a"` unless explicitly normalized
    

---

## 🔗 Leetcode Link

- [Leetcode 242 – Valid Anagram](https://leetcode.com/problems/valid-anagram/)
    

---

## ✅ Summary

- Use **character frequency comparison**.
    
- For only lowercase a–z → use fixed array.
    
- For Unicode → use HashMap.
    
- Avoid sorting in interviews unless asked for lexicographic output.
    

---

Would you like:

- A version that handles whitespace, punctuation, or case-insensitive?
    
- Practice problems based on anagram variations (group anagrams, isomorphic strings, etc.)?