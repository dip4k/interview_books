# 🧠 Week 2: Linear Structures - Day 4

# Stacks & Queues: LIFO/FIFO, Memory Layout, Applications

## 🗓 Metadata
**Topic:** Stacks & Queues  
**Week:** Week 2  
**Day:** Day 4 of 5  
**Category:** Linear Structures  
**Difficulty:** 🟡 Medium  
**Status:** 🔍 In Study  
**Last Reviewed:** —  
**Confidence Level (1–5):** —/5  

---

## 1️⃣ The Why — Engineering Motivation

### Real-World Problem

Some computational patterns demand **strict ordering disciplines**:

- **Stacks (LIFO):** Undo/redo systems, function calls, expression evaluation. Most recent action is the first to be undone.
- **Queues (FIFO):** Job scheduling, message systems, breadth-first search. First-in, first-out ensures fairness.

Both are **abstract data types** — the important part is the policy, not the backing storage.

### Design Problem Solved

- Enforce ordering constraints at the API level.
- Simple, predictable behavior.
- Natural fit for many algorithms (BFS, DFS, expression parsing).

Trade-off: You can only access ends (head/tail), not arbitrary positions.

### Real System Usage

- **Stack:** Function call stacks in all CPUs; expression evaluation (infix to postfix); undo systems.
- **Queue:** Task schedulers, message passing systems, BFS algorithms, rate limiting.

---

## 2️⃣ The What — Mental Model & Intuition

### Core Analogy

- **Stack:** A vertical **pile of trays**. You place a new tray on top; you remove from the top.
- **Queue:** A **line of customers at a bank**. New customers join the back; the cashier serves from the front.

The discipline is more important than the mechanism.

---

## 3️⃣ The How — Mechanical Walkthrough

### Array-Backed Stack

**State:**
- `array`: buffer of elements.
- `top`: index of the next free position (also the count of elements).

**Operations:**

Push(x):
1. array[top] = x
2. top++
3. Cost: O(1)

Pop():
1. top--
2. return array[top]
3. Cost: O(1)

### Circular Buffer Queue

**State:**
- `array`: buffer of size capacity.
- `head`: index of the first element.
- `tail`: index of the next insertion point.
- `count`: number of elements.

**Operations:**

Enqueue(x):
1. array[tail] = x
2. tail = (tail + 1) % capacity
3. count++
4. Cost: O(1)

Dequeue():
1. x = array[head]
2. head = (head + 1) % capacity
3. count--
4. return x
5. Cost: O(1)

The modulo operation wraps indices around, avoiding the need to shift the entire buffer.

### Linked-List Backed Stack/Queue

- Stack: Push at head, pop from head.
- Queue: Enqueue at tail, dequeue from head.

Both operations are O(1) once you maintain head and tail pointers.

---

## 4️⃣ Visualization — The Simulation

### Stack Example

```
Step 1: Push(10)
[10, _, _]
top = 1

Step 2: Push(20)
[10, 20, _]
top = 2

Step 3: Pop()
[10, 20, _]
top = 1
return 20

Step 4: Push(30)
[10, 30, _]
top = 2
```

### Circular Queue Example

Capacity = 5

```
Initial: head=0, tail=0, count=0
[_, _, _, _, _]

Enqueue(10): array[0]=10, tail=1, count=1
[10, _, _, _, _]

Enqueue(20): array[1]=20, tail=2, count=2
[10, 20, _, _, _]

Enqueue(30): array[2]=30, tail=3, count=3
[10, 20, 30, _, _]

Dequeue(): head=(0+1)%5=1, count=2, return 10
[10, 20, 30, _, _]
    ^

Enqueue(40): array[3]=40, tail=4, count=3
[10, 20, 30, 40, _]

Enqueue(50): array[4]=50, tail=(4+1)%5=0, count=4
[50, 20, 30, 40, 50]
 ^           
(tail wraps)

Dequeue(): head=(1+1)%5=2, count=3, return 20
[50, 20, 30, 40, 50]
       ^
```

---

## 5️⃣ Critical Analysis — Performance & Robustness

### Complexity Table

| Structure | Operation   | Time | Notes                      |
|-----------|-------------|------|---------------------------|
| Stack     | push        | O(1) | Constant time              |
| Stack     | pop         | O(1) | Constant time              |
| Queue     | enqueue     | O(1) | Tail operation only        |
| Queue     | dequeue     | O(1) | Head operation only        |
| Queue     | circular    | O(1) | No shifting; modulo wrap   |

### Backing Storage Trade-offs

| Aspect | Array-backed | Linked-list |
|--------|--------------|------------|
| Cache behavior | Excellent (contiguous) | Poor (scattered) |
| Space overhead | Minimal | Extra pointers |
| Resize cost | Amortized O(1) | No resizing needed |
| Access pattern | Sequential | Pointer chasing |

Array-backed stacks are typically 10-100x faster in practice due to cache locality.

### Edge Cases & Failure Modes

- **Stack underflow:** Pop from empty stack → undefined behavior.
- **Stack overflow:** Push beyond capacity → must resize (dynamic array) or error.
- **Queue wraparound:** Circular queue requires careful modulo arithmetic.
- **Capacity checks:** Both structures need size checks before operations.

---

## 6️⃣ Real System Integration

### Function Call Stack

- CPU maintains a stack pointer (SP) register.
- Each function call: push return address and local variables.
- Each return: pop and jump to return address.
- Stack overflow: infinite recursion → SP exceeds stack limit → segmentation fault.

### Expression Evaluation

- Infix: "3 + 4 * 2" → requires precedence rules.
- Postfix: "3 4 2 * +" → left-to-right with stack.
- Stack-based evaluation: push operands, pop and compute on operators.

### BFS (Breadth-First Search)

- Uses a queue to explore graph level by level.
- Enqueue: newly discovered nodes.
- Dequeue: process next node.

### Message Passing

- Producer enqueues messages.
- Consumer dequeues and processes.
- Naturally decouples components.

---

## 7️⃣ Concept Crossovers

### Predecessors
- **Arrays (Day 1):** Stack can be array-backed.
- **Dynamic arrays (Day 2):** Grow stack with amortized cost.
- **Linked lists (Day 3):** Alternative backing for stack/queue.

### Successors
- **Recursion (Week 1, Day 3):** Every function call uses the call stack.
- **BFS/DFS (Week 6):** Queue for BFS, stack for DFS.
- **Expression parsing:** Stacks for infix-to-postfix conversion.

---

## 8️⃣ Mathematical & Theoretical Perspective

Stacks and queues are **abstract data types (ADTs)** defined by operations and their behavior:

- **Stack:** {push, pop, empty} with LIFO discipline.
- **Queue:** {enqueue, dequeue, empty} with FIFO discipline.

Implementation can vary (array, linked list, deque), but interface is constant.

---

## 9️⃣ Algorithmic Design Intuition

### When to Choose Stacks

1. **Undo/redo:** Most recent action is undone first.
2. **DFS:** Implicit stack through recursion.
3. **Expression evaluation:** Natural for operator precedence.

### When to Choose Queues

1. **BFS:** Level-by-level exploration.
2. **Fair scheduling:** Process tasks in order received.
3. **Asynchronous messaging:** Decouple producers and consumers.

---

## 🔟 Knowledge Check — Socratic

1. Why does a circular queue avoid the need to shift elements when dequeuing?
   - Answer: Modulo arithmetic wraps indices; dequeue just increments head index.

2. When implementing a stack in a fixed-size array, what happens on overflow?
   - Answer: Either raise an exception or use a dynamic array (resize).

3. In a recursive DFS, where is the stack implicitly maintained?
   - Answer: In the call stack; each recursive call pushes a frame; returns pop frames.

4. Why would you use a circular queue instead of a regular array queue?
   - Answer: Circular queue avoids waste from shifting; head and tail pointers wrap around.

---

## 11️⃣ Retention Hook

**One-liner:** Stacks and queues are **ordering policies** (LIFO/FIFO) layered on top of arrays or linked lists, enforcing access constraints.

---

## 🧭 Navigation

**← [Previous: Day 3 - Linked Lists](./03_Linked_Lists.md)**  
**→ [Next: Day 5 - Binary Search](./05_Binary_Search.md)**  
**↑ [Back to README](../README.md)**

