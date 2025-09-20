Here’s a **complete, interview-ready guide to Monotonic Stacks** — covering concept, types, templates, variations, and must-know problems, all with Java-based focus.

---

# 📘 Monotonic Stacks – Full Notes

---

## ✅ What is a Monotonic Stack?

A **Monotonic Stack** is a stack that maintains its elements in **monotonic (increasing or decreasing)** order from **bottom to top**.

It's used to **optimize problems** involving comparisons between current and nearby elements (e.g., next/previous greater/smaller).

---

### 🔁 Why Use a Monotonic Stack?

To avoid **O(n²) brute-force** checks by storing only **"useful" candidates** in a structured way, achieving **O(n)** time.

---

## 🧱 Types of Monotonic Stacks

|Type|Stack Order (Top to Bottom)|Use Case|
|---|---|---|
|Monotonic **Increasing**|small → large|Next/Prev Smaller Element|
|Monotonic **Decreasing**|large → small|Next/Prev Greater Element|

---

## 🔧 When Do You Use Each?

|Problem Type|Traverse|Stack Type|
|---|---|---|
|Next Greater Element|Right → Left|Decreasing Stack|
|Next Smaller Element|Right → Left|Increasing Stack|
|Previous Greater Element|Left → Right|Decreasing Stack|
|Previous Smaller Element|Left → Right|Increasing Stack|

---

## 🧠 Real-World Analogy

Imagine you're lining people up and want to answer:

- “Who is taller than me on my right?”
    
- “Who is shorter than me to my left?”
    

Instead of checking everyone manually, you **discard people who are definitely not the answer** for anyone else — just like popping elements from the stack.

---

# 📦 Java Templates

---

## 1. **Next Greater Element (NGE)**

Right → Left, Monotonic **Decreasing Stack**

```java
public int[] nextGreater(int[] nums) {
    int n = nums.length;
    int[] res = new int[n];
    Stack<Integer> stack = new Stack<>();

    for (int i = n - 1; i >= 0; i--) {
        while (!stack.isEmpty() && stack.peek() <= nums[i])
            stack.pop();

        res[i] = stack.isEmpty() ? -1 : stack.peek();
        stack.push(nums[i]);
    }
    return res;
}
```

---

## 2. **Next Smaller Element (NSE)**

Right → Left, Monotonic **Increasing Stack**

```java
public int[] nextSmaller(int[] nums) {
    int n = nums.length;
    int[] res = new int[n];
    Stack<Integer> stack = new Stack<>();

    for (int i = n - 1; i >= 0; i--) {
        while (!stack.isEmpty() && stack.peek() >= nums[i])
            stack.pop();

        res[i] = stack.isEmpty() ? -1 : stack.peek();
        stack.push(nums[i]);
    }
    return res;
}
```

---

## 3. **Previous Greater Element (PGE)**

Left → Right, Monotonic **Decreasing Stack**

```java
public int[] previousGreater(int[] nums) {
    int n = nums.length;
    int[] res = new int[n];
    Stack<Integer> stack = new Stack<>();

    for (int i = 0; i < n; i++) {
        while (!stack.isEmpty() && stack.peek() <= nums[i])
            stack.pop();

        res[i] = stack.isEmpty() ? -1 : stack.peek();
        stack.push(nums[i]);
    }
    return res;
}
```

---

## 4. **Previous Smaller Element (PSE)**

Left → Right, Monotonic **Increasing Stack**

```java
public int[] previousSmaller(int[] nums) {
    int n = nums.length;
    int[] res = new int[n];
    Stack<Integer> stack = new Stack<>();

    for (int i = 0; i < n; i++) {
        while (!stack.isEmpty() && stack.peek() >= nums[i])
            stack.pop();

        res[i] = stack.isEmpty() ? -1 : stack.peek();
        stack.push(nums[i]);
    }
    return res;
}
```

---

# 🚨 Key Properties

|Feature|Monotonic Stack Value|
|---|---|
|Time Complexity|O(n)|
|Space Complexity|O(n) (stack)|
|Push/Pop frequency|Each element ≤ 1 push and 1 pop|

Each element is **pushed and popped once**, making it very efficient.

---

# 🔍 Visual Example

### Input: `[4, 5, 2, 10, 8]`

🔸 Find Next Greater Element → Output: `[5, 10, 10, -1, -1]`

- Use **Decreasing Stack**
    
- Traverse from right to left
    
- Remove all smaller elements before pushing current
    

---

# 🔄 Variants to Learn

|Variant|Strategy|
|---|---|
|Next Greater **to Left**|Left → Right + Decreasing Stack|
|Next Greater **in Circular Array**|Use modulo + simulate 2n|
|**With Index/Distance**|Push indices instead of values|
|**Custom Comparisons**|Use comparators/custom logic|

---

# 🔗 Must-Know Monotonic Stack Problems

|Leetcode ID|Problem|Stack Type|
|---|---|---|
|496|Next Greater Element I|Mono decreasing|
|503|Next Greater Element II (circular)|Mono decreasing|
|739|Daily Temperatures|Mono decreasing|
|901|Stock Span|Mono increasing|
|84|Largest Rectangle in Histogram|Mono increasing|
|85|Max Rectangle in Binary Matrix|Histogram + DP|
|42|Trapping Rain Water|Mono + 2-pointers|
|1019|Next Greater Node in Linked List|Mono decreasing|

---

# 🧠 Tips for Mastery

- Always **track what the stack is storing**: values or **indices**
    
- Use **arrays for faster** solutions if input size is fixed
    
- For **"distance to next X"**, store indices and calculate difference
    
- For **circular arrays**, loop from `2n - 1 to 0` and use `i % n`
    

---

# 📌 Summary Table

|Problem|Traverse|Stack Type|Comparison Logic|
|---|---|---|---|
|Next Greater Element|Right→Left|Decreasing|`stack.peek() <= nums[i]`|
|Next Smaller Element|Right→Left|Increasing|`stack.peek() >= nums[i]`|
|Previous Greater Element|Left→Right|Decreasing|`stack.peek() <= nums[i]`|
|Previous Smaller Element|Left→Right|Increasing|`stack.peek() >= nums[i]`|

---

Would you like me to:

- Create a **PDF notes** version of this?
    
- Add **diagrams for each pattern**?
    
- Help with **Daily Temperatures, Rain Water, Histogram** using this concept?
    

Let me know, and I’ll generate exactly what you need.