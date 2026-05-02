# O(n⁵) Time Complexity

## Definition

An algorithm is **O(n⁵)** when total operations grow proportional to:

```
n × n × n × n × n → n⁵
```

- Typically from **five levels of work**
- Rare in practice, mostly appears in **brute force / theoretical cases**

---

## Core Understanding

Think:

- “For each element → process all quadruples”

```
n elements × n⁴ work → n⁵
```

---

## Basic Patterns

### 1. Five Nested Loops

```cpp
for(int a = 0; a < n; a++) {
    for(int b = 0; b < n; b++) {
        for(int c = 0; c < n; c++) {
            for(int d = 0; d < n; d++) {
                for(int e = 0; e < n; e++) {
                    // work
                }
            }
        }
    }
}
```

---

### 2. 5-Element Combinations

```cpp
for(int a = 0; a < n; a++) {
    for(int b = a + 1; b < n; b++) {
        for(int c = b + 1; c < n; c++) {
            for(int d = c + 1; d < n; d++) {
                for(int e = d + 1; e < n; e++) {
                    // process (a, b, c, d, e)
                }
            }
        }
    }
}
```

---

## ⚠️ Conditional Nested Cases (Important)

### Case 1: All Conditions Always True

```cpp
for(int a = 0; a < n; a++) {
    if(true) {
        for(int b = 0; b < n; b++) {
            if(true) {
                for(int c = 0; c < n; c++) {
                    if(true) {
                        for(int d = 0; d < n; d++) {
                            if(true) {
                                for(int e = 0; e < n; e++) {
                                    // work
                                }
                            }
                        }
                    }
                }
            }
        }
    }
}
```

👉 All loops fully execute  
👉 **O(n⁵)**

---

### Case 2: Conditions Often True (Worst Case)

```cpp
if(arr[a] > 0)
```

👉 Worst case behaves like always true  
👉 **O(n⁵)**

---

### Case 3: Each Condition Restricts One Level

```cpp
if(a == 0)
if(b == 0)
if(c == 0)
if(d == 0)
```

👉 Execution:

```
n × 1 × 1 × 1 × n → O(n²)
```

---

### Case 4: One Rare Condition

```cpp
if(a == 0)
```

👉 Only first loop restricted  
👉 Total:

```
1 × n × n × n × n → O(n⁴)
```

---

### Case 5: Deep Rare Condition

```cpp
if(d == 0)
```

👉 Only deepest levels reduced  
👉 Total:

```
n × n × n × 1 × n → O(n⁴)
```

---

### Case 6: Constant Range Conditions

```cpp
if(a < 10)
if(b < 10)
```

👉 Constants don’t scale with n  
👉 Total:

```
n × constant × constant × n × n → O(n³)
```

---

### Case 7: Break Reduces One Level

```cpp
for(int e = 0; e < n; e++) {
    if(e == 0) break;
}
```

👉 Innermost loop becomes constant  
👉 Reduces one dimension

---

## 🔥 Key Rule

- If deepest loop runs ≈ n⁴ times → O(n⁵)
- If reduced → lower complexity

👉 Always count:
**how many times innermost loop executes**

---

## Hidden O(n⁵) Case

### Function inside 4 loops

```cpp
for(int a = 0; a < n; a++) {
    for(int b = 0; b < n; b++) {
        for(int c = 0; c < n; c++) {
            for(int d = 0; d < n; d++) {
                processArray(); // O(n)
            }
        }
    }
}
```

👉 Hidden 5th factor → **O(n⁵)**

---

## Recognition Strategy

Check:

1. Are there 5 levels of work?
2. Does inner work run frequently?
3. Any hidden loop/function inside?

---

## Quick Table

| Innermost Runs | Complexity      |
| -------------- | --------------- |
| ~ n⁴ times     | O(n⁵)           |
| ~ n³ times     | O(n⁴)           |
| ~ n² times     | O(n³)           |
| ~ n times      | O(n²)           |
| constant       | outer dominates |

---

## Summary

- Five nested loops → O(n⁵)
- Condition:
    - always / often true → O(n⁵)
    - rare → reduces level
- Hidden loop inside function → O(n⁵)

**Key idea:**  
Count real executions of deepest operation
