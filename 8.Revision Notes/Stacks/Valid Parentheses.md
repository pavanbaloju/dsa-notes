### **Valid Parentheses – Full Notes**

#### **Problem Statement**

Given a string `s` containing just the characters `'(', ')', '{', '}', '[' and ']'`, determine if the input string is **valid**.

A string is **valid** if:

1. Open brackets must be closed by the same type of brackets.
    
2. Open brackets must be closed in the correct order.
    
3. Every close bracket has a corresponding open bracket of the same type.
    

---

### **Example Cases**

#### ✅ **Valid Cases**

|Input|Output|Explanation|
|---|---|---|
|`s = "()"`|✅ `true`|Open and close match.|
|`s = "()[]{}"`|✅ `true`|All brackets are correctly closed.|
|`s = "{[()()]}"`|✅ `true`|Nested correctly.|

#### ❌ **Invalid Cases**

|Input|Output|Explanation|
|---|---|---|
|`s = "(]"`|❌ `false`|`)` expected, but `]` found.|
|`s = "([)]"`|❌ `false`|Brackets closed in the wrong order.|
|`s = "{("`|❌ `false`|Missing closing brackets.|

---

## **Approach 1: Using Stack (Basic Approach)**

Since we need to check **matching pairs** and **correct order**, we use a **stack**, which follows **LIFO (Last In, First Out)**.

### **Algorithm**

1. Use a **stack** to store **opening brackets**.
    
2. If a **closing bracket** appears:
    
    - If the stack is empty → **invalid**.
        
    - Pop from the stack and check if it matches the expected bracket.
        
3. If the stack is **empty at the end**, the string is valid.
    

### **Code (Java)**

```java
import java.util.Stack;

class Solution {
    public boolean isValid(String s) {
        Stack<Character> stack = new Stack<>();

        for (char c : s.toCharArray()) {
            if (c == '(' || c == '{' || c == '[') {
                stack.push(c); // Push opening bracket
            } else {
                if (stack.isEmpty()) return false; // No matching open bracket
                char top = stack.pop(); // Get the last open bracket
                if ((c == ')' && top != '(') ||
                    (c == '}' && top != '{') ||
                    (c == ']' && top != '[')) {
                    return false; // Mismatch
                }
            }
        }
        return stack.isEmpty(); // Ensure all brackets are closed
    }
}
```

### **Time & Space Complexity**

- **Time Complexity:** **O(N)** → We iterate once through the string.
    
- **Space Complexity:** **O(N)** → In the worst case, the stack holds `N/2` elements.
    

---

## **Approach 2: Optimized – Push Closing Brackets Instead of Opening Brackets**

**Instead of pushing opening brackets, we push the expected closing brackets**.  
When encountering a closing bracket, we simply compare it with the top of the stack.

### **Algorithm**

1. Push the **expected closing bracket** when encountering an opening bracket.
    
2. If a closing bracket appears:
    
    - If the stack is empty or does not match → return **false**.
        
    - Otherwise, pop the stack.
        
3. If the stack is empty at the end, return **true**.
    

### **Optimized Code**

```java
import java.util.Stack;

class Solution {
    public boolean isValid(String s) {
        Stack<Character> stack = new Stack<>();

        for (char c : s.toCharArray()) {
            if (c == '(') stack.push(')');
            else if (c == '{') stack.push('}');
            else if (c == '[') stack.push(']');
            else {
                if (stack.isEmpty() || stack.pop() != c) {
                    return false; // Mismatch or stack empty
                }
            }
        }
        return stack.isEmpty(); // Stack must be empty if valid
    }
}
```

### **Why Is This More Efficient?**

✅ **No Need for Character Comparisons** – We directly check if the popped element matches the current closing bracket.  
✅ **Avoids Extra Mapping** – Instead of checking against `if` conditions, we store closing brackets directly.  
✅ **Same Time Complexity:** **O(N)**  
✅ **Same Space Complexity:** **O(N)**

---

### **Edge Cases Considered**

1. **Empty String** – ✅ Valid (`""` is always valid).
    
2. **Single Closing Bracket** – ❌ Invalid (`"]"`, `"{"`).
    
3. **Only Open Brackets** – ❌ Invalid (`"((("`).
    
4. **Only Close Brackets** – ❌ Invalid (`")))"`).
    
5. **Mixed Brackets in Wrong Order** – ❌ Invalid (`"[{)]"`).
    

---

### **Final Summary**

|Approach|Idea|Time Complexity|Space Complexity|Pros|Cons|
|---|---|---|---|---|---|
|**Basic Stack**|Push open brackets, pop and match with close brackets|**O(N)**|**O(N)**|Simple & readable|Extra `if` conditions for matching|
|**Optimized Stack**|Push **closing brackets** instead of opening brackets|**O(N)**|**O(N)**|Fewer `if` conditions, cleaner logic|Slightly harder to grasp initially|

Both approaches work efficiently, but **pushing closing brackets** is a more **intuitive and optimized solution**.

Let me know if you need a dry run! 🚀