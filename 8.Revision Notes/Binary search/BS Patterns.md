Here’s a **comprehensive summary of all distinct binary search patterns**, based on the **type of search** and **search goal**. This is structured to help you recognize when to use which variation, with concise cues, loop behaviors, and template ideas.

---

## 🧠 **Core Decision: What Are You Searching For?**

Binary search variations fall under these **five major categories**:

---

### **1. Exact Match Search**

#### ✅ Goal:

Find an element exactly equal to the `target`.

#### 🔍 Cues:

- “Return index if found, else -1”
    
- “Check if element exists”
    

#### 🧱 Template:

```java
while (left <= right) {
    int mid = left + (right - left) / 2;
    if (arr[mid] == target) return mid;
    else if (arr[mid] < target) left = mid + 1;
    else right = mid - 1;
}
return -1;
```

---

### **2. First Occurrence (Leftmost Index of Target)**

#### ✅ Goal:

Return **leftmost** index where `arr[i] == target`.

#### 🔍 Cues:

- “Find first index of X”
    
- “Target may appear multiple times”
    

#### 🧱 Key Logic:

Store answer and **shrink right**

```java
if (arr[mid] == target) {
    ans = mid;
    right = mid - 1;
}
```

---

### **3. Last Occurrence (Rightmost Index of Target)**

#### ✅ Goal:

Return **rightmost** index where `arr[i] == target`.

#### 🔍 Cues:

- “Find last index of X”
    
- “How many times X appears?”
    

#### 🧱 Key Logic:

Store answer and **shrink left**

```java
if (arr[mid] == target) {
    ans = mid;
    left = mid + 1;
}
```

---

### **4. Lower Bound (First Element ≥ Target)**

#### ✅ Goal:

Find the first index `i` such that `arr[i] >= target`

#### 🔍 Cues:

- “Smallest number ≥ X”
    
- “Ceil of X”
    
- “Insertion point in sorted array”
    

#### 🧱 Key Logic:

```java
if (arr[mid] >= target) {
    ans = mid;
    right = mid - 1;
} else {
    left = mid + 1;
}
```

#### 🧠 `ans` ends at index of lower bound.

---

### **5. Upper Bound (First Element > Target)**

#### ✅ Goal:

Find first index `i` where `arr[i] > target`

#### 🔍 Cues:

- “Next greater number than X”
    
- “Count of numbers ≤ X = upperBoundIndex”
    

#### 🧱 Key Logic:

```java
if (arr[mid] > target) {
    ans = mid;
    right = mid - 1;
} else {
    left = mid + 1;
}
```

---

### ✅ Bonus Patterns

---

### **6. Binary Search on Answer (Search Space is Not an Array)**

#### ✅ Goal:

Use binary search to find the **minimum or maximum value** that satisfies a condition.

#### 🔍 Cues:

- “Min/max value such that...”
    
- “Optimize some property”
    
- The array is **not** the search space — integers, times, capacity, etc. are.
    

#### 🧱 Template:

```java
while (left <= right) {
    int mid = left + (right - left) / 2;
    if (isValid(mid)) {
        ans = mid;
        right = mid - 1; // search left half for better answer
    } else {
        left = mid + 1;
    }
}
```

---

### **7. Peak Element / Bitonic Search**

#### ✅ Goal:

Find local max/min or peak

#### 🔍 Cues:

- “Find any peak”
    
- “Array is mountain-shaped”
    
- "Unimodal function"
    

#### 🧱 Example:

```java
if (arr[mid] > arr[mid + 1]) {
    right = mid; // Peak is in left
} else {
    left = mid + 1; // Peak is in right
}
```

---

## 🪜 Summary Table

|Pattern|Loop|Answer Location|Discard Side|Use Case Cues|
|---|---|---|---|---|
|Exact Match|`<=`|return on `==`|Normal binary|Find X exactly|
|First Occurrence|`<=`|`ans = mid`|`right = mid -1`|First index where `arr[i] == X`|
|Last Occurrence|`<=`|`ans = mid`|`left = mid + 1`|Last index where `arr[i] == X`|
|Lower Bound (≥ X)|`<=`|`ans = mid`|`right = mid -1`|First element ≥ target|
|Upper Bound (> X)|`<=`|`ans = mid`|`right = mid -1`|First element > target|
|Binary Search Answer|`<=`|`ans = mid`|condition-based|Find min/max satisfying condition|
|Peak Element|`<`|`left/right`|depends on slope|Peak in mountain or local max|

---

Would you like this as an **Anki Deck**, **cheat sheet**, or **Java file with all code templates**?