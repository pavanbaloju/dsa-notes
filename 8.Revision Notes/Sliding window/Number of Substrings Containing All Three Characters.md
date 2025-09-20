### **Number of Substrings Containing All Three Characters (Leetcode 1358)**

---

## **1. Problem Statement**

Given a string `s` consisting only of characters **'a'**, **'b'**, and **'c'**, return the **number of substrings that contain at least one 'a', one 'b', and one 'c'**.

#### **Example Input & Output**

```plaintext
Input:  s = "abcabc"
Output: 10
Explanation: The substrings are ["abc", "abca", "abcab", "abcabc", "bca", "bcab", "bcabc", "cab", "cabc", "abc"]
```

---

## **2. Intuition & Observations**

- The substring **must contain at least one 'a', one 'b', and one 'c'**.
- Instead of generating all substrings (**O(n²)** brute force), we can use a **Sliding Window (Two Pointers)** approach.
- **Key Idea:**
    - Expand `end++` until we have at least one 'a', 'b', and 'c'.
    - Once valid, **every substring starting from `start` to `end` is also valid**.
    - Count the number of valid substrings efficiently.

---

## **3. Optimized Approach – Sliding Window (O(n))**

### **Key Idea:**

1. **Expand (`end++`)** until the substring contains at least one 'a', 'b', and 'c'.
2. **Once valid, every substring starting at `start` is also valid** (since removing characters from the end does not affect validity).
3. **Count valid substrings:**
    - For a fixed `end`, all substrings starting from `start` to `n-1` are valid.
    - Add `(n - end)` to the result.
4. **Shrink (`start++`)** to check for new valid substrings.
5. **Time Complexity:** **O(n)** (each character processed at most twice).

---

## **4. Optimized Code (Sliding Window + HashMap)**

```java
public class SubstringsWithAllThreeChars {
    public static int numberOfSubstrings(String s) {
        int[] count = new int[3]; // Count occurrences of 'a', 'b', 'c'
        int start = 0, result = 0;

        for (int end = 0; end < s.length(); end++) {
            count[s.charAt(end) - 'a']++; // Increment character frequency

            // If all characters are present, count valid substrings
            while (count[0] > 0 && count[1] > 0 && count[2] > 0) {
                result += s.length() - end; // All substrings (start → end, ..., start → n-1) are valid
                count[s.charAt(start) - 'a']--; // Shrink window from the left
                start++;
            }
        }

        return result;
    }

    public static void main(String[] args) {
        String s = "abcabc";
        System.out.println("Number of substrings: " + numberOfSubstrings(s));
        // Output: 10
    }
}
```

---

## **5. Example Walkthrough**

#### **Input:**

```plaintext
s = "abcabc"
```

#### **Window Processing Steps**

|Step|`end`|`start`|Window|Valid?|Valid Substrings Count|
|---|---|---|---|---|---|
|1|`0` (`a`)|`0`|`"a"`|❌|`0`|
|2|`1` (`b`)|`0`|`"ab"`|❌|`0`|
|3|`2` (`c`)|`0`|`"abc"`|✅|`4` (Substrings: `"abc", "abca", "abcab", "abcabc"`)|
|4|`3` (`a`)|`1`|`"bca"`|✅|`3` (Substrings: `"bca", "bcab", "bcabc"`)|
|5|`4` (`b`)|`2`|`"cab"`|✅|`2` (Substrings: `"cab", "cabc"`)|
|6|`5` (`c`)|`3`|`"abc"`|✅|`1` (Substring: `"abc"`)|

✅ **Final Output:** `10`

---

## **6. Time Complexity Analysis**

|**Operation**|**Time Complexity**|
|---|---|
|**Processing each character once**|**O(n)**|
|**Updating Frequency Array**|**O(1)**|
|**Total Complexity**|**O(n)**|

---

## **7. Summary & Key Takeaways**

✅ **Sliding Window reduces O(n²) brute force to O(n).**  
✅ **Counting valid substrings efficiently avoids generating all substrings.**  
✅ **Each character is processed at most twice (added & removed).**  
✅ **Works efficiently for large constraints (`n ≤ 10⁵`).**

Would you like a **variation of this problem explained**? 🚀