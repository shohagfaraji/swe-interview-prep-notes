# Stack (LIFO - Last In First Out)

## 🔹 What is a Stack?

- Linear data structure
- Follows **LIFO (Last In First Out)**
- Insertion & deletion happen from **TOP only**

Example:
Push: 1 → 2 → 3  
Pop: removes 3 first

---

## 🔹 Time & Space Complexity

| Operation | Time Complexity | Notes         |
| --------- | --------------- | ------------- |
| push      | O(1)            | Insert at top |
| pop       | O(1)            | Remove top    |
| top       | O(1)            | Access top    |
| empty     | O(1)            | Check empty   |

Space Complexity: O(n)

---

## 🔹 STL Stack (C++)

```cpp
#include <stack>
using namespace std;

stack<int> st;

st.push(10);
st.push(20);
st.pop();

cout << st.top(); // 10
```

⚠️ Interview Tip:

- STL stack is **restricted** (no iteration)
- Internally uses **deque by default**

---

## 🔹 Implementation Using Vector (RECOMMENDED)

### Why Vector?

- Dynamic size (no overflow)
- Cleaner implementation
- Same performance

---

### Stack Class (Vector Based)

```cpp
#include <bits/stdc++.h>
using namespace std;

class Stack {
private:
    vector<int> v;

public:
    // Push
    void push(int x) {
        v.push_back(x);
    }
    // Time: O(1) amortized
    // Space: O(1)

    // Pop
    void pop() {
        if (v.empty()) {
            cout << "Stack Underflow\n";
            return;
        }
        v.pop_back();
    }
    // Time: O(1)
    // Space: O(1)

    // Top
    int top() {
        if (v.empty()) {
            cout << "Stack is empty\n";
            return -1;
        }
        return v.back();
    }
    // Time: O(1)

    // isEmpty
    bool empty() {
        return v.empty();
    }
    // Time: O(1)

    // Size
    int size() {
        return v.size();
    }
    // Time: O(1)
};
```

---

## 🔹 Implementation Using Array

### When to Use?

- Fixed size known
- Low-level systems

---

### Stack Class (Array Based)

```cpp
#include <bits/stdc++.h>
using namespace std;

class Stack {
private:
    int topIndex;
    int arr[1000]; // fixed size

public:
    Stack() {
        topIndex = -1;
    }

    // Push
    void push(int x) {
        if (topIndex == 999) {
            cout << "Stack Overflow\n";
            return;
        }
        arr[++topIndex] = x;
    }
    // Time: O(1)

    // Pop
    void pop() {
        if (topIndex == -1) {
            cout << "Stack Underflow\n";
            return;
        }
        topIndex--;
    }
    // Time: O(1)

    // Top
    int top() {
        if (topIndex == -1) {
            cout << "Empty Stack\n";
            return -1;
        }
        return arr[topIndex];
    }
    // Time: O(1)

    // Empty
    bool empty() {
        return topIndex == -1;
    }

    // Size
    int size() {
        return topIndex + 1;
    }
};
```

---

## 🔹 Vector vs Array Stack

| Feature       | Vector Stack   | Array Stack |
| ------------- | -------------- | ----------- |
| Size          | Dynamic        | Fixed       |
| Overflow      | ❌             | ✅          |
| Ease of use   | Easy           | Medium      |
| Interview Use | ⭐ Recommended | For basics  |

---

## 🔹 Common Interview Patterns

### 1. Balanced Parentheses

```cpp
bool isValid(string s) {
    stack<char> st;

    for(char c : s) {
        if(c == '(' || c == '{' || c == '[')
            st.push(c);
        else {
            if(st.empty()) return false;

            char t = st.top();
            st.pop();

            if((c == ')' && t != '(') ||
               (c == '}' && t != '{') ||
               (c == ']' && t != '['))
                return false;
        }
    }
    return st.empty();
}
```

Time: O(n)  
Space: O(n)

---

### 2. Next Greater Element

```cpp
vector<int> nge(vector<int>& arr) {
    int n = arr.size();
    vector<int> res(n, -1);
    stack<int> st;

    for(int i = n-1; i >= 0; i--) {
        while(!st.empty() && st.top() <= arr[i])
            st.pop();

        if(!st.empty())
            res[i] = st.top();

        st.push(arr[i]);
    }
    return res;
}
```

Time: O(n)  
Space: O(n)

---

### 3. Monotonic Stack Pattern

- Increasing stack
- Decreasing stack

Used in:

- Histogram problems
- Stock span
- Sliding window max

---

## 🔹 Important Edge Cases

- Pop from empty stack
- Top on empty stack
- Overflow (array implementation)
- Large input → recursion stack overflow (if used)

---

## 🔹 Common Mistakes

❌ Forgetting empty check before pop/top  
❌ Using stack when queue needed  
❌ Not understanding LIFO properly  
❌ Using recursion without thinking about stack limits

---

## 🔹 When to Use Stack?

✅ Undo/Redo operations  
✅ Expression evaluation  
✅ DFS (recursive/iterative)  
✅ Parentheses problems  
✅ Monotonic problems

---

## 🔹 Common Interview Questions

- Implement stack using queue
- Implement min stack
- Valid parentheses
- Next greater/smaller element
- Largest rectangle in histogram

---

## 🔹 Pro Tips (High Value)

🔥 Use vector for custom stack (clean + safe)  
🔥 Learn monotonic stack (VERY IMPORTANT)  
🔥 Always check empty before pop/top

---

## 🔹 Quick Summary

- Stack = LIFO
- push/pop/top → O(1)
- Vector-based implementation preferred
- Used in many important problems
