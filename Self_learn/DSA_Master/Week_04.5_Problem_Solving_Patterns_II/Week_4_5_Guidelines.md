# Week 4.5 (Tier 1): Critical Problem-Solving Patterns — Guidelines

## 📅 Daily Breakdown & Time Allocation

**Total Week:** 12-14 hours (2.5-2.8 hours per day)

| Day | Topic | Time | Coverage |
|-----|-------|------|----------|
| **1** | Hash Map / Hash Set | 2.5h | 70% of problems! |
| **2** | Monotonic Stack | 2.5h | 20-30% stack problems |
| **3** | Merge Operations | 2.5h | 30% array/list problems |
| **4** | Partition + Kadane | 2.5h | 15% + 10% problems |
| **Weekend** | Integration & Review | 2h | Pattern combinations |

---

## 🎯 Learning Objectives

### By End of Week 4.5
- [ ] Master Hash Map/Set (70% coverage foundation!)
- [ ] Understand Monotonic Stack mechanics
- [ ] Know Merge operations thoroughly
- [ ] Implement Partition and Kadane from scratch
- [ ] Recognize Tier 1 patterns across problems
- [ ] Solve 50-60% of LeetCode medium problems

---

## 📚 Core Concepts Overview

**Concept 1: Hash-Based Lookup**  
O(1) membership checking and frequency counting. Replaces O(n) searches.

**Concept 2: Monotonic Invariants**  
Maintaining ordered stack enables O(n) next greater/smaller in single pass.

**Concept 3: Two-Pointer Merging**  
Combining sorted structures without resorting, leveraging monotonicity.

**Concept 4: In-Place Segregation**  
Partitioning without extra space using pointer movement and swapping.

**Concept 5: DP as Greedy Choice**  
Kadane shows DP can have O(1) space by tracking only current decision.

---

## 🔄 Recommended Learning Path

**Morning (90 min):**
- Read daily instructional file (all 11 sections)
- Trace examples by hand
- Understand core mechanics

**Afternoon (60 min):**
- Answer Socratic questions
- Solve 5-6 practice problems
- Implement pattern from scratch

**Evening (30 min):**
- Review checklist
- Rate confidence (1-5)
- Compare to similar patterns

---

## ⚠️ Common Mistakes to Avoid

**Mistake 1: Hash only gives O(1)**  
Reality: Average O(1), worst O(n). Load factor and collisions matter.

**Mistake 2: Monotonic Stack is magic**  
Reality: Understand WHY popping works. It finds the answer for popped elements.

**Mistake 3: Merge only for sorting**  
Reality: Merge is tool for combining ANY sorted structures (lists, intervals).

**Mistake 4: Partition is just quicksort**  
Reality: Partition has broader use (Dutch flag, segregation problems).

**Mistake 5: Kadane is only for max subarray**  
Reality: Template works for max product, longest subarray, many variants.

---

## 🎓 Practice Problems Guide

### Hash Map/Set (10+ problems)
1. Two Sum
2. Contains Duplicate
3. Valid Anagram
4. Group Anagrams
5. Two Sum II (sorted)
6. Majority Element
7. Intersection of Arrays
8. Happy Number
9. Isomorphic Strings
10. Find All Duplicates

### Monotonic Stack (8+ problems)
1. Next Greater Element
2. Daily Temperatures
3. Trapping Rain Water
4. Largest Rectangle in Histogram
5. Stock Span
6. Remove K Digits
7. Validate Stack Sequences
8. Next Greater Element II

### Merge Operations (6+ problems)
1. Merge Sorted Array
2. Merge Sorted List
3. Merge K Sorted Lists
4. Merge Intervals
5. Interval List Intersections
6. Largest Merge of Two Numbers

### Partition (4+ problems)
1. Move Zeroes
2. Partition Equal Subset
3. Dutch National Flag
4. Separate The Numbers

### Kadane's Algorithm (4+ problems)
1. Maximum Subarray
2. Maximum Product Subarray
3. Largest Sum of Averages
4. House Robber

---

## 💼 Interview Preparation

**Tier 1 Coverage:** 70-80% of interview problems (combined with Weeks 1-4)

**Key Interview Patterns:**
- Hash: appears in 40% of problems
- Monotonic: appears in 15% of hard problems
- Merge: appears in 20% of array problems
- Partition: appears in 10% of problems
- Kadane: appears in 5-10% of DP problems

**Interview Strategy:**
1. Identify problem type (hash, stack, merge, etc.)
2. Default to Tier 1 pattern
3. Explain time/space trade-offs
4. Code and test edge cases

---

## 📊 Connection to Weeks 5+

**Week 5 (Trees):** Tree traversals use stacks/queues (extension of stack concepts)

**Week 6-7 (Graphs):** BFS/DFS use hash sets for visited tracking

**Week 11 (DP):** Memoization uses hash maps (Kadane is simple DP)

---

## ❓ Frequently Asked Questions

**Q: Is Tier 1 enough for interview?**
A: 70-80% coverage. Combine with basic weeks 1-4 for 50-60% total.

**Q: How long until patterns feel automatic?**
A: 20-30 problems per pattern, ~2 weeks of daily practice.

**Q: Can I skip hash and use other methods?**
A: Possible but inefficient. Hash is essential foundation.

**Q: Do all problems fit exactly one pattern?**
A: Most do. Some combine patterns (hash + heap, hash + DP).

---

**Before Week 5:**
- [ ] Rate 4/5 or higher on all 5 days
- [ ] Can recognize pattern instantly
- [ ] Can solve variants without hints

