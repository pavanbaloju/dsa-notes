### **Leetcode 278 – First Bad Version (Revision Notes)**

---

## **1️⃣ Problem Statement**

You are given an API `isBadVersion(version)`, which returns `true` if a version is **bad** and `false` otherwise. You need to find the **first bad version** in a sequence `[1, 2, ..., n]`.

🔹 **Constraints:**

- `1 ≤ n ≤ 2³¹ - 1` (**Large Input Size**)
- There is at least **one** bad version.

---

## **2️⃣ Key Idea – Binary Search on First Occurrence**

✅ **Why Binary Search?**

- Instead of checking every version **(`O(n)`)**, we use **Binary Search (`O(log n)`)**.
- If `mid` is **bad**, the first bad version is **left** of `mid` (including `mid`).
- If `mid` is **not bad**, the first bad version is **right** of `mid` (excluding `mid`).

✅ **Time Complexity:** **O(log n)**  
✅ **Space Complexity:** **O(1) (Iterative)**

---

## **3️⃣ Binary Search Approach (Iterative)**

### **Algorithm Steps:**

1. Initialize **`left = 1`** and **`right = n`**.
2. Compute `mid = left + (right - left) / 2` (to prevent overflow).
3. **Check if `mid` is a bad version:**
    - If `isBadVersion(mid) == true`, search **left half** (`right = mid`).
    - Else, search **right half** (`left = mid + 1`).
4. Repeat until `left == right`.
5. Return `left` as the **first bad version**.

---

## **4️⃣ Code Implementation (Iterative)**

```java
public class Solution extends VersionControl {
    public int firstBadVersion(int n) {
        int left = 1, right = n;

        while (left < right) { // Continue while search space > 1
            int mid = left + (right - left) / 2; // Prevent overflow

            if (isBadVersion(mid)) {
                right = mid; // Search left (including mid)
            } else {
                left = mid + 1; // Search right (excluding mid)
            }
        }

        return left; // First bad version
    }
}
```

✅ **Why `right = mid` and not `mid - 1`?**

- `mid` could be the **first bad version**, so we **include** it in the search.

✅ **Why stop at `left == right`?**

- `left` will point to the **first bad version**, ensuring correctness.

---

## **5️⃣ Example Walkthrough**

🔹 **Input:**

```plaintext
n = 5, firstBadVersion = 4
isBadVersion(1) -> false
isBadVersion(2) -> false
isBadVersion(3) -> false
isBadVersion(4) -> true
isBadVersion(5) -> true
```

🔹 **Execution Steps:**

|Iteration|`left`|`right`|`mid`|`isBadVersion(mid)`|Action|
|---|---|---|---|---|---|
|1|`1`|`5`|`3`|`false`|Search right (`left = 4`)|
|2|`4`|`5`|`4`|`true`|Search left (`right = 4`)|
|3 (Exit)|`4`|`4`|`4`|**Found**|Return `4`|

✅ **Output:** `4` (First bad version)

---

## **6️⃣ Edge Cases & Handling**

|**Case**|**Example**|**Handling**|
|---|---|---|
|**Only One Version (`n = 1`)**|`isBadVersion(1) == true`|Returns `1` immediately|
|**First Version is Bad**|`n = 100, firstBadVersion = 1`|Stops at first iteration|
|**Last Version is Bad**|`n = 100, firstBadVersion = 100`|Finds `100` efficiently|
|**Large `n` Values**|`n = 2³¹ - 1`|Handles large numbers efficiently using `O(log n)`|

---

## **7️⃣ Recursive Approach (Alternative)**

```java
public class Solution extends VersionControl {
    public int firstBadVersion(int left, int right) {
        if (left >= right) return left;

        int mid = left + (right - left) / 2;

        if (isBadVersion(mid)) return firstBadVersion(left, mid);
        else return firstBadVersion(mid + 1, right);
    }

    public int firstBadVersion(int n) {
        return firstBadVersion(1, n);
    }
}
```

✅ **Drawback:** Uses **O(log n) stack space**, making **iterative preferred**.

---

## **8️⃣ Why Binary Search is Ideal Here**

🔹 **Without Binary Search (Linear Search O(n))**

- Checking all versions one-by-one is **too slow for large `n`** (`n = 2³¹ - 1`).

🔹 **With Binary Search (O(log n))**

- Instead of checking all versions, we cut the **search space in half** each step.
- For `n = 1,000,000`, only **20 checks** are needed (`log₂(1,000,000) ≈ 20`).

✅ **Binary Search is the best approach for "first occurrence" problems.**

---

## **9️⃣ Similar Problems & Variations**

|**Problem**|**Concept**|**Leetcode**|
|---|---|---|
|**Find First and Last Occurrence in Sorted Array**|Lower & Upper Bound Binary Search|**Leetcode 34**|
|**Find Peak Element in Array**|Binary Search on Monotonic Function|**Leetcode 162**|
|**Search Insert Position**|Binary Search for Index|**Leetcode 35**|
|**Find Minimum in Rotated Sorted Array**|Binary Search on Rotated Arrays|**Leetcode 153**|

---

## **🔟 Summary & Key Takeaways**

✅ **Use Binary Search (O(log n))** for finding the **first occurrence**.  
✅ **Adjust `right = mid` instead of `mid - 1`** to ensure first bad version isn't skipped.  
✅ **Stopping condition `left == right` guarantees correctness**.  
✅ **Handles large values (`n = 2³¹ - 1`) efficiently**.

---

Would you like **a breakdown of another Binary Search variation (e.g., rotated search, lower bound)?** 🚀