# Queue (FIFO - First In First Out)

## 🔹 What is a Queue?

- Linear data structure
- Follows **FIFO (First In First Out)**
- Insertion at **rear**, deletion from **front**

Example:
Push: 1 → 2 → 3  
Pop: removes 1 first

---

## 🔹 Time & Space Complexity

| Operation | Time Complexity | Notes             |
| --------- | --------------- | ----------------- |
| push      | O(1)            | Insert at rear    |
| pop       | O(1)            | Remove from front |
| front     | O(1)            | Access front      |
| empty     | O(1)            | Check empty       |

Space Complexity: O(n)

---

## 🔹 STL Queue (C++)

```cpp
#include <queue>
using namespace std;

queue<int> q;

q.push(10);
q.push(20);
q.pop();

cout << q.front(); // 20
```

⚠️ Interview Tip:

- Internally uses **deque**
- No direct iteration

---

## 🔹 Types of Queue

- Simple Queue ❌ (not efficient)
- Circular Queue ✅ (IMPORTANT)
- Deque (Double-ended queue)
- Priority Queue (heap based)

---

## 🔹 Implementation Using Circular Array (BEST for Interviews)

### Why Circular?

- Reuses empty space
- Avoids shifting
- Efficient memory usage

---

### Queue Class (Circular Array)

```cpp
#include <bits/stdc++.h>
using namespace std;

class Queue {
private:
    int arr[1000];
    int frontIndex, rearIndex, size, capacity;

public:
    Queue(int cap = 1000) {
        capacity = cap;
        frontIndex = 0;
        rearIndex = -1;
        size = 0;
    }

    // Push
    void push(int x) {
        if (size == capacity) {
            cout << "Queue Overflow\n";
            return;
        }
        rearIndex = (rearIndex + 1) % capacity;
        arr[rearIndex] = x;
        size++;
    }
    // Time: O(1)

    // Pop
    void pop() {
        if (size == 0) {
            cout << "Queue Underflow\n";
            return;
        }
        frontIndex = (frontIndex + 1) % capacity;
        size--;
    }
    // Time: O(1)

    // Front
    int front() {
        if (size == 0) {
            cout << "Empty Queue\n";
            return -1;
        }
        return arr[frontIndex];
    }
    // Time: O(1)

    // Empty
    bool empty() {
        return size == 0;
    }

    // Size
    int getSize() {
        return size;
    }
};
```

---

## 🔹 Implementation Using Vector (Simple but Less Ideal)

```cpp
#include <bits/stdc++.h>
using namespace std;

class Queue {
private:
    vector<int> v;

public:
    void push(int x) {
        v.push_back(x);
    }
    // Time: O(1) amortized

    void pop() {
        if (v.empty()) {
            cout << "Underflow\n";
            return;
        }
        v.erase(v.begin()); // costly
    }
    // Time: O(n)

    int front() {
        if (v.empty()) return -1;
        return v[0];
    }
};
```

⚠️ Interview Warning:

- `erase(v.begin())` = O(n) → BAD
- Avoid this implementation in interviews

---

## 🔹 Better Alternative: Deque

```cpp
#include <deque>
deque<int> dq;

dq.push_back(10);
dq.pop_front();
```

Time: O(1) for both ends

---

## 🔹 Queue vs Deque vs Stack

| Feature  | Queue | Deque    | Stack |
| -------- | ----- | -------- | ----- |
| Insert   | Rear  | Both     | Top   |
| Delete   | Front | Both     | Top   |
| Use Case | FIFO  | Flexible | LIFO  |

---

## 🔹 Common Interview Patterns

### 1. BFS (VERY IMPORTANT)

```cpp
void bfs(int start, vector<vector<int>>& adj) {
    queue<int> q;
    vector<bool> vis(adj.size(), false);

    q.push(start);
    vis[start] = true;

    while(!q.empty()) {
        int node = q.front();
        q.pop();

        for(int nei : adj[node]) {
            if(!vis[nei]) {
                vis[nei] = true;
                q.push(nei);
            }
        }
    }
}
```

Time: O(V + E)  
Space: O(V)

---

### 2. Sliding Window Maximum (Deque)

```cpp
vector<int> maxSlidingWindow(vector<int>& nums, int k) {
    deque<int> dq;
    vector<int> res;

    for(int i = 0; i < nums.size(); i++) {
        if(!dq.empty() && dq.front() == i - k)
            dq.pop_front();

        while(!dq.empty() && nums[dq.back()] < nums[i])
            dq.pop_back();

        dq.push_back(i);

        if(i >= k - 1)
            res.push_back(nums[dq.front()]);
    }
    return res;
}
```

Time: O(n)  
Space: O(n)

---

### 3. Level Order Traversal (Tree)

Uses queue internally (BFS)

---

## 🔹 Important Edge Cases

- Pop from empty queue
- Single element queue
- Full queue (array implementation)
- Circular index overflow handling

---

## 🔹 Common Mistakes

❌ Using simple array queue (wastes space)  
❌ Using vector erase (O(n))  
❌ Not handling circular wrap properly  
❌ Confusing front vs rear

---

## 🔹 When to Use Queue?

✅ BFS traversal  
✅ Scheduling problems  
✅ Producer-consumer problems  
✅ Streaming data

---

## 🔹 Common Interview Questions

- Implement queue using stacks
- Implement circular queue
- Sliding window problems
- Rotten oranges (BFS)
- Level order traversal

---

## 🔹 Pro Tips (High Value)

🔥 Prefer deque for flexibility  
🔥 Circular queue = interview favorite  
🔥 Queue is core of BFS (VERY IMPORTANT)

---

## 🔹 Quick Summary

- Queue = FIFO
- push/pop → O(1)
- Circular array best implementation
- Avoid vector erase
- Used heavily in BFS
