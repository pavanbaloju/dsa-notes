The **Boyer-Moore Voting Algorithm** efficiently finds the **majority element** in an array if one exists. A majority element is defined as an element that appears more than n/2, where n is the size of the array. This algorithm runs in **O(n)** time and uses **O(1)** space.

### **Algorithm Overview**

1. **Candidate Selection**:
    
    - Traverse the array while maintaining a `candidate` for the majority element and a `count`.
    - Increment `count` if the current element matches the `candidate`.
    - Decrement `count` if the current element does not match the `candidate`. If `count` becomes zero, update the `candidate` to the current element and reset `count` to 1.
2. **Candidate Verification**:
    
    - The algorithm identifies a candidate that could be the majority element. To ensure the candidate is valid, perform a second pass to count its occurrences. If the count is greater than n / 2, it is the majority element.

---

### **Proof of Correctness**

#### **Candidate Selection Phase**

The algorithm hinges on the observation that:

- If the **majority element** exists, its occurrences will "cancel out" the occurrences of other elements.

##### **Key Ideas**:

1. Each non-majority element can pair with a majority element and reduce its `count`, but this cannot fully cancel out the majority element's dominance since it appears more than n/2n/2 times.
2. When `count` is reset to 1 (after reaching 0), the remaining elements still preserve the majority element's dominance because there are more majority elements than all others combined.

#### **Case Analysis**:

1. If the current element is the same as the `candidate`, the `count` increases. This reinforces the candidate's likelihood.
2. If the current element differs from the `candidate`, the `count` decreases. This simulates "canceling out" one occurrence of the majority element with one occurrence of a minority element.
3. When `count` reaches zero, it implies that the elements seen so far have an equal mix of the `candidate` and other elements. At this point, the next unprocessed element is chosen as the new `candidate`.

By the end of the traversal, if a majority element exists, it will be the `candidate`, as its dominance ensures it survives all cancellations.

---

#### **Candidate Verification Phase**

After selecting the `candidate`, a second pass counts its occurrences. If the count exceeds n/2n/2, the candidate is confirmed as the majority element.

---

### **Why It Works**

1. **Majority Element Always Survives**:
    - During the selection phase, the majority element's surplus occurrences ensure it remains the `candidate`.
2. **Resetting the Candidate**:
    - When `count` reaches zero, the remaining elements are sufficient to ensure the majority element's re-selection if it has not yet been chosen.
3. **Second Pass Guarantees Validity**:
    - This step ensures that the final `candidate` is indeed the majority element.

---

### **Example Walkthrough**

Array: [3,3,4,2,4,4,2,4,4][3, 3, 4, 2, 4, 4, 2, 4, 4]

1. **Candidate Selection**:
    
    - Initialize: `candidate = None`, `count = 0`
    - 33: Set `candidate = 3`, `count = 1`
    - 33: `candidate = 3`, `count = 2`
    - 44: `candidate = 3`, `count = 1`
    - 22: `candidate = 3`, `count = 0` → Reset: `candidate = 2`, `count = 1`
    - 44: `candidate = 2`, `count = 0` → Reset: `candidate = 4`, `count = 1`
    - 44: `candidate = 4`, `count = 2`
    - 22: `candidate = 4`, `count = 1`
    - 44: `candidate = 4`, `count = 2`
    - 44: `candidate = 4`, `count = 3`
    
    Final `candidate = 4`.
    
2. **Verification**:
    
    - Count occurrences of 44: 5>⌊9/2⌋=45 > \lfloor 9/2 \rfloor = 4.
    - 44 is the majority element.

---

### **Complexity**

1. **Time Complexity**:
    
    - Selection: O(n)O(n)
    - Verification: O(n)O(n)
    - Total: O(n)O(n)
2. **Space Complexity**:
    
    - Uses only variables `candidate` and `count`: O(1)O(1).

## Tags
[[Special]]
[[Majority Element]]
[[Top 150 Leetcode]]