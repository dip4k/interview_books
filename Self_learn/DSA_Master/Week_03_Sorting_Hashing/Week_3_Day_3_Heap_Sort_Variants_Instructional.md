# Week 3, Day 3: Heap Sort & Variants

## 🗓 Metadata
**Week:** 3 | **Day:** 3 of 5 | **Topic:** Heap Sort & Variants  
**Difficulty:** 🔴 Hard | **Time:** 90-120 minutes

---

## 1️⃣ THE WHY — Engineering Motivation

**Real-World Problem:**
Quick sort can degrade to O(n²) on adversarial input. Need guaranteed O(n log n) with O(1) space.

**Design Problems Solved:**
- Guaranteed O(n log n) worst-case
- O(1) extra space (in-place)
- Priority queue abstraction
- Selection problem (find kth largest)

---

## 2️⃣ THE WHAT — Mental Model & Intuition

**Heap Concept:**
Binary tree where parent ≥ children (max-heap) or parent ≤ children (min-heap).

```
Max-Heap:
        9
       / \
      7   8
     / \
    3   6

Property: arr[i] ≥ arr[2i+1] and arr[i] ≥ arr[2i+2]
```

**Heap Sort Analogy:**
1. Build max-heap from array
2. Extract max (swap root with last), heapify remainder
3. Repeat until sorted

---

## 3️⃣ THE HOW — Mechanical Walkthrough

**Heapify (maintain heap property):**
```
Algorithm:
  heapify(arr, i, n):
    largest = i
    left = 2i + 1
    right = 2i + 2
    
    if left < n and arr[left] > arr[largest]:
      largest = left
    if right < n and arr[right] > arr[largest]:
      largest = right
    
    if largest != i:
      swap(arr[i], arr[largest])
      heapify(arr, largest, n)

Cost: O(log n) per heapify
```

**Heap Sort:**
```
Algorithm:
  heapSort(arr):
    // Build heap (O(n))
    for i = n/2 - 1 down to 0:
      heapify(arr, i, n)
    
    // Extract elements (O(n log n))
    for i = n-1 down to 1:
      swap(arr[0], arr[i])
      heapify(arr, 0, i)

Cost: O(n log n) guaranteed
Space: O(1) in-place
```

---

## 4️⃣ VISUALIZATION — Simulation & Examples

**Heap Sort on [3,7,8,5,2,1,9,5]:**
```
Build heap: [9,7,8,5,2,1,3,5] (max-heap)

Extract max:
  Swap 9,5: [5,7,8,5,2,1,3,|9] heapify → [8,7,5,5,2,1,3,|9]
  Swap 8,3: [3,7,5,5,2,1,8,|9] heapify → [7,5,5,3,2,1,8,|9]
  Continue...
  
Result: [1,2,3,5,5,7,8,9]
```

---

## 5️⃣ CRITICAL ANALYSIS — Performance & Robustness

| Sort | Best | Average | Worst | Space | Stable |
|------|------|---------|-------|-------|--------|
| **Heap** | O(n log n) | O(n log n) | O(n log n) | O(1) | ✗ No |

**Advantages:** Guaranteed O(n log n), O(1) space, handles worst-case  
**Disadvantages:** Slower than quick sort in practice (cache misses), unstable

---

## 6️⃣ REAL SYSTEM INTEGRATION

**C++ std::sort:** Uses intro-sort (quick sort → heap sort if too deep)  
**Priority Queues:** Use heaps for efficient min/max extraction  
**Dijkstra's Algorithm:** Uses heap for greedy selection  

---

## 7️⃣ CONCEPT CROSSOVERS

**Builds on:** Binary trees (next week), heap property  
**Built by:** Priority queues, selection algorithms  

---

## 8️⃣ MATHEMATICAL & THEORETICAL PERSPECTIVE

**Building heap:** O(n) time (not O(n log n) as might seem)

Proof: Sum of times for heapify at each level = O(n/2×1 + n/4×2 + n/8×3 + ...) = O(n)

---

## 9️⃣ ALGORITHMIC DESIGN INTUITION

**When to use:** Guaranteed O(n log n) worst-case required, adversarial input possible  
**When NOT to use:** Default choice (quick sort faster), need stability

---

## 🔟 KNOWLEDGE CHECK — Socratic Reasoning

**Q1:** Why is building a heap O(n) and not O(n log n)?

**Q2:** Can you use heap sort to find the kth largest element?

**Q3:** Why is heap sort unstable?

**Q4:** Compare quick sort vs heap sort: when choose which?

---

## 1️⃣1️⃣ RETENTION HOOK

**One-Liner:**
> **Heap Sort: O(n log n) guaranteed, O(1) space, slower than quick in practice.**

---

**Supplementary:** Practice building/heapifying, tracing heap sort on arrays

