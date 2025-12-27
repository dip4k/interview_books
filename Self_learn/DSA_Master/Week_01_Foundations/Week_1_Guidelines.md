# Week 1: Foundations - Guidelines

**Week:** 1 | **Week Title:** Foundations  
**Goal:** Understand how computers work and measure algorithm efficiency  
**Duration:** 5 days (90-120 min each) + 3-5 hours practice  
**Difficulty:** 🟡 Medium (Easy concepts, Medium depth)

---

## 1️⃣ Daily Breakdown & Time Allocation

| Day | Topic | Core Time | Practice | Total |
|-----|-------|-----------|----------|-------|
| **1** | RAM Model & Pointers | 90 min | 60 min | 2.5 hrs |
| **2** | Asymptotic Analysis | 100 min | 60 min | 2.5 hrs |
| **3** | Space Complexity | 90 min | 45 min | 2.25 hrs |
| **4** | Recursion I | 100 min | 75 min | 3 hrs |
| **5** | Recursion II | 120 min | 90 min | 3.5 hrs |
| **Integration** | Weekly synthesis | - | 120 min | 2 hrs |
| **TOTAL** | **Week 1** | **~500 min** | **~450 min** | **~15 hrs** |

---

## 2️⃣ Learning Objectives

### Knowledge (Understand)
- [ ] Explain how RAM model addresses memory
- [ ] Define Big-O, Omega, Theta notation correctly
- [ ] Distinguish time complexity from space complexity
- [ ] Identify base cases and recursive calls
- [ ] Analyze recurrence relations

### Skills (Apply)
- [ ] Count operations to derive time complexity
- [ ] Identify space usage in algorithms
- [ ] Trace recursive algorithms by hand
- [ ] Convert non-tail recursion to tail-recursive form
- [ ] Apply memoization to optimize recursive solutions

### Application (Create/Design)
- [ ] Choose between arrays, lists based on operations
- [ ] Predict algorithm performance without running
- [ ] Design recursive solutions to problems
- [ ] Optimize naive recursive algorithms
- [ ] Reason about memory constraints

---

## 3️⃣ Core Concepts Overview

**Concept 1: RAM Model**
- Memory is linear, addressable (0, 1, 2, ...)
- Variables have addresses; pointers store addresses
- Dereferencing (*ptr) follows the address
- Pointer arithmetic scales by sizeof(element_type)
- Cache locality affects real-world performance

**Concept 2: Asymptotic Analysis**
- Big-O measures worst-case growth rate
- Constants and lower-order terms ignored
- Hierarchy: O(1) < O(log n) < O(n) < O(n²) < O(2^n)
- Algorithm choice depends on input size

**Concept 3: Space Complexity**
- Measures extra memory beyond input
- Stack space from recursion depth
- Heap allocations from dynamic memory
- Trade space for time (indexing, memoization)

**Concept 4: Recursion**
- Function calls itself on smaller problem
- Must have base case (stopping condition)
- Stack frames accumulate → call stack depth = space
- Time = work per call × number of calls

**Concept 5: Advanced Recursion**
- Tail recursion: optimizes to O(1) space if compiler supports
- Memoization: caching eliminates recomputation
- Mutual recursion: functions call each other (parsing)

---

## 4️⃣ Recommended Learning Path

### Suggested Order (Same as Days 1-5)
1. Start with **RAM Model** (Day 1) — foundation for all complexity analysis
2. Then **Asymptotic Analysis** (Day 2) — how to measure algorithms
3. Then **Space Complexity** (Day 3) — measures memory like Big-O measures time
4. Then **Recursion I** (Day 4) — applying complexity analysis to recursive problems
5. Finally **Recursion II** (Day 5) — optimizing recursive solutions

**Reasoning:**
- Days 1-3 are conceptual foundations (how computers work)
- Days 4-5 apply these concepts (recursion examples)
- Each day builds on previous knowledge

---

## 5️⃣ Common Mistakes to Avoid

| Mistake | Why It's Wrong | Fix |
|---------|-----------------|-----|
| Ignoring constants | For n=100, 1000n might beat 0.5n² | Count operations precisely initially |
| Confusing Big-O with actual time | O(n) doesn't mean "fast" | Remember: constants matter in practice |
| Assuming O(1) is always instant | Cache misses make it slow | Reason about cache locality |
| Forgetting recursion has space cost | Stack depth = O(n) is huge | Always count call stack depth |
| Trying to memoize everything | Caching costs space | Only memoize expensive subproblems |
| Assuming tail-call optimization exists | Python and Java don't do it | Verify with your language |
| Not considering base cases | Infinite recursion → crash | Always define base case first |

---

## 6️⃣ Practice Problems Guide

### Level 1: Foundational (Easy)
- [ ] Implement factorial iteratively and recursively
- [ ] Count operations in simple loops (O(n), O(n²))
- [ ] Calculate pointer addresses given memory layout
- [ ] Identify Big-O of simple functions (Best/Avg/Worst)
- [ ] Trace array sum recursion by hand

**Resources:**
- LeetCode: Easy tag, "Recursion" problems
- HackerRank: Basic recursion practice
- Project Euler: Math-heavy but good for recursion

### Level 2: Intermediate (Medium)
- [ ] Analyze binary search recurrence (T(n) = T(n/2) + O(1))
- [ ] Convert factorial to tail-recursive form
- [ ] Apply memoization to Fibonacci
- [ ] Trace merge sort, analyze O(n log n)
- [ ] Implement power(x, n) recursively

**Resources:**
- LeetCode Medium: "Recursion", "Memoization"
- Algorithm textbooks (CLRS, Algo Design Manual)
- YouTube: Abdul Bari, MIT OpenCourseWare lectures

### Level 3: Advanced (Hard)
- [ ] Analyze complex recurrence relations (Master Theorem)
- [ ] Optimize mutual recursion (parsing)
- [ ] Implement backtracking with pruning
- [ ] Recognize optimization opportunities
- [ ] Debug stack overflow in recursion

**Resources:**
- CLRS (Introduction to Algorithms)
- LeetCode Hard tag
- Codeforces problems tagged "Recursion"

---

## 7️⃣ Interview Preparation

### Common Interview Questions

**On RAM Model & Pointers:**
- "Explain what a pointer is and how dereferencing works"
- "Why does array access beat linked list access?" (cache locality)
- "How would you implement a memory pool?"

**On Complexity Analysis:**
- "What's the time and space complexity of [algorithm]?"
- "How would you optimize this to O(n) time?"
- "Can you trade space for time here?"

**On Recursion:**
- "Can you solve this recursively?"
- "What's the recurrence relation? Solve it."
- "Why might recursion fail here? How would you fix it?"
- "How many times is this subproblem computed?" (optimization)

**Example Interview Problem:**
```
Q: Implement power(x, n) where n can be negative.
   Optimize for large n.

Analysis:
- Naive: power(x, n) = x * power(x, n-1) → O(n) time
- Optimized: power(x, n) = power(x, n/2) * power(x, n/2) → O(log n) time
- Handle negative: 1/power(x, -n)
- Handle memoization: store previously computed powers
```

---

## 8️⃣ Resources & References

### Books
- **"Introduction to Algorithms" (CLRS):** Chapters 1-3 (complexity), Chapter 4 (recurrence)
- **"Algorithm Design Manual" (Skiena):** Chapters 2 (analysis), 5 (recursion)

### Online Courses
- **MIT 6.006 (Introduction to Algorithms):** Lectures on complexity, recursion
- **Coursera Data Structures & Algorithms (Levin):** Foundations part
- **Abdul Bari (YouTube):** Asymptotic analysis, recursion lectures

### Practice Platforms
- **LeetCode:** Filter by "Recursion", "Memoization"
- **HackerRank:** Recursion tutorial + practice
- **Project Euler:** Math problems requiring recursion

### Visualization Tools
- **VisuAlgo.net:** Algorithm visualization (complexity examples)
- **Recursion Visualizer:** Step through recursive calls
- **Big-O Cheat Sheet:** https://www.bigocheatsheet.com/

---

## 9️⃣ Assessment & Success Criteria

### Knowledge Check (Self-Assessment)

Rate yourself 1-5 on each:

**Competency** | **Confidence** |
|---|---|
| Explain RAM model and pointers | ___ / 5 |
| Derive Big-O from algorithm code | ___ / 5 |
| Analyze space complexity | ___ / 5 |
| Write recursive solutions | ___ / 5 |
| Optimize recursion (tail, memoization) | ___ / 5 |

**Target:** 4/5 on all before moving to Week 2

### Practical Assessment

- [ ] Can trace pointer arithmetic for array indexing
- [ ] Can count operations and derive O(n²) from code
- [ ] Can identify call stack depth for recursion
- [ ] Can implement tail-recursive factorial
- [ ] Can add memoization to slow recursive function

---

## 🔟 Connection to Future Weeks

**Week 2 (Linear Structures):** Apply complexity analysis to arrays, lists, stacks, queues
- Big-O analysis tells us arrays are O(1) access, lists are O(n) access
- Recursion appears in linked list traversal

**Week 3 (Sorting & Hashing):** Recursion and complexity essential
- Merge sort: recursive divide-and-conquer
- Quicksort: recursive partitioning
- Analyzing O(n log n) complexity

**Week 4 (Problem-Solving Patterns):** Recursion in patterns
- Two pointers, sliding window often implemented recursively
- Cycle detection uses recursion (DFS)

**Week 4.5+ (TIER 1):** Memoization heavily used
- Hash Map problems: memoize lookups
- Dynamic programming: recursive + memoization

---

## 1️⃣1️⃣ Frequently Asked Questions

**Q: Why do I need to understand RAM model? Can't I just use Big-O?**
A: Big-O is incomplete. Cache misses, pointer dereferences, and memory allocation affect real performance. Understanding RAM model explains *why* Big-O matters.

**Q: Will my language optimize tail recursion?**
A: Scheme: Yes (guaranteed). Java, C++: Sometimes (depends on flags). Python: No (by design). Check your language's documentation.

**Q: Isn't memoization just caching? Why the fancy name?**
A: Yes, they're the same. "Memoization" emphasizes caching function results in dynamic programming; "caching" is broader (cache hardware, software caches, etc.).

**Q: When should I use recursion vs iteration?**
A: Recursion shines for tree/graph problems and divide-and-conquer. Use iteration for simple loops. If recursion gets deep (n > 10,000), convert to iteration.

**Q: How do I know if my algorithm is O(n²)?**
A: Count nested loops. Two loops over n = O(n²). One loop over n in loop over n = O(n²). One loop over n, one over 100 = O(n). Constants don't matter for Big-O.

---

## 1️⃣2️⃣ Before Moving to Week 2

### Checklist (Must Complete)
- [ ] Completed all 5 daily instructional files
- [ ] Understand RAM model (pointers, dereferencing, cache)
- [ ] Confidently derive Big-O from code
- [ ] Know what O(1), O(n), O(n²), O(2^n) mean in practice
- [ ] Can write and trace recursive algorithms
- [ ] Understand tail recursion and memoization

### Recommended Review
- [ ] Revisit Day 1 if you don't understand pointers
- [ ] Revisit Day 2 if Big-O notation feels confusing
- [ ] Revisit Days 4-5 if recursion is shaky
- [ ] Practice 5-10 recursion problems before moving on

### Red Flags (Seek Help)
- ❌ "I don't understand what a pointer is"
- ❌ "I can't derive Big-O from code"
- ❌ "Recursion always confuses me"
- ❌ "I don't see why space complexity matters"

---

## 1️⃣3️⃣ Week 1 Quick Summary Table

| Topic | Key Insight | Complexity Formula |
|-------|-------------|-------------------|
| RAM | Memory is addressable; pointers store addresses | Access: O(1) |
| Big-O | Measures growth rate; constants irrelevant | Compare O(n) vs O(n²) |
| Space | Stack grows with recursion; heap with allocation | Depth O(n), space O(n) |
| Recursion | Base case + recursive case; trust the recursion | T(n) = T(n-1) + O(1) |
| Optimization | Tail recursion → O(1) space; memoization → less recomputation | 2^n → n with memo |

---

## 1️⃣4️⃣ Status & Next Steps

**Week 1 Status:** ✅ COMPLETE

**What You've Learned:**
- Foundational concepts: RAM, Big-O, space, recursion
- Practical optimization techniques
- How to analyze algorithms theoretically and practically

**Next:** Week 2 (Linear Structures) applies these foundations to arrays, lists, stacks, queues, and binary search.

**Action:** Choose 5-10 practice problems above, complete them, then move to Week 2.

