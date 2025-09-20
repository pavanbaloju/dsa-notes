### **Longest Substring with At Most K Distinct Characters – Revision Notes**

---

## **1. Problem Statement**

Given a string `s` and an integer `k`, find the **length of the longest substring** that contains at most `k` distinct characters.

---

## **2. Naive Approach – Brute Force (O(n²))**

- Generate **all substrings** and count distinct characters in each.
- If a substring has **≤ k distinct characters**, update the max length.
- **Time Complexity:** **O(n²)** (checking distinct characters in every substring).

#### **Brute Force Code:**

```java
public static int longestSubstringBruteForce(String s, int k) {
    int maxLength = 0;

    for (int i = 0; i < s.length(); i++) {
        Set<Character> distinct = new HashSet<>();
        for (int j = i; j < s.length(); j++) {
            distinct.add(s.charAt(j));
            if (distinct.size() > k) break;
            maxLength = Math.max(maxLength, j - i + 1);
        }
    }

    return maxLength;
}
```

✅ **Works, but inefficient for large `n` (`n ≤ 10⁵`).**

---

## **3. Optimized Approach – Sliding Window + HashMap (O(n))**

### **Key Idea:**

- Use **two pointers (`start` and `end`)** to maintain a **window** with **≤ k distinct characters**.
- Use a **HashMap** to store character frequencies.
- **Sliding Window Mechanism:**
    1. Expand `end++` to include characters in the window.
    2. If distinct characters **exceed `k`**, shrink `start++` to restore validity.
    3. Keep track of the **maximum valid window size**.
- **Time Complexity:** **O(n)** (each character processed at most twice).

---

### **4. Optimized Code (Sliding Window + HashMap)**

```java
import java.util.*;

public class LongestSubstringAtMostKDistinct {
    public static int longestSubstring(String s, int k) {
        Map<Character, Integer> freqMap = new HashMap<>();
        int start = 0, maxLength = 0;

        for (int end = 0; end < s.length(); end++) {
            char ch = s.charAt(end);
            freqMap.put(ch, freqMap.getOrDefault(ch, 0) + 1);

            // If distinct character count exceeds k, shrink window
            while (freqMap.size() > k) {
                char leftChar = s.charAt(start);
                freqMap.put(leftChar, freqMap.get(leftChar) - 1);
                if (freqMap.get(leftChar) == 0) {
                    freqMap.remove(leftChar);
                }
                start++;
            }

            maxLength = Math.max(maxLength, end - start + 1);
        }

        return maxLength;
    }

    public static void main(String[] args) {
        String s = "aabacbebebe";
        int k = 3;
        System.out.println("Longest substring length: " + longestSubstring(s, k));
        // Output: 7 ("cbebebe")
    }
}
```

---

### **5. Example Walkthrough**

#### **Input:**

```plaintext
s = "aabacbebebe", k = 3
```

#### **Window Processing Steps**

|Step|`end`|`start`|Window|Distinct Count|Max Length|
|---|---|---|---|---|---|
|1|`0` (`a`)|`0`|`"a"`|`1`|`1`|
|2|`1` (`a`)|`0`|`"aa"`|`1`|`2`|
|3|`2` (`b`)|`0`|`"aab"`|`2`|`3`|
|4|`3` (`a`)|`0`|`"aaba"`|`2`|`4`|
|5|`4` (`c`)|`0`|`"aabac"`|`3`|`5`|
|6|`5` (`b`)|`0`|`"aabacb"`|`3`|`6`|
|7|`6` (`e`)|`0`|`"aabacbe"`|`4` ❌|`6`|
|8|`7` (`b`)|`2`|`"bacbeb"`|`3` ✅|`6`|
|9|`8` (`e`)|`2`|`"bacbebe"`|`3` ✅|`7`|
|10|`9` (`b`)|`2`|`"cbebebe"`|`3` ✅|`7`|
|11|`10` (`e`)|`2`|`"cbebebe"`|`3` ✅|`7`|

✅ **Final Output:** `7` (Substring: `"cbebebe"`)

---

### **6. Time Complexity Analysis**

|**Operation**|**Time Complexity**|
|---|---|
|**Processing each character once**|**O(n)**|
|**Updating HashMap**|**O(1)**|
|**Total Complexity**|**O(n)**|

---

### **7. Key Takeaways**

✅ **Brute force takes O(n²), while sliding window reduces it to O(n).**  
✅ **HashMap efficiently tracks character frequencies.**  
✅ **Each character is processed at most twice (added & removed).**  
✅ **Handles large constraints (`n ≤ 10⁵`) efficiently.**

Would you like any variations of this problem? 🚀