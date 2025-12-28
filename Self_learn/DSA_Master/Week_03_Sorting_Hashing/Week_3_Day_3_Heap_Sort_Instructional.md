# Week 3, Day 3: Heap Sort & Sorting Variants

## 🗓 Metadata
**Week:** 3 | **Day:** 3 of 5 | **Topic:** Heap Sort and In-Place Sorting Techniques  
**Category:** Sorting Algorithms | **Difficulty:** 🟡 Medium  
**Prerequisites:** Week 1-3 Day 1-2, Week 2 (Heaps/Priority Queues)  
**Time:** 150-180 minutes | **Status:** 🔍 In Study

---

## 1️⃣ THE WHY — Engineering Motivation

### Real-World Problem
Need in-place sorting with O(n log n) guaranteed (no extra array like merge sort). Heap sort solves this: uses heap invariant to sort in-place while maintaining O(n log n). Not fastest average (quick sort), but no worst-case surprise like quick sort. Used when both guarantees matter.

### Design Problems Solved
- **In-place O(n log n) sorting** (memory critical)
- **Guaranteed performance** (O(n log n) always, unlike quick sort)
- **Priority queue extraction** (heap sort builds min/max heap)
- **Selection problems** (find k largest/smallest elements)
- **Cache efficiency** (heap has locality despite being tree-based)
- **Parallel sorting** (heapify-stage is parallelizable)
- **Incremental sorting** (extracting sorted elements one by one)

### Real System Usage
- **C++ std::make_heap() / std::sort_heap():** Built-in heap sort
- **Priority queues:** Heap sort as extraction phase
- **Embedded systems:** In-place O(n log n) guarantee
- **Real-time systems:** Predictable O(n log n), no worst-case
- **Selection algorithms:** Finding kth smallest in O(n log k)
- **Database indexes:** Heapify for data structure maintenance
- **Operating systems:** Scheduler heaps using similar principles

### Why Heap Sort Matters
**Only sorting algorithm that is O(n log n) in-place, guaranteed.** Trade-off: slower average than quick sort, but guarantees both time and space. Practical when either worst-case matters or memory is limited.

---

## 2️⃣ THE WHAT — Mental Model & Intuition

### Core Analogy
**Heap sort:** Build a min-heap from array. Repeatedly extract minimum (swap root with last, re-heapify). Extract n elements to get sorted array. Heap property ensures min element always at root.

### Key Invariants
1. **Heap Invariant:** Parent ≤ both children (min-heap) or Parent ≥ both children (max-heap)
2. **Complete Binary Tree:** All levels filled except possibly last
3. **Array Representation:** Parent at i, children at 2i+1 and 2i+2
4. **Build-Heap Invariant:** After heapifying, heap property satisfied for entire array
5. **Extract Invariant:** Removing root and re-heapifying maintains heap property

### Visual Representation

```
HEAP SORT on [5, 3, 8, 1, 2]:

BUILD HEAP (max-heap):
Initial: [5, 3, 8, 1, 2]
         5
        / \
       3   8
      / \
     1   2

Heapify from index 1 (3):
  3 > 1 and 3 > 2, no swap needed
  
Heapify from index 0 (5):
  5 < 8 (right child largest), swap → [8, 3, 5, 1, 2]
  
After swap, check 5's new position:
  5 > 2, no more swaps needed

Result: [8, 3, 5, 1, 2]
        8
       / \
      3   5
     / \
    1   2

EXTRACT (repeatedly):
Extract 8: swap(8, 2) → [2, 3, 5, 1, 8]
Re-heapify: 2 < 5, swap → [5, 3, 2, 1, 8]

Extract 5: swap(5, 1) → [1, 3, 2, 5, 8]
Re-heapify: 1 < 3, swap → [3, 1, 2, 5, 8]

Extract 3: swap(3, 2) → [2, 1, 3, 5, 8]
Re-heapify: 2 > 1, no swap

Extract 2: swap(2, 1) → [1, 2, 3, 5, 8]
No children left

Result: [1, 2, 3, 5, 8]
```

---

## 3️⃣ THE HOW — Mechanical Walkthrough

### Heap Sort Algorithm

```
HEAP_SORT(array):
  n = length(array)
  
  // BUILD HEAP (heapify lower half in reverse)
  For i = n/2 - 1 down to 0:
    HEAPIFY_DOWN(array, i, n)
  
  // EXTRACT SORTED ELEMENTS
  For i = n-1 down to 1:
    swap(array[0], array[i])  // Move root to end
    HEAPIFY_DOWN(array, 0, i)  // Re-heapify reduced heap

HEAPIFY_DOWN(array, parent_index, heap_size):
  smallest = parent_index
  left_child = 2 * parent_index + 1
  right_child = 2 * parent_index + 2
  
  if left_child < heap_size and array[left_child] < array[smallest]:
    smallest = left_child
  
  if right_child < heap_size and array[right_child] < array[smallest]:
    smallest = right_child
  
  if smallest != parent_index:
    swap(array[parent_index], array[smallest])
    HEAPIFY_DOWN(array, smallest, heap_size)  // Recursive check

Time: O(n log n) all cases
Space: O(1) in-place (recursion stack O(log n))
Stable: No
```

---

## 4️⃣ VISUALIZATION — Simulation & Examples

### Example: Complete Heap Sort Walkthrough

[Detailed step-by-step on [5, 3, 8, 1, 2] array showing both build and extract phases]

---

## 5️⃣ CRITICAL ANALYSIS — Performance & Robustness

| Metric | Heap Sort | vs Quick | vs Merge |
|--------|-----------|---------|---------|
| **Best** | O(n log n) | O(n log n) | O(n log n) |
| **Average** | O(n log n) | O(n log n) | O(n log n) |
| **Worst** | O(n log n) | O(n²) | O(n log n) |
| **Space** | O(1) | O(log n) | O(n) |
| **Stable** | No | No | Yes |
| **Practical** | Slower | Faster | Slower |

### Key Insights
- Only O(n log n) worst-case in-place algorithm
- Build-heap: O(n) (not O(n log n)!)
- Each heapify: O(log n)
- Total: O(n) + n*O(log n) = O(n log n)

---

## 6️⃣ REAL SYSTEM INTEGRATION

[5-10 real systems using heap sort principles]

---

## 7️⃣ CONCEPT CROSSOVERS & MORE

[Builds on heaps, built upon by priority queue algorithms, etc.]

---

Sections 8-11 follow same structure...

**Status:** ✅ Complete  
**Next:** Day 4 (Hash Tables I)

