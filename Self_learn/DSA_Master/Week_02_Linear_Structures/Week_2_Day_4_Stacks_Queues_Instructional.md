# Week 2, Day 4: Stacks & Queues

## 🗓 Metadata
**Week:** 2 | **Day:** 4 of 5 | **Topic:** Stacks & Queues  
**Category:** Linear Structures | **Difficulty:** 🟡 Medium  
**Prerequisites:** Week 2 Days 1-3 | **Time:** 90-120 minutes

---

## 1️⃣ THE WHY — Engineering Motivation

**Real-World Problem:**
Browser uses Ctrl+Z to undo. Each action pushed onto stack. Latest action popped for undo. Perfect LIFO (Last-In-First-Out) semantics.

Similarly, print jobs queue up. First job submitted prints first (FIFO: First-In-First-Out).

**Design Problems Solved:**
- LIFO ordering for undo/redo, recursion
- FIFO ordering for task scheduling, breadth-first search
- O(1) push/pop, enqueue/dequeue operations
- Abstract data type separating interface from implementation

---

## 2️⃣ THE WHAT — Mental Model & Intuition

**Stack Analogy:**
Stack of dinner plates. Add to top (push). Remove from top (pop). Last plate added is first removed.

```
        ┌─────┐
        │ P3  │ (top)
        ├─────┤
        │ P2  │
        ├─────┤
        │ P1  │ (bottom)
        └─────┘
```

**Queue Analogy:**
Checkout line. Customers join at back (enqueue). Serve from front (dequeue). First to arrive is first served.

```
Front → [C1] → [C2] → [C3] → ← Back
        (serve)              (join)
```

---

## 3️⃣ THE HOW — Mechanical Walkthrough

**Stack (using array):**
```
struct Stack {
    int* buffer;
    int top;        // index of top element
    int capacity;
};

Push(x):
    if (top == capacity) grow()
    buffer[++top] = x
    
Pop():
    if (top < 0) error
    return buffer[top--]
    
Cost: O(1)
```

**Queue (using circular buffer):**
```
struct Queue {
    int* buffer;
    int front, rear;
    int capacity;
};

Enqueue(x):
    if (size == capacity) grow()
    buffer[rear] = x
    rear = (rear + 1) % capacity
    
Dequeue():
    if (front == rear) error
    x = buffer[front]
    front = (front + 1) % capacity
    return x
    
Cost: O(1)
```

---

## 4️⃣ VISUALIZATION — Simulation & Examples

**Stack Example: Undo operations**

```
User actions: type 'a', type 'b', type 'c', hit undo

Stack:
    After 'a': [a]
    After 'b': [a, b]
    After 'c': [a, b, c]
    
    Undo (pop): [a, b]
    State: "ab"
```

**Queue Example: Print jobs**

```
Jobs submitted: job1, job2, job3

Queue (front=0, rear=3):
    buffer: [job1, job2, job3, null]
    Process job1 (front=1): [empty, job2, job3, null]
    Process job2 (front=2): [empty, empty, job3, null]
    Process job3 (front=3): [empty, empty, empty, null]
```

---

## 5️⃣ CRITICAL ANALYSIS — Performance & Robustness

| Operation | Time | Space | Notes |
|-----------|------|-------|-------|
| **Stack push** | O(1) | O(n) | Amortized with exponential growth |
| **Stack pop** | O(1) | — | Just decrement pointer |
| **Queue enqueue** | O(1) amortized | O(n) | Circular buffer avoids shifting |
| **Queue dequeue** | O(1) | — | Just increment front pointer |

**Key Insight:** Both can be O(1) per operation using proper implementation (array with pointers, not shifting).

---

## 6️⃣ REAL SYSTEM INTEGRATION

**Operating System:**
- CPU call stack: function calls push return address, pop on return
- Process ready queue: scheduler dequeues process to run

**Browsers:**
- History stack: push page when navigating, pop on back button
- DOM parsing: stack for tracking open tags

---

## 7️⃣ CONCEPT CROSSOVERS

**Stack Applications:** Recursion, DFS, undo/redo, expression parsing  
**Queue Applications:** BFS, scheduling, asynchronous tasks  

---

## 8️⃣ MATHEMATICAL & THEORETICAL PERSPECTIVE

**Stack with n operations:**
- Each push: O(1) amortized
- Total: O(n)

**Proof:** Same as dynamic array. Resizes happen O(log n) times.

---

## 9️⃣ ALGORITHMIC DESIGN INTUITION

**Use stack when:** LIFO access matters (undo, recursion, parentheses matching)

**Use queue when:** FIFO access matters (scheduling, BFS, fair ordering)

---

## 🔟 KNOWLEDGE CHECK — Socratic Reasoning

**Q1:** Function calls use a call stack. When you call func1, which calls func2, which calls func3, where's return address stored?

**Q2:** Why does a circular buffer (queue) need modulo arithmetic? What would happen without it?

**Q3:** Can you implement a queue using two stacks? How?

**Q4:** If a stack uses exponential growth, what's the maximum pause time for n operations?

---

## 1️⃣1️⃣ RETENTION HOOK — Memory Anchors

**Stack:** LIFO (Last-In-First-Out), like a spring-loaded stack of plates  
**Queue:** FIFO (First-In-First-Out), like a checkout line  
**Both:** O(1) push/pop/enqueue/dequeue

