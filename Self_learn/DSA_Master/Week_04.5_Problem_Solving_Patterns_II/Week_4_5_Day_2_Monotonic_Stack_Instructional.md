# Week 4.5, Day 2: Monotonic Stack

## 🗓 Metadata
**Week:** 4.5 (Tier 1) | **Day:** 2 of 5 | **Topic:** Monotonic Stack  
**Category:** Critical Problem-Solving Patterns | **Difficulty:** 🔴 Hard  
**Time:** 90-120 minutes  
**Interview Coverage:** **20-30% of stack problems**

---

## 1️⃣ THE WHY — Engineering Motivation

**Real-World Problem:**
Array: [2,1,2,4,3]. Find next greater element for each. Naive: O(n²). Better: monotonic stack, O(n).

**Design Problems Solved:**
- Next greater/smaller element efficiently
- Trapping rain water (2D problem reduction)
- Largest rectangle in histogram
- Stock span problems
- Daily temperatures

**Real System Usage:**
- **Compilers:** Matching brackets, parentheses
- **Networking:** TCP congestion control (monotonic decreasing windows)
- **Graphics:** Visibility culling (monotonic stack for silhouette edges)
- **Robotics:** Path planning with obstacles (monotonic decreasing distance)

---

## 2️⃣ THE WHAT — Mental Model & Intuition

**Core Analogy:**
Imagine buildings in a line. You want to find the next taller building. A monotonic stack maintains buildings in increasing height order — when new building is taller, pop shorter ones.

```
Buildings: [2, 1, 2, 4, 3]
Monotonic Decreasing Stack:
Process 2: stack = [2]
Process 1: 1 < 2, stack = [2, 1]
Process 2: 2 > 1, pop 1, 2 > 2? No, stack = [2, 2]
Process 4: 4 > 2, pop all, stack = [4]
Process 3: 3 < 4, stack = [4, 3]
```

**Key Invariants:**
- Stack maintains elements in increasing/decreasing order
- When new element violates order, pop until valid
- Each element pushed/popped once → O(n)

---

## 3️⃣ THE HOW — Mechanical Walkthrough

**Operation: Next Greater Element**
```
1. stack = []
2. for i from 0 to n-1:
     while stack not empty AND arr[stack.top()] < arr[i]:
       j = stack.pop()
       result[j] = arr[i]  // arr[i] is next greater
     stack.push(i)
3. remaining stack: no next greater (-1)

Cost: O(n) time, O(n) space
```

---

## 4️⃣ VISUALIZATION — Simulation & Examples

```
Array: [2,1,2,4,3]
Output: [-1, 2, 4, -1, -1]  (next greater elements)

Process:
i=0, arr[0]=2: stack=[0]
i=1, arr[1]=1: 1<2, stack=[0,1]
i=2, arr[2]=2: 2>1, pop 1, result[1]=2
               2<2? No, stack=[0,2]
i=3, arr[3]=4: 4>2, pop 2, result[2]=4
               4>2? Yes, pop 0, result[0]=4
               stack=[3]
i=4, arr[4]=3: 3<4, stack=[3,4]
Final: result=[4,2,4,-1,-1]
```

---

## 5️⃣ CRITICAL ANALYSIS — Performance & Robustness

| Operation | Time | Space |
|-----------|------|-------|
| **Next Greater** | O(n) | O(n) |
| **Trapping Rain** | O(n) | O(n) |

Each element pushed/popped once, despite nested while loop.

---

## 6️⃣ REAL SYSTEM INTEGRATION

**Stock market:** Daily span = number of consecutive days stock price ≥ today's price. Monotonic stack reduces O(n²) to O(n).

---

## 7️⃣-1️⃣1️⃣ (Continue with standard structure)

**One-Liner:**
> **Monotonic Stack: O(n) by maintaining strictly increasing/decreasing order. When new element breaks order, it's the next extreme for popped elements.**

**Cognitive Lenses:**
| **Computational** | Each element pushed/popped once despite nested loop → O(n) amortized |
| **Psychological** | Natural: taller building blocks view of shorter ones |
| **Design** | Trade space for time: store indices, not values |
| **AI/ML** | Similar to: attention mechanism (current token attends to previous in order) |
| **Historical** | Widely used in compiler parser stacks |

