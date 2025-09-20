Here’s a complete DSA breakdown of the classic problem: **Palindrome Linked List**, with **brute to optimal solutions**, clean **Java code**, and detailed reasoning.

---

# ✅ Problem: Palindrome Linked List

(Leetcode 234 – [Palindrome Linked List](https://leetcode.com/problems/palindrome-linked-list/))

---

## 🔹 Problem Statement

> Given the head of a singly linked list, return `true` if the list is a **palindrome**.

---

### 🔸 Examples

```text
Input:  1 → 2 → 2 → 1  
Output: true

Input:  1 → 2 → 3 → 2 → 1  
Output: true

Input:  1 → 2 → 3  
Output: false
```

---

## 🔁 Pattern

- **Find middle** of the list
    
- **Reverse second half**
    
- **Compare two halves**
    
- (Optional) **Restore** the list structure (good practice)
    

---

# 🔻 Approach 1: Brute Force using Array/List

### 🔸 Idea:

- Store values in an array/list, then check if it's a palindrome.
    

---

### ✅ Java Code

```java
public boolean isPalindrome(ListNode head) {
    List<Integer> vals = new ArrayList<>();

    while (head != null) {
        vals.add(head.val);
        head = head.next;
    }

    int left = 0, right = vals.size() - 1;
    while (left < right) {
        if (!vals.get(left).equals(vals.get(right))) return false;
        left++;
        right--;
    }

    return true;
}
```

---

### ⏱ Time & Space:

- Time: `O(n)`
    
- Space: `O(n)`
    
- ✅ Simple, but not in-place
    

---

# ✅ Optimal Approach: Reverse Second Half In-Place

### 🔸 Steps:

1. Use **slow and fast pointers** to find the **middle**
    
2. Reverse second half
    
3. Compare first and second halves
    
4. (Optional) Reverse again to **restore** the list
    

---

### ✅ Java Code:

```java
public boolean isPalindrome(ListNode head) {
    if (head == null || head.next == null) return true;

    // Step 1: Find middle
    ListNode slow = head, fast = head;
    while (fast != null && fast.next != null) {
        slow = slow.next;
        fast = fast.next.next;
    }

    // Step 2: Reverse second half
    ListNode secondHalf = reverseList(slow);

    // Step 3: Compare first and second half
    ListNode firstHalf = head;
    ListNode secondHalfCopy = secondHalf;
    while (secondHalf != null) {
        if (firstHalf.val != secondHalf.val) return false;
        firstHalf = firstHalf.next;
        secondHalf = secondHalf.next;
    }

    // Optional Step 4: Restore the list (not required by Leetcode)
    reverseList(secondHalfCopy);

    return true;
}

// Utility: Reverse a linked list
private ListNode reverseList(ListNode head) {
    ListNode prev = null, curr = head;
    while (curr != null) {
        ListNode next = curr.next;
        curr.next = prev;
        prev = curr;
        curr = next;
    }
    return prev;
}
```

---

### ⏱ Time & Space:

- Time: `O(n)`
    
- Space: `O(1)`
    
- ✅ Most optimal, in-place
    
- ✅ Common interview pattern
    

---

## 🔁 Dry Run Example

### Input: `1 → 2 → 3 → 2 → 1`

- Middle at `3`
    
- Reverse second half: `1 ← 2`
    
- Compare `1 → 2 → 3` and `1 → 2`
    
- All values match ✅
    

---

## 📊 Comparison Table

|Approach|Time|Space|Notes|
|---|---|---|---|
|Array/List|O(n)|O(n)|Simple, but not in-place|
|✅ Reverse + Compare|O(n)|O(1)|✅ Optimal, in-place, elegant|

---

## 🧠 Edge Cases

|Case|Result|
|---|---|
|Empty list|true|
|Single node|true|
|Even/odd length|handled|
|Non-palindrome values|false|

---

## 🔗 Leetcode Link

- [Leetcode 234 – Palindrome Linked List](https://leetcode.com/problems/palindrome-linked-list/)
    

---

## ✅ Summary

- Use **slow & fast pointers** to split
    
- **Reverse and compare** technique is widely used (like reorder list, half reversal, etc.)
    
- Optional: restore the original structure (important in some real systems)
    

---

Would you like:

- A utility to print linked list for debugging?
    
- A reusable Java class to **split, reverse, and merge** linked lists?
    
- Follow-up questions like “Reorder List” or “Check if list is a rotated palindrome”?