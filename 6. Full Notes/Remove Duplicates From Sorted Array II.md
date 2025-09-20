### Problem Statement

Link: https://leetcode.com/problems/remove-duplicates-from-sorted-array-ii/description/?envType=study-plan-v2&envId=top-interview-150

### Brute Force Approach
1. Use hash map to keep elements and frequency
2. Copy them to input array as many times as frequency where frequency <=2

### Solution
```java
  
class RemoveDuplicatesFromSortedArrayIIUsingHashSet {  
  
  public static void main(String[] args) {  
    RemoveDuplicatesFromSortedArrayIIUsingHashSet obj = new RemoveDuplicatesFromSortedArrayIIUsingHashSet();  
    int[] arr = {0, 0, 1, 1, 1, 2, 2, 3, 3, 4};  
    int n = obj.removeDuplicates(arr);  
    for (int i = 0; i < n; i++) {  
      System.out.print(arr[i] + " ");  
    }  
  }  
  
  private int removeDuplicates(int[] arr) {  
    HashMap<Integer, Integer> hashMap = new HashMap<>();  
    for (int num : arr) {  
      hashMap.put(num, hashMap.getOrDefault(num, 0) + 1);  
    }  
  
    Iterator<Entry<Integer, Integer>> iterator = hashMap.entrySet().iterator();  
    int nextUniqueElementIndex;  
    for (nextUniqueElementIndex = 0; iterator.hasNext(); ) {  
        
      Entry<Integer, Integer> entry = iterator.next();  
      int element = entry.getKey();  
      int frequency = entry.getValue();  
        
      for (int allowedDuplicatesSize = 0; allowedDuplicatesSize < Math.min(2, frequency); allowedDuplicatesSize++) {  
        arr[nextUniqueElementIndex++] = element;  
      }  
        
    }  
    return nextUniqueElementIndex;  
  }  
}
```

### Complexity analysis
##### Time
Adding a number to hashmap takes O(1)
Iteration for n elements to create hashmap O(n)
Copy to array from hashset O(n)

Overall O(n) + O(n) = O(n)

##### Space
O(n)

### Optimal Approach
1. Keep a index pointer for nextUniqueElement
2. Every time an element is found to be different than the element 2 places before nextUniqueElement, place it at nextUniqueElement index and move this pointer ahead
3. 0th index and 1st index are already unique or max 2 times duplicates. So start from 2

### Solution
```java
class RemoveDuplicatesFromSortedArrayIIInPlace {  
  
  public static void main(String[] args) {  
    RemoveDuplicatesFromSortedArrayIIInPlace obj = new RemoveDuplicatesFromSortedArrayIIInPlace();  
    int[] arr = {0, 0, 1, 1, 1, 2, 2, 3, 3, 4};  
    int n = obj.removeDuplicates(arr);  
    for (int i = 0; i < n; i++) {  
      System.out.print(arr[i] + " ");  
    }  
  }  
  
  private int removeDuplicates(int[] arr) {  
    int n = arr.length;  
    int allowedDuplicatesSize = 2;  
  
    if (n <= allowedDuplicatesSize) {  
      return n;  
    }  
  
    int nextUniqueElementIndex = allowedDuplicatesSize;  
  
    for (int i = allowedDuplicatesSize; i < n; i++) {  
      int currentElement = arr[i];  
      int previousElement = arr[nextUniqueElementIndex - allowedDuplicatesSize];  
  
      if (currentElement != previousElement) {  
        arr[nextUniqueElementIndex++] = currentElement;  
      }  
  
    }  
    return nextUniqueElementIndex;  
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
[[Hashing]]
[[Top 150 Leetcode]]
[[6. Full Notes/Remove Duplicates From Sorted Array]]
[[Arrays]]


## NOTES

From previous problem to this, only allowed duplicates value changed. So in the code this can be achieved by just a slight modification. We keep a allowedDuplicates variable which decides which index we need to compare for duplicates and where to start iterating from. For any number of allowed duplicates this code should work

### References