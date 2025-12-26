# Week 3: Sorting & Search Fundamentals - Guidelines

**Week Focus:** Master sorting algorithms, search techniques, and complexity analysis  
**Total Time Investment:** 10-12 hours (learning + practice)  
**Difficulty Level:** 🟡 Medium  
**Prerequisites:** Week 1-2 (Arrays, data structures)

---

## 📅 Daily Breakdown & Time Allocation

| Day | Topic | Time | Key Outcomes |
|-----|-------|------|--------------|
| **1** | Sorting Fundamentals & Bubble/Selection Sort | 95 min | Comparison-based sorting, O(n²) algorithms |
| **2** | Merge Sort & Quick Sort | 100 min | Divide-and-conquer, O(n log n), stability |
| **3** | Heap Sort & Counting/Radix Sort | 90 min | Heap-based, non-comparison sorts |
| **4** | Linear Search & Binary Search Intro | 85 min | Search algorithms, time complexity |
| **5** | Sorting Integration & Problem-Solving | 80 min | Choose right sort, optimize problems |

**Total Core Learning:** ~450 minutes (7.5 hours)  
**Practice & Consolidation:** ~4-5 hours  

---

## 🎯 Week 3 Learning Objectives

### By Week End, You Should:

**Knowledge:**
- [ ] Understand sorting comparison
- [ ] Know O(n²) vs O(n log n) sorting
- [ ] Understand stability in sorting
- [ ] Know when to use each algorithm
- [ ] Understand search complexity

**Skills:**
- [ ] Implement Bubble, Selection, Insertion Sort
- [ ] Implement Merge Sort, Quick Sort
- [ ] Implement Heap Sort
- [ ] Implement Binary Search
- [ ] Analyze algorithm efficiency

**Application:**
- [ ] Choose optimal sort for constraint
- [ ] Optimize sorting problems
- [ ] Use binary search efficiently
- [ ] Combine with data structures
- [ ] Solve complex sorting problems

---

## 📚 Core Concepts Overview

### Sorting Algorithms Comparison

| Algorithm | Time Best | Time Avg | Time Worst | Space | Stable |
|-----------|-----------|----------|-----------|-------|--------|
| **Bubble** | O(n) | O(n²) | O(n²) | O(1) | Yes |
| **Selection** | O(n²) | O(n²) | O(n²) | O(1) | No |
| **Insertion** | O(n) | O(n²) | O(n²) | O(1) | Yes |
| **Merge** | O(n log n) | O(n log n) | O(n log n) | O(n) | Yes |
| **Quick** | O(n log n) | O(n log n) | O(n²) | O(log n) | No |
| **Heap** | O(n log n) | O(n log n) | O(n log n) | O(1) | No |

### Stability
```
Stable: Relative order of equal elements preserved
Example: [(1,a), (2,b), (1,c)] after sort → [(1,a), (1,c), (2,b)]
Merge Sort: Stable
Quick Sort: Unstable (depends on partition)
```

---

## 🔄 Recommended Learning Path

**Best Order to Study:**

1. **Day 1:** Sorting Fundamentals
   - Understand comparison-based sorting
   - Simple O(n²) algorithms (Bubble, Selection)
   - How sorting works conceptually

2. **Day 2:** Efficient Sorting
   - Merge sort (divide-and-conquer)
   - Quick sort (average O(n log n))
   - Why faster than O(n²)

3. **Day 3:** Specialized Sorts
   - Heap sort (uses heap structure)
   - Non-comparison sorts (Counting, Radix)
   - When to use each type

4. **Day 4:** Search Algorithms
   - Linear search (O(n))
   - Binary search (O(log n))
   - Binary search variants

5. **Day 5:** Integration
   - Optimize sorting problems
   - Combine sort with other techniques
   - Choose right algorithm

**Why This Order?**
- Simple sorts build intuition
- Efficient sorts teach divide-and-conquer
- Specialized sorts show flexibility
- Search builds on sorted data
- Integration uses everything

---

## ⚠️ Common Mistakes to Avoid

### Sorting-Related

| Mistake | Fix |
|---------|-----|
| **Using O(n²) when O(n log n) available** | Choose Merge/Quick/Heap Sort |
| **Not handling duplicate elements** | Test with duplicates, ensure stability if needed |
| **Quicksort worst case O(n²)** | Use median-of-3 or random pivot |
| **Forgetting merge sort uses O(n) space** | Trade-off: stable sort needs space |
| **Confusing in-place requirement** | Merge sort not in-place, others are |

### Search-Related

| Mistake | Fix |
|---------|-----|
| **Using binary search on unsorted** | Must sort first (or verify sorted) |
| **Off-by-one in binary search** | Use left ≤ right, mid = (left+right)//2 |
| **Forgetting to check boundaries** | Always check left ≤ right condition |

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
- Time: 45-60 min

### Search Problems

**Easy:**
- Binary search
- Search insert position
- Peak element
- Time: 15-25 min

**Medium:**
- Search in rotated array
- Find first/last position
- Search 2D matrix
- Time: 25-40 min

**Sources:** LeetCode, GeeksforGeeks, HackerRank

---

## 💼 Interview Preparation

### Common Week 3 Questions

**Sorting:**
- "When would you use Quicksort vs Mergesort?"
- "How to optimize sorting with duplicates?"
- "Implement quicksort from scratch"
- "Sort 1 million numbers with limited memory"

**Search:**
- "Implement binary search"
- "Find element in rotated sorted array"
- "Search in 2D sorted matrix"

**Optimization:**
- "Kth largest element efficiently"
- "Median of two sorted arrays"
- "Sort by frequency"

### Interview Tips
1. **Clarify constraints:** "In-place? Stable? Memory limit?"
2. **Justify choice:** "I chose Mergesort because stable"
3. **Discuss trade-offs:** "Quicksort faster average, Mergesort worst-case"
4. **Test edge cases:** "Empty array, one element, duplicates"
5. **Explain complexity:** "Time O(n log n), space O(n) for merge sort"

---

## 🔗 Resources & References

### Online Platforms
- **LeetCode:** Sorting and searching problems
- **GeeksforGeeks:** Algorithm tutorials with animations
- **Khan Academy:** Algorithm videos

### Visualization Tools
- **VisuAlgo:** https://www.cs.usfca.edu/~galles/visualization/ (Sort, Search)
- **Algorithm Visualizer:** https://algorithm-visualizer.org/

### Recommended Books
- "Introduction to Algorithms" - CLRS (Chapter 6-9)
- "Cracking the Coding Interview" - Chapter 11
- "The Algorithm Design Manual" - Skiena (Chapter 4)

---

## ✅ Assessment & Success Criteria

### Knowledge Check
- [ ] Know time complexity of each sort
- [ ] Understand divide-and-conquer concept
- [ ] Know when sorting is stable
- [ ] Understand binary search requirements
- [ ] Can choose optimal algorithm

### Practical Skills
- [ ] Implement 6 sorting algorithms
- [ ] Implement binary search
- [ ] Analyze algorithm efficiency
- [ ] Optimize sorting problems
- [ ] Handle edge cases

### Confidence Targets
| Algorithm | Target |
|-----------|--------|
| O(n²) Sorts | 5/5 |
| Mergesort | 4-5/5 |
| Quicksort | 4/5 |
| Heap Sort | 3-4/5 |
| Binary Search | 4-5/5 |
| Integration | 3-4/5 |
| Overall Week 3 | 4/5 |

---

## 📊 Connection to Future Weeks

### Week 4: Optimization Uses Sorting
```
Week 3 Sorting
    ↓
Week 4 Two pointers requires sorted array
    ↓
Must understand sorting for optimization
```

### Week 4.5: Binary Search Enhancement
```
Week 3 Binary search intro
    ↓
Week 4.5 Advanced binary search patterns
    ↓
Foundation from Week 3 essential
```

### Week 5+: Advanced Algorithms
```
Weeks 1-3 Fundamentals, Data Structures, Sorting/Search
    ↓
Weeks 5+ Greedy, DP, Graphs (often combined with sorting)
    ↓
Mastery of sorting critical for success
```

---

## ❓ Frequently Asked Questions

### Q1: Why learn simple O(n²) sorts if O(n log n) exist?
**A:** Understanding basics helps understanding advanced. Plus, O(n²) is acceptable for small n (< 1000).

### Q2: When would you use Bubble sort in real code?
**A:** Rarely. But if nearly sorted, Bubble/Insertion better. Good for teaching stability concept.

### Q3: Quicksort O(n²) worst case - is it acceptable?
**A:** With random pivot or median-of-3, worst case unlikely. Trade-off: simpler implementation vs guaranteed O(n log n).

### Q4: Do I need to memorize all sorts?
**A:** No. Understand logic. Interview: implement 2-3 well rather than all poorly.

### Q5: How to choose sort in interview?
**A:** Ask: "Stable needed?" (use Merge), "In-place?" (use Quick), "Worst-case guaranteed?" (use Merge/Heap)

### Q6: Binary search vs linear for small arrays?
**A:** Linear faster for very small (< 100). Binary better for large. Consider setup cost.

---

## 🎯 Before Moving to Week 4

**Checklist:**
- [ ] Implement 6 sorting algorithms
- [ ] Implement binary search (3+ variants)
- [ ] Solve 15+ sorting problems
- [ ] Solve 10+ search problems
- [ ] Can choose optimal sort for constraint
- [ ] Understand trade-offs (time, space, stability)
- [ ] Overall confidence: 4/5 or higher

**If not ready:**
- Implement more sorts
- Solve more practice problems
- Don't rush Week 4

---

## 📝 Week 3 Quick Summary

| Algorithm | Best | Avg | Worst | Space | Notes |
|-----------|------|-----|-------|-------|-------|
| Bubble | O(n) | O(n²) | O(n²) | O(1) | Nearly sorted |
| Selection | O(n²) | O(n²) | O(n²) | O(1) | Min swaps |
| Merge | O(n log n) | O(n log n) | O(n log n) | O(n) | Stable, guaranteed |
| Quick | O(n log n) | O(n log n) | O(n²) | O(log n) | Fast average |
| Heap | O(n log n) | O(n log n) | O(n log n) | O(1) | In-place |

---

**Status:** Week 3 Ready for Study ✓  
**Expected Completion:** 1 week focused study  
**Success Rate:** 85%+ with consistent practice  

