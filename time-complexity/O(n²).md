# O(n²) Time Complexity

## Definition
An algorithm is **O(n²)** when:
- Each element is processed with **every other element**
- There are **nested loops over the same input size**

👉 Total operations grow quadratically with `n`

---

## Core Understanding

Think:
- “For every element, I scan the entire array again”

Common pattern:
```
n elements × n work each → n²
```

---

## Basic Patterns

### 1. Full Nested Loop
```cpp
for(int i = 0; i < n; i++) {
    for(int j = 0; j < n; j++) {
        cout << i << " " << j << endl;
    }
}
```

---

### 2. Pairwise Comparison
```cpp
for(int i = 0; i < n; i++) {
    for(int j = i + 1; j < n; j++) {
        cout << arr[i] << " " << arr[j] << endl;
    }
}
```

---

### 3. Check All Pairs (Brute Force)
```cpp
for(int i = 0; i < n; i++) {
    for(int j = 0; j < n; j++) {
        if(i != j) {
            // compare
        }
    }
}
```

---

## Common Problem Patterns

### 4. Finding Duplicate Elements
```cpp
for(int i = 0; i < n; i++) {
    for(int j = i + 1; j < n; j++) {
        if(arr[i] == arr[j]) {
            cout << "Duplicate";
        }
    }
}
```

---

### 5. Bubble Sort
```cpp
for(int i = 0; i < n; i++) {
    for(int j = 0; j < n - i - 1; j++) {
        if(arr[j] > arr[j + 1]) {
            swap(arr[j], arr[j + 1]);
        }
    }
}
```

---

### 6. Selection Sort
```cpp
for(int i = 0; i < n; i++) {
    int minIdx = i;

    for(int j = i + 1; j < n; j++) {
        if(arr[j] < arr[minIdx]) {
            minIdx = j;
        }
    }

    swap(arr[i], arr[minIdx]);
}
```

---

### 7. Insertion Sort
```cpp
for(int i = 1; i < n; i++) {
    int key = arr[i];
    int j = i - 1;

    while(j >= 0 && arr[j] > key) {
        arr[j + 1] = arr[j];
        j--;
    }

    arr[j + 1] = key;
}
```

---

## Matrix / Grid Patterns

### 8. 2D Grid Traversal
```cpp
for(int i = 0; i < n; i++) {
    for(int j = 0; j < n; j++) {
        cout << grid[i][j];
    }
}
```

---

### 9. Counting Submatrices (Brute Force)
```cpp
for(int i = 0; i < n; i++) {
    for(int j = 0; j < n; j++) {
        // process submatrix
    }
}
```

---

## String Patterns

### 10. Compare All Substrings
```cpp
for(int i = 0; i < n; i++) {
    for(int j = i; j < n; j++) {
        string sub = s.substr(i, j - i + 1);
    }
}
```

---

## Tricky Cases

### Case 1: Dependent Nested Loop
```cpp
for(int i = 0; i < n; i++) {
    for(int j = 0; j < i; j++) {
        cout << i << j;
    }
}
```
👉 Still O(n²) (triangular sum)

---

### Case 2: Reverse Pair Checking
```cpp
for(int i = 0; i < n; i++) {
    for(int j = i; j < n; j++) {
        // work
    }
}
```

---

### Case 3: Hidden Quadratic Work
```cpp
for(int i = 0; i < n; i++) {
    for(int j = 0; j < n; j++) {
        // constant work
    }
}
```

---

## Common Mistakes

### Mistake 1: Thinking triangular loop is smaller
```cpp
for(int i = 0; i < n; i++)
    for(int j = i; j < n; j++)
```
Still O(n²)

---

### Mistake 2: Ignoring nested string operations
```cpp
for(int i = 0; i < n; i++) {
    for(int j = i; j < n; j++) {
        s.substr(i, j);
    }
}
```

---

### Mistake 3: Mixing independent loops incorrectly
Two loops one after another ≠ O(n²)

---

## Key Observations

- Two nested loops over same range → O(n²)
- Even triangular loops → O(n²)
- Pairwise comparisons → O(n²)
- Brute force checking → O(n²)

---

## Recognition Strategy

Check:
1. Is there a loop inside a loop over same input?
2. Are all pairs being checked?
3. Is every element compared with others?

If yes → **O(n²)**

---

## Summary

- Nested loops → O(n²)
- Pair comparisons → O(n²)
- Sorting algorithms (simple ones) → O(n²)
- Grid traversal → O(n²)
- Brute force solutions → O(n²)

**Key idea:**  
Every element interacts with every other element