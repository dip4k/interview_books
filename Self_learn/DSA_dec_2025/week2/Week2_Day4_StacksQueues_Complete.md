# 🧠 DSA Deep-Dive: Week 2, Day 4
## Stacks & Queues: LIFO/FIFO Logic, and Monotonic Stack Intuition

---

## 1. The "Why" (Engineering Motivation)

**Scenario 1: Browser History (Stack)**

You're implementing browser back/forward buttons:
```
Visit pages: Google → Amazon → Netflix → Reddit

History stack:
├─ Google    (oldest - bottom)
├─ Amazon
├─ Netflix
└─ Reddit    (newest - top)

Click BACK:
- Remove Reddit (top)
- Show Netflix

Click BACK again:
- Remove Netflix
- Show Amazon

Click FORWARD:
- Add Netflix (top)
```

**Scenario 2: Printer Queue (Queue)**

Multiple users send print jobs:
```
Print jobs arrive:
User1 job → Printer (starts immediately)

User2 job arrives:
Queue: [User2]

User3 job arrives:
Queue: [User2, User3]

User1 finishes:
Queue: [User3]
User2 now printing

Result: First come, first served (FIFO)
```

**Scenario 3: Stock Market (Monotonic Stack)**

Prices: [2, 1, 2, 4, 3]

**Question:** For each price, find the next **greater** price to the right.

```
Price 2: Next greater is 4 (index 3)
Price 1: Next greater is 2 (index 2)
Price 2: Next greater is 4 (index 3)
Price 4: Next greater is NONE
Price 3: Next greater is NONE

Naive solution: O(n²) - for each element, scan right
Smart solution: Use monotonic stack - O(n)
```

**The insight:** Stacks and queues aren't just simple structures. They're the foundation of solving many problems efficiently.

---

## 2. The Mental Model (The "What")

### Stack: Pancake Stack

```
├─ Pancake 1  ← Only access from top!
├─ Pancake 2
├─ Pancake 3
├─ Pancake 4
└─ Pancake 5

Push: Add pancake on top
Pop: Remove pancake from top
Peek: Look at top without removing

Can't access Pancake 3 without removing Pancakes 1 and 2 first!
LIFO: Last In, First Out
```

### Queue: Bank Line

```
Front → [Person1] → [Person2] → [Person3] → [Person4] ← Back

Enqueue: Person5 arrives, joins back of line
Dequeue: Person1 is served, leaves front

FIFO: First In, First Out
Fair! Nobody cuts in.
```

---

## 3. Under the Hood (The "How")

### 3.1 Stack Implementation (Using Array)

```python
class Stack:
    def __init__(self):
        self.items = []  # Dynamic array
        self.top = -1    # Points to top element
    
    def push(value):
        # Append to end of array
        self.items.append(value)
        self.top += 1
        # Time: O(1) amortized
    
    def pop():
        # Remove from end of array
        if self.top >= 0:
            value = self.items[self.top]
            self.items.pop()
            self.top -= 1
            return value
        # Time: O(1)
    
    def peek():
        # Look at top without removing
        return self.items[self.top]
        # Time: O(1)
```

**Memory layout:**

```
Array: [1, 2, 3, 4, 5, ?, ?, ?]
Index:  0  1  2  3  4  5  6  7
Top pointer: 4 (points to value 5)

Push 6:
Array: [1, 2, 3, 4, 5, 6, ?, ?]
Top pointer: 5

Pop:
Array: [1, 2, 3, 4, 5, ?, ?, ?]
Top pointer: 4 (back to 5)
```

### 3.2 Queue Implementation (Using Array with Circular Buffer)

**Naive approach (WRONG):**

```
Enqueue: Add to end
Dequeue: Remove from front

Array: [1, 2, 3, 4, 5]
Front→ 0  1  2  3  4 ←Back

Dequeue 1, 2:
Array: [?, ?, 3, 4, 5]
       0  1  2  3  4
       
Now indices 0-1 are wasted!
```

**Better approach: Circular buffer**

```
Use modulo arithmetic to reuse space:

Initial:
Array: [?, ?, ?, ?, ?]
Front: 0
Back: -1 (empty)

Enqueue 1, 2, 3:
Array: [1, 2, 3, ?, ?]
Front: 0
Back: 2

Enqueue 4, 5:
Array: [1, 2, 3, 4, 5]
Front: 0
Back: 4

Dequeue 1, 2:
Array: [?, ?, 3, 4, 5]
Front: 2 (moved forward)
Back: 4

Enqueue 6 (wrap around):
next_back = (4 + 1) % 5 = 0
Array: [6, 2, 3, 4, 5]
Front: 2
Back: 0

The array is reused! No wasted space.
```

### 3.3 Monotonic Stack: The Key Insight

**Problem:** Find next greater element to the right for each element.

```
Array: [2, 1, 2, 4, 3]

Result:
- 2: next greater is 4
- 1: next greater is 2
- 2: next greater is 4
- 4: none
- 3: none
```

**Naive O(n²):**

```
for each i:
    for j = i+1 to end:
        if arr[j] > arr[i]:
            result[i] = j
            break

Time: O(n²)
```

**Smart O(n) using monotonic stack:**

```
Idea: Maintain a stack of indices in DECREASING order of values

Step 1: Process 2
Stack: [2]
2 has no greater to its right yet

Step 2: Process 1
1 < 2, so 2 hasn't found its greater yet
Stack: [2, 1]
Keep 2 waiting

Step 3: Process 2
2 > 1, so 1's greater is 2!
Pop 1, result[1] = 2
2 = 2, so not greater
Stack: [2, 2]

Step 4: Process 4
4 > 2, so both 2's greater is 4!
Pop 2, result[2] = 4
Pop 2, result[0] = 4
Stack: [4]

Step 5: Process 3
3 < 4, so 4 hasn't found its greater yet
Stack: [4, 3]

Done:
Result: [4, 2, 4, none, none]
Time: O(n) - each element pushed and popped once!
```

---

## 4. Visual Walkthrough: Stack Operations

**Scenario:** Evaluate expression using stack: Push 5, Push 3, Add, Push 2, Multiply

### Step 1: Push 5
```
Stack: [5]
Top: 5

Visualization:
┌───┐
│ 5 │ ← Top
└───┘
```

### Step 2: Push 3
```
Stack: [5, 3]
Top: 3

Visualization:
┌───┐
│ 3 │ ← Top
├───┤
│ 5 │
└───┘
```

### Step 3: Add (Pop 3, Pop 5, Push 8)
```
Pop: 3
Stack: [5]

Pop: 5
Stack: []

Push: 3 + 5 = 8
Stack: [8]

Visualization:
┌───┐
│ 8 │ ← Top
└───┘
```

### Step 4: Push 2
```
Stack: [8, 2]
Top: 2

Visualization:
┌───┐
│ 2 │ ← Top
├───┤
│ 8 │
└───┘
```

### Step 5: Multiply (Pop 2, Pop 8, Push 16)
```
Pop: 2
Stack: [8]

Pop: 8
Stack: []

Push: 8 * 2 = 16
Stack: [16]

Final result: 16
```

---

## 5. Critical Analysis

### 5.1 Time Complexity

| Operation | Stack | Queue |
|-----------|-------|-------|
| Push/Enqueue | O(1) | O(1) |
| Pop/Dequeue | O(1) | O(1) |
| Peek | O(1) | O(1) |
| Search | O(n) | O(n) |
| Access at position | O(n) | O(n) |

### 5.2 Space Complexity

**Stack (size n):**
```
Space = n × element_size + O(1) overhead
Example: 1000 integers = 4000 bytes
Overhead: Just the top pointer
```

**Queue (size n):**
```
Space = n × element_size + O(1) overhead
Example: 1000 integers = 4000 bytes
Overhead: Front and back pointers
```

**Both are efficient! The magic is in the restricted operations (LIFO/FIFO).**

### 5.3 Edge Cases

**1. Empty stack operations**
```
Stack: []

Pop: Error! Stack underflow
Peek: Error! Stack empty
Push x: OK, creates first element
```

**2. Stack overflow (from Week 1)**
```
Recursive function uses call stack
Each function call = push to stack
Recursion depth > 349,525:
Stack overflow! Program crashes.
```

**3. Queue with capacity limit**
```
Queue: [1, 2, 3, 4, 5] (capacity 5)

Enqueue 6: Error! Queue full
Wait or reject?
```

**4. Circular queue wrap-around**
```
Front = 4, Back = 1
Array: [6, 7, 3, 4, 5]
        ↑  ↑  ↑  ↑  ↑
        B  F        (positions)

Is queue full or empty?
Need to check: (Back + 1) % capacity == Front
```

---

## 6. System Connection

### Call Stack (Week 1 Revisited)

```c
void function_A() {
    function_B();  // Push function_B to call stack
}

void function_B() {
    function_C();  // Push function_C to call stack
}

void function_C() {
    // Top of call stack
}

// Return: Pop function_C
// Return: Pop function_B
// Return: Pop function_A
```

**This is a stack!** LIFO exactly.

### BFS (Breadth-First Search) Uses Queues

```
Queue: [start_node]

While queue not empty:
  node = dequeue()
  visit(node)
  for each neighbor:
    if not visited:
      enqueue(neighbor)

Result: Visit nodes level-by-level (breadth first)
```

### Browser Back Button (Real Stack Implementation)

```javascript
history = new Stack()

function navigate(url) {
    history.push(url)
    display(url)
}

function back() {
    history.pop()  // Current page
    prev_url = history.peek()  // Previous page
    display(prev_url)
}
```

---

## 7. Knowledge Check

**Question 1: Monotonic Stack**

Prices: [3, 1, 4, 1, 5]

Find next greater for each:
```
3: ___
1: ___
4: ___
1: ___
5: ___
```

Solve step-by-step using monotonic stack.

---

**Question 2: Stack vs Queue**

You have 10 print jobs queued. Should they be processed as a:
A) Stack
B) Queue

Explain why.

---

**Question 3: Circular Queue**

Capacity 5, currently: Front=2, Back=4
Array: [?, 8, 9, 10, 11]

A. Dequeue (pop from front)
B. Enqueue 12
C. What's the state after?

---

## Summary: Day 4 Core Concepts

**Stacks (LIFO):**
- **Push:** O(1) - add to top
- **Pop:** O(1) - remove from top
- **Peek:** O(1) - look at top
- **Use cases:** Function calls, browser history, expression evaluation

**Queues (FIFO):**
- **Enqueue:** O(1) - add to back
- **Dequeue:** O(1) - remove from front
- **Peek:** O(1) - look at front
- **Use cases:** BFS, printer queue, task scheduling

**Monotonic Stack Pattern:**
- Maintain decreasing (or increasing) order
- Solves "next greater/smaller element" in O(n)
- Each element pushed/popped once
- Extremely useful for competitive programming

**When to use:**
- ✅ LIFO semantics needed (stacks)
- ✅ FIFO semantics needed (queues)
- ✅ Need O(1) insertion/deletion
- ✅ Don't need random access

---

**End of Day 4: Stacks & Queues Deep-Dive**
