### **Lower Bound vs Upper Bound – Key Differences**

|**Feature**|**Lower Bound (`≥ target`)**|**Upper Bound (`> target`)**|
|---|---|---|
|**Definition**|Smallest index `i` such that `nums[i] ≥ target`|Smallest index `i` such that `nums[i] > target`|
|**When `target` Exists**|Returns the **first occurrence** of `target`|Returns the index **after the last occurrence** of `target`|
|**When `target` is Missing**|Returns the position where `target` should be inserted to maintain order|Returns the position where `target` should be inserted but **skips duplicates**|
|**Condition in Binary Search**|`if (nums[mid] ≥ target) right = mid;`|`if (nums[mid] > target) right = mid;`|
|**Condition for Right Movement**|`else left = mid + 1;`|`else left = mid + 1;`|
|**Final Return Value**|`left` (First occurrence or insert position)|`left` (First greater element or insert position)|
|**Use Case**|Finding the **first occurrence** of `target` in a sorted array|Finding **next greater** element or counting occurrences|
|**Related Problems**|`searchInsertPosition()` (Leetcode 35), Count of elements `≤ target`|Counting frequency of `target`, Finding the first greater element|

---

### **Example Walkthrough**

#### **Example 1: Target Exists**

```plaintext
nums = [1, 2, 4, 4, 6, 8], target = 4
```

|Method|Output|Explanation|
|---|---|---|
|**Lower Bound (`≥ 4`)**|`2`|First occurrence of `4` at index `2`|
|**Upper Bound (`> 4`)**|`4`|First greater element (`6`) at index `4`|

---

#### **Example 2: Target Missing (Insert Position)**

```plaintext
nums = [1, 2, 4, 4, 6, 8], target = 5
```

|Method|Output|Explanation|
|---|---|---|
|**Lower Bound (`≥ 5`)**|`4`|`5` should be inserted at index `4`|
|**Upper Bound (`> 5`)**|`4`|`5` should be inserted at index `4`, same as lower bound|

---

#### **Example 3: All Elements Smaller**

```plaintext
nums = [1, 2, 3], target = 4
```

|Method|Output|Explanation|
|---|---|---|
|**Lower Bound (`≥ 4`)**|`3`|`4` should be inserted at index `3` (end of array)|
|**Upper Bound (`> 4`)**|`3`|`4` should be inserted at index `3`|

---

#### **Example 4: All Elements Greater**

```plaintext
nums = [5, 6, 7], target = 4
```

|Method|Output|Explanation|
|---|---|---|
|**Lower Bound (`≥ 4`)**|`0`|`4` should be inserted at index `0` (beginning)|
|**Upper Bound (`> 4`)**|`0`|`4` should be inserted at index `0`|

---

### **Formula for Counting Occurrences**

```plaintext
Occurrences of `target` = Upper Bound - Lower Bound
```

🔹 **Example:** `nums = [1,2,4,4,4,6]`, `target = 4`

- **Lower Bound (`≥ 4`)** → `2`
- **Upper Bound (`> 4`)** → `5`
- **Occurrences = `5 - 2 = 3`**

---

### **Key Takeaways**

✅ **Lower Bound (`≥ target`)** → Finds the **first occurrence** or **insert position**.  
✅ **Upper Bound (`> target`)** → Finds the **next greater element** or **insert position skipping duplicates**.  
✅ **If `target` exists**, **upper bound** is **always greater than the last occurrence**.  
✅ **Can be used for frequency counting** (`upper - lower`).

Would you like **code implementations side by side** for better clarity? 🚀