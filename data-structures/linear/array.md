# Arrays

## 🔹 What is an Array?

- Contiguous memory allocation
- Stores elements of same type
- Supports O(1) random access via index

⚠️ Interview Tip:

- “Contiguous memory” is VERY important — interviewers often ask this
- This is why insertion/deletion is costly

---

## 🔹 Time & Space Complexity

| Operation         | Time Complexity | Notes                           |
| ----------------- | --------------- | ------------------------------- |
| Access (arr[i])   | O(1)            | Direct indexing                 |
| Update            | O(1)            | Same as access                  |
| Insert (end)      | O(1) amortized  | Only for dynamic array (vector) |
| Insert (middle)   | O(n)            | Need shifting                   |
| Delete            | O(n)            | Need shifting                   |
| Search (unsorted) | O(n)            | Linear search                   |
| Search (sorted)   | O(log n)        | Binary search                   |

Space Complexity: O(n)

---

## 🔹 Static Array vs Dynamic Array

| Feature       | Static Array | Dynamic Array (vector) |
| ------------- | ------------ | ---------------------- |
| Size          | Fixed        | Resizable              |
| Memory        | Stack/Heap   | Heap                   |
| Resize Cost   | Not possible | O(n) (reallocation)    |
| Insert at end | O(1)         | O(1) amortized         |

⚠️ Interview Tip:

- “Amortized O(1)” is commonly asked
- Doubling strategy used in vectors

---

## 🔹 Basic Operations (C++)

### 1. Declaration

```cpp
int arr[5] = {1, 2, 3, 4, 5};
```

Time: O(1)  
Space: O(n)

---

### 2. Traversal

```cpp
for(int i = 0; i < n; i++) {
    cout << arr[i] << " ";
}
```

Time: O(n)  
Space: O(1)

---

### 3. Insertion at End

```cpp
arr[n] = x;
n++;
```

Time: O(1)  
Space: O(1)

⚠️ Only valid if space exists

---

### 4. Insertion at Position

```cpp
for(int i = n-1; i >= pos; i--) {
    arr[i+1] = arr[i];
}
arr[pos] = x;
n++;
```

Time: O(n)  
Space: O(1)

---

### 5. Deletion

```cpp
for(int i = pos; i < n-1; i++) {
    arr[i] = arr[i+1];
}
n--;
```

Time: O(n)  
Space: O(1)

---

### 6. Linear Search

```cpp
for(int i = 0; i < n; i++) {
    if(arr[i] == target) return i;
}
return -1;
```

Time: O(n)  
Space: O(1)

---

### 7. Binary Search (Sorted Array)

```cpp
int binarySearch(int arr[], int n, int target) {
    int l = 0, r = n - 1;
    while(l <= r) {
        int mid = l + (r - l) / 2;

        if(arr[mid] == target) return mid;
        else if(arr[mid] < target) l = mid + 1;
        else r = mid - 1;
    }
    return -1;
}
```

Time: O(log n)  
Space: O(1)

⚠️ Interview Tip:

- Always use `mid = l + (r - l) / 2` to avoid overflow

---

## 🔹 Common Interview Patterns

### 1. Prefix Sum

```cpp
prefix[0] = arr[0];
for(int i = 1; i < n; i++) {
    prefix[i] = prefix[i-1] + arr[i];
}
```

Time: O(n)  
Space: O(n)

Use: Range sum queries

---

### 2. Two Pointers

```cpp
int l = 0, r = n - 1;
while(l < r) {
    if(arr[l] + arr[r] == target) break;
    else if(arr[l] + arr[r] < target) l++;
    else r--;
}
```

Time: O(n)  
Space: O(1)

---

### 3. Sliding Window

```cpp
int sum = 0, l = 0;
for(int r = 0; r < n; r++) {
    sum += arr[r];

    while(sum > k) {
        sum -= arr[l];
        l++;
    }
}
```

Time: O(n)  
Space: O(1)

---

## 🔹 Important Edge Cases (VERY IMPORTANT)

- Empty array (n = 0)
- Single element
- Large input (overflow risk)
- Negative numbers (breaks some sliding window logic)
- Sorted vs unsorted (affects approach)

---

## 🔹 Common Mistakes

❌ Forgetting bounds → segmentation fault  
❌ Using binary search on unsorted array  
❌ Not handling duplicates  
❌ Off-by-one errors

---

## 🔹 When to Use Array?

✅ Fast index access needed  
✅ Fixed-size data  
✅ Cache-friendly operations

❌ Avoid when:

- Frequent insert/delete in middle → use linked list
- Dynamic resizing heavy → use vector

---

## 🔹 Interview Questions You MUST Know

- Two Sum
- Maximum Subarray (Kadane’s Algorithm)
- Best Time to Buy & Sell Stock
- Product of Array Except Self
- Merge Intervals
- Rotate Array

---

## 🔹 Pro Tips (High Value)

- Arrays = **foundation of almost everything**
- Many DS (heap, hash table, matrix) are built on arrays
- Master patterns → Sliding Window, Prefix Sum, Two Pointer

🔥 If you are short on time:
Focus on:

1. Traversal
2. Binary Search
3. Sliding Window
4. Prefix Sum

```

```
