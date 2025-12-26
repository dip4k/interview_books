# Week 3: Strategic Learning Roadmap & Time Budget

**Master Plan for Week 3: 5 Days of Focused Learning**

---

## 🗺 Overview: The Learning Journey

**Week 3 Mission:** Master sorting and hashing to build algorithmic foundation.

**Why This Order?**
1. Start with **O(n²)** to establish baseline (why optimization matters)
2. Progress to **O(n log n)** divide-and-conquer (giant leap in efficiency)
3. Add **heaps** (different structure, priority queues)
4. Shift to **hashing** (completely different problem)
5. Implement **hash techniques** (collision strategies)

**Total Time Investment:** 6.5-8.5 hours of focused learning + 2-3 hours implementation

---

## 📅 Phase 1: Elementary Sorts (Monday - Day 1)

**Goal:** Establish O(n²) baseline, understand why it fails at scale.

### 90-Minute Study Plan

**Phase 1a: Mental Models (30 min)**
1. **Read Sections 1-2** (Why + What)
   - Understand sorting motivation
   - Visualize bubble, insertion, selection
   - Time: 15 min

2. **Read Section 4** (Examples)
   - Trace each algorithm by hand
   - Feel the mechanics
   - Time: 15 min

**Phase 1b: Analysis & Application (35 min)**
1. **Read Section 5** (Complexity)
   - Understand O(n²) formula: n(n-1)/2
   - Know when each algorithm best
   - Time: 15 min

2. **Read Section 3** (Mechanics)
   - Understand implementations
   - See pseudocode
   - Time: 10 min

3. **Read Section 6** (Real Systems)
   - Timsort uses insertion sort!
   - Motivates future learning
   - Time: 10 min

**Phase 1c: Synthesis (15 min)**
1. Answer Day 1 Q&A questions: 10 min
2. Create summary card: 5 min

### Confidence Checkpoint
By end of Day 1:
- [ ] Can trace bubble, insertion, selection by hand
- [ ] Know O(n²) formula and why
- [ ] Understand Timsort uses insertion sort
- [ ] Rate confidence 3-4/5

**Time Actual:** __ / 90 min

---

## 📅 Phase 2: Divide-and-Conquer (Tuesday - Day 2)

**Goal:** Master O(n log n), apply Master Theorem, understand trade-offs.

### 90-Minute Study Plan

**Phase 2a: Foundations (20 min)**
1. **Read Section 8** (Master Theorem)
   - Understand recurrence relations
   - Apply to T(n) = 2T(n/2) + O(n)
   - Recognize where O(n log n) comes from
   - Time: 20 min

**Phase 2b: Merge Sort Deep Dive (30 min)**
1. **Read Sections 2-4** (Mental model → Examples)
   - Understand split-and-merge
   - Trace merge operation carefully
   - Stability comes from merge
   - Time: 15 min

2. **Read Section 5** (Complexity)
   - Why always O(n log n)
   - Space cost O(n)
   - Best for guarantees
   - Time: 15 min

**Phase 2c: Quick Sort Deep Dive (30 min)**
1. **Read Sections 2-4** (Mental model → Examples)
   - Understand partition concept
   - Trace quicksort with different pivots
   - See why pivot matters
   - Time: 15 min

2. **Read Section 5** (Complexity)
   - Good pivot: O(n log n) balanced
   - Bad pivot: O(n²) unbalanced
   - Average case vs worst case
   - Time: 15 min

**Phase 2d: Comparison & Integration (5 min)**
1. **Read Section 9** (Design Intuition)
   - When to choose merge vs quick
   - Know about hybrids (introsort, timsort)
   - Time: 5 min

**Phase 2e: Synthesis (5 min)**
1. Answer Day 2 Q&A questions: 5 min

### Confidence Checkpoint
By end of Day 2:
- [ ] Understand Master Theorem application
- [ ] Can trace merge sort completely
- [ ] Can trace quicksort completely
- [ ] Know merge guarantees, quick practical
- [ ] Rate confidence 3-4/5

**Time Actual:** __ / 90 min

---

## 📅 Phase 3: Heap Sort (Wednesday - Day 3)

**Goal:** Guaranteed O(n log n) in-place, understand priority queues, recognize Dijkstra.

### 75-Minute Study Plan

**Phase 3a: Heap Fundamentals (25 min)**
1. **Read Section 2** (Mental Model)
   - Visualize complete binary tree
   - Understand parent-child relationships
   - Time: 10 min

2. **Read Sections 3-4** (Mechanics + Examples)
   - Understand heapify-down
   - Build heap from array
   - Trace buildHeap step-by-step
   - Time: 15 min

**Phase 3b: Heap Sort Algorithm (25 min)**
1. **Read Section 3-5** (Algorithm + Complexity)
   - Full heapsort walkthrough
   - Critical insight: O(n) buildHeap, not O(n log n)
   - Why it works geometrically
   - Guaranteed O(n log n)
   - Time: 15 min

2. **Read Section 6** (Real Systems)
   - Dijkstra's algorithm uses heaps!
   - A* pathfinding
   - Task scheduling
   - Time: 10 min

**Phase 3c: Synthesis (10 min)**
1. Understand why heaps are slow in practice: 5 min
2. Answer Day 3 Q&A questions: 5 min

### Confidence Checkpoint
By end of Day 3:
- [ ] Can build heap from array
- [ ] Understand heapify-down operation
- [ ] Know buildHeap is O(n) insight
- [ ] Recognize Dijkstra dependency
- [ ] Rate confidence 3-4/5

**Time Actual:** __ / 75 min

---

## 📅 Phase 4: Hash Fundamentals (Thursday - Day 4)

**Goal:** Understand O(1) lookup, design hash functions, grasp load factor.

### 60-Minute Study Plan

**Phase 4a: Concept Shift (15 min)**
1. **Read Sections 1-2** (Why + What)
   - This is NOT sorting!
   - Different goal: instant lookup, not ordering
   - Fundamental shift in thinking
   - Time: 15 min

**Phase 4b: Hash Functions & Load Factor (25 min)**
1. **Read Sections 3-5** (How + Mechanics + Analysis)
   - Hash function properties
   - h(k) = k mod m concepts
   - Load factor α = n/m
   - Resizing strategy
   - Time: 15 min

2. **Read Section 8** (Birthday Paradox)
   - √m items cause collisions
   - Mathematical insight
   - Keep α < 0.75 to stay safe
   - Time: 10 min

**Phase 4c: Real Systems (15 min)**
1. **Read Section 6** (Real Systems)
   - Virtual memory (page tables)
   - Compiler symbol tables
   - Database indexes
   - CPU caches
   - Time: 15 min

**Phase 4d: Synthesis (5 min)**
1. Answer Day 4 Q&A questions: 5 min

### Confidence Checkpoint
By end of Day 4:
- [ ] Understand O(1) lookup via direct addressing
- [ ] Know hash function properties
- [ ] Understand load factor management
- [ ] Know birthday paradox probability
- [ ] Rate confidence 3-4/5

**Time Actual:** __ / 60 min

---

## 📅 Phase 5: Hash Implementation (Friday - Day 5)

**Goal:** Compare collision strategies, implement both, understand trade-offs.

### 75-Minute Study Plan

**Phase 5a: Chaining Strategy (25 min)**
1. **Read Sections 2-4** (What + How + Examples)
   - Linked list per slot
   - Insert, lookup, delete mechanics
   - Simple deletion (just remove from list)
   - Time: 15 min

2. **Read Section 5** (Complexity)
   - O(1 + α) expected lookup
   - With α = 0.75: ~1.75 comparisons
   - Scalable (can handle α > 1.0)
   - Time: 10 min

**Phase 5b: Open Addressing Strategy (25 min)**
1. **Read Sections 2-4** (What + How + Examples)
   - Single array, no pointers
   - Linear, quadratic, double hashing
   - Tombstones for deletion
   - Time: 15 min

2. **Read Section 5** (Complexity)
   - O(1/(1-α)) expected lookup
   - Must keep α < 0.75
   - Faster in practice (cache)
   - Complex deletion
   - Time: 10 min

**Phase 5c: Comparison & Choice (15 min)**
1. **Read Section 9** (Design Intuition)
   - When to use chaining
   - When to use open addressing
   - Tradeoffs: simple vs fast
   - Time: 10 min

2. **Read Section 6** (Real Systems)
   - Python uses open addressing
   - Java uses chaining
   - Why different choices?
   - Time: 5 min

**Phase 5d: Synthesis (5 min)**
1. Answer Day 5 Q&A questions: 5 min

### Confidence Checkpoint
By end of Day 5:
- [ ] Understand both chaining and open addressing
- [ ] Know when to use each
- [ ] Understand deletion challenges
- [ ] Know real-world choices (Python, Java)
- [ ] Rate confidence 3-4/5

**Time Actual:** __ / 75 min

---

## ⏱ Weekly Time Budget Summary

```
Day 1 (Elementary):    90 min
Day 2 (Merge/Quick):   90 min
Day 3 (Heap):          75 min
Day 4 (Hash I):        60 min
Day 5 (Hash II):       75 min
                       ────────
Subtotal:             390 min (6.5 hours)

Q&A Practice:         120 min (2 hours)
Implementation:       120 min (2 hours)
Review & Synthesis:    30 min
                       ────────
Total:               ~660 min (11 hours)
```

---

## 📖 Optimal Reading Path Per Day

**For each day, recommended reading order:**

1. **Section 1** (The Why) — Motivation
2. **Section 2** (The What) — Mental models first
3. **Section 4** (Visualization) — See concrete examples
4. **Section 3** (The How) — Now understand mechanics
5. **Section 5** (Analysis) — Complexity matters
6. **Section 6** (Real Systems) — Why you should care
7. **Sections 7-9** — Connections and intuition
8. **Section 8** (Theory) — Optional deep dive
9. **Section 10** (Questions) — Test understanding
10. **Section 11** (Hooks) — Remember it

**Why this order?** Build understanding gradually, not front-load theory.

---

## 🎯 Cross-Week Integration

### Prerequisite Knowledge Needed
- **Arrays & Indexing:** All algorithms use arrays
- **Linked Lists:** Chaining uses linked lists
- **Recursion:** Merge sort, quick sort, heaps
- **Complexity Analysis:** Essential for understanding

### Knowledge Transfer to Week 4
- **Two Pointers:** Works best on sorted arrays
- **Sliding Window:** Frequency counting uses hash tables
- **Prefix Sums:** Building on space-time trade-off concept

### Knowledge Transfer to Week 6
- **Dijkstra's Algorithm:** Uses heaps for priority queue
- **Graph Algorithms:** Often need hash tables for visited sets

### Knowledge Transfer to Week 11
- **Dynamic Programming:** Memoization uses hash tables
- **Optimization:** Sorting can optimize some DP problems

---

## ✅ Weekly Milestone Checklist

### After Wednesday (Sorting Complete)
- [ ] Understand O(n²) vs O(n log n)
- [ ] Know all 6 sorting algorithms
- [ ] Can implement merge sort from scratch
- [ ] Can implement quick sort from scratch
- [ ] Understand Master Theorem
- [ ] Know why hybrids (Timsort) work
- [ ] Can explain trade-offs

### After Friday (Hashing Complete)
- [ ] Know hash table O(1) average lookup
- [ ] Understand load factor and resizing
- [ ] Know both chaining and open addressing
- [ ] Can implement hash table from scratch
- [ ] Know when to use each technique
- [ ] Understand birthday paradox
- [ ] Know real-world implementations

### End of Week 3
- [ ] Answered all 50 Q&A questions
- [ ] Implemented all algorithms
- [ ] Created summary cards
- [ ] Can explain to someone else
- [ ] Confidence level 4-5/5 on all topics
- [ ] Ready for Week 4!

---

## 🚀 How to Recover if Behind

**If you're running behind:**

1. **Day 1-2 (Sorting):** Core, don't skip
   - Can reduce time by focusing on merge and quick sort
   - Bubble/insertion/selection less critical

2. **Day 3 (Heaps):** Important for graphs (Week 6)
   - Minimum: Understand concept, why O(n) buildHeap
   - Can skip implementation practice initially

3. **Day 4-5 (Hashing):** Both essential
   - Can't skip; hash tables everywhere
   - Focus on concepts over deep theory

**Catch-up strategy:** Focus on Sections 1-5, skip optional theory (Section 8) initially. Return to theory later if time.

---

## 🎓 Success Path

```
[START] → Read Day 1 → Trace examples → Code → Q&A
           ↓
           Read Day 2 → Trace examples → Code → Q&A
           ↓
           Read Day 3 → Trace examples → Code → Q&A
           ↓
           Read Day 4 → Trace examples → Code → Q&A
           ↓
           Read Day 5 → Trace examples → Code → Q&A
           ↓
           Review summary → Answer 50 Q → Teach someone
           ↓
           [MASTERY!]
           ↓
           Ready for Week 4
```

---

## 📌 Key Dates & Milestones

**Monday (Day 1):**
- [ ] Complete elementary sorts
- [ ] Understand O(n²) baseline

**Tuesday (Day 2):**
- [ ] Master divide-and-conquer
- [ ] Sorting knowledge complete

**Wednesday (Day 3):**
- [ ] Heap sort mastered
- [ ] Understand priority queues

**Thursday (Day 4):**
- [ ] Hash fundamentals done
- [ ] Conceptual shift from sorting to hashing

**Friday (Day 5):**
- [ ] Hash implementation complete
- [ ] Week 3 knowledge complete

**Weekend:**
- [ ] Review and practice
- [ ] Prepare for Week 4

---

## 💡 Pro Tips for Success

1. **Trace before you code**
   - Don't jump to implementation
   - Understanding by hand is essential
   - Code comes naturally after

2. **Do the Q&A questions**
   - Don't skip them!
   - They expose gaps in understanding
   - Better to find gaps during learning than in interview

3. **Implement in language you know**
   - Python, C++, Java, C# all work
   - Focus on understanding, not language syntax
   - Can always convert later

4. **Compare algorithms, don't just learn**
   - What's better and why?
   - When would you choose each?
   - This thinking matters more than details

5. **Connect to real systems**
   - Section 6 isn't optional—it's context
   - Knowing "Timsort uses insertion sort" helps you remember
   - Real uses are better than abstract theory

---

**Week 3 Roadmap Complete!** 🗺

**Ready to begin? Start with Day 1 material and follow the phases above.** 

**Estimated Total Time:** 6.5-11 hours (depending on depth)  
**Target Completion:** 1 week of focused study  
**Success Metric:** Confidence 4-5/5 on all topics + can explain to others

