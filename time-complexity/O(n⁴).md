# Conditional Nested Loops (O(n⁴) and Variations)

## Core Rule

- `if` itself is **O(1)**
- Complexity depends on:
  👉 **How many times the inner loop actually executes**

---

## Case 1: Condition Always True → O(n⁴)

```cpp
for(int i = 0; i < n; i++) {
    for(int j = 0; j < n; j++) {
        for(int k = 0; k < n; k++) {
            if(true) {
                for(int l = 0; l < n; l++) {
                    // work
                }
            }
        }
    }
}
```

👉 Inner loop runs every time  
👉 Total = n × n × n × n → **O(n⁴)**

---

## Case 2: Condition Depends on Data (Worst Case) → O(n⁴)

```cpp
for(int i = 0; i < n; i++) {
    for(int j = 0; j < n; j++) {
        for(int k = 0; k < n; k++) {
            if(arr[k] > 0) {
                for(int l = 0; l < n; l++) {
                    // work
                }
            }
        }
    }
}
```

👉 If condition is often true → behaves like always true  
👉 Worst case = **O(n⁴)**

---

## Case 3: Condition Depends on Loop Variable (Rare Execution)

```cpp
for(int i = 0; i < n; i++) {
    for(int j = 0; j < n; j++) {
        for(int k = 0; k < n; k++) {
            if(k == 0) {
                for(int l = 0; l < n; l++) {
                    // work
                }
            }
        }
    }
}
```

👉 Inner loop runs only once per (i, j)  
👉 Total = n × n × n → **O(n³)**

---

## Case 4: Very Rare Condition (Constant Times Total)

```cpp
for(int i = 0; i < n; i++) {
    for(int j = 0; j < n; j++) {
        for(int k = 0; k < n; k++) {
            if(i == 0 && j == 0 && k == 0) {
                for(int l = 0; l < n; l++) {
                    // work
                }
            }
        }
    }
}
```

👉 Inner loop runs only once overall  
👉 Total = n³ + n → **O(n³)**

---

## Case 5: Condition Reduces Loop Size (Dynamic Bound)

```cpp
for(int i = 0; i < n; i++) {
    for(int j = 0; j < n; j++) {
        for(int k = 0; k < n; k++) {
            if(k < 5) {
                for(int l = 0; l < n; l++) {
                    // work
                }
            }
        }
    }
}
```

👉 Inner loop runs constant times per (i, j)  
👉 Total = n² × n → **O(n³)**

---

## Case 6: Condition Inside Inner Loop (No Reduction)

```cpp
for(int i = 0; i < n; i++) {
    for(int j = 0; j < n; j++) {
        for(int k = 0; k < n; k++) {
            for(int l = 0; l < n; l++) {
                if(l % 2 == 0) {
                    // work
                }
            }
        }
    }
}
```

👉 Inner loop still runs n times  
👉 Condition only filters work  
👉 Total = **O(n⁴)**

---

## Case 7: Condition with Break (Important)

```cpp
for(int i = 0; i < n; i++) {
    for(int j = 0; j < n; j++) {
        for(int k = 0; k < n; k++) {
            for(int l = 0; l < n; l++) {
                if(l == 0) break;
            }
        }
    }
}
```

👉 Inner loop stops early  
👉 Runs constant time  
👉 Total = n³ → **O(n³)**

---

## Case 8: Condition Skips Most Iterations

```cpp
for(int i = 0; i < n; i++) {
    for(int j = 0; j < n; j++) {
        for(int k = 0; k < n; k++) {
            if(k % n != 0) continue;

            for(int l = 0; l < n; l++) {
                // work
            }
        }
    }
}
```

👉 Inner loop runs only when k = 0  
👉 Total = n³ → **O(n³)**

---

# Deep Nested Loops with Conditions

## Structure

```cpp
for(i = 0; i < n; i++) {
    if(cond1) {
        for(j = 0; j < n; j++) {
            if(cond2) {
                for(k = 0; k < n; k++) {
                    if(cond3) {
                        for(l = 0; l < n; l++) {
                            // work
                        }
                    }
                }
            }
        }
    }
}
```

---

## 🔥 Core Rule

> Complexity = total number of times the **innermost loop runs**

---

## Case 1: All Conditions Always True

```cpp
if(true)
```

👉 All loops execute fully

```
n × n × n × n → O(n⁴)
```

---

## Case 2: Conditions Often True (Worst Case)

```cpp
if(arr[i] > 0)
```

👉 If true for most iterations → behaves like always true

👉 **O(n⁴)**

---

## Case 3: Each Condition Restricts One Level

```cpp
if(i == 0)
if(j == 0)
if(k == 0)
```

👉 Execution becomes:

- i loop runs n times
- j loop runs only once per i
- k loop runs only once per j
- l loop runs only once per k

👉 Total:

```
n × 1 × 1 × n → O(n²)
```

---

## Case 4: Conditions Reduce Gradually

```cpp
if(i < 10)
if(j < 10)
if(k < 10)
```

👉 Each level runs constant times

👉 Total:

```
n × constant × constant × n → O(n²)
```

---

## Case 5: Only Last Condition Rare

```cpp
if(cond1)   // often true
if(cond2)   // often true
if(cond3)   // rarely true
```

👉 First 3 loops behave like full loops  
👉 Last loop runs few times

👉 Total:

```
n × n × n × few → O(n³)
```

---

## Case 6: Conditions Independent (Worst Case Wins)

```cpp
if(random_condition)
```

👉 Cannot guarantee reduction  
👉 Worst case → all true

👉 Always consider:

```
O(n⁴)
```

---

## Case 7: Break / Continue Effect

```cpp
for(l = 0; l < n; l++) {
    if(l == 0) break;
}
```

👉 Innermost loop runs constant time

👉 Reduces one level

👉 Example result:
```
O(n³)
```

---

## 🧠 General Formula

Let:
- Outer loops = n × n × n × n
- Each condition allows execution `f1, f2, f3` fraction of times

Then:

```
Total ≈ n × (f1·n) × (f2·n) × (f3·n)
```

---

## 🔥 Mental Shortcut

Ask:

1. Does this `if` run inner loop most of the time?
   → YES → ignore it (does not reduce complexity)

2. Does it run rarely?
   → YES → reduces one level

3. Does it run constant times?
   → reduces one dimension

---

## 📊 Summary Table

| Condition Behavior        | Result Complexity |
|--------------------------|------------------|
| Always true              | O(n⁴)            |
| Often true               | O(n⁴)            |
| Rare at one level        | O(n³)            |
| Rare at two levels       | O(n²)            |
| Constant overall         | O(n³)            |
| Break early              | reduces level    |

---

## Final Insight

- `if` does not change complexity by itself  
- Only **limits execution count** can reduce complexity  
- Always count **how many times deepest loop actually runs**

**Key idea:**  
Ignore structure → count real executions