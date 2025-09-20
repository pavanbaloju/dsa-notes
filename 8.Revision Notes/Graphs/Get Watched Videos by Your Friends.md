Here are the **full notes for Leetcode 1311 – Get Watched Videos by Your Friends**, including problem breakdown, key concepts, step-by-step approach, code with comments, edge cases, and complexity analysis.

---

## ✅ Problem Summary:

**Leetcode 1311 – Get Watched Videos by Your Friends**  
You are given:

- A list of `videos` watched by each person.
    
- A `friends` list where `friends[i]` is the list of person `i`'s direct friends.
    
- An integer `id` (starting person) and `level`.
    

**Goal:**  
Return a list of video names watched by friends at the _given level of friendship_ (BFS level), **sorted by frequency (asc), then lexicographically.**

---

## ✅ Example:

```text
Input:
videos = [["A", "B"], ["C"], ["B", "C"], ["D"]],
friends = [[1, 2], [0, 3], [0, 3], [1, 2]],
id = 0,
level = 1

Output:
["C", "D"]
```

- Person 0 has friends [1,2] at level 1.
    
- Their videos are: ["C"] (from 1), ["B", "C"] (from 2)
    
- Combine: ["C", "B", "C"] → Frequencies: C=2, B=1 → Sorted: B(1), C(2) → ["B", "C"]
    

Oops! Actually the output should be:

```text
["B", "C"]
```

---

## ✅ Core Concepts:

1. **BFS** to traverse the graph of friends up to the given level.
    
2. **Map for frequency counting** of video names.
    
3. **Sorting by frequency then lexicographically.**
    

---

## ✅ Step-by-Step Plan:

1. **Use BFS** from `id` to collect all friends at `level`.
    
2. Collect all the videos they watched.
    
3. Use a `Map<String, Integer>` to count frequencies.
    
4. Use a custom comparator to sort by:
    
    - Frequency ascending
        
    - Name lexicographically if frequency is same.
        

---

## ✅ Java Code (with comments)

```java
import java.util.*;

public class WatchedVideosByFriends {

    public List<String> watchedVideosByFriends(List<List<String>> watchedVideos, int[][] friends, int id, int level) {
        int n = friends.length;

        // Step 1: BFS to find friends at the given level
        boolean[] visited = new boolean[n];
        Queue<Integer> queue = new LinkedList<>();
        visited[id] = true;
        queue.offer(id);

        int currentLevel = 0;

        while (!queue.isEmpty() && currentLevel < level) {
            int size = queue.size();

            for (int i = 0; i < size; i++) {
                int person = queue.poll();
                for (int friend : friends[person]) {
                    if (!visited[friend]) {
                        visited[friend] = true;
                        queue.offer(friend);
                    }
                }
            }

            currentLevel++;
        }

        // Step 2: Count video frequencies for friends at the desired level
        Map<String, Integer> videoFreq = new HashMap<>();

        while (!queue.isEmpty()) {
            int person = queue.poll();
            for (String video : watchedVideos.get(person)) {
                videoFreq.put(video, videoFreq.getOrDefault(video, 0) + 1);
            }
        }

        // Step 3: Sort videos by frequency and lexicographical order
        List<String> result = new ArrayList<>(videoFreq.keySet());

        result.sort((a, b) -> {
            int freqCompare = Integer.compare(videoFreq.get(a), videoFreq.get(b));
            if (freqCompare == 0) {
                return a.compareTo(b);
            }
            return freqCompare;
        });

        return result;
    }
}
```

---

## ✅ Time & Space Complexity:

Let:

- `n = number of people`
    
- `v = average number of videos per person`
    
- `f = number of friends at given level`
    

**Time Complexity:**

- BFS traversal: `O(n + E)` where E = total edges
    
- Collecting videos: `O(f * v)`
    
- Sorting videos: `O(m log m)` where `m = number of unique videos`
    

**Space Complexity:**

- `O(n)` for visited and queue
    
- `O(m)` for frequency map
    
- `O(m)` for result list
    

---

## ✅ Edge Cases:

- `level == 0`: return videos of the person themselves
    
- Person has no friends at that level → return `[]`
    
- Two videos have same frequency → must be sorted alphabetically
    
- Video list can contain duplicates — handled by counting frequency
    

---

## ✅ Sample Dry Run:

```java
watchedVideos = [["A", "B"], ["C"], ["B", "C"], ["D"]]
friends =        [[1, 2],    [0, 3], [0, 3],    [1, 2]]
id = 0
level = 2

→ BFS:
Level 0: [0]
Level 1: [1, 2]
Level 2: [3]

→ Person 3 watched: ["D"]

→ Result: ["D"]
```

---

## ✅ Summary

|Step|Purpose|
|---|---|
|**BFS**|To reach all friends at a specific level|
|**Frequency Map**|Count how often each video appears|
|**Custom Sort**|By frequency ascending, then lexicographically|
|**Edge Handling**|No friends, self-loop, same frequency|

---

Let me know if you’d like the **DFS** version or **Python equivalent** as well.