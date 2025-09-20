### 🔍 Word Ladder I – Full Notes with Explanation and Code

---

### ✅ Problem Statement (Leetcode 127 – Word Ladder I)

Given:

- A `beginWord`, a `endWord`, and a `wordList` (a list of words).
    
- You can transform a word by changing only **one letter** at a time.
    
- Each transformed word **must** exist in the wordList.
    

Goal:  
Return the **length of the shortest transformation sequence** from `beginWord` to `endWord`.

If no transformation is possible, return `0`.

---

### 🧠 Key Observations:

1. **Transformation is unweighted** – each move costs 1.
    
2. Problem reduces to **Unweighted Single-Source Shortest Path**.
    
3. Can be solved using **BFS** since we're looking for shortest path (level-wise traversal).
    
4. We treat each word as a node, and two nodes (words) are connected if they differ by exactly one letter.
    

---

### 💡 High-Level Idea:

1. Build an implicit graph:
    
    - Each word is a node.
        
    - Connect nodes if words differ by one character.
        
2. Use **BFS** starting from `beginWord`.
    
3. At each level of BFS, transform the current word to all possible valid next words by changing one character at a time.
    
4. Track visited nodes to avoid cycles.
    

---

### 🔁 Step-by-step Algorithm:

1. Convert `wordList` to a `HashSet` for O(1) lookups.
    
2. Initialize a queue for BFS and a visited set.
    
3. At each BFS level, generate all possible words by changing one character at a time.
    
4. If the new word is in `wordSet` and not visited, enqueue it.
    
5. Stop when you reach `endWord`, return the level count.
    
6. If queue is empty and `endWord` was not reached, return 0.
    

---

### ✅ Time and Space Complexity

- **Time Complexity:** O(N * L²)
    
    - N = size of wordList
        
    - L = length of each word
        
    - For each word, we try changing every character (L positions) to 26 possibilities.
        
- **Space Complexity:** O(N * L)
    
    - Storing wordList in set and queue for BFS.
        

---

### ✅ Java Code (With Comments)

```java
import java.util.*;

public class WordLadder {
    public int ladderLength(String beginWord, String endWord, List<String> wordList) {
        Set<String> wordSet = new HashSet<>(wordList); // For O(1) lookup
        if (!wordSet.contains(endWord)) return 0;

        Queue<String> queue = new LinkedList<>();
        queue.offer(beginWord);
        Set<String> visited = new HashSet<>();
        visited.add(beginWord);

        int steps = 1;

        while (!queue.isEmpty()) {
            int size = queue.size();

            // Process all words at current BFS level
            for (int i = 0; i < size; i++) {
                String word = queue.poll();

                // Try changing every character in the word
                for (int j = 0; j < word.length(); j++) {
                    char[] wordChars = word.toCharArray();
                    for (char c = 'a'; c <= 'z'; c++) {
                        if (wordChars[j] == c) continue;
                        wordChars[j] = c;
                        String newWord = new String(wordChars);

                        if (newWord.equals(endWord)) {
                            return steps + 1;
                        }

                        if (wordSet.contains(newWord) && !visited.contains(newWord)) {
                            visited.add(newWord);
                            queue.offer(newWord);
                        }
                    }
                }
            }

            steps++;
        }

        return 0; // No path found
    }
}
```

---

### 📌 Example

```java
beginWord = "hit"
endWord = "cog"
wordList = ["hot","dot","dog","lot","log","cog"]

BFS:
Level 1: hit
Level 2: hot
Level 3: dot, lot
Level 4: dog, log
Level 5: cog => return 5
```

---

### ❗ Why BFS and not DFS?

- DFS explores one path deeply but doesn't guarantee shortest path.
    
- BFS explores all possibilities at the same depth first — exactly what’s needed for the shortest transformation.
    

---

### 🔄 Extensions / Variants

1. **Word Ladder II** – Return all shortest paths (requires BFS + backtracking).
    
2. Use **bidirectional BFS** for better performance (from `beginWord` and `endWord` simultaneously).
    
3. Build an **adjacency list** based on wildcard patterns (like `h*t`, `ho*`) to optimize neighbor lookup.
    

---

Would you like me to explain **bidirectional BFS** or **Word Ladder II** next?