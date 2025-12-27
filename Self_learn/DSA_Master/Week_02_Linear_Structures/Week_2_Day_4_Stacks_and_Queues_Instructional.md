# Week 2, Day 4: Stacks & Queues

**Week:** 2 | **Day:** 4 | **Topic:** Stacks & Queues  
**Difficulty:** 🟡 Medium  
**Time Investment:** 90-120 minutes  
**Prerequisites:** Week 2, Days 1-3 (Arrays, Dynamic Arrays, Linked Lists)

---

## 1️⃣ THE WHY — Engineering Motivation

### Real-World Problems

Many systems need to process items in a specific order:
- **Browser back button:** Last page visited first (LIFO = Stack)
- **Printer queue:** First job submitted first (FIFO = Queue)
- **Function call stack:** Last called first returns (LIFO = Stack)
- **Message queue:** Messages processed in order (FIFO = Queue)

Abstract data structures that enforce ordering.

### Real System Usage

- **Call Stack:** CPU hardware feature (function calls)
- **Undo/Redo:** Stack of previous states
- **DFS (Depth-First Search):** Uses stack
- **BFS (Breadth-First Search):** Uses queue
- **OS Job Scheduler:** Queue of ready processes
- **Network Routers:** Queues for packet transmission

### Why This Topic Exists

**Without understanding stacks/queues:**
- Can't implement many algorithms (DFS, BFS, etc.)
- Can't build interactive features (undo, browser history)
- Don't understand call stack behavior

**With mastery:**
- Design problem-solving algorithms
- Implement system features efficiently
- Understand execution model

---

## 2️⃣ THE WHAT — Mental Model & Intuition

### Core Analogy: Stack of Plates

**Stack (LIFO):**
```
Imagine a stack of dinner plates:
- Push new plate: place on top
- Pop plate: take from top (most recent first)
- Last In, First Out

Real example: Back button
1. Visit page A
2. Visit page B
3. Visit page C
4. Click back: pop C, show B
5. Click back: pop B, show A
```

**Queue (FIFO):**
```
Imagine a line at a coffee shop:
- Enqueue: new customer joins at end
- Dequeue: first customer served and leaves
- First In, First Out

Real example: Printer queue
1. User A prints document 1
2. User B prints document 2
3. User C prints document 3
4. Printer processes: 1, then 2, then 3 (first come, first served)
```

### Key Invariants

**Stack:**
- Insert and remove from SAME end (top)
- Last element added is first removed
- LIFO ordering

**Queue:**
- Insert at ONE end (back), remove from OTHER end (front)
- First element added is first removed
- FIFO ordering

---

## 3️⃣ THE HOW — Mechanical Walkthrough

### Stack Operations

```
Stack: [10, 20, 30] (top at right)

Push 40:
1. Add element to top
2. Stack: [10, 20, 30, 40]
3. Time: O(1)

Pop:
1. Remove top element
2. Return 40
3. Stack: [10, 20, 30]
4. Time: O(1)

Peek:
1. Return top element
2. Don't remove it
3. Stack: [10, 20, 30, 40]
4. Time: O(1)

Implementation: Array with pointer to top
top = 3
stack[3] = 40  ← top of stack
```

### Queue Operations

```
Queue: [10, 20, 30] (front at left, back at right)

Enqueue 40:
1. Add to back
2. Queue: [10, 20, 30, 40]
3. Time: O(1)

Dequeue:
1. Remove from front
2. Return 10
3. Queue: [20, 30, 40]
4. Time: O(1) with ring buffer, O(n) with shift

Front/Peek:
1. Return front element
2. Queue: [20, 30, 40]
3. Time: O(1)

Implementation: Ring buffer (circular array)
front = 0, back = 3
queue[0] = 10  ← front
queue[1] = 20
queue[2] = 30
queue[3] = 40  ← back
```

---

## 4️⃣ VISUALIZATION — Simulation & Examples

### Stack Execution Example

```
Code:
push(10)
push(20)
push(30)
val = pop()  // val = 30
push(40)
val = pop()  // val = 40
val = pop()  // val = 20

Visualization:
push(10):  [10]
push(20):  [10, 20]
push(30):  [10, 20, 30]
pop():     [10, 20], return 30
push(40):  [10, 20, 40]
pop():     [10, 20], return 40
pop():     [10], return 20
```

### Queue Execution Example

```
Code:
enqueue(10)
enqueue(20)
enqueue(30)
val = dequeue()  // val = 10
enqueue(40)
val = dequeue()  // val = 20
val = dequeue()  // val = 30

Visualization:
enqueue(10):  [10]
enqueue(20):  [10, 20]
enqueue(30):  [10, 20, 30]
dequeue():    [20, 30], return 10
enqueue(40):  [20, 30, 40]
dequeue():    [30, 40], return 20
dequeue():    [40], return 30
```

---

## 5️⃣ CRITICAL ANALYSIS — Performance & Robustness

### Complexity Table

| Operation | Stack | Queue | Notes |
|-----------|-------|-------|-------|
| **Push/Enqueue** | O(1) | O(1) | Append to array |
| **Pop/Dequeue** | O(1) | O(1) | Ring buffer or deque |
| **Peek** | O(1) | O(1) | Just check front/top |
| **Size** | O(1) | O(1) | Maintain counter |
| **Is Empty** | O(1) | O(1) | Check size counter |
| **Space** | O(n) | O(n) | For n elements |

### Dequeue Implementation Gotcha

```
Naive array queue:
enqueue: O(1) append
dequeue: O(n) shift everything left!

Ring buffer queue:
- Circular array with front/back pointers
- front++, back++ (modulo capacity)
- Both O(1)
- Space: unused slots in circular region

Dynamic deque:
- Deque (double-ended queue)
- O(1) push/pop at both ends
- Needs careful implementation
```

---

## 6️⃣ REAL SYSTEM INTEGRATION

### CPU Call Stack

```
main() {
    funcA();
}

funcA() {
    funcB();
}

funcB() {
    return;
}

Execution stack:
[main frame]
[main, funcA frame]
[main, funcA, funcB frame]
[main, funcA frame]  (funcB returns)
[main frame]  (funcA returns)
[]  (main returns)

Each function call pushes frame
Each return pops frame
LIFO ordering implemented by CPU
```

### Browser Back Button

```
Visited pages stack:
visit google.com:    [google]
visit github.com:    [google, github]
visit stackoverflow: [google, github, stackoverflow]
click back:          pop stackoverflow → [google, github]
click back:          pop github → [google]

Implementation:
- Stack stores URLs
- Back button = pop
- Forward button = push to separate "forward stack"
```

### OS Process Scheduler

```
Ready queue:
[Process A] → [Process B] → [Process C]

Scheduler runs process A (quantum expires)
- dequeue Process A
- enqueue at back: [Process B] → [Process C] → [Process A]

FIFO round-robin: fair scheduling
```

---

## 7️⃣ CONCEPT CROSSOVERS

### Builds On
- Arrays (Day 1)
- Dynamic Arrays (Day 2)
- Linked Lists (Day 3)

### Builds To
- Depth-First Search (DFS) uses stack
- Breadth-First Search (BFS) uses queue
- Expression evaluation uses stack
- Graph algorithms depend on both

---

## 8️⃣ MATHEMATICAL & THEORETICAL PERSPECTIVE

### Stack Operations Proof

**Theorem:** Stack push/pop are O(1).

**Proof:**
- Push: add element to array[top], top++, O(1)
- Pop: val = array[top], top--, return val, O(1)
✓

### Ring Buffer Math

**Circular array with capacity c:**
```
front = 5, back = 8, capacity = 10

Next position after 8: (8 + 1) % 10 = 9
Next position after 9: (9 + 1) % 10 = 0
Queue wraps around
```

---

## 9️⃣ ALGORITHMIC DESIGN INTUITION

### When to Use Each

**Stack:**
- DFS traversal
- Undo/Redo
- Expression parsing
- Function calls (automatic)
- Balanced parentheses checking

**Queue:**
- BFS traversal
- Job scheduling (FIFO)
- Message passing
- Resource buffering
- Breadth-first problems

---

## 🔟 KNOWLEDGE CHECK — Socratic Reasoning

1. **Why is stack "LIFO" and queue "FIFO"?**
   - Hint: Think about which end you add/remove from.

2. **How can a dequeue be O(1) with a simple array?**
   - Hint: Ring buffer (circular array with pointers).

3. **What problem does stack solve that array doesn't?**
   - Hint: Forced ordering (only access top).

4. **Why does browser history need both stacks (back + forward)?**
   - Hint: Back button pops stack, forward button pushes.

5. **When would you use queue vs stack for graph traversal?**
   - Hint: BFS = queue, DFS = stack.

---

## 1️⃣1️⃣ RETENTION HOOK

**One-Line Essence:**
*"Stacks enforce LIFO (last in, first out), queues enforce FIFO (first in, first out). Both are O(1) push/pop abstractions with specific ordering semantics."*

**Mnemonic:** "LIFO vs FIFO"
- **L**ast **I**n **F**irst **O**ut = Stack
- **F**irst **I**n **F**irst **O**ut = Queue

**5 Cognitive Lenses:**
- 🖥️ **Computational:** Enforced ordering eliminates choice (efficiency + correctness)
- 🧠 **Psychological:** Stacks intuitive (plates), queues intuitive (lines)
- 🔄 **Design:** Different problems need different orderings
- 🤖 **AI/ML:** Stack for parsing neural network definitions, queue for parallelization
- 📚 **Historical:** Stacks tied to function calls (Von Neumann 1945), queues to OS (1960s)

---

## Summary & Next Steps

**Stacks and queues are abstract data structures that enforce specific ordering. Both achieve O(1) operations, but for different use cases. Stack = LIFO, Queue = FIFO.**

**Key Takeaways:**
1. Stack: LIFO, last element added removed first
2. Queue: FIFO, first element added removed first
3. Both: O(1) push/pop with proper implementation
4. Stack: Array implementation simple
5. Queue: Ring buffer prevents O(n) dequeue

**Next:** Day 5 (Binary Search) uses sorted arrays.

