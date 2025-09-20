Here are the **full notes** for **Leetcode 71 – Simplify Path**, including:

- Problem statement
    
- Intuition
    
- Key rules for Unix paths
    
- Brute explanation
    
- Optimized stack-based solution
    
- Java code
    
- Edge cases and dry run
    
- Time and space complexities
    

---

# 📘 Leetcode 71 – Simplify Path

---

## ✅ Problem Statement

> Given an **absolute path** for a file (Unix-style), return the **simplified canonical path**.

---

### 🧪 Examples

```text
Input: "/home/"               → Output: "/home"
Input: "/../"                 → Output: "/"
Input: "/home//foo/"          → Output: "/home/foo"
Input: "/a/./b/../../c/"      → Output: "/c"
```

---

## 📂 Unix File System Rules

|Component|Meaning|
|---|---|
|`.`|Current directory → Skip it|
|`..`|Move one directory up → Pop from path stack|
|`//`|Treated as a single `/`|
|Anything else|A valid directory → Push to stack|

---

## 🧠 Intuition

1. Split the path by `'/'`
    
2. Use a stack to simulate navigating the file system
    
3. For each token:
    
    - Skip if empty `""` or `"."`
        
    - If `".."` → pop from stack if not empty
        
    - Else → push the directory
        
4. Join the stack using `'/'`
    

---

## ✅ Java Code (Stack-Based)

```java
public String simplifyPath(String path) {
    Stack<String> stack = new Stack<>();
    String[] parts = path.split("/");

    for (String part : parts) {
        if (part.equals("") || part.equals(".")) {
            continue;
        } else if (part.equals("..")) {
            if (!stack.isEmpty()) stack.pop();
        } else {
            stack.push(part);
        }
    }

    return "/" + String.join("/", stack);
}
```

---

## 🧪 Dry Run Example

```text
Input: "/a/./b/../../c/"
→ Parts: ["", "a", ".", "b", "..", "..", "c"]

Stack Trace:
- ""     → skip
- "a"    → push → ["a"]
- "."    → skip
- "b"    → push → ["a", "b"]
- ".."   → pop  → ["a"]
- ".."   → pop  → []
- "c"    → push → ["c"]

Final: "/" + "c" → "/c"
```

---

## 🔍 Edge Cases

|Case|Output|
|---|---|
|`"/"`|`"/"`|
|`"/../"`|`"/"`|
|`"/home//foo/"`|`"/home/foo"`|
|`"/./.././a/../"`|`"/"`|
|`"////"`|`"/"`|
|`"/a/b/c/../../"`|`"/a"`|

---

## ⏱️ Time and Space Complexity

|Metric|Value|
|---|---|
|Time|O(n), where n = path length|
|Space|O(n) for the stack and output|

---

## 🔄 Summary

|Component|Logic|
|---|---|
|`""` or `"."`|Skip (no-op)|
|`".."`|Go one level up → pop stack if any|
|`"dir"`|Push directory to stack|
|Result|Join with `'/'` and prefix with `'/'`|

---

## ✅ Final Output Format

Always starts with a `/`  
No trailing `/`  
No `"."` or `".."` in final result  
No double slashes (`//`)

---

## 🔗 Related Problems

|Problem|Type|
|---|---|
|Leetcode 71|Path simplifier|
|Leetcode 841|Graph DFS Stack|
|Leetcode 394|Decode String (Stack)|

---

Would you like:

- A **helper utility class** to reuse this logic?
    
- Versions with **Deque** or **StringBuilder**?
    
- Challenge: Can you implement **without using a stack**?
    

Let me know — I can build it for you.