Great! Let's walk through both implementations step by step — starting with a **normal (linear) queue using array**, and then optimizing it using a **circular queue**.

---

## ✅ 1️⃣ Normal Queue Using Array

### 🔧 **How It Works**

- Elements are enqueued at the **rear**.
    
- Elements are dequeued from the **front**.
    
- We maintain `front` and `rear` pointers.
    
- **Limitation**: After some dequeues, even if the array has free space in front, we **can’t reuse it**.
    

---

### 🔸 Code: Normal Queue (Fixed-Size, No Reuse)

```java
public class SimpleQueue {
    private int[] data;
    private int front;
    private int rear;
    private int capacity;

    public SimpleQueue(int capacity) {
        this.capacity = capacity;
        data = new int[capacity];
        front = 0;
        rear = -1;
    }

    public boolean enqueue(int val) {
        if (rear == capacity - 1) {
            System.out.println("Queue is full");
            return false;
        }
        rear++;
        data[rear] = val;
        return true;
    }

    public int dequeue() {
        if (isEmpty()) {
            throw new RuntimeException("Queue is empty");
        }
        int value = data[front];
        front++;
        return value;
    }

    public boolean isEmpty() {
        return front > rear;
    }

    public int peek() {
        if (isEmpty()) {
            throw new RuntimeException("Queue is empty");
        }
        return data[front];
    }

    public int size() {
        return rear - front + 1;
    }
}
```

---

### 🔍 **Limitations**

- Once `rear` reaches the end (`capacity - 1`), no new elements can be added, even if earlier elements were dequeued.
    
- Waste of space → Time to optimize!
    

---

## ✅ 2️⃣ Circular Queue Using Array

### 🔧 **What's Improved?**

- When `rear` reaches the end, we wrap it to the beginning if space is available.
    
- We use modulo (`%`) to wrap around indices.
    

---

### 🔸 Code: Circular Queue

```java
public class CircularQueue {
    private int[] data;
    private int front;
    private int rear;
    private int size;
    private int capacity;

    public CircularQueue(int capacity) {
        this.capacity = capacity;
        data = new int[capacity];
        front = 0;
        rear = -1;
        size = 0;
    }

    public boolean enqueue(int val) {
        if (isFull()) {
            System.out.println("Queue is full");
            return false;
        }
        rear = (rear + 1) % capacity;
        data[rear] = val;
        size++;
        return true;
    }

    public int dequeue() {
        if (isEmpty()) {
            throw new RuntimeException("Queue is empty");
        }
        int val = data[front];
        front = (front + 1) % capacity;
        size--;
        return val;
    }

    public int peek() {
        if (isEmpty()) {
            throw new RuntimeException("Queue is empty");
        }
        return data[front];
    }

    public boolean isEmpty() {
        return size == 0;
    }

    public boolean isFull() {
        return size == capacity;
    }

    public int size() {
        return size;
    }
}
```

---

### 🔄 Why `(rear + 1) % capacity`?

To wrap around to the beginning of the array when rear reaches the end — for example:

- If `capacity = 5` and `rear = 4`, then next position becomes `(4 + 1) % 5 = 0`.
    

---

## ✅ Summary

|Feature|Normal Queue|Circular Queue|
|---|---|---|
|Space reuse|❌ No reuse|✅ Efficient reuse|
|Implementation|Simple, intuitive|Slightly more complex|
|Performance|Poor for long runs|Optimal and clean|
|Ideal for|Small static queues|Real-world applications|

---

Let me know if you want a **dynamic resizing queue**, or to move to **Deque (double-ended queue)** next!