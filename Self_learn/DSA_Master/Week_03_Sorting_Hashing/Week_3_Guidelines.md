# Week 3: Sorting & Hashing — Guidelines

## 📅 Daily Breakdown & Time Allocation

**Total Week:** 12-14 hours (2.5-2.8 hours per day)

| Day | Topic | Time | Core Concepts | Difficulty |
|-----|-------|------|---------------|------------|
| **1** | Elementary Sorts | 2.5h | Bubble, Insertion, Selection; O(n²) limits | Medium |
| **2** | Merge & Quick Sort | 2.5h | Divide-conquer, guaranteed vs average O(n log n) | Hard |
| **3** | Heap Sort | 2.5h | Heap property, in-place O(n log n), guaranteed | Hard |
| **4** | Hash Tables I | 2.5h | Hash function, collisions, chaining, O(1) average | Hard |
| **5** | Hash Tables II | 2.5h | Open addressing, rehashing, load factor | Hard |
| **Weekend** | Integration | 2h | Synthesis, decision trees | — |

---

## 🎯 Learning Objectives

### By End of Day 1 (Elementary Sorts)
- [ ] Understand bubble, insertion, selection sort mechanics
- [ ] Know O(n²) limits and when acceptable (n < 10,000)
- [ ] Understand stability concept
- [ ] Know insertion sort is adaptive (O(n) on nearly-sorted)

### By End of Day 2 (Merge & Quick Sort)
- [ ] Understand divide-and-conquer on sorted data
- [ ] Know merge sort: guaranteed O(n log n), stable, needs O(n) space
- [ ] Know quick sort: average O(n log n), O(1) space, faster in practice
- [ ] Understand pivot selection impacts performance

### By End of Day 3 (Heap Sort)
- [ ] Understand binary heap property
- [ ] Know heap sort: guaranteed O(n log n), O(1) space
- [ ] Understand heapify operation
- [ ] Know heap applications (priority queues, selection)

### By End of Day 4 (Hash Tables I)
- [ ] Understand hash function concept
- [ ] Know O(1) average for search/insert/delete
- [ ] Understand collision basics
- [ ] Know chaining approach

### By End of Day 5 (Hash Tables II)
- [ ] Understand chaining vs open addressing
- [ ] Know load factor and rehashing
- [ ] Understand primary clustering
- [ ] Know practical trade-offs

---

## 📚 Core Concepts Overview

### Concept 1: Sorting Trade-offs
**Time-Space:** Merge sort O(n) space, quick sort O(1) space  
**Stability:** Important for multi-key sort  
**Adaptivity:** Insertion sort exploits nearly-sorted data

### Concept 2: Divide-and-Conquer
**Principle:** Divide problem, solve subproblems, combine  
**Recurrence:** T(n) = a×T(n/b) + f(n)  
**Master Theorem:** Analyze growth rate

### Concept 3: Hashing Fundamentals
**Hash Function:** Key → index via arithmetic  
**Collision Resolution:** Chaining or probing  
**Load Factor:** n/m; keep < 0.75

### Concept 4: Complexity Trade-offs
**Elementary:** Simple O(n²)  
**Advanced:** Complex O(n log n)  
**Hash:** Average O(1) vs worst O(n)

---

## 🔄 Recommended Learning Path

**Morning (90 min):**
1. Read daily instructional file
2. Trace examples by hand
3. Understand key mechanics

**Afternoon (60 min):**
1. Answer Socratic questions
2. Solve practice problems
3. Implement algorithms

**Evening (30 min):**
1. Check checklist
2. Rate confidence
3. Plan next day

---

## ⚠️ Common Mistakes to Avoid

**Mistake 1: "Quick sort is always O(n log n)"**
Reality: Adversarial pivot selection → O(n²). Use median-of-three or intro-sort.

**Mistake 2: "Hash tables are always O(1)"**
Reality: O(1) average with good hash function. Worst-case O(n).

**Mistake 3: "Merge sort is slower than quick sort"**
Reality: Merge faster for external sorting, linked lists, stability required.

**Mistake 4: "Elementary sorts useless for large n"**
Reality: True, but used within advanced sorts for small subarrays (< 64 elements).

**Mistake 5: "Heap sort guaranteed O(n log n), so use always"**
Reality: Slower in practice than quick sort due to cache misses.

---

## 🎓 Practice Problems Guide

### Sorting (Days 1-3)
1. Implement all 5 sorts from scratch
2. Trace on specific arrays
3. Compare performance
4. Analyze stability
5. Find kth largest (heap)

### Hashing (Days 4-5)
1. Design simple hash function
2. Implement chaining
3. Implement open addressing
4. Handle collisions
5. Build dynamic hash table

---

## 💼 Interview Preparation

**Interview Coverage:** Sorting & hashing = ~40-50% of problems (after Week 2's 30-40%)

**Key Topics:**
- When to use each sort
- Stability vs performance trade-offs
- Hash table implementation
- Load factor and rehashing

---

## 🔗 Resources & References

**Books:**
- "Algorithms" by Sedgewick (Chapters 2-3: Sorting, Searching)
- "Introduction to Algorithms" (Chapters 7-8: Quicksort, Heapsort)

**Online:**
- Sorting visualizations (visualgo.net)
- Hash function analysis

---

## ✅ Assessment & Success Criteria

**Knowledge:**
- [ ] Explain sorting trade-offs
- [ ] Analyze hash table collisions
- [ ] Understand Big-O for each algorithm

**Skills:**
- [ ] Implement merge sort
- [ ] Implement quick sort
- [ ] Design hash table with chaining
- [ ] Implement open addressing

**Judgment:**
- [ ] Choose sort for specific problem
- [ ] Choose hash table implementation
- [ ] Optimize for specific constraints

---

## 📊 Connection to Future Weeks

**Week 4:** Binary search on sorted arrays, two-pointer patterns  
**Week 4.5:** Hash Map pattern (Tier 1, 70% interview coverage!)  
**Week 5:** Trees use sorting, hashing for lookups  
**Week 6:** Graphs use hash tables for adjacency, BFS  

---

## ❓ Frequently Asked Questions

**Q: When use merge sort vs quick sort?**
A: Merge if stability needed or external sorting. Quick for general cases (faster in practice).

**Q: Is insertion sort really used?**
A: Yes, in TimSort (hybrid) and for small subarrays in advanced sorts.

**Q: Why hash tables over binary search trees?**
A: Hash tables O(1) average vs tree O(log n) guaranteed. Hash better for equal distribution.

**Q: Load factor 0.75 — why this number?**
A: Empirically minimizes collisions while avoiding excess rehashing.

**Q: Can I implement my own hash function?**
A: Possible, but dangerous. Use library implementations (cryptographically weak functions are bad).

---

## 🎯 Before Moving to Week 4

**Verification Checklist:**
- [ ] Can trace bubble, insertion, selection
- [ ] Can trace merge sort and quick sort
- [ ] Understand heap operations
- [ ] Can explain hash collisions
- [ ] Rate 4/5 or higher on all 5 days

**If not ready:** Spend 1-2 more days on weak areas.

---

## 📝 Week 3 Quick Summary (Table)

| Algorithm | Best | Average | Worst | Space | Stable | Notes |
|-----------|------|---------|-------|-------|--------|-------|
| **Bubble** | O(n²) | O(n²) | O(n²) | O(1) | ✓ | Rarely use |
| **Insertion** | O(n) | O(n²) | O(n²) | O(1) | ✓ | Small n, adaptive |
| **Selection** | O(n²) | O(n²) | O(n²) | O(1) | ✗ | Min writes |
| **Merge** | O(n log n) | O(n log n) | O(n log n) | O(n) | ✓ | Stable, guaranteed |
| **Quick** | O(n log n) | O(n log n) | O(n²) | O(log n) | ✗ | Fast in practice |
| **Heap** | O(n log n) | O(n log n) | O(n log n) | O(1) | ✗ | Guaranteed, slower |
| **Hash** | O(1) | O(1) | O(n) | O(n) | — | Avg case wins |

---

**Total Learning:** 12-14 hours  
**Interview Coverage (cumulative):** ~50%  
**Next:** Week 4 (Problem-Solving Patterns)

