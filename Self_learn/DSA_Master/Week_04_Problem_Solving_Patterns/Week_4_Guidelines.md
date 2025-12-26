# Week 4: Optimization Techniques - Guidelines

**Week Focus:** Master array/string optimization patterns (Two Pointers, Sliding Window, Prefix Sums, Advanced)  
**Total Time Investment:** 11-13 hours (learning + practice)  
**Difficulty Level:** 🔴 Hard  
**Prerequisites:** Week 1-3 (Arrays, data structures, sorting)

---

## 📅 Daily Breakdown & Time Allocation

| Day | Topic | Time | Key Outcomes |
|-----|-------|------|--------------|
| **1** | Two Pointers Technique | 80 min | O(n) on sorted, converging pattern |
| **2** | Sliding Window Pattern | 85 min | O(n) on unsorted, dynamic window |
| **3** | Prefix Sums Optimization | 70 min | O(n) preprocessing, O(1) queries |
| **4** | Advanced Two Pointers | 70 min | 3Sum, 4Sum, kSum patterns |
| **5** | Integration & Complex Patterns | 60 min | Combine techniques, tradeoffs |

**Total Core Learning:** ~365 minutes (6.1 hours)  
**Practice & Consolidation:** ~5-7 hours  

---

## 🎯 Week 4 Learning Objectives

### By Week End, You Should:

**Knowledge:**
- [ ] Understand when each technique works
- [ ] Know complexity of each approach
- [ ] Know space vs time tradeoffs
- [ ] Recognize technique patterns
- [ ] Understand technique synergies

**Skills:**
- [ ] Implement two pointers
- [ ] Implement sliding window
- [ ] Build prefix sum arrays
- [ ] Solve 3Sum, 4Sum
- [ ] Combine techniques strategically

**Application:**
- [ ] Recognize technique in new problem
- [ ] Choose optimal approach
- [ ] Handle duplicates and edge cases
- [ ] Integrate multiple techniques
- [ ] Solve complex optimization problems

---

## 📚 Core Concepts Overview

### Two Pointers
```
When: Sorted array, find pairs/elements
How: Converging from opposite ends
Complexity: O(n) time, O(1) space
Key Insight: Directional movement eliminates half
```

### Sliding Window
```
When: Subarray properties, unsorted OK
How: Expand window, shrink when invalid
Complexity: O(n) time, O(k) space
Key Insight: Each element touched ≤ 2 times
```

### Prefix Sums
```
When: Multiple range queries, static array
How: Precompute cumulative sums
Complexity: O(n) build + O(1) per query
Key Insight: Trade space for query speed
```

### Advanced Two Pointers
```
When: Multiple targets (3Sum, 4Sum)
How: Fix k-2 elements, two pointers on rest
Complexity: O(n^(k-1)) vs O(n^k) brute force
Key Insight: Nesting reduces exponential complexity
```

---

## 🔄 Recommended Learning Path

**Best Order to Study:**

1. **Day 1:** Two Pointers Foundation
   - Understand converging from ends
   - Learn sorted requirement
   - Practice movement strategy
   - Solve basic pairs problems

2. **Day 2:** Sliding Window
   - Understand expand/shrink logic
   - Learn without sorting
   - Practice incremental updates
   - Solve subarray problems

3. **Day 3:** Prefix Sums
   - Understand cumulative concept
   - Learn range queries
   - Extend to 2D
   - Solve range problems

4. **Day 4:** Advanced Two Pointers
   - Extend to multiple targets
   - Handle duplicates
   - Nest pointers efficiently
   - Solve 3Sum, 4Sum

5. **Day 5:** Integration
   - Combine techniques
   - Understand synergies
   - Make design choices
   - Solve complex problems

**Why This Order?**
- Two pointers most intuitive (start there)
- Sliding window extends to unsorted
- Prefix sums introduces preprocessing
- Advanced TP multiplies complexity
- Integration ties everything together

---

## ⚠️ Common Mistakes to Avoid

### Two Pointers

| Mistake | Fix |
|---------|-----|
| **Forgetting sorted requirement** | Must sort first if unsorted |
| **Moving wrong pointer** | Move pointer toward target |
| **Off-by-one errors** | Use left < right, check boundaries |
| **Not returning all pairs** | Ensure you find all matches |

### Sliding Window

| Mistake | Fix |
|---------|-----|
| **Metric not incrementally updatable** | Check if metric can update O(1) |
| **Forgetting window can shrink** | Handle when no valid window |
| **Missing duplicates in frequency** | Use hash map for counts |

### Prefix Sums

| Mistake | Fix |
|---------|-----|
| **Index confusion** | prefix[i+1] = prefix[i] + arr[i] |
| **Forgetting static requirement** | Updates need rebuild |
| **Query range errors** | sum(l,r) = prefix[r+1] - prefix[l] |

### Advanced Two Pointers

| Mistake | Fix |
|---------|-----|
| **Not skipping duplicates** | Skip duplicates in result |
| **Forgetting duplicate handling** | Leads to duplicate triplets |
| **Exponential complexity for large k** | O(n^4) for 4Sum is expensive |

---

## 🎓 Practice Problems Guide

### Two Pointers

**Easy:**
- Two sum II (sorted)
- Valid palindrome
- Container with most water
- Time: 15-25 min

**Medium:**
- 3Sum closest
- Remove duplicates
- Reverse words
- Time: 25-40 min

### Sliding Window

**Easy:**
- Longest unique substring
- Max consecutive ones
- Time: 15-25 min

**Medium:**
- Minimum window substring
- Longest substring with k distinct
- Sliding window maximum
- Time: 30-50 min

### Prefix Sums

**Easy:**
- Running sum
- Subarray sum equals k
- Time: 15-20 min

**Medium:**
- Product of array except self
- Range sum query
- 2D rectangle sum
- Time: 25-40 min

### Advanced Two Pointers

**Medium:**
- 3Sum
- 3Sum closest
- Time: 25-40 min

**Hard:**
- 4Sum
- kSum
- Time: 40-60 min

**Sources:** LeetCode, GeeksforGeeks, HackerRank

---

## 💼 Interview Preparation

### Common Week 4 Questions

**Two Pointers:**
- "Optimize O(n²) nested loop" → Two pointers
- "Palindrome valid after deletion?"
- "Container with max water"

**Sliding Window:**
- "Longest substring without repeating"
- "Minimum window containing all chars"
- "Anagrams in string"

**Prefix Sums:**
- "Range sum queries efficiently"
- "Product of array except self"
- "Subarray sum equals k"

**Advanced:**
- "All unique triplets summing to target"
- "kSum problem"
- "Duplicate handling"

### Interview Tips
1. **Ask about constraints:** "Sorted? Duplicates? Memory limit?"
2. **Justify choice:** "I chose sliding window because O(n)"
3. **Discuss trade-offs:** "Two pointers O(1) space vs prefix O(n) space"
4. **Explain movement:** "When sum too large, shrink window"
5. **Handle edge cases:** "Empty array, single element, duplicates"

---

## 🔗 Resources & References

### Online Platforms
- **LeetCode:** Array/String sections (all difficulties)
- **GeeksforGeeks:** Technique tutorials with code
- **HackerRank:** Array problems

### Visualization Tools
- **Algorithm Visualizer:** https://algorithm-visualizer.org/
- **LeetCode Discuss:** Solutions and explanations

### Recommended Books
- "Cracking the Coding Interview" - Chapter 1-2
- "The Algorithm Design Manual" - Chapter 2
- "Elements of Programming Interviews" - Chapter 5

---

## ✅ Assessment & Success Criteria

### Knowledge Check
- [ ] Know when to use each technique
- [ ] Understand complexity comparison
- [ ] Know space vs time tradeoffs
- [ ] Recognize technique patterns
- [ ] Understand technique combinations

### Practical Skills
- [ ] Implement two pointers (3+ variations)
- [ ] Implement sliding window (2+ variations)
- [ ] Build prefix sum arrays
- [ ] Solve 3Sum, 4Sum
- [ ] Combine techniques for complex problems

### Confidence Targets
| Technique | Target |
|-----------|--------|
| Two Pointers | 4-5/5 |
| Sliding Window | 4-5/5 |
| Prefix Sums | 3-4/5 |
| Advanced TP | 3-4/5 |
| Integration | 3-4/5 |
| Overall Week 4 | 4/5 |

---

## 📊 Connection to Future Weeks

### Week 4.5: Binary Search & Integration
```
Week 4 Optimization Techniques
    ↓
Week 4.5 Binary search on sorted, bit manipulation
    ↓
Week 4 is foundation for Week 4.5 integration
```

### Week 5: Advanced Algorithms
```
Weeks 1-4 Fundamentals, Structures, Sorting, Optimization
    ↓
Week 5 Greedy, DP, Graphs (combine with Week 4 techniques)
    ↓
Mastery of Week 4 essential for Week 5 success
```

### Interview Success
```
Weeks 1-4 Core Algorithms
    ↓
Week 4 Techniques appear in 70%+ of interview problems
    ↓
Strong Week 4 → High interview success rate
```

---

## ❓ Frequently Asked Questions

### Q1: When to use two pointers vs sliding window?
**A:** Two pointers if sorted (pairs), sliding window if unsorted (subarrays). Can use both on sorted!

### Q2: Sliding window vs hash table for duplicates?
**A:** Sliding window if need subarray, hash table if just need existence. Sliding window better O(n).

### Q3: Prefix sums vs segment tree?
**A:** Prefix for static arrays, segment tree for updates. Prefix simpler, segment more powerful.

### Q4: How to handle 3Sum duplicates correctly?
**A:** Skip duplicate i values, skip duplicate left/right pointers after finding match.

### Q5: Is advanced two pointers worth learning?
**A:** Yes! 3Sum/4Sum appear in interviews. Understanding pattern useful for kSum.

### Q6: When to combine techniques?
**A:** When single technique incomplete. Example: Binary search on answer + sliding window validation.

---

## 🎯 Before Moving to Week 4.5

**Checklist:**
- [ ] Implement all 5-day material
- [ ] Solve 20+ problems across all techniques
- [ ] Can recognize technique in new problem
- [ ] Understand when to combine techniques
- [ ] Handle all edge cases
- [ ] Confident explaining approach
- [ ] Overall confidence: 4/5 or higher

**If not ready:**
- Review weak technique
- Solve 10+ more problems in weak area
- Don't rush to Week 4.5

---

## 📝 Week 4 Quick Summary

| Technique | When | Complexity | Space |
|-----------|------|-----------|-------|
| **Two Pointers** | Sorted pairs | O(n) | O(1) |
| **Sliding Window** | Unsorted subarray | O(n) | O(k) |
| **Prefix Sums** | Range queries | O(n)+O(1) | O(n) |
| **Advanced TP** | Multiple targets | O(n^(k-1)) | O(1) |

---

**Status:** Week 4 Ready for Study ✓  
**Expected Completion:** 1-2 weeks focused study  
**Success Rate:** 80%+ with consistent practice  
**Next Step:** Week 4.5 (Binary Search, Bit Manipulation, Integration)

