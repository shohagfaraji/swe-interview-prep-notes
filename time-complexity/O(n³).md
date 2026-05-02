# O(n³) Time Complexity

## Definition
An algorithm is **O(n³)** when total operations grow proportional to **n × n × n**.

- Usually from **three nested levels of work**
- Often appears in **triplet processing, matrix operations, or repeated full scans**

---

## Core Understanding

Think:
```
For each element → process all pairs
n × n × n → n³
```

Even if loops are not perfectly symmetric, total work can still sum to n³.

---

## Basic Patterns

### 1. Three Nested Loops
```cpp
for(int i = 0; i < n; i++) {
    for(int j = 0; j < n; j++) {
        for(int k = 0; k < n; k++) {
            cout << i << j << k << endl;
        }
    }
}
```

---

### 2. Triplet Iteration
```cpp
for(int i = 0; i < n; i++) {
    for(int j = i + 1; j < n; j++) {
        for(int k = j + 1; k < n; k++) {
            // process (i, j, k)
        }
    }
}
```

---

## ⚠️ Important Case: Inner Loop Inside Condition

### Case 1: Condition Always True
```cpp
for(int i = 0; i < n; i++) {
    for(int j = 0; j < n; j++) {
        if(true) {
            for(int k = 0; k < n; k++) {
                // work
            }
        }
    }
}
```

👉 Inner loop runs **every time**  
👉 Total = n × n × n → **O(n³)**

---

### Case 2: Condition Depends on Data (Worst Case Matters)
```cpp
for(int i = 0; i < n; i++) {
    for(int j = 0; j < n; j++) {
        if(arr[j] > 0) {
            for(int k = 0; k < n; k++) {
                // work
            }
        }
    }
}
```

👉 If condition is true often (worst case: always true)  
👉 Still **O(n³)**

---

### Case 3: Condition Rare (Important Insight)
```cpp
for(int i = 0; i < n; i++) {
    for(int j = 0; j < n; j++) {
        if(j == 0) {
            for(int k = 0; k < n; k++) {
                // work
            }
        }
    }
}
```

👉 Inner loop runs only once per `i`  
👉 Total = n × n → **O(n²)**

---

## 🔥 Key Rule (Very Important)

- If inner loop runs **frequently (proportional to n² times)** → O(n³)
- If inner loop runs **only limited times overall** → lower complexity

👉 Always analyze **total executions**, not structure

---

## Common Problem Patterns

### 3. Brute Force 3-Sum
```cpp
for(int i = 0; i < n; i++) {
    for(int j = 0; j < n; j++) {
        for(int k = 0; k < n; k++) {
            if(arr[i] + arr[j] + arr[k] == target) {
                // found
            }
        }
    }
}
```

---

### 4. Matrix Multiplication
```cpp
for(int i = 0; i < n; i++) {
    for(int j = 0; j < n; j++) {
        for(int k = 0; k < n; k++) {
            result[i][j] += A[i][k] * B[k][j];
        }
    }
}
```

---

### 5. Floyd–Warshall
```cpp
for(int k = 0; k < n; k++) {
    for(int i = 0; i < n; i++) {
        for(int j = 0; j < n; j++) {
            dist[i][j] = min(dist[i][j], dist[i][k] + dist[k][j]);
        }
    }
}
```

---

## Tricky Cases

### Case 4: Dependent Bounds
```cpp
for(int i = 0; i < n; i++) {
    for(int j = i; j < n; j++) {
        for(int k = j; k < n; k++) {
            // work
        }
    }
}
```
Still O(n³)

---

### Case 5: Hidden Third Loop
```cpp
for(int i = 0; i < n; i++) {
    for(int j = 0; j < n; j++) {
        someFunction(); // if O(n), total becomes O(n³)
    }
}
```

---

## Common Mistakes

### Mistake 1: Ignoring Condition Frequency
- `if` does NOT reduce complexity automatically

---

### Mistake 2: Looking Only at Structure
- Need to count total executions

---

### Mistake 3: Assuming Reduced Bounds Change Order
- Triangular loops still cubic if nested 3 times

---

## Recognition Strategy

Check:
1. Are there 3 levels of work?
2. Does inner work run many times (not rare)?
3. Does each element interact with pairs?

If yes → **O(n³)**

---

## Summary

- Triple nested loops → O(n³)
- Inner loop inside condition:
  - runs often → O(n³)
  - runs rarely → smaller complexity
- Always analyze **worst-case total executions**

**Key idea:**  
Count how many times the innermost work actually runs