Let's now implement a **Queue using a Linked List** — this approach gives us **dynamic memory allocation**, so we don't have to worry about fixed size or circular behavior.

---

## ✅ Queue Using Linked List

### 🔧 How It Works:

- Use a **singly linked list**.
    
- Maintain two pointers:
    
    - `head`: Points to the front of the queue (for dequeue).
        
    - `tail`: Points to the rear of the queue (for enqueue).
        
- All operations are **O(1)**.
    

---

### 🔸 Java Code

```java
public class LinkedListQueue {
    private static class Node {
        int val;
        Node next;
        
        Node(int val) {
            this.val = val;
        }
    }

    private Node head; // Front of the queue
    private Node tail; // End of the queue
    private int size;

    // Enqueue operation: Add to the tail
    public void enqueue(int val) {
        Node newNode = new Node(val);
        if (tail != null) {
            tail.next = newNode;
        }
        tail = newNode;

        // If queue was empty, head should also point to newNode
        if (head == null) {
            head = newNode;
        }
        size++;
    }

    // Dequeue operation: Remove from the head
    public int dequeue() {
        if (isEmpty()) {
            throw new RuntimeException("Queue is empty");
        }

        int val = head.val;
        head = head.next;
        size--;

        // If queue becomes empty, tail should also be null
        if (head == null) {
            tail = null;
        }
        return val;
    }

    // Peek front element
    public int peek() {
        if (isEmpty()) {
            throw new RuntimeException("Queue is empty");
        }
        return head.val;
    }

    public boolean isEmpty() {
        return size == 0;
    }

    public int size() {
        return size;
    }
}
```

---

### ✅ Example Usage

```java
public class Main {
    public static void main(String[] args) {
        LinkedListQueue q = new LinkedListQueue();
        q.enqueue(10);
        q.enqueue(20);
        System.out.println(q.dequeue()); // 10
        q.enqueue(30);
        System.out.println(q.peek());    // 20
        System.out.println(q.dequeue()); // 20
        System.out.println(q.dequeue()); // 30
        System.out.println(q.isEmpty()); // true
    }
}
```

---

### 🔍 Advantages

- **No fixed size** — memory-efficient for growing queues.
    
- **All operations are O(1)**.
    
- Simpler than resizing arrays or circular logic.
    

Let me know if you want to build a **Deque (Double-ended Queue)** or implement **Queue using two stacks** next!