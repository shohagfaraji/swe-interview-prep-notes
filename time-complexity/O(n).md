# O(n) Time Complexity

## Definition

An algorithm is **O(n)** if the total number of operations grows **linearly** with input size `n`.

- Each element is processed **once or a constant number of times**
- Total work is proportional to `n`

---

## Core Understanding

Focus on:

- How many times each element is used
- Whether pointers or indices **repeat work**

If every element contributes constant work → **O(n)**

---

## Basic Patterns

### 1. Single Traversal

```cpp
for(int i = 0; i < n; i++) {
    cout << arr[i] << " ";
}
```

---

### 2. Aggregation

```cpp
long long sum = 0;
for(int i = 0; i < n; i++) {
    sum += arr[i];
}
```

---

### 3. Minimum / Maximum

```cpp
int mn = arr[0];
for(int i = 1; i < n; i++) {
    if(arr[i] < mn) mn = arr[i];
}
```

---

### 4. Using Hash Structure (average constant work)

```cpp
unordered_map<int,int> freq;
for(int i = 0; i < n; i++) {
    freq[arr[i]]++;
}
```

**Key:** Average case $O(n)$ but in Worst case $O(n^2)$

---

## Important Linear Structures

### 5. Two Pointers (No Reset)

```cpp
int l = 0, r = n - 1;

while(l < r) {
    if(arr[l] + arr[r] > target) r--;
    else l++;
}
```

**Key:** both pointers move forward only → total movement is linear

---

### 6. Sliding Window

#### General Template

```cpp
int l = 0;

for(int r = 0; r < n; r++) {
    // include arr[r] in window

    while(window is invalid) {
        // remove arr[l] from window
        l++;
    }
}
```

#### Example 1: Sum constraint

```cpp
int l = 0, sum = 0;

for(int r = 0; r < n; r++) {
    sum += arr[r];

    while(sum > k) {
        sum -= arr[l];
        l++;
    }
}
```

#### Example 2: No duplicates in window

```cpp
unordered_map<int,int> freq;
int l = 0;

for(int r = 0; r < n; r++) {
    freq[arr[r]]++;

    while(freq[arr[r]] > 1) {
        freq[arr[l]]--;
        l++;
    }
}
```

#### Example 3: Fixed window size

```cpp
int l = 0;

for(int r = 0; r < n; r++) {
    if(r - l + 1 > k) {
        l++;
    }
}
```

**Key Insight:**  
Even with `while`, total `l++` and `r++` ≤ `n` → O(n)

---

### 7. Prefix Sum

```cpp
vector<int> pref(n);
pref[0] = arr[0];

for(int i = 1; i < n; i++) {
    pref[i] = pref[i - 1] + arr[i];
}
```

---

### 8. Stack-Based Processing

```cpp
stack<int> st;

for(int i = 0; i < n; i++) {
    while(!st.empty() && st.top() > arr[i]) {
        st.pop();
    }
    st.push(arr[i]);
}
```

Each element pushed and popped at most once

---

## Tricky Cases (Looks Non-Linear but O(n))

### Case 1: Nested but Linear

```cpp
int j = 0;

for(int i = 0; i < n; i++) {
    while(j < n) {
        j++;
    }
}
```

`j` runs once overall

---

### Case 2: Dependent Pointers

```cpp
int j = 0;

for(int i = 0; i < n; i++) {
    while(j < n && arr[j] < arr[i]) {
        j++;
    }
}
```

`j` only moves forward

---

### Case 3: Removing Elements

```cpp
while(!v.empty()) {
    v.pop_back();
}
```

Each element removed once

---

### Case 4: String Traversal

```cpp
for(char c : s) {
    cout << c;
}
```

---

### Case 5: Linear Recursion

```cpp
void f(int n) {
    if(n == 0) return;
    f(n - 1);
}
```

---

## Common Mistakes

### Mistake 1: Resetting Work

```cpp
for(int i = 0; i < n; i++) {
    int j = 0;
    while(j < n) {
        j++;
    }
}
```

---

### Mistake 2: Full Nested Loop

```cpp
for(int i = 0; i < n; i++) {
    for(int j = 0; j < n; j++) {
        cout << i << j;
    }
}
```

---

### Mistake 3: Hidden Heavy Work Inside Loop

```cpp
for(int i = 0; i < n; i++) {
    // expensive operation repeated fully
}
```

---

## Key Observations

### Multiple Linear Passes

```cpp
for(int i = 0; i < n; i++) {}
for(int i = 0; i < n; i++) {}
```

---

### Mixed Work

```cpp
for(int i = 0; i < n; i++) {}
for(int i = 0; i < smaller_range; i++) {}
```

---

### Input Reading

```cpp
for(int i = 0; i < n; i++) cin >> arr[i];
```

---

## Recognition Strategy

To confirm O(n), check:

1. Does any loop restart full work repeatedly?
2. Do pointers only move forward?
3. Is each element processed constant times?
4. Are nested loops actually sharing work?

---

## Summary

- Single traversal → O(n)
- Two pointers (no reset) → O(n)
- Sliding window → O(n)
- Stack-based processing → O(n)
- Key idea: count **total operations**, not number of loops
