# Week 3: Summary & Key Concepts

## 📖 Week Overview

**Week 3 teaches efficient data organization** — sorting and key-value mapping. After Week 2's fundamental structures, you now learn algorithms that power most systems.

**Central theme:** **Algorithmic paradigms.** Divide-and-conquer for sorting, hashing for fast lookup.

---

## 📊 Algorithm Comparison Table

| Algorithm | Best | Average | Worst | Space | Stable |
|-----------|------|---------|-------|-------|--------|
| **Bubble Sort** | O(n²) | O(n²) | O(n²) | O(1) | ✓ |
| **Insertion Sort** | O(n) | O(n²) | O(n²) | O(1) | ✓ |
| **Selection Sort** | O(n²) | O(n²) | O(n²) | O(1) | ✗ |
| **Merge Sort** | O(n log n) | O(n log n) | O(n log n) | O(n) | ✓ |
| **Quick Sort** | O(n log n) | O(n log n) | O(n²) | O(log n) | ✗ |
| **Heap Sort** | O(n log n) | O(n log n) | O(n log n) | O(1) | ✗ |
| **Hash Table** | O(1) | O(1) | O(n) | O(n) | — |

---

## 🧠 Key Insights

### Insight 1: Sorting Paradigms
- **Elementary:** Intuitive O(n²), use for n < 50
- **Divide-and-Conquer:** O(n log n), merge/quick/heap
- **Specialized:** Counting sort, radix sort (not this week)

### Insight 2: Stability Matters
- When sorting by multiple keys (sort by name, then age)
- Merge and insertion sorts preserve order
- Selection, quick, heap sorts don't

### Insight 3: Hashing is Probabilistic
- Average case O(1) (good hash + low load factor)
- Worst-case O(n) (all collisions)
- Practical: nearly always O(1)

### Insight 4: Trade-offs Everywhere
- Merge: guaranteed O(n log n), needs space
- Quick: faster practice, can degrade to O(n²)
- Heap: guaranteed, slower than quick
- Hash: O(1) average vs O(log n) guaranteed (tree)

### Insight 5: Real Systems Use Hybrids
- TimSort: insertion (small) + merge (large)
- Intro-sort: quick sort + heap sort (fallback)
- Hash tables: chaining + probing strategies

---

## 🎯 Common Problem Patterns

### Pattern 1: Choose Sort Algorithm
- Small n → insertion sort
- Need stability → merge sort
- General case → quick sort
- Guaranteed O(n log n) → heap sort

### Pattern 2: Design Hash System
- Key-value lookup → hash table
- Handle collisions → chaining or probing
- Manage growth → rehashing

---

## ❌ Common Misconceptions Fixed

### ❌ "Quick sort is always O(n log n)"
✅ **Reality:** O(n log n) average, O(n²) worst-case if bad pivot selection.

### ❌ "Hash tables are always O(1)"
✅ **Reality:** O(1) average with good hash and load factor. O(n) worst-case.

### ❌ "Merge sort slower than quick sort"
✅ **Reality:** Merge sort guaranteed, same asymptotic, but quick sort has better constants.

### ❌ "Insertion sort useless"
✅ **Reality:** O(n) on nearly-sorted, used in hybrids, better cache than merge for small arrays.

### ❌ "Heap sort best guaranteed"
✅ **Reality:** Guaranteed O(n log n), but slower in practice due to cache misses.

---

## 📈 Mastery Progression

### Level 1: Recognition (Days 1-2)
- Name algorithms, state complexity
- Identify when to use each

### Level 2: Understanding (Days 3-4)
- Explain why complexity is what it is
- Understand stability and trade-offs

### Level 3: Application (Days 5+)
- Implement correctly
- Trace by hand
- Analyze specific scenarios

### Level 4: Mastery (Week 4+)
- Combine with other techniques
- Optimize for constraints
- Design hybrid solutions

---

## 🔗 Week 3 → Week 4+ Connections

**Week 4:** Two-pointers on sorted arrays (binary search preprocessing)  
**Week 4.5:** Hash Map/Set (Tier 1: 70% interview coverage!)  
**Week 5:** Tree operations use heap, sorting  
**Week 6:** Graphs use hash tables for adjacency, sorting for topological  

---

## ❓ Quick-Reference FAQ

**Q: When use merge vs quick sort?**
A: Merge if stability required or external sorting. Quick for general cases.

**Q: Is insertion sort still used?**
A: Yes, in hybrids (TimSort) and for small subarrays.

**Q: Why hash tables over trees?**
A: O(1) average vs O(log n). Hash better for equal distribution.

**Q: Load factor importance?**
A: Directly impacts collision rate. Keep < 0.75 for O(1) average.

**Q: Chaining vs open addressing?**
A: Chaining simpler, worse cache. Open addressing better cache, harder to implement.

---

## ✨ Week 3 Key Takeaway

> **Master sorting paradigms (elementary, divide-and-conquer, guaranteed) and hashing mechanics (hash function, collisions, load factor). These power most systems.**

---

## 🎓 Before Week 4

**Confidence Check:**
- [ ] Rate yourself 4/5 or higher on each day
- [ ] Can you choose sort for problem?
- [ ] Understand hash collisions?
- [ ] Ready for pattern-based problems (Week 4)?

---

**Cumulative:** Weeks 1-3 = ~50% interview coverage

