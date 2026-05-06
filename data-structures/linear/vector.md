# Vector (C++ Dynamic Array)

## 🔹 What is a Vector?

- Dynamic array provided by STL (`<vector>`)
- Resizable (automatically grows)
- Stores elements in **contiguous memory**
- Supports **random access O(1)**

⚠️ Interview Tip:

- Vector = dynamic array (NOT linked list)
- Internally uses **array doubling strategy**

---

## 🔹 Time & Space Complexity

| Operation     | Time Complexity | Notes              |
| ------------- | --------------- | ------------------ |
| Access (v[i]) | O(1)            | Same as array      |
| Update        | O(1)            | Direct indexing    |
| push_back()   | O(1) amortized  | May trigger resize |
| pop_back()    | O(1)            | Removes last       |
| insert()      | O(n)            | Shift elements     |
| erase()       | O(n)            | Shift elements     |
| size()        | O(1)            | Stored internally  |
| capacity()    | O(1)            | Stored internally  |
| clear()       | O(n)            | Destroys elements  |

Space Complexity: O(n)

---

## 🔹 Key Concepts (VERY IMPORTANT)

### 1. Size vs Capacity

| Term       | Meaning            |
| ---------- | ------------------ |
| size()     | Number of elements |
| capacity() | Allocated memory   |

```cpp
vector<int> v;
v.push_back(1);

cout << v.size();     // 1
cout << v.capacity(); // >=1
```

⚠️ Interview Tip:

- Capacity usually **doubles**
- Reallocation = expensive (O(n))

---

### 2. Reallocation (Hidden Cost)

- When capacity is full → new memory allocated
- Old elements copied → O(n)

⚠️ Interview Question:
👉 Why push_back is O(1) amortized?

- Because resizing doesn’t happen every time

---

## 🔹 Basic Operations (C++)

### 1. Declaration

```cpp
vector<int> v;
vector<int> v2(5, 10); // size 5, all 10
```

Time: O(n) (if initialized)  
Space: O(n)

---

### 2. Traversal

```cpp
for(int i = 0; i < v.size(); i++) {
    cout << v[i] << " ";
}
```

OR

```cpp
for(auto x : v) {
    cout << x << " ";
}
```

Time: O(n)  
Space: O(1)

---

### 3. push_back()

```cpp
v.push_back(10);
```

Time: O(1) amortized  
Space: O(1)

---

### 4. pop_back()

```cpp
v.pop_back();
```

Time: O(1)  
Space: O(1)

---

### 5. insert()

```cpp
v.insert(v.begin() + pos, value);
```

Time: O(n)  
Space: O(1)

---

### 6. erase()

```cpp
v.erase(v.begin() + pos);
```

Time: O(n)  
Space: O(1)

---

### 7. clear()

```cpp
v.clear();
```

Time: O(n)  
Space: O(1)

⚠️ Important:

- Capacity is NOT reduced

---

### 8. Resize

```cpp
v.resize(10);        // fills with 0
v.resize(5);         // trims
```

Time: O(n)  
Space: O(n)

---

### 9. Reserve (VERY IMPORTANT)

```cpp
v.reserve(100);
```

Time: O(n) (once)  
Space: O(n)

🔥 Use when size is known → avoids multiple reallocations

---

## 🔹 Common Interview Patterns

### 1. Dynamic Input Storage

```cpp
int x;
while(cin >> x) {
    v.push_back(x);
}
```

---

### 2. Using as Stack

```cpp
v.push_back(x);
v.pop_back();
```

Same as stack (faster than stack in practice)

---

### 3. 2D Vector

```cpp
vector<vector<int>> grid(n, vector<int>(m, 0));
```

⚠️ Interview Tip:

- Jagged arrays possible

---

### 4. Sorting

```cpp
sort(v.begin(), v.end());
```

Time: O(n log n)

---

## 🔹 Important Edge Cases

- Empty vector → accessing v[0] crashes
- After erase → iterators become invalid
- Resize shrink → data lost
- Large input → multiple reallocations

---

## 🔹 Common Mistakes

❌ Using `v[i]` without checking size  
❌ Confusing size vs capacity  
❌ Not reserving space when needed  
❌ Using insert/erase frequently (slow)  
❌ Iterator invalidation after modification

---

## 🔹 Iterator Invalidation (VERY IMPORTANT)

| Operation   | Effect                           |
| ----------- | -------------------------------- |
| push_back() | May invalidate all iterators     |
| insert()    | Invalidates from position onward |
| erase()     | Invalidates from position onward |

⚠️ Interview Trap:

- Using iterator after erase → undefined behavior

---

## 🔹 When to Use Vector?

✅ Need dynamic resizing  
✅ Need fast random access  
✅ Most common default choice

❌ Avoid when:

- Frequent insert/delete in middle → use list
- Strict memory constraints → array

---

## 🔹 Vector vs Array

| Feature     | Array      | Vector  |
| ----------- | ---------- | ------- |
| Size        | Fixed      | Dynamic |
| Memory      | Stack/Heap | Heap    |
| Resize      | ❌         | ✅      |
| STL Support | ❌         | ✅      |

---

## 🔹 Common Interview Questions

- Dynamic array implementation
- Why vector is faster than list?
- Difference: vector vs deque
- When does reallocation happen?
- What is capacity growth strategy?

---

## 🔹 Real Problems Using Vector

- Two Sum
- Merge Intervals
- Kth Largest Element
- Sliding Window Maximum
- Matrix Problems (2D vector)

---

## 🔹 Pro Tips (High Value)

🔥 Always prefer vector over array in interviews  
🔥 Use reserve() for performance optimization  
🔥 Avoid insert/erase in middle in loops

---

## 🔹 Quick Summary

- Vector = dynamic array
- Contiguous memory
- push_back → amortized O(1)
- insert/delete → O(n)
- reserve() = performance booster
