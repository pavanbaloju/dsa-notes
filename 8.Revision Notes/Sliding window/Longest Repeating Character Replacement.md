### **Leetcode 424: Longest Repeating Character Replacement – Revision Notes**

---

## **1. Problem Statement**

You are given a string `s` and an integer `k`.  
You can **replace at most `k` characters** in `s` to make the longest possible substring that contains **only one distinct character**.

**Return the length of the longest possible substring** after performing the replacements.

#### **Example Input & Output**

```plaintext
Input: s = "AABABBA", k = 1  
Output: 4  
Explanation: Replace one 'B' with 'A' to get "AAAA".
```

---

## **2. Intuition & Observations**

- We need to find the **longest contiguous substring** with at most **`k` changes** allowed.
- Since we can replace only `k` characters, we must keep track of **the most frequent character in the current window**.
- **Key Observation:**
    - The **window size - most frequent character count** gives the **number of replacements needed**.
    - If replacements needed **exceed `k`**, shrink the window.

---

## **3. Optimized Approach – Sliding Window (O(n))**

### **Key Idea:**

1. **Expand (`end++`) the window** while keeping track of **character frequencies**.
2. **Calculate required replacements:**
    
    ```plaintext
    Window size - count of most frequent character
    ```
    
3. If **replacements exceed `k`**, **shrink (`start++`)** the window.
4. Keep track of the **maximum valid window size**.
5. **Time Complexity:** **O(n)** (each character is processed at most twice).

---

## **4. Optimized Code (Sliding Window + Frequency Array)**

```java
import java.util.*;

public class LongestRepeatingCharacterReplacement {
    public static int characterReplacement(String s, int k) {
        int[] freq = new int[26]; // Frequency array for A-Z
        int start = 0, maxFreq = 0, maxLength = 0;

        for (int end = 0; end < s.length(); end++) {
            char ch = s.charAt(end);
            freq[ch - 'A']++;
            maxFreq = Math.max(maxFreq, freq[ch - 'A']);

            // If replacements needed > k, shrink window
            while ((end - start + 1) - maxFreq > k) {
                freq[s.charAt(start) - 'A']--;
                start++;
            }

            maxLength = Math.max(maxLength, end - start + 1);
        }

        return maxLength;
    }

    public static void main(String[] args) {
        String s = "AABABBA";
        int k = 1;
        System.out.println("Longest substring length: " + characterReplacement(s, k));
        // Output: 4
    }
}
```

---

## **5. Example Walkthrough**

#### **Input:**

```plaintext
s = "AABABBA", k = 1
```

#### **Window Processing Steps**

|Step|`end`|`start`|Window|Max Frequency|Replacements Needed|Valid?|Max Length|
|---|---|---|---|---|---|---|---|
|1|`0` (`A`)|`0`|`"A"`|`1`|`0`|✅|`1`|
|2|`1` (`A`)|`0`|`"AA"`|`2`|`0`|✅|`2`|
|3|`2` (`B`)|`0`|`"AAB"`|`2`|`1`|✅|`3`|
|4|`3` (`A`)|`0`|`"AABA"`|`3`|`1`|✅|`4`|
|5|`4` (`B`)|`0`|`"AABAB"`|`3`|`2` ❌|❌ Shrink||
|6|`4` (`B`)|`1`|`"ABAB"`|`2`|`2` ❌|❌ Shrink||
|7|`4` (`B`)|`2`|`"BAB"`|`2`|`1`|✅|`4`|
|8|`5` (`B`)|`2`|`"BABB"`|`3`|`1`|✅|`4`|
|9|`6` (`A`)|`2`|`"BABBA"`|`3`|`2` ❌|❌ Shrink||
|10|`6` (`A`)|`3`|`"ABBA"`|`2`|`2` ❌|❌ Shrink||
|11|`6` (`A`)|`4`|`"BBA"`|`2`|`1`|✅|`4`|

✅ **Final Output:** `4` (Substring: `"AABA"` or `"BABB"`)

---

## **6. Time Complexity Analysis**

|**Operation**|**Time Complexity**|
|---|---|
|**Processing each character once**|**O(n)**|
|**Updating Frequency Array**|**O(1)**|
|**Total Complexity**|**O(n)**|

---

## **7. Summary & Key Takeaways**

✅ **Sliding Window allows O(n) solution instead of O(n²).**  
✅ **Tracking most frequent character helps optimize replacements.**  
✅ **Each character is processed at most twice (once added, once removed).**  
✅ **Works efficiently for large constraints (`n ≤ 10⁵`).**

Would you like a **variation of this problem explained**? 🚀