# O(√n) Time Complexity

## Definition
An algorithm is **O(√n)** if the number of operations grows proportional to the **square root of n**.

- Much faster than O(n)
- Common when reducing search space using **factors or blocks**

---

## Core Understanding

Key idea:
- Instead of checking all values up to `n`, you only go up to `√n`
- Often used when:
  - Working with **divisors**
  - Splitting range into **blocks**
  - Jumping in steps instead of linear scan

---

## Basic Pattern

### 1. Loop up to √n
```cpp
for(int i = 1; i * i <= n; i++) {
    // work
}
```

---

## Important Applications

### 2. Finding Divisors
```cpp
vector<int> divisors;

for(int i = 1; i * i <= n; i++) {
    if(n % i == 0) {
        divisors.push_back(i);

        if(i != n / i) {
            divisors.push_back(n / i);
        }
    }
}
```

**Key Insight:**
Divisors come in pairs → reduces work to √n

---

### 3. Check if Number is Prime
```cpp
bool isPrime(int n) {
    if(n < 2) return false;

    for(int i = 2; i * i <= n; i++) {
        if(n % i == 0) return false;
    }

    return true;
}
```

---

### 4. Perfect Square Check
```cpp
bool isPerfectSquare(int n) {
    for(int i = 1; i * i <= n; i++) {
        if(i * i == n) return true;
    }
    return false;
}
```

---

### 5. Counting Divisors
```cpp
int cnt = 0;

for(int i = 1; i * i <= n; i++) {
    if(n % i == 0) {
        cnt++;
        if(i != n / i) cnt++;
    }
}
```

---

## Block / Jump Pattern

### 6. Iterating in √n Blocks
```cpp
int block = sqrt(n);

for(int i = 0; i < n; i += block) {
    // process block
}
```

Used in:
- Range queries
- Square root decomposition

---

## Tricky Cases

### Case 1: Condition `i * i <= n`
```cpp
for(int i = 1; i * i <= n; i++) {}
```
Not running `n` times — stops at √n

---

### Case 2: Divisor Pairing
```cpp
if(n % i == 0) {
    // i and n/i handled together
}
```
Avoids double work

---

### Case 3: Avoid Floating sqrt in Loop
```cpp
for(int i = 1; i * i <= n; i++) {}
```
Better than:
```cpp
for(int i = 1; i <= sqrt(n); i++) {}
```

---

## Common Mistakes

### Mistake 1: Looping till n
```cpp
for(int i = 1; i <= n; i++) {
    if(n % i == 0)
}
```

---

### Mistake 2: Double Counting Divisors
```cpp
// missing check
if(i != n / i)
```

---

### Mistake 3: Using sqrt inside loop repeatedly
```cpp
for(int i = 1; i <= sqrt(n); i++) {}
```
Avoid recomputing sqrt

---

## Key Observations

- Divisors always come in pairs `(i, n/i)`
- Only need to iterate till √n
- Used when:
  - Factorization
  - Prime checks
  - Divisor-related problems

---

## Recognition Strategy

Check:
1. Are you iterating only up to `i * i <= n`?
2. Are values processed in pairs?
3. Are you reducing search space using math?

If yes → O(√n)

---

## Summary

- Loop up to √n → O(√n)
- Divisor problems → O(√n)
- Prime checking → O(√n)
- Block-based iteration → O(√n)

**Key idea:**  
Reduce `n` work into `√n` by pairing or grouping