# Week 4: Problem-Solving Patterns - Guidelines

**Week Focus:** Learn systematic techniques for solving many problem types using optimization patterns  
**Total Time Investment:** 12-14 hours (learning + practice)  
**Difficulty Level:** 🔴 Hard  
**Prerequisites:** Week 1-3 (Foundations, structures, sorting)

---

## 📅 Daily Breakdown & Time Allocation

| Day | Topic | Time | Key Outcomes |
|-----|-------|------|--------------|
| **1** | Two Pointers | 110 min | Strategy, when/why it works, O(n) on sorted data |
| **2** | Sliding Window (Fixed) | 105 min | Fixed-size window over array, moving average concept |
| **3** | Sliding Window (Variable) | 110 min | Dynamic window, expand/shrink, optimization |
| **4** | Prefix Sums | 100 min | Trade space for time, range queries, 2D extension |
| **5** | Cycle Detection | 100 min | Floyd's algorithm, graph cycles, advanced applications |

**Total Core Learning:** ~525 minutes (8.75 hours)  
**Practice & Consolidation:** ~4-5 hours  

---

## 🎯 Week 4 Learning Objectives

### By Week End, You Should:

**Knowledge:**
- [ ] Know when each technique applies (sorted vs unsorted, etc)
- [ ] Understand complexity difference vs naive approach
- [ ] Know space vs time tradeoffs
- [ ] Recognize technique patterns in new problems
- [ ] Understand how techniques synergize

**Skills:**
- [ ] Implement two pointers (converging, chasing, etc)
- [ ] Implement sliding window (fixed and variable)
- [ ] Build and use prefix sum arrays
- [ ] Implement Floyd's cycle detection
- [ ] Combine multiple techniques

**Application:**
- [ ] Recognize technique in disguised problems
- [ ] Choose optimal approach for constraints
- [ ] Handle edge cases and duplicates
- [ ] Integrate multiple patterns
- [ ] Optimize from naive O(n²) to O(n)

---

## 📚 Core Concepts Overview

### Two Pointers

```
Pattern: Two indices starting from opposite ends or same side
When: Sorted arrays, find pairs/elements
How: Converging based on comparison

Example: Find two numbers that sum to target
  Array: [1, 3, 5, 7, 9]
  Start: left=0 (value 1), right=4 (value 9)
  1+9=10 > 8? Move right pointer left
  1+7=8 == 8? Found!
  
Complexity: O(n) time, O(1) space vs O(n²) naive
```

### Sliding Window (Fixed)

```
Pattern: Window of fixed size moves through array
When: Subarray of size k with property (max, min, sum, etc)

Example: Maximum sum of 3 consecutive elements
  Array: [1, 3, -1, -3, 5, 3, 6, 7]
  Window size: 3
  Windows: [1,3,-1], [3,-1,-3], [-1,-3,5], ...
  
Complexity: O(n) with incremental update vs O(nk) naive
```

### Sliding Window (Variable)

```
Pattern: Expand window until condition met, shrink until not
When: Subarray with property (at least k elements, sum > X, etc)

Example: Longest substring with at most 2 distinct chars
  Expand right to add char
  If > 2 distinct, shrink left to remove char
  Track maximum window seen
  
Complexity: O(n) because each element touched ≤ 2 times
```

### Prefix Sums

```
Pattern: Precompute cumulative sums for O(1) range queries
When: Multiple range queries on static array

Build: prefix[i] = sum of arr[0..i-1]
Query: sum(l,r) = prefix[r+1] - prefix[l]

Time: O(n) build + O(1) per query vs O(n) per query
Space: O(n) extra
```

### Floyd's Cycle Detection

```
Pattern: Two pointers at different speeds
When: Detect cycle in linked list or array

Tortoise (slow): moves 1 step
Hare (fast): moves 2 steps
If cycle: they meet inside cycle

Example: Find start of cycle in linked list
  Phase 1: Detect cycle (slow and fast meet)
  Phase 2: Find entry point (reset slow to head, move both 1 step)
  
Complexity: O(n) time, O(1) space (no hash table)
```

---

## 🔄 Recommended Learning Path

**Best Order to Study:**

1. **Day 1:** Two Pointers
   - Understand converging from ends
   - Learn sorted requirement
   - Practice movement strategy
   - Solve basic pairs problems
   - Extension: chasing pointers

2. **Day 2:** Sliding Window (Fixed)
   - Understand fixed-size window
   - Learn incremental updates
   - Practice tracking sum/max/min
   - Avoid O(nk) naively

3. **Day 3:** Sliding Window (Variable)
   - Understand expand/shrink logic
   - Practice condition checking
   - Track maximum window
   - Extend to 2-pointer integration

4. **Day 4:** Prefix Sums
   - Build prefix sum array
   - Use for range queries
   - Extend to 2D
   - Handle prefix in problems

5. **Day 5:** Cycle Detection & Integration
   - Floyd's algorithm fundamentals
   - Detect and find cycle
   - Combine with other patterns
   - Solve complex integrated problems

**Why This Order?**
- Two pointers most intuitive
- Sliding window extends thinking
- Prefix sums introduces preprocessing
- Floyd's algorithm more specialized
- Integration shows synergies

---

## ⚠️ Common Mistakes to Avoid

### Two Pointers

| Mistake | Fix |
|---------|-----|
| **Forgetting sorted requirement** | Must sort first if unsorted |
| **Wrong pointer movement** | Think about which to move for target |
| **Off-by-one errors** | Use left < right, check boundaries |
| **Not finding all pairs** | Ensure complete iteration |

### Sliding Window (Fixed)

| Mistake | Fix |
|---------|-----|
| **Not maintaining exact size** | Remove from left when adding to right |
| **Wrong incremental update** | Metric must update O(1) when element added/removed |
| **Missing edge cases** | Array smaller than window size |

### Sliding Window (Variable)

| Mistake | Fix |
|---------|-----|
| **Condition not incrementally checkable** | Must be able to check in O(1) |
| **Shrinking logic backwards** | Shrink when invalid, stop when valid |
| **Forgetting to track answer** | Update answer before shrinking |

### Prefix Sums

| Mistake | Fix |
|---------|-----|
| **Index confusion** | prefix[i] = sum of arr[0..i-1], off-by-one crucial |
| **Not rebuilding on updates** | Prefix sums only for static arrays |
| **Query formula wrong** | sum(l,r) = prefix[r+1] - prefix[l] |

### Floyd's Algorithm

| Mistake | Fix |
|---------|-----|
| **Skipping slow-fast initialization** | Both start at head for linked list |
| **Phase 2 wrong** | Reset one pointer to head, move both 1 step |
| **Ignoring no-cycle case** | Fast pointer reaches null = no cycle |

---

## 🎓 Practice Problems Guide

### Two Pointers

**Easy:**
- Two sum II (sorted array)
- Valid palindrome
- Container with most water
- Time: 15-25 min

**Medium:**
- 3Sum
- 3Sum closest
- Remove duplicates sorted array II
- Time: 25-40 min

### Sliding Window (Fixed)

**Easy:**
- Max average subarray
- Number of sub-arrays of size k
- Time: 15-20 min

**Medium:**
- Sliding window maximum
- Longest substring with k distinct
- Time: 30-40 min

### Sliding Window (Variable)

**Easy:**
- Longest substring without repeating
- Time: 20-30 min

**Medium:**
- Minimum window substring
- Longest substring with at most k distinct
- Longest repeating character replacement
- Time: 35-50 min

### Prefix Sums

**Easy:**
- Running sum
- Subarray sum equals k
- Time: 15-20 min

**Medium:**
- Product of array except self
- Range sum query (with 1D and 2D)
- 2D matrix sum
- Time: 25-40 min

### Floyd's Algorithm

**Easy:**
- Linked list cycle
- Find duplicate in array (treat as linked list)
- Time: 20-30 min

**Medium:**
- Find start of cycle
- Happy number
- Time: 30-45 min

**Sources:** LeetCode, GeeksforGeeks, HackerRank

---

## 💼 Interview Preparation

### Common Week 4 Questions

**Two Pointers:**
- "Optimize O(n²) nested loop to O(n)"
- "Palindrome after optional deletion?"
- "Container with maximum water"
- "All unique triplets summing to target"

**Sliding Window:**
- "Longest substring without repeating characters"
- "Minimum window containing all characters"
- "Longest substring with at most k distinct"

**Prefix Sums:**
- "Range sum queries efficiently"
- "Product of array except self (without division)"
- "Subarray sum equals k"

**Cycle Detection:**
- "Detect cycle in linked list"
- "Find start of cycle"
- "Find duplicate in array"

**Integration:**
- "Optimize O(n²) problem to O(n)"
- "Combine multiple patterns"
- "Complex edge cases"

### Interview Tips
1. **Recognize pattern:** "This looks like sliding window"
2. **State constraints:** "Array sorted? Duplicates? In-place?"
3. **Optimize step-by-step:** "Brute O(n²), then optimize"
4. **Explain approach:** "I'll use two pointers because..."
5. **Code carefully:** Boundary conditions critical

---

## 🔗 Resources & References

### Online Platforms
- **LeetCode:** All techniques (Easy to Hard)
- **GeeksforGeeks:** Technique tutorials with examples
- **InterviewBit:** Pattern-based problems
- **HackerRank:** Array manipulation challenges

### Visualization Tools
- **Algorithm Visualizer:** https://algorithm-visualizer.org/
- **LeetCode Discuss:** Solutions and explanations
- **Python Tutor:** Step-by-step execution

### Recommended Books
- "Cracking the Coding Interview" - Chapter 1-2
- "The Algorithm Design Manual" - Skiena (Chapter 2)
- "Elements of Programming Interviews" - Chapter 5

---

## ✅ Assessment & Success Criteria

### Knowledge Check
- [ ] Know when to use each technique
- [ ] Understand complexity vs naive approach
- [ ] Know space vs time tradeoffs
- [ ] Recognize patterns in new problems
- [ ] Understand technique combinations

### Practical Skills
- [ ] Implement two pointers (3+ variations)
- [ ] Implement sliding window (fixed and variable)
- [ ] Build prefix sum arrays (1D and 2D)
- [ ] Implement Floyd's cycle detection
- [ ] Combine multiple techniques

### Confidence Targets
| Technique | Target |
|---|---|
| Two Pointers | 4-5/5 |
| Sliding Window (Fixed) | 4-5/5 |
| Sliding Window (Variable) | 4-5/5 |
| Prefix Sums | 3-4/5 |
| Floyd's Algorithm | 3-4/5 |
| Integration | 3-4/5 |
| Overall Week 4 | 4/5 |

---

## 📊 Connection to Future Weeks

### Week 4.5: Binary Search & Bit Manipulation
```
Week 4 Optimization patterns on arrays
    ↓
Week 4.5 Binary search on sorted, bit operations
    ↓
Week 4 foundation for advanced search patterns
```

### Week 5+: Advanced Algorithms
```
Weeks 1-4 Fundamentals, Structures, Sorting, Optimization
    ↓
Weeks 5+ Greedy, DP, Graphs (all combine Week 4 patterns)
    ↓
Mastery of Week 4 critical for advanced success
```

### Interview Success
```
Weeks 1-4 Core algorithms
    ↓
Week 4 patterns appear in 70%+ interview problems
    ↓
Strong Week 4 → High interview success rate
```

---

## ❓ Frequently Asked Questions

### Q1: When to use two pointers vs sliding window?

**A:** Two pointers if sorted (converging), sliding window if unsorted (expanding). Can use both on sorted!

### Q2: Sliding window vs hash table for duplicates?

**A:** Sliding window if need subarray position, hash table if just need existence. Sliding window often O(n) winner.

### Q3: Prefix sums vs on-the-fly calculation?

**A:** Prefix if multiple queries (build once, query O(1)), on-the-fly if single query (save space).

### Q4: How to handle 3Sum duplicates correctly?

**A:** Skip duplicate i values, skip duplicate left/right pointers after finding match.

### Q5: Is advanced two pointers worth learning?

**A:** Yes! 3Sum/4Sum common in interviews. Understanding pattern useful for kSum.

### Q6: When to combine techniques?

**A:** When single technique incomplete. Example: binary search on answer + sliding window validation.

---

## 🎯 Before Moving to Week 4.5

**Checklist:**
- [ ] Implement all 5 techniques from scratch
- [ ] Solve 25+ problems across techniques
- [ ] Can recognize technique in new problem
- [ ] Understand when to combine techniques
- [ ] Handle all edge cases confidently
- [ ] Confident explaining each approach
- [ ] Overall confidence: 4/5 or higher

**If not ready:**
- Review weak technique
- Solve 10+ more problems in weak area
- Don't rush to Week 4.5

---

## 📝 Week 4 Quick Summary

| Technique | When | Complexity | Space | Key Insight |
|---|---|---|---|---|
| **Two Pointers** | Sorted pairs | O(n) | O(1) | Converging eliminates half |
| **Sliding (Fixed)** | Subarray size k | O(n) | O(k) | Window size constant |
| **Sliding (Var)** | Subarray property | O(n) | O(k) | Each element ≤ 2x |
| **Prefix Sums** | Range queries | O(n)+O(1) | O(n) | Trade space for time |
| **Floyd's** | Cycle detection | O(n) | O(1) | Different speeds meet |

---

**Status:** Week 4 Ready for Study ✓  
**Expected Completion:** 1-2 weeks focused study  
**Success Rate:** 75%+ with consistent practice  
**Cumulative Progress:** 60-65% of total curriculum

