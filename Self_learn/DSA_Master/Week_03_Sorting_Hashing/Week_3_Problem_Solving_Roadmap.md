# Week 3: Problem-Solving Roadmap & Decision Trees

## 📊 Problem-Solving Framework

**For EVERY sorting/hashing problem, follow this 5-step process:**

1. **IDENTIFY:** What operation? (sorting, lookup, counting, duplicate detection)
2. **RECOGNIZE:** Which category? (elementary, divide-conquer, hash-based)
3. **SELECT:** Which algorithm? (consider time/space/stability constraints)
4. **IMPLEMENT:** Code with proper data structures
5. **OPTIMIZE:** Handle edge cases, improve based on constraints

---

## 🎯 Sorting Decision Tree

```
Is input DATA SMALL (< 50 elements)?
├─ YES: Is it NEARLY SORTED?
│   ├─ YES: Use INSERTION SORT → O(n) best, O(1) space
│   └─ NO: Use SELECTION SORT → O(n²) but only n swaps
└─ NO: Continue below

Is STABILITY REQUIRED (equal elements maintain order)?
├─ YES: Use MERGE SORT → O(n log n) guaranteed, stable
└─ NO: Continue below

Is SPACE CRITICAL (O(1) required)?
├─ YES: Use HEAP SORT → O(n log n) guaranteed, in-place
└─ NO: Continue below

Is AVERAGE PERFORMANCE most important?
├─ YES: Use QUICK SORT → O(n log n) average, fast
└─ NO: Use MERGE SORT (guarantee O(n log n))
```

---

## 🎯 Hashing Decision Tree

```
Is EXACT LOOKUP needed?
├─ YES: Is ORDERING important?
│   ├─ YES: Use BALANCED BST or SORTED ARRAY
│   └─ NO: Use HASH TABLE → O(1) average
└─ NO: Continue below

Is FREQUENCY/COUNTING needed?
├─ YES: Use HASH MAP (key → count)
└─ NO: Continue below

Is DUPLICATE DETECTION needed?
├─ YES: Use HASH SET → O(1) average
└─ NO: Different problem type
```

---

## 🌳 Sort-Specific Roadmaps

### ELEMENTARY SORTS (Bubble, Insertion, Selection)

**Template:**
```
1. Check: Is n < 50?
2. Select: Insertion (nearly sorted) or Selection (minimize writes)
3. Implement: Simple loops, track comparisons/swaps
4. Verify: Works for size 1, 2, and reverse-sorted
```

### MERGE SORT (Divide-and-Conquer Stable)

**Template:**
```
1. Base: If n ≤ 1, return (trivially sorted)
2. Divide: Split array in half
3. Conquer: Recursively sort both halves
4. Combine: Merge two sorted halves (O(n))
5. Verify: Merge function preserves stability
```

### QUICK SORT (Divide-and-Conquer Fast Average)

**Template:**
```
1. Base: If n ≤ 1, return
2. Partition: Choose pivot, split into smaller/larger
3. Conquer: Recursively sort both partitions
4. Combine: Pivot in final position (no merge needed)
5. Optimize: Good pivot selection critical
```

### HEAP SORT (Divide-and-Conquer In-Place)

**Template:**
```
1. Build: Heapify array into max-heap (O(n))
2. Extract: Repeatedly swap root with last, heapify
3. Key: After each extraction, heap shrinks
4. Verify: Heap invariant maintained throughout
```

### HASH TABLES

**Template:**
```
1. Hash: Map key via hash function
2. Index: Get bucket index (hash % table_size)
3. Handle: Collision via chaining or probing
4. Rehash: When load factor > 0.75
5. Verify: All operations O(1) average, O(n) worst
```

---

## 🔍 Common Pitfalls & Recovery

### Pitfall 1: Choosing Wrong Algorithm
**Symptom:** Solution correct but inefficient for constraints
**Recovery:** Use decision tree. Quick sort for average? Merge for stable? Heap for guaranteed in-place?

### Pitfall 2: Off-by-One in Recursive Base Case
**Symptom:** Stack overflow or incorrect result
**Recovery:** Explicit base cases: if n ≤ 1 return. Check boundary.

### Pitfall 3: Not Handling Hash Collisions
**Symptom:** Data overwrites or lookup failures
**Recovery:** Implement chaining or probing properly. Test with intentional collisions.

### Pitfall 4: Ignoring Stability
**Symptom:** Multi-key sorting breaks
**Recovery:** Use merge sort if stability matters. Know which sorts unstable.

### Pitfall 5: Bad Hash Function
**Symptom:** All keys hash to same bucket
**Recovery:** Use good hash function (polynomial rolling hash, crypto hash). Test uniformity.

---

## 📋 Quick Reference Matrix

| Problem | Best Approach | Time | Space | Notes |
|---------|---|------|-------|-------|
| Sort array | Quick sort | O(n log n) avg | O(log n) | If not stable, else merge |
| Sort + stability required | Merge sort | O(n log n) | O(n) | Guaranteed |
| Sort + limited memory | Heap sort | O(n log n) | O(1) | Only guaranteed in-place |
| Two Sum | Hash table | O(n) | O(n) | One pass with lookup |
| Duplicate check | Hash set | O(n) | O(n) | Membership test |
| Frequency count | Hash map | O(n) | O(n) | Each key → count |
| Top K elements | Heap | O(n log k) | O(k) | Or quickselect O(n) avg |
| Find median | Hash or sort | O(n) or O(n log n) | O(n) | Stream: use heap |

---

**Use this roadmap during problem-solving. Clear decision-making → correct algorithm → fast implementation.**

