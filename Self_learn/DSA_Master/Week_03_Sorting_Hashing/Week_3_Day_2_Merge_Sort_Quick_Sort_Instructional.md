# Week 3, Day 2: Merge Sort & Quick Sort

## 🗓 Metadata
**Week:** 3 | **Day:** 2 of 5 | **Topic:** Merge Sort & Quick Sort  
**Category:** Sorting & Hashing | **Difficulty:** 🔴 Hard  
**Prerequisites:** Week 2 (Arrays), Week 1 (Recursion, Big-O)  
**Time:** 90-120 minutes

---

## 1️⃣ THE WHY — Engineering Motivation

**Real-World Problem:**
Elementary sorts O(n²) fail on 1 million records. Need O(n log n). Both merge sort (guaranteed) and quick sort (average) achieve this.

**Design Problems Solved:**
- O(n log n) comparison-based sorting
- Merge sort: guaranteed O(n log n), stable, needs O(n) space
- Quick sort: average O(n log n), O(1) space, faster in practice
- Divide-and-conquer paradigm foundation

**Real System Usage:**
- **Merge Sort:** Databases (stable required), external sorting, streaming
- **Quick Sort:** Standard library (C++ sort, Python sorted), general purpose
- **TimSort:** Hybrid (insertion + merge), used by Python/Java

---

## 2️⃣ THE WHAT — Mental Model & Intuition

### Merge Sort
**Analogy:** Divide array in half, sort each half, merge two sorted halves.

```
[5, 2, 8, 1]
Divide:     [5,2]  [8,1]
Further:   [5][2] [8][1]
Sort each:  [2,5]  [1,8]
Merge:      [1,2,5,8]
```

### Quick Sort
**Analogy:** Pick pivot, partition array (smaller left, larger right), recurse on halves.

```
[5, 2, 8, 1, 9]
Pivot 5:    [2,1] [5] [8,9]
Recurse:   [1,2]  [5]  [8,9]
Result:     [1,2,5,8,9]
```

---

## 3️⃣ THE HOW — Mechanical Walkthrough

### Merge Sort
```
Algorithm:
  mergeSort(arr, left, right):
    if left < right:
      mid = (left + right) / 2
      mergeSort(arr, left, mid)
      mergeSort(arr, mid+1, right)
      merge(arr, left, mid, right)
      
  merge(arr, left, mid, right):
    Create temp arrays L and R
    Merge L and R back into arr in sorted order

Cost: T(n) = 2×T(n/2) + O(n) = O(n log n)
Space: O(n) for temporary arrays
```

### Quick Sort
```
Algorithm:
  quickSort(arr, left, right):
    if left < right:
      p = partition(arr, left, right)
      quickSort(arr, left, p-1)
      quickSort(arr, p+1, right)
      
  partition(arr, left, right):
    pivot = arr[right]
    i = left - 1
    for j = left to right-1:
      if arr[j] < pivot:
        i++
        swap(arr[i], arr[j])
    swap(arr[i+1], arr[right])
    return i+1

Best/Avg: O(n log n)
Worst: O(n²) if pivot always largest/smallest
```

---

## 4️⃣ VISUALIZATION — Simulation & Examples

**Merge Sort on [5,2,8,1]:**
```
Division:
[5,2,8,1]
  [5,2]    [8,1]
 [5] [2]  [8] [1]

Merging:
[2,5]    [1,8]
  [1,2,5,8]
```

**Quick Sort on [5,2,8,1,9]:**
```
Partition with pivot=5:
[2,1]  [5]  [8,9]

Left: partition with pivot=1:
[]  [1]  [2]
Result left: [1,2]

Right: partition with pivot=9:
[8]  [9]  []
Result right: [8,9]

Final: [1,2,5,8,9]
```

---

## 5️⃣ CRITICAL ANALYSIS — Performance & Robustness

| Sort | Best | Average | Worst | Space | Stable |
|------|------|---------|-------|-------|--------|
| **Merge** | O(n log n) | O(n log n) | O(n log n) | O(n) | ✓ Yes |
| **Quick** | O(n log n) | O(n log n) | O(n²) | O(log n) | ✗ No |

**Key Insight:** Quick sort faster in practice due to:
- Better cache locality (in-place)
- Fewer data movements
- Average case common

**Worst-case:** Already-sorted array with naive pivot selection

---

## 6️⃣ REAL SYSTEM INTEGRATION

**Linux kernel (qsort):** Quick sort with median-of-three pivot  
**Python (Timsort):** Uses insertion for small subarrays, merge for large  
**C++ (std::sort):** Intro-sort (quick sort → heap sort if depth too deep)  
**Databases:** Merge sort for stability requirement  

---

## 7️⃣ CONCEPT CROSSOVERS

**Builds on:** Divide-and-conquer (Week 1), arrays, comparisons  
**Built by:** Sorting networks, hybrid sorts  
**Used in:** External sorting, merge-based algorithms

---

## 8️⃣ MATHEMATICAL & THEORETICAL PERSPECTIVE

**Merge Sort Recurrence:**
```
T(n) = 2×T(n/2) + O(n) = O(n log n)
Proof: At each level, n comparisons. log n levels. Total O(n log n).
```

**Quick Sort Analysis:**
```
Best case: Balanced partition → O(n log n)
Worst case: Unbalanced (size 0, n-1) → O(n²)
Average case (random pivot) → O(n log n) with high probability
```

---

## 9️⃣ ALGORITHMIC DESIGN INTUITION

**When to use:**
- **Merge:** Stability required, guaranteed O(n log n), external sorting
- **Quick:** Speed critical, cache matters, default choice

**When NOT to use:**
- **Merge:** Memory limited (needs O(n) space)
- **Quick:** Need stability guarantee

---

## 🔟 KNOWLEDGE CHECK — Socratic Reasoning

**Q1:** Why is quick sort faster than merge sort in practice despite both being O(n log n)?

**Q2:** Can you modify quick sort to guarantee O(n log n) worst-case?

**Q3:** Merge sort is stable. Why is stability important in databases?

**Q4:** Why does choosing pivot wisely (median-of-three) improve quick sort?

---

## 1️⃣1️⃣ RETENTION HOOK — Memory Anchors

**One-Liner:**
> **Merge Sort: Guaranteed O(n log n), stable, needs O(n) space. Quick Sort: Average O(n log n), fast in practice, O(1) space.**

**Mnemonic:** "Merge = Stable, Quick = Fast"

---

## Supplementary: Practice

1. Trace merge sort and quick sort by hand
2. Implement both from scratch
3. Analyze pivot choices and their impact
4. Compare stability with examples

