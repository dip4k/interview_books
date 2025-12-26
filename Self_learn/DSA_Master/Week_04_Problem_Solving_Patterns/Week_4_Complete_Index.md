# Week 4: Complete Index & Navigation Guide

**Master Navigation for All Week 4 Learning Materials**

---

## 📁 File Structure

### Primary Learning Materials (5 Core Files)

| File | Purpose | Time |
|------|---------|------|
| **Week_4_Day_1_Two_Pointers.md** | Two pointer fundamentals | 80 min |
| **Week_4_Day_2_Sliding_Window.md** | Sliding window patterns | 85 min |
| **Week_4_Day_3_Prefix_Sums.md** | Prefix sum optimization | 70 min |
| **Week_4_Day_4_Advanced_Two_Pointers.md** | 3Sum, 4Sum, kSum | 70 min |
| **Week_4_Day_5_Integration.md** | Combining techniques | 60 min |

**Total:** ~365 minutes (6+ hours)

### Support Materials (6 Files)

| File | Purpose |
|------|---------|
| **Week_4_Checklist_Progress.md** | Track daily progress |
| **Week_4_Summary.md** | Quick reference guide |
| **Week_4_Roadmap.md** | Strategic learning plan |
| **Week_4_QA_10_Questions_Per_Day.md** | 50 practice questions |
| **Week_4_Complete_Index.md** | Navigation (this file) |

---

## 🗺️ Quick Navigation

### By Algorithm

| Algorithm | Day | Key Concepts | Q&A |
|-----------|-----|--------------|-----|
| **Two Pointers** | 1 | Converging, sorted, O(n) | Q1.1-1.10 |
| **Sliding Window** | 2 | Dynamic expand/shrink, O(n) | Q2.1-2.10 |
| **Prefix Sums** | 3 | Preprocessing, O(1) queries | Q3.1-3.10 |
| **3Sum/4Sum** | 4 | Nested pointers, duplicates | Q4.1-4.10 |
| **Integration** | 5 | Choose technique, tradeoffs | Q5.1-5.10 |

### By Problem Type

| Problem | Technique | Day |
|---------|-----------|-----|
| Two Sum (sorted) | Two Pointers | 1 |
| Valid Palindrome | Two Pointers | 1 |
| Container Max Water | Two Pointers | 1 |
| Longest Substring Unique | Sliding Window | 2 |
| Minimum Window | Sliding Window | 2 |
| Running Sum | Prefix Sums | 3 |
| Product Except Self | Prefix Sums | 3 |
| 3Sum | Advanced TP | 4 |
| 4Sum | Advanced TP | 4 |
| Trapping Rain Water | Integration | 5 |

---

## 📅 Daily Learning Path

### Day 1: Two Pointers (80 min)
**Read:** Week_4_Day_1_Two_Pointers.md
**Practice:** Q1.1-1.10
**Code:** Two Sum, Valid Palindrome, Container Max Water

### Day 2: Sliding Window (85 min)
**Read:** Week_4_Day_2_Sliding_Window.md
**Practice:** Q2.1-2.10
**Code:** Longest Substring, Minimum Window, Fixed Window

### Day 3: Prefix Sums (70 min)
**Read:** Week_4_Day_3_Prefix_Sums.md
**Practice:** Q3.1-3.10
**Code:** Running Sum, Product Except, 2D Rectangle Sum

### Day 4: Advanced Two Pointers (70 min)
**Read:** Week_4_Day_4_Advanced_Two_Pointers.md
**Practice:** Q4.1-4.10
**Code:** 3Sum, 4Sum, Duplicate Handling

### Day 5: Integration (60 min)
**Read:** Week_4_Day_5_Integration.md
**Practice:** Q5.1-5.10
**Code:** Trapping Rain Water (both approaches)

---

## 📊 Complexity Reference

### Time Complexity by Technique

| Technique | Time | Space | Requirement |
|-----------|------|-------|-------------|
| Two Pointers | O(n) | O(1) | Sorted |
| Sliding Window | O(n) | O(k) | Monotonic validity |
| Prefix Sums | O(n) build + O(1) query | O(n) | Static array |
| Advanced TP | O(n^(k-1)) | O(1) | Sorted |

---

## 🎯 Technique Decision Matrix

```
Two Pointers when:
  ✓ Array is sorted
  ✓ Need pairs
  ✓ Space critical O(1)
  ✗ Unsorted (sort first)
  ✗ Max/min in window

Sliding Window when:
  ✓ Need subarray property
  ✓ Can increment metric
  ✓ Works unsorted
  ✗ Metric not incrementable
  ✗ Need all subarrays

Prefix Sums when:
  ✓ Multiple queries
  ✓ Static array
  ✓ Want O(1) query
  ✗ Frequent updates
  ✗ Single query

Advanced TP when:
  ✓ Multiple targets (3+)
  ✓ Need unique results
  ✓ Sorted data available
  ✗ Very large k
  ✗ Need all combinations
```

---

## 🔍 Search Index

### Find by Concept

| Concept | Location |
|---------|----------|
| **Converging Pointers** | Day 1, Section 2 |
| **Movement Strategy** | Day 1, Section 3 |
| **Monotonicity** | Day 1, Section 5 |
| **Dynamic Window** | Day 2, Section 2 |
| **Incremental Update** | Day 2, Section 3 |
| **Frequency Tracking** | Day 2, Section 3-4 |
| **Cumulative Sum** | Day 3, Section 2 |
| **Range Query** | Day 3, Section 3 |
| **2D Prefix** | Day 3, Section 3 |
| **Nested Pointers** | Day 4, Section 2 |
| **Duplicate Skipping** | Day 4, Section 3 |
| **Space vs Time** | Day 5, Section 1 |
| **Integration** | Day 5, Section 2 |

---

## 📚 Study Path

**Recommended Reading Order:**

1. **Start with Roadmap** (Week_4_Roadmap.md) - 10 min
2. **Day 1: Two Pointers** - 80 min
3. **Day 2: Sliding Window** - 85 min
4. **Day 3: Prefix Sums** - 70 min
5. **Day 4: Advanced TP** - 70 min
6. **Day 5: Integration** - 60 min
7. **Review Summary** (Week_4_Summary.md) - 15 min
8. **Practice Q&A** (Week_4_QA_10_Questions_Per_Day.md) - 5-6 hours
9. **Track Progress** (Week_4_Checklist_Progress.md) - ongoing

**Total Time:** ~11-12 hours with practice

---

## ✅ Milestones

**After Day 1:**
- [ ] Understand two pointers concept
- [ ] Know why sorted required
- [ ] Can trace on paper

**After Day 2:**
- [ ] Understand sliding window
- [ ] Know expand/shrink logic
- [ ] Can implement

**After Day 3:**
- [ ] Understand prefix sums
- [ ] Know O(n)+O(1) pattern
- [ ] Can generalize to 2D

**After Day 4:**
- [ ] Understand 3Sum/4Sum
- [ ] Can handle duplicates
- [ ] Know complexity O(n^(k-1))

**After Day 5:**
- [ ] Can choose technique
- [ ] Understand trade-offs
- [ ] Can combine approaches

---

## 🏆 Success Criteria

**Knowledge:**
- [ ] Know when to use each technique
- [ ] Understand why each works
- [ ] Know complexity of each

**Skills:**
- [ ] Implement two pointers
- [ ] Implement sliding window
- [ ] Build prefix sums
- [ ] Solve 3Sum/4Sum
- [ ] Integrate techniques

**Application:**
- [ ] Recognize in new problems
- [ ] Choose optimal approach
- [ ] Handle edge cases
- [ ] Explain clearly

---

## 📞 Common Problems Map

| Problem | Solution | Technique |
|---------|----------|-----------|
| Two Sum II (sorted) | Day 1 | Two Pointers |
| 3Sum Closest | Day 4 | Advanced TP |
| Longest Palindrome | Day 1/2 | Sliding Window or TP |
| Substring Unique | Day 2 | Sliding Window |
| Subarray Sum Equals K | Day 3 | Prefix Sums |
| Max Sliding Window | Day 2 | Sliding Window |
| Trapping Rain | Day 5 | Integration |

---

## 🔗 External References

**LeetCode:**
- Two Sum II: https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/
- Longest Substring: https://leetcode.com/problems/longest-substring-without-repeating-characters/
- 3Sum: https://leetcode.com/problems/3sum/
- Trapping Rain Water: https://leetcode.com/problems/trapping-rain-water/

**Visualizers:**
- Algorithm Visualizer
- LeetCode Discuss

---

## 📝 Note-Taking Guide

**For each technique:**
1. Note the core concept (2-3 sentences)
2. Note when to use (2-3 conditions)
3. Note the algorithm sketch
4. Note complexity and space
5. Note one example with trace
6. Note one common mistake

---

## 🎓 Interview Prep

**Common questions:**
- "How would you optimize this O(n²)?" → Identify technique
- "Can you do this in-place?" → Two pointers (O(1) space)
- "How many queries?" → Multiple → Prefix sums
- "What if array is unsorted?" → Sliding window or hash

**Practice:**
- Solve each problem multiple times
- Try different approaches
- Explain before coding
- Code without hints
- Test edge cases

---

## 📊 Progress Tracking

**Use Week_4_Checklist_Progress.md to track:**
- [ ] Daily reading progress
- [ ] Section completion
- [ ] Hands-on coding
- [ ] Q&A practice
- [ ] Confidence levels
- [ ] Time spent
- [ ] Key insights

---

**Week 4 Mastery Checklist:**

- [ ] Read all 5 days material
- [ ] Answer all 50 Q&A questions
- [ ] Code all 10 main problems
- [ ] Trace 3+ examples by hand per technique
- [ ] Know when to use each
- [ ] Solve LeetCode medium level
- [ ] Explain to someone else
- [ ] Achieve 4-5/5 confidence

---

**Status:** Week 4 Complete! Ready for Week 5 (Binary Search, Greedy, Dynamic Programming)?

