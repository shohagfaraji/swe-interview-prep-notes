# O(n log n) Time Complexity

## Definition
An algorithm is **O(n log n)** when:
- There is a **linear operation O(n)**
- And inside it, a **logarithmic operation O(log n)** happens repeatedly

👉 Typical idea:  
**Do something O(log n) for each of n elements**

---

## Core Understanding

Most O(n log n) comes from:
- Sorting
- Divide & conquer
- Balanced tree operations inside loops

Think:
- “Each element contributes log n work”

---

## Most Important Source: Sorting

### 1. Standard Sorting
```cpp
sort(arr.begin(), arr.end());
```

👉 Internally O(n log n)

---

### 2. Sorting then Processing
```cpp
sort(arr.begin(), arr.end());

for(int i = 0; i < n; i++) {
    cout << arr[i] << " ";
}
```

👉 O(n log n) + O(n) = O(n log n)

---

## Divide & Conquer Patterns

### 3. Merge Sort (Classic)
```cpp
void mergeSort(vector<int>& arr, int l, int r) {
    if(l >= r) return;

    int mid = (l + r) / 2;

    mergeSort(arr, l, mid);
    mergeSort(arr, mid + 1, r);

    merge(arr, l, mid, r);
}
```

👉 Each level processes n elements  
👉 Height = log n  
👉 Total = O(n log n)

---

### 4. Quick Sort (Average Case)
```cpp
void quickSort(vector<int>& arr, int l, int r) {
    if(l >= r) return;

    int pivot = partition(arr, l, r);

    quickSort(arr, l, pivot - 1);
    quickSort(arr, pivot + 1, r);
}
```

👉 Average: O(n log n)

---

## Data Structure Based O(n log n)

### 5. Insert into Balanced Tree in Loop
```cpp
set<int> s;

for(int i = 0; i < n; i++) {
    s.insert(arr[i]);
}
```

👉 Each insert = log n → total O(n log n)

---

### 6. Map Operations in Loop
```cpp
map<int,int> mp;

for(int i = 0; i < n; i++) {
    mp[arr[i]]++;
}
```

👉 Each operation log n → O(n log n)

---

## Heap-Based Patterns

### 7. Priority Queue Build + Operations
```cpp
priority_queue<int> pq;

for(int i = 0; i < n; i++) {
    pq.push(arr[i]);
}
```

👉 Each push = log n → O(n log n)

---

### 8. Extracting Elements
```cpp
while(!pq.empty()) {
    pq.pop();
}
```

---

## Classic Problem Patterns

### 9. K largest / smallest elements
```cpp
priority_queue<int> pq;

for(int i = 0; i < n; i++) {
    pq.push(arr[i]);
}
```

---

### 10. Interval Sorting Problems
```cpp
sort(intervals.begin(), intervals.end());
```

Used in:
- Merge intervals
- Scheduling problems

---

### 11. Greedy after Sorting
```cpp
sort(arr.begin(), arr.end());

for(int i = 0; i < n; i++) {
    // greedy decision
}
```

---

## Why O(n log n) Happens

### Pattern:
- Loop over n elements
- Each operation costs log n

Examples:
- Insert into BST → log n
- Heap push → log n
- Sort internally → n log n

---

## Divide & Conquer Insight

At each level:
- Work done = O(n)

Number of levels:
- log n (because problem size halves)

👉 Total:
```
O(n) × O(log n) = O(n log n)
```

---

## Tricky Cases

### Case 1: Sorting inside loop (very important mistake)
```cpp
for(int i = 0; i < n; i++) {
    sort(arr.begin(), arr.end());
}
```
👉 Repeated sorting → still O(n log n) per iteration → worse total, but base operation is n log n

---

### Case 2: Set inside loop
```cpp
set<int> s;

for(int i = 0; i < n; i++) {
    s.insert(arr[i]);
}
```

---

### Case 3: Heap rebuild vs push
- Push n elements → O(n log n)
- Extract all → O(n log n)

---

## Common Mistakes

### Mistake 1: Thinking sorting is O(n)
It is always **O(n log n)**

---

### Mistake 2: Ignoring log factor in loops
```cpp
for(int i = 0; i < n; i++) {
    set.insert(x);
}
```

---

### Mistake 3: Confusing linear scan after sorting
Sorting dominates complexity

---

## Recognition Strategy

Check:
1. Is there sorting?
2. Is there a loop + log operation?
3. Is recursion dividing input?

If yes → **O(n log n)**

---

## Summary

- Sorting → O(n log n)
- Merge / Quick sort → O(n log n)
- Heap operations in loop → O(n log n)
- Set / Map insertions in loop → O(n log n)
- Divide & conquer → O(n log n)

**Key idea:**  
n operations × log n work per operation