# Week 3: Problem-Solving Roadmap

## 📊 Problem-Solving Framework

**5-Step Process for Sorting/Hashing Problems:**

1. **Understand** input, output, constraints
2. **Identify** if sorting or hashing applies
3. **Choose** algorithm based on requirements
4. **Implement** correctly
5. **Verify** with examples

---

## 🎯 Sorting Problem-Type Roadmap

### Type 1: General Sort
**Pattern:** "Sort array, need output in order"
- **Decision:** Use quick sort (most languages)
- **Cost:** O(n log n) average, O(1) space

### Type 2: Stable Sort Required
**Pattern:** "Sort by primary, secondary key"
- **Decision:** Merge sort or insertion sort
- **Cost:** O(n log n) guaranteed, stable

### Type 3: Small Array
**Pattern:** "n < 50, simplicity matters"
- **Decision:** Insertion sort
- **Cost:** O(n²) acceptable, simpler code

### Type 4: Nearly-Sorted Data
**Pattern:** "Data mostly ordered with few changes"
- **Decision:** Insertion sort
- **Cost:** O(n) on nearly-sorted data

### Type 5: Guaranteed O(n log n) Needed
**Pattern:** "Hard deadline, worst-case matters"
- **Decision:** Merge sort or heap sort
- **Cost:** O(n log n) guaranteed

### Type 6: Find Kth Largest
**Pattern:** "Find kth element without fully sorting"
- **Decision:** Heap (min-heap of k elements) or quickselect
- **Cost:** O(n log k) for heap, O(n) average for quickselect

---

## 🎯 Hashing Problem-Type Roadmap

### Type 1: Find Duplicates
**Pattern:** "Check if element appears twice"
- **Decision:** Hash set
- **Cost:** O(1) insert/lookup, O(n) total

### Type 2: Frequency Count
**Pattern:** "Count occurrences of elements"
- **Decision:** Hash map (element → count)
- **Cost:** O(1) per update, O(n) total

### Type 3: Check Anagrams
**Pattern:** "Verify two strings are anagrams"
- **Decision:** Hash map of character frequencies
- **Cost:** O(n) to build, O(1) to compare

### Type 4: Two Sum / Pair Problems
**Pattern:** "Find pair of elements with specific sum"
- **Decision:** Hash set or hash map
- **Cost:** O(1) lookup, O(n) total

### Type 5: Intersection/Union
**Pattern:** "Find common/unique elements"
- **Decision:** Hash sets
- **Cost:** O(n) for intersection, O(n) for union

---

## 🌳 Decision Tree: Sorting

```
START: "I need to sort data"

1. Is array already mostly sorted?
   ├─ YES → Insertion sort (O(n))
   └─ NO → Continue

2. Must preserve relative order of equal elements?
   ├─ YES → Merge sort (stable)
   └─ NO → Continue

3. Need guaranteed O(n log n) worst-case?
   ├─ YES → Merge sort or heap sort
   └─ NO → Continue

4. Is array size small (n < 50)?
   ├─ YES → Insertion sort (simpler)
   └─ NO → Quick sort (faster in practice)
```

---

## 🌳 Decision Tree: Hashing

```
START: "I need fast key-value lookup"

1. Need ordered iteration?
   ├─ YES → Use tree, not hash table
   └─ NO → Continue

2. Know all keys in advance?
   ├─ YES → Consider perfect hashing
   └─ NO → Dynamic hash table

3. Deletions frequent?
   ├─ YES → Chaining better than open addressing
   └─ NO → Open addressing acceptable

4. Build hash table size?
   └─→ Start with capacity = 2×expected size, rehash at 0.75
```

---

## 🔍 Common Pitfalls & Recovery

### Pitfall 1: "Use quick sort always"
**Recovery:** Merge sort if stability needed or external sorting.

### Pitfall 2: "Hash tables guarantee O(1)"
**Recovery:** O(1) average with good hash. Worst-case O(n).

### Pitfall 3: "Choosing bad pivot in quicksort"
**Recovery:** Use median-of-three or random pivot.

### Pitfall 4: "Load factor too high"
**Recovery:** Keep load factor < 0.75, rehash when exceeded.

---

## 📋 Problem-Solving Template

```
PROBLEM: [Sorting or Hashing]

UNDERSTAND:
- Input: [Array? Size range?]
- Output: [Sorted? Pairs? Counts?]
- Constraints: [Time? Space? Stable?]

IDENTIFY:
- Sorting or hashing?
- Which algorithm?

CHOOSE:
- Why this algorithm?
- Trade-offs acceptable?

IMPLEMENT:
- [Algorithm]
- [Trace example]

VERIFY:
- Edge cases: [empty, duplicates, single element]
- Correct: [yes/no]
```

---

## 📊 Quick Decision Matrix

| Problem Type | Recommended | Why |
|--------------|-------------|-----|
| General sort | Quick sort | Fast practice |
| Stable sort | Merge sort | Preserves order |
| Small n | Insertion sort | Simple |
| Guaranteed O(n log n) | Merge/heap | Worst-case |
| Find duplicates | Hash set | O(1) lookup |
| Count frequency | Hash map | O(1) per element |
| Two sum | Hash set | O(n) total |

---

## ✅ Practice Problems

### Sorting (Days 1-3)
1. Sort array with all three elementary sorts
2. Implement merge sort and quick sort
3. Use heap sort to find kth largest
4. Trace each on [3,1,4,1,5,9,2,6]
5. Compare stability: why matters

### Hashing (Days 4-5)
1. Find first non-repeating character
2. Two sum problem
3. Check if anagrams
4. Count word frequencies
5. Implement hash table with chaining

---

## Summary

**Master decision trees.** Most problems fit patterns. Choose correct algorithm, implement carefully, verify thoroughly.

