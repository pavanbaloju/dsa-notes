Here’s a complete breakdown of the classic problem **“Group Anagrams”** — from logic to **Java code**, with optimal approaches, dry run examples, and follow-up variations.

---

# ✅ Problem: Group Anagrams (Leetcode 49)

---

## 🔹 Problem Statement

> Given an array of strings, group the anagrams together.  
> Return a list of groups, where each group contains strings that are anagrams of each other.

---

### 🔸 Example:

```text
Input: ["eat","tea","tan","ate","nat","bat"]
Output:
[
  ["eat","tea","ate"],
  ["tan","nat"],
  ["bat"]
]
```

---

## 🔁 Pattern

- **Hashing based on anagram signature**
    
- **Map<String, List>** to collect groups
    
- Efficient string normalization (sorted string or char frequency)
    

---

# 🔻 Approach 1: Sort Each String and Use It as Key

### 🔸 Idea:

- Sort characters of each string → gives the **same key** for all anagrams.
    
- Use this sorted string as a **key in HashMap**.
    

---

### ✅ Java Code:

```java
public List<List<String>> groupAnagrams(String[] strs) {
    Map<String, List<String>> map = new HashMap<>();

    for (String str : strs) {
        char[] chars = str.toCharArray();
        Arrays.sort(chars);
        String key = new String(chars); // sorted key

        map.computeIfAbsent(key, k -> new ArrayList<>()).add(str);
    }

    return new ArrayList<>(map.values());
}
```

---

### ⏱ Time & Space:

- Time: `O(n * k log k)`
    
    - `n`: number of strings
        
    - `k`: average string length (for sorting)
        
- Space: `O(n * k)`
    
    - to store all groups and sorted keys
        

---

### ✅ Simple, readable, and very effective

### ✅ Commonly used in interviews

---

# ✅ Approach 2: Character Count Array as Key (Optimal for lowercase a–z)

### 🔸 Idea:

- Each anagram has the **same frequency of characters**
    
- Use a **count array of size 26**, then convert it to a unique key string
    

---

### ✅ Java Code:

```java
public List<List<String>> groupAnagrams(String[] strs) {
    Map<String, List<String>> map = new HashMap<>();

    for (String str : strs) {
        int[] count = new int[26];
        for (char c : str.toCharArray()) {
            count[c - 'a']++;
        }

        // Build a unique key from character counts
        StringBuilder sb = new StringBuilder();
        for (int freq : count) {
            sb.append(freq).append('#'); // delimiter to avoid ambiguity
        }

        String key = sb.toString();
        map.computeIfAbsent(key, k -> new ArrayList<>()).add(str);
    }

    return new ArrayList<>(map.values());
}
```

---

### ⏱ Time & Space:

- Time: `O(n * k)` → no sorting, just counting
    
- Space: `O(n * k)`
    

### ✅ More efficient than sorting for long strings

### ✅ Best if only lowercase letters (a–z)

---

## 🔁 Dry Run Example:

Input: `["eat", "tea", "tan", "ate", "nat", "bat"]`

- `"eat"` → sorted = `"aet"`
    
- `"tea"` → `"aet"`
    
- `"tan"` → `"ant"`
    
- `"ate"` → `"aet"`
    
- `"nat"` → `"ant"`
    
- `"bat"` → `"abt"`
    

Groups:

- `"aet"` → `["eat", "tea", "ate"]`
    
- `"ant"` → `["tan", "nat"]`
    
- `"abt"` → `["bat"]`
    

---

## 📊 Comparison Table

|Approach|Time Complexity|Space Complexity|Notes|
|---|---|---|---|
|Sort Each String (key)|O(n × k log k)|O(n × k)|✅ Easy and clean|
|Char Count Array (key)|O(n × k)|O(n × k)|✅ Faster, more efficient|

---

## 📦 Variations

|Variant|Description|
|---|---|
|Group anagrams ignoring case|Normalize strings to lowercase|
|Group anagrams with unicode|Use `Map<Character, Integer>` instead of 26-length array|
|Count number of anagram groups|Return only count of groups|
|Return largest anagram group|Track max group while forming|

---

## 🔗 Leetcode Link

- [Leetcode 49 – Group Anagrams](https://leetcode.com/problems/group-anagrams/)
    

---

## ✅ Summary

- Use **sorted string** or **character frequency array** as key in HashMap.
    
- Sorting is simple and readable.
    
- Frequency array is faster and space-efficient for a–z strings.
    
- Commonly asked by Google, Amazon, Microsoft, etc.
    

---

Would you like:

- A version that handles case-insensitive anagrams?
    
- Practice problems on anagram families and groupings?
    
- Visualization of how keys are formed and grouped?