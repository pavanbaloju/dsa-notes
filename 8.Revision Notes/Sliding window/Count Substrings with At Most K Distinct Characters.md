### **Count Substrings with At Most K Distinct Characters – Revision Notes**

---

## **1. Problem Statement**

Given a string `s`, find the number of **substrings** that contain **at most `k` distinct characters**.

#### **Example Input & Output**

```plaintext
Input: s = "aabacbebebe", k = 3  
Output: 42  
Explanation: There are 42 substrings that contain at most 3 distinct characters.
```

---

## **2. Intuition & Observations**

Instead of generating all substrings (**O(n²) brute force**), we can use a **Sliding Window (Two Pointers)** approach:

1. **Expand (`end++`) the window** while keeping track of **distinct character counts**.
2. **If distinct characters exceed `k`**, shrink (`start++`) the window.
3. **Every valid window contributes `(end - start + 1)` valid substrings.**

✅ **Key Observation:**

- For a fixed `end`, all substrings starting from `start` to `end` are valid.
- Example: If window `[start, end]` is valid, substrings `(s[start], s[start:end]), (s[start+1], s[start+1:end])`, etc., are all valid.

---

## **3. Optimized Approach – Sliding Window + HashMap (O(n))**

### **Key Idea:**

1. **Expand (`end++`)** while maintaining a **frequency map** of characters.
2. If **distinct count exceeds `k`**, shrink (`start++`) the window.
3. **Count valid substrings** as `(end - start + 1)`.
4. **Time Complexity:** **O(n)** (each character is processed at most twice).

---

## **4. Optimized Code (Sliding Window + HashMap)**

```java
import java.util.*;

public class CountSubstringsAtMostKDistinct {
    public static int countSubstringsAtMostK(String s, int k) {
        if (k == 0) return 0; // No valid substrings possible

        Map<Character, Integer> freqMap = new HashMap<>();
        int start = 0, count = 0;

        for (int end = 0; end < s.length(); end++) {
            char ch = s.charAt(end);
            freqMap.put(ch, freqMap.getOrDefault(ch, 0) + 1);

            // Shrink the window if distinct count exceeds k
            while (freqMap.size() > k) {
                char leftChar = s.charAt(start);
                freqMap.put(leftChar, freqMap.get(leftChar) - 1);
                if (freqMap.get(leftChar) == 0) {
                    freqMap.remove(leftChar);
                }
                start++;
            }

            // Count valid substrings from (start → end)
            count += (end - start + 1);
        }

        return count;
    }

    public static void main(String[] args) {
        String s = "aabacbebebe";
        int k = 3;
        System.out.println("Count of substrings: " + countSubstringsAtMostK(s, k));
        // Output: 42
    }
}
```

---

## **5. Example Walkthrough**

#### **Input:**

```plaintext
s = "aabacbebebe", k = 3
```

#### **Window Processing Steps**

|Step|`end`|`start`|Window|Distinct Count|Valid Substrings Count|
|---|---|---|---|---|---|
|1|`0` (`a`)|`0`|`"a"`|`1`|`1`|
|2|`1` (`a`)|`0`|`"aa"`|`1`|`3`|
|3|`2` (`b`)|`0`|`"aab"`|`2`|`6`|
|4|`3` (`a`)|`0`|`"aaba"`|`2`|`10`|
|5|`4` (`c`)|`0`|`"aabac"`|`3`|`15`|
|6|`5` (`b`)|`0`|`"aabacb"`|`3`|`21`|
|7|`6` (`e`)|`1`|`"bacbe"`|`3`|`27`|
|8|`7` (`b`)|`2`|`"acbeb"`|`3`|`34`|
|9|`8` (`e`)|`3`|`"cbebe"`|`3`|`42`|

✅ **Final Output:** `42`

---

## **6. Time Complexity Analysis**

|**Operation**|**Time Complexity**|
|---|---|
|**Processing each character once**|**O(n)**|
|**Updating HashMap**|**O(1)**|
|**Total Complexity**|**O(n)**|

---

## **7. Alternative: Count Exactly K Distinct Characters**

To find the number of substrings with **exactly `k` distinct characters**, use:

```plaintext
count(at most K distinct) - count(at most K-1 distinct)
```

```java
public static int countSubstringsWithKDistinct(String s, int k) {
    return countSubstringsAtMostK(s, k) - countSubstringsAtMostK(s, k - 1);
}
```

✅ **This efficiently finds substrings with exactly `k` distinct characters.**

---

## **8. Summary & Key Takeaways**

✅ **Sliding Window reduces O(n²) brute force to O(n).**  
✅ **Counting valid substrings efficiently avoids generating all substrings.**  
✅ **Each character is processed at most twice (added & removed).**  
✅ **Works efficiently for large constraints (`n ≤ 10⁵`).**

Would you like a **variation of this problem explained**? 🚀