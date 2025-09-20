Here are **complete notes on Word Ladder II**, covering the problem statement, intuition, approach, and clean Java code with **line-by-line comments**.

---

## ✅ Word Ladder II — Full Notes

### 🔸 Problem Statement:

You are given:

- A `beginWord`, an `endWord`, and a `wordList`.
    
- Transform `beginWord` to `endWord` by changing only **one character at a time**.
    
- Each transformed word must be in the `wordList`.
    
- **Return all shortest transformation sequences** from `beginWord` to `endWord`.
    

---

### 🔸 Constraints:

- All words are of same length.
    
- Only one letter can change per transformation.
    
- Words must exist in the dictionary.
    

---

### 🔸 Example:

**Input:**

```text
beginWord = "hit"
endWord = "cog"
wordList = ["hot","dot","dog","lot","log","cog"]
```

**Output:**

```text
[
  ["hit","hot","dot","dog","cog"],
  ["hit","hot","lot","log","cog"]
]
```

---

## 🔍 Intuition:

- This is a **shortest path problem** on an **unweighted graph**, where each word is a node.
    
- We need to **find all paths of minimal length** from `beginWord` to `endWord`.
    
- Use **BFS** to build the graph with shortest connections.
    
- Then use **DFS** to backtrack from `endWord` to `beginWord` using a parent map.
    

---

## ✅ Strategy:

### Step 1: **BFS**

- Build a **parent map** (child → list of parents) using BFS.
    
- Store only the shortest paths.
    

### Step 2: **DFS**

- Backtrack from `endWord` to `beginWord` using the parent map to get all sequences.
    

---

## ✅ Java Code (With Comments)

```java
class Solution {
    public List<List<String>> findLadders(String beginWord, String endWord, List<String> wordList) {
        Set<String> wordSet = new HashSet<>(wordList);
        List<List<String>> result = new ArrayList<>();

        if (!wordSet.contains(endWord)) return result;

        // Step 1: BFS to build the graph with shortest paths
        Map<String, List<String>> parentMap = new HashMap<>();
        bfs(beginWord, endWord, wordSet, parentMap);

        // Step 2: DFS to build all paths from endWord to beginWord
        List<String> path = new ArrayList<>();
        dfs(endWord, beginWord, parentMap, path, result);

        return result;
    }

    // BFS builds parent relationships for shortest paths only
    private void bfs(String beginWord, String endWord, Set<String> wordSet, 
                     Map<String, List<String>> parentMap) {
        Queue<String> queue = new LinkedList<>();
        queue.offer(beginWord);

        Set<String> visited = new HashSet<>();
        visited.add(beginWord);

        boolean foundEnd = false;

        while (!queue.isEmpty() && !foundEnd) {
            Set<String> visitedThisLevel = new HashSet<>();
            int size = queue.size();

            for (int i = 0; i < size; i++) {
                String word = queue.poll();

                // Try changing each character
                for (int j = 0; j < word.length(); j++) {
                    char[] chars = word.toCharArray();

                    for (char c = 'a'; c <= 'z'; c++) {
                        chars[j] = c;
                        String nextWord = new String(chars);

                        if (!wordSet.contains(nextWord) || visited.contains(nextWord)) continue;

                        // Add current word as parent of nextWord
                        parentMap.computeIfAbsent(nextWord, k -> new ArrayList<>()).add(word);

                        if (nextWord.equals(endWord)) {
                            foundEnd = true;
                        }

                        // Only add once per level
                        if (!visitedThisLevel.contains(nextWord)) {
                            visitedThisLevel.add(nextWord);
                            queue.offer(nextWord);
                        }
                    }
                }
            }

            // Update global visited to prevent revisits in next levels
            visited.addAll(visitedThisLevel);
        }
    }

    // DFS to backtrack and build all paths from endWord to beginWord
    private void dfs(String word, String beginWord, Map<String, List<String>> parentMap, 
                     List<String> path, List<List<String>> result) {
        path.add(word);

        if (word.equals(beginWord)) {
            // We reached the beginning, reverse the path and add to result
            List<String> validPath = new ArrayList<>(path);
            Collections.reverse(validPath);
            result.add(validPath);
        } else {
            // Recur for all parents of current word
            for (String parent : parentMap.getOrDefault(word, new ArrayList<>())) {
                dfs(parent, beginWord, parentMap, path, result);
            }
        }

        // Backtrack
        path.remove(path.size() - 1);
    }
}
```

---

## 🧠 Key Concepts:

|Concept|Description|
|---|---|
|**BFS**|Ensures we only record shortest paths by tracking levels.|
|**visitedThisLevel**|Prevents revisiting words within the same level to avoid longer paths.|
|**parentMap**|Stores child → parent(s) relationships used for DFS.|
|**DFS**|Reconstructs all paths using parentMap recursively.|
|**Collections.reverse()**|Reverses each path because DFS goes from endWord → beginWord.|

---

## 🔄 Dry Run Example

For:

```text
beginWord = "hit"
endWord = "cog"
wordList = ["hot","dot","dog","lot","log","cog"]
```

1. BFS:
    
    - hit → hot
        
    - hot → dot, lot
        
    - dot → dog; lot → log
        
    - dog → cog; log → cog
        
2. parentMap:
    

```text
"hot" → ["hit"]
"dot" → ["hot"]
"lot" → ["hot"]
"dog" → ["dot"]
"log" → ["lot"]
"cog" → ["dog", "log"]
```

3. DFS:
    
    - cog → dog → dot → hot → hit
        
    - cog → log → lot → hot → hit
        
    
    Reversed = output paths.
    

---

## ✅ Time and Space Complexity

|Operation|Complexity|
|---|---|
|BFS|O(N * L²) where N = number of words, L = word length|
|DFS|Exponential in worst case (but bounded due to shortest paths only)|
|Space|O(N) for parentMap and queue|

---

## ✅ When to Use This Pattern:

- All shortest paths (not just one).
    
- One-character transformations.
    
- Word ladder variants or maze/grid variants (multi-paths).
    

---

Let me know if you'd like:

- A Python version
    
- A diagram of the BFS + DFS
    
- A test harness to run this code interactively