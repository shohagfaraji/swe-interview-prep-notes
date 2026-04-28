# O(log n) Time Complexity

## Definition
An algorithm is **O(log n)** if the input size is reduced by a **constant factor (usually half)** at each step.

- Growth is very slow
- Even for large `n`, operations are small
- Common in **divide & reduce techniques**

---

## Core Idea

At each step:
- Reduce problem size: `n → n/2 → n/4 → n/8 ...`
- Number of steps = number of times we can divide by 2 until 1

👉 This is why binary operations give **log n**

---

## Fundamental Pattern: Binary Reduction

### 1. Iterative Binary Reduction
```cpp
while(n > 1) {
    n /= 2;
}
```

---

### 2. Power of Two Check
```cpp
bool isPowerOfTwo(int n) {
    return (n & (n - 1)) == 0;
}
```

---

## Binary Search (Most Important Use of O(log n))

### 3. Basic Binary Search
```cpp
int l = 0, r = n - 1;

while(l <= r) {
    int mid = l + (r - l) / 2;

    if(arr[mid] == target) return mid;
    else if(arr[mid] < target) l = mid + 1;
    else r = mid - 1;
}
```

---

### 4. Lower Bound (First >= target)
```cpp
int l = 0, r = n;

while(l < r) {
    int mid = (l + r) / 2;

    if(arr[mid] < target) l = mid + 1;
    else r = mid;
}
```

---

### 5. Upper Bound (First > target)
```cpp
int l = 0, r = n;

while(l < r) {
    int mid = (l + r) / 2;

    if(arr[mid] <= target) l = mid + 1;
    else r = mid;
}
```

---

## Binary Search on Answer (Very Important)

### 6. Minimum Valid Answer
```cpp
int l = 0, r = 1e9, ans = -1;

while(l <= r) {
    int mid = (l + r) / 2;

    if(check(mid)) {
        ans = mid;
        r = mid - 1;
    } else {
        l = mid + 1;
    }
}
```

👉 Used in:
- Minimum maximum problems
- Optimization problems
- Feasibility check problems

---

## Data Structures with O(log n)

### 7. Ordered Set
```cpp
#include <ext/pb_ds/assoc_container.hpp>
using namespace __gnu_pbds;

tree<int, null_type, less<int>, rb_tree_tag,
     tree_order_statistics_node_update> s;
```

Operations:
```cpp
s.insert(x);        // O(log n)
s.erase(x);         // O(log n)
s.find_by_order(k); // O(log n)
s.order_of_key(x);  // O(log n)
```

---

### 8. Multiset Operations
```cpp
multiset<int> ms;

ms.insert(x);   // O(log n)
ms.erase(x);    // O(log n)
```

---

### 9. Map / Set
```cpp
map<int,int> mp;

mp[x] = 10;
mp.find(x);
```

Each operation is logarithmic due to tree structure.

---

## Mathematical Log Patterns

### 10. Count Steps by Division
```cpp
int cnt = 0;
while(n > 1) {
    n /= 2;
    cnt++;
}
```

👉 cnt = log₂(n)

---

### 11. Fast Exponentiation (Binary Exponentiation)

```cpp
long long power(long long a, long long b) {
    long long res = 1;

    while(b > 0) {
        if(b & 1) res *= a;

        a *= a;
        b >>= 1;
    }

    return res;
}
```

👉 Each step halves exponent → O(log n)

---

## Bitwise Log Patterns

### 12. Highest Power of 2
```cpp
int x = 1;

while(x <= n) {
    x <<= 1;
}
```

---

### 13. Bit Length
```cpp
int bits = 0;

while(n > 0) {
    n >>= 1;
    bits++;
}
```

---

## Tricky Cases (Important)

### Case 1: Log inside loop still log n
```cpp
for(int i = 1; i <= n; i *= 2) {
}
```

---

### Case 2: Repeated halving
```cpp
while(n > 1) {
    n /= 2;
}
```

---

### Case 3: Binary search shrinking space
- Each iteration halves search space
- Never revisits eliminated half

---

## Common Mistakes

### Mistake 1: Linear loop disguised as log
```cpp
for(int i = 0; i < n; i++) {}
```

---

### Mistake 2: Incorrect binary search boundaries
- Wrong mid update → infinite loop

---

### Mistake 3: Not reducing search space
```cpp
while(l < r) {
    mid = (l + r) / 2;
    // missing update → not log n
}
```

---

## Classic Problems Using O(log n)

- Binary search in sorted array
- First/last occurrence of element
- Square root / floor sqrt
- Search in rotated array
- Minimum in rotated array
- K-th element using order statistics
- Exponentiation problems
- Feasibility + optimization problems

---

## Recognition Strategy

Ask:
1. Is the search space halved each step?
2. Are we using divide-and-reduce?
3. Is the structure a BST or sorted array?

If yes → **O(log n)**

---

## Summary

- Halving problem size → O(log n)
- Binary search → O(log n)
- Tree structures → O(log n)
- Bitwise reduction → O(log n)
- Fast exponentiation → O(log n)

**Key idea:**  
Every step removes half the remaining work