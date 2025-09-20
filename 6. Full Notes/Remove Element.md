### Problem Statement

Link: https://leetcode.com/problems/remove-element/description/?envType=study-plan-v2&envId=top-interview-150

### Optimal Approach
1. Just maintain a index pointer for element != val
2. Iterate the array and if the value != val, copy it to where the index pointer is and move the pointer forward

### Solution
```java
class RemoveElement {  
  
    public static void main(String[] args) {  
        int[] nums = {3, 2, 2, 3};  
        int val = 3;  
        int len = removeElement(nums, val);  
        System.out.println(len);  
    }  
  
    private static int removeElement(int[] nums, int val) {  
        int k = 0;  
        for (int i = 0; i < nums.length; i++) {  
            // if the element is not equal to val, then move it to the front  
            if (nums[i] != val) {  
                nums[k++] = nums[i];  
            }  
        }  
        return k;  
    }  
}
```

### Complexity analysis
##### Time 
O(n)

##### Space
O(1)

### Attachments


### Tags
[[2 pointer]]
[[Arrays]]
[[Top 150 Leetcode]]

### References