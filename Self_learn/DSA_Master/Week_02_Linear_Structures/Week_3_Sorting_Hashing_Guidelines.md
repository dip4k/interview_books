# Week 3: Sorting & Hashing - Guidelines

**Week Focus:** Master sorting algorithms and understand hash tables deeply  
**Total Time Investment:** 12-14 hours (learning + practice)  
**Difficulty Level:** 🔴 Hard  
**Prerequisites:** Week 1-2 (Foundations, linear structures)

---

## 📅 Daily Breakdown & Time Allocation

| Day | Topic | Time | Key Outcomes |
|-----|-------|------|--------------|
| **1** | Elementary Sorts | 110 min | Bubble, insertion, selection; understand limits O(n²) |
| **2** | Merge Sort & Quick Sort | 120 min | Divide-and-conquer, O(n log n), stability, average vs worst case |
| **3** | Heap Sort & Variants | 110 min | Heapify, in-place sorting, comparison of all sorts |
| **4** | Hash Tables I | 115 min | Hash functions, collision theory, load factor, open addressing |
| **5** | Hash Tables II | 110 min | Chaining vs open addressing, real implementations, analysis |

**Total Core Learning:** ~565 minutes (9.4 hours)  
**Practice & Consolidation:** ~3-4 hours  

---

## 🎯 Week 3 Learning Objectives

### By Week End, You Should:

**Knowledge:**
- [ ] Know all major sorting algorithms and complexities
- [ ] Understand divide-and-conquer paradigm deeply
- [ ] Know stability in sorting and when it matters
- [ ] Understand hash functions and collision handling
- [ ] Know load factor and why it matters
- [ ] Understand hash table implementation deeply

**Skills:**
- [ ] Implement 6 sorting algorithms from scratch
- [ ] Implement binary heap (min and max)
- [ ] Implement hash table with chaining
- [ ] Implement hash table with open addressing
- [ ] Analyze hash function quality
- [ ] Choose optimal sort for constraints

**Application:**
- [ ] Optimize sorting for specific constraints
- [ ] Understand why certain sorts chosen in practice
- [ ] Use hashing for deduplication and caching
- [ ] Handle collisions in real implementations
- [ ] Combine sorting and hashing for complex problems

---

## 📚 Core Concepts Overview

### Sorting Algorithms

```
Elementary Sorts:
  - Bubble: O(n²) worst, O(n) best, O(1) space, stable
  - Selection: O(n²) all cases, O(1) space, unstable
  - Insertion: O(n²) worst, O(n) best, O(1) space, stable

Efficient Sorts:
  - Merge: O(n log n) all cases, O(n) space, stable, divide-and-conquer
  - Quick: O(n log n) average, O(n²) worst, O(log n) space, unstable
  - Heap: O(n log n) all cases, O(1) space, unstable, in-place

Key: Elementary for learning, efficient for real use
```

### Divide-and-Conquer

```
Pattern:
  1. Divide: Split problem into subproblems
  2. Conquer: Solve subproblems recursively
  3. Combine: Merge solutions together
  
Example: Merge sort divides array, sorts halves, merges sorted halves
Time: Usually O(n log n) for sorting
```

### Hash Tables

```
Concept: Map keys to values using hash function
Hash Function: key → index in hash table
Operations:
  - Insert: O(1) average, O(n) worst
  - Delete: O(1) average, O(n) worst
  - Lookup: O(1) average, O(n) worst
  
Worst case happens when collisions high (bad hash function)
```

### Collision Handling

```
Chaining:
  - Store list at each index
  - Insert: add to list O(1) to find, O(1) to add
  - Search: search list O(L) where L = list length
  - Space: O(n + m) where m = table size

Open Addressing:
  - Find another spot if occupied
  - Linear probing: try next index
  - Quadratic probing: try index + 1², + 2², ...
  - Double hashing: use second hash function
  - More space-efficient but complex
```

### Load Factor

```
Definition: α = n / m (items / table size)
Impact:
  - Low α: faster lookups, more space waste
  - High α: slower lookups, space efficient
  
Typical: Resize when α > 0.75 (double table size)
Result: Amortized O(1) operations
```

---

## 🔄 Recommended Learning Path

**Best Order to Study:**

1. **Day 1:** Elementary Sorts
   - Understand simple sorting concepts
   - Learn O(n²) behavior
   - Understand stability
   - Practice step-by-step visualization

2. **Day 2:** Divide-and-Conquer Sorts
   - Understand divide-and-conquer paradigm
   - Merge sort (guaranteed O(n log n))
   - Quick sort (average O(n log n), practical)
   - Compare worst vs average case

3. **Day 3:** Heap Sort & Comparison
   - Build heaps (min and max)
   - Understand in-place sorting
   - Compare all sorts: space, stability, worst case
   - Choose sort based on constraints

4. **Day 4:** Hash Tables I
   - Understand hash functions
   - Learn collision theory
   - Study load factor concept
   - Practice open addressing techniques

5. **Day 5:** Hash Tables II
   - Implement chaining thoroughly
   - Understand real-world hash tables
   - Analyze resize strategies
   - Practice hash table problems

**Why This Order?**
- Elementary sorts easiest to understand
- Divide-and-conquer more complex but cleaner
- Heap sort uses earlier data structure (heap)
- Hash tables completely different paradigm
- Second hash table day for depth

---

## ⚠️ Common Mistakes to Avoid

### Sorting

| Mistake | Fix |
|---------|-----|
| **Using O(n²) for large n** | Choose merge/quick/heap sort for n > 1000 |
| **Quick sort guaranteed O(n²)** | It's O(n log n) average, O(n²) worst case worst |
| **Merge sort in-place misconception** | Merge sort needs O(n) space, not O(1) |
| **Stability confusion** | Matters if you need original order preserved |
| **Forgetting to analyze actual problem** | n = 100? Maybe bubble fine. n = 1M? Never |

### Hashing

| Mistake | Fix |
|---------|-----|
| **Bad hash function** | Use built-in or proven function, not naive |
| **Ignoring collisions** | They WILL happen, must handle properly |
| **High load factor** | Resize when α > 0.75 to maintain O(1) |
| **Confusing chaining/open addressing** | Chaining: list at index, Open: find new index |
| **Assuming worst case impossible** | It happens! Understand when and why |

---

## 🎓 Practice Problems Guide

### Sorting Problems

**Easy:**
- Sort array of 0s and 1s
- Merge sorted arrays
- Check if array is sorted
- Time: 15-20 min

**Medium:**
- Kth largest element
- Merge intervals
- Top K frequent elements
- Time: 25-40 min

**Hard:**
- Reverse pairs
- Sliding window median
- Count of range sum
- Time: 45-60 min

### Hash Table Problems

**Easy:**
- Two sum
- Contains duplicate
- Valid anagram
- Time: 15-20 min

**Medium:**
- Group anagrams
- LRU cache
- Longest substring without repeating
- Time: 30-45 min

**Hard:**
- LFU cache
- All O(1) data structure
- Design key-value store
- Time: 60-90 min

**Sources:** LeetCode, GeeksforGeeks, InterviewBit

---

## 💼 Interview Preparation

### Common Week 3 Questions

**Sorting:**
- "Implement quicksort from scratch"
- "When would you use merge sort vs quicksort?"
- "How to optimize sorting with duplicates?"
- "Sort 1 million numbers with limited memory"
- "Kth largest element efficiently"

**Hashing:**
- "Implement hash table from scratch"
- "How to handle collisions?"
- "Design LRU cache"
- "Design LFU cache"
- "Two sum problem (hash table solution)"

**Trade-offs:**
- "Time vs space: sort vs hash trade-offs"
- "When is stable sorting important?"
- "Hash table worst case - what causes it?"

### Interview Tips
1. **Clarify problem:** "Stable? In-place? Memory limit?"
2. **Choose algorithm:** "I'll use merge sort because guaranteed O(n log n)"
3. **Discuss trade-offs:** "Quick sort faster average, merge sort guaranteed"
4. **Implement correctly:** "Hash function here, collision here"
5. **Test edge cases:** "Empty array, duplicates, single element"

---

## 🔗 Resources & References

### Online Platforms
- **LeetCode:** Sorting and hash table problems
- **GeeksforGeeks:** Algorithm tutorials with animations
- **Khan Academy:** Algorithm videos
- **InterviewBit:** Sorting challenges

### Visualization Tools
- **VisuAlgo:** https://www.cs.usfca.edu/~galles/visualization/ (Sorting)
- **Algorithm Visualizer:** https://algorithm-visualizer.org/
- **Sorting Visualizer:** https://www.cs.usfca.edu/~galles/visualization/ComparisonSort.html

### Recommended Books
- "Introduction to Algorithms" - CLRS (Chapter 2-3, 6-9, 11)
- "Cracking the Coding Interview" - Chapter 11 (Sorting)
- "The Algorithm Design Manual" - Skiena (Chapter 4)

---

## ✅ Assessment & Success Criteria

### Knowledge Check
- [ ] Know time/space complexity of all major sorts
- [ ] Understand divide-and-conquer paradigm
- [ ] Know stability definition and importance
- [ ] Understand hash function and collision handling
- [ ] Know load factor and resize strategy

### Practical Skills
- [ ] Implement 6 sorting algorithms
- [ ] Implement min and max heaps
- [ ] Implement hash table with chaining
- [ ] Implement hash table with open addressing
- [ ] Analyze hash function quality
- [ ] Choose optimal sort for problem

### Confidence Targets
| Topic | Target |
|---|---|
| Elementary Sorts | 5/5 |
| Merge Sort | 4-5/5 |
| Quick Sort | 4-5/5 |
| Heap Sort | 3-4/5 |
| Hash Fundamentals | 4/5 |
| Collision Handling | 3-4/5 |
| Overall Week 3 | 4/5 |

---

## 📊 Connection to Future Weeks

### Week 4: Problem-Solving Patterns
```
Week 3 Sorting (especially quicksort partitioning)
    ↓
Week 4 Two pointers requires sorted arrays
    ↓
Sorting expertise enables optimization patterns
```

### Week 5+: Advanced Algorithms
```
Weeks 1-3 Fundamentals, Structures, Sorting/Hashing
    ↓
Weeks 5+ Greedy, DP, Graphs (all combine with sorting/hashing)
    ↓
Mastery of Week 3 critical for advanced problems
```

### System Design
```
Week 3 Hash tables deep understanding
    ↓
Future: Design caches, databases, indexes
    ↓
Week 3 foundation crucial for system design interviews
```

---

## ❓ Frequently Asked Questions

### Q1: Do I really need to implement quicksort?

**A:** Yes! Shows understanding of partitioning, pivot selection, worst case. Quicksort interview question common.

### Q2: Merge sort vs quicksort - which is better?

**A:** Quick sort faster average (fewer moves), merge sort guaranteed O(n log n). Trade off: quick sort simpler, merge sort predictable.

### Q3: When would I use bubble sort in real code?

**A:** Rarely. But good for teaching and nearly-sorted data. Know it, don't use it unless required.

### Q4: Is my hash function good?

**A:** Uniform distribution across keys. Minimize collisions. Use built-in for safety. Interview: understand why function chosen.

### Q5: What load factor should I target?

**A:** Typical: α < 0.75. Less: space waste. More: collision slowdown. Resize when exceeded.

### Q6: Chaining vs open addressing?

**A:** Chaining simpler (just use list), open addressing more space efficient. Chaining typical in practice.

---

## 🎯 Before Moving to Week 4

**Checklist:**
- [ ] Implement all 6 major sorting algorithms
- [ ] Implement min and max heaps
- [ ] Implement hash table with chaining
- [ ] Implement hash table with open addressing
- [ ] Solve 20+ sorting problems
- [ ] Solve 15+ hash table problems
- [ ] Can choose optimal sort for constraints
- [ ] Overall confidence: 4/5 or higher

**If not ready:**
- Review weak algorithms
- Implement again from scratch
- Solve 10+ more practice problems per algorithm
- Don't rush to Week 4

---

## 📝 Week 3 Quick Summary

### Sorting Comparison

| Algorithm | Best | Average | Worst | Space | Stable |
|---|---|---|---|---|---|
| **Bubble** | O(n) | O(n²) | O(n²) | O(1) | Yes |
| **Selection** | O(n²) | O(n²) | O(n²) | O(1) | No |
| **Insertion** | O(n) | O(n²) | O(n²) | O(1) | Yes |
| **Merge** | O(n log n) | O(n log n) | O(n log n) | O(n) | Yes |
| **Quick** | O(n log n) | O(n log n) | O(n²) | O(log n) | No |
| **Heap** | O(n log n) | O(n log n) | O(n log n) | O(1) | No |

### Hash Table Operations

| Operation | Average | Worst | Notes |
|---|---|---|---|
| **Insert** | O(1) | O(n) | Good hash, low α |
| **Delete** | O(1) | O(n) | Good hash, low α |
| **Lookup** | O(1) | O(n) | Collision handling crucial |

---

**Status:** Week 3 Ready for Study ✓  
**Expected Completion:** 1-2 weeks focused study  
**Success Rate:** 80%+ with consistent practice  
**Cumulative Progress:** 45-50% of total curriculum

