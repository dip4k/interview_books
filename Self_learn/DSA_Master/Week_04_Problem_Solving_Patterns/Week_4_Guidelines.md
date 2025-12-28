# Week 4: Guidelines & Master Plan

## 📅 Daily Breakdown & Time Allocation

| Day | Topic | Time | Morning Focus | Afternoon Focus | Evening Focus |
|-----|-------|------|---|---|---|
| **1** | Two Pointers | 120-150 min | Convergent/chasing patterns | 3-4 LeetCode problems | Answer Q&A, trace examples |
| **2** | Sliding Window (Fixed) | 120-150 min | Window maintenance, rolling aggregates | 3-4 problems (deque, max) | Review summary, roadmap |
| **3** | Sliding Window (Variable) | 150-180 min | Constraint satisfaction, expansion/contraction | 3-4 hard problems | Deep dive on edge cases |
| **4** | Prefix Sums | 120-150 min | Preprocessing + query logic | 3-4 range query problems | 2D prefix sums |
| **5** | Cycle Detection | 150-180 min | Floyd's algorithm mechanics | 3-4 linked list problems | Functional iteration practice |
| **Week** | **TOTAL** | **630-770 min** | | | |

**Expected Pace:** 2-2.5 hours daily, 10-12 hours weekly

---

## 🎯 Learning Objectives (Week 4)

### Core Competencies
- [ ] Identify when two-pointer technique applies
- [ ] Distinguish converging vs chasing pointer patterns
- [ ] Build and query fixed-size sliding windows O(n)
- [ ] Implement variable sliding window with constraint satisfaction
- [ ] Apply prefix sum preprocessing for O(1) range queries
- [ ] Detect and find cycles using Floyd's algorithm O(1) space
- [ ] Choose optimal pattern for given problem
- [ ] Trace algorithms by hand (at least 5 complete examples)
- [ ] Answer 50+ interview Q&A pairs fluently
- [ ] Solve 30+ practice problems across patterns

### Sub-Competencies

**Two Pointers:**
- [ ] Understand sorted array invariants
- [ ] Code converging pattern from scratch
- [ ] Code chasing (in-place) pattern from scratch
- [ ] Handle palindrome checking
- [ ] Optimize from O(n²) to O(n)

**Fixed Sliding Window:**
- [ ] Build initial window O(k)
- [ ] Slide and update aggregate O(1)
- [ ] Use deque for window max/min
- [ ] Handle edge cases (k=n, k>n)

**Variable Sliding Window:**
- [ ] Expand until constraint satisfied
- [ ] Contract until constraint violated
- [ ] Maintain hash map of constraints
- [ ] Find minimum/maximum valid window

**Prefix Sums:**
- [ ] Build prefix array O(n)
- [ ] Query range sums O(1)
- [ ] Use for subarray sum problems
- [ ] Handle 2D prefix sums
- [ ] Use with hash map (subarray sum = k)

**Cycle Detection:**
- [ ] Understand relative speed convergence
- [ ] Implement Floyd's algorithm
- [ ] Find cycle start node
- [ ] Calculate cycle length
- [ ] Apply to functional sequences

---

## 🔄 Recommended Learning Path

### Morning (90-120 min)
1. **Read instructional file (Sections 1-6):** 40-50 min
   - WHY: Motivation + real systems
   - WHAT: Mental model + intuition
   - HOW: Detailed mechanics
   - VISUALIZATION: 3+ full examples
   - CRITICAL ANALYSIS: Performance + edge cases
   - REAL SYSTEMS: 5-10 integrations

2. **Trace examples by hand:** 20-30 min
   - Work through each example yourself
   - Don't just read, simulate
   - Cover both normal and edge cases

3. **Answer Socratic questions:** 15-20 min
   - Section 10: 5 open-ended questions
   - Write answers, don't just think

### Afternoon (90-120 min)
1. **Solve 3-4 practice problems:** 75-100 min
   - Start with easy problems
   - Match to algorithm from section
   - Trace solution for your own problem
   - Handle edge cases

2. **Use problem-solving roadmap:** 15-20 min
   - Identify problem type
   - Match to correct pattern
   - Review algorithm before coding

### Evening (40-50 min)
1. **Review daily checklist:** 10 min
   - Check off completed objectives
   - Rate confidence 1-5

2. **Study 5+ interview Q&A:** 15-20 min
   - From daily checklist Q&A
   - Understand answer fully

3. **Quick summary review:** 10-15 min
   - Skim summary key concepts
   - Connect to other patterns

---

## ⚠️ Common Mistakes to Avoid

### Mistake 1: Memorizing Without Understanding
**❌ Problem:** "Just code the solution without understanding why"
**✅ Solution:** Trace examples completely before coding. Explain algorithm to someone.

### Mistake 2: Skipping Edge Cases
**❌ Problem:** Solution works for happy path but fails on edge cases
**✅ Solution:** For each problem, test: empty input, single element, all same values, no solution

### Mistake 3: Not Recognizing Pattern Variants
**❌ Problem:** "This looks like fixed sliding window but requires variable window"
**✅ Solution:** Use decision trees in roadmap to classify before solving

### Mistake 4: Ignoring Space Complexity
**❌ Problem:** Use O(n) hash table when O(1) solution exists
**✅ Solution:** Problem says "O(1) space required"? → Floyd's, two-pointers, in-place operations

### Mistake 5: Mixing Pointer Patterns
**❌ Problem:** Two-pointer code in sliding window problem
**✅ Solution:** Understand distinctly: two-pointers (pair finding), sliding window (contiguous subarrays), Floyd's (cycle detection)

### Mistake 6: Not Handling Negative Numbers
**❌ Problem:** Prefix sums code assumes all positive
**✅ Solution:** Test with negative numbers. Code should work regardless.

### Mistake 7: Off-by-One Errors
**❌ Problem:** Array indices wrong, loop termination incorrect
**✅ Solution:** Draw array with indices. Code loop bounds explicitly (left=0, right=n-1, etc.)

### Mistake 8: Ignoring Time Constraints
**❌ Problem:** Optimize O(n) algorithm when n=10⁶ (still passes, but not elegant)
**✅ Solution:** Check constraints. If interview asks for O(1) space, provide it.

---

## 📚 Practice Problems Guide

### By Difficulty

**Easy (6-8 problems):** 15-20 min each
- Two Sum II (sorted array)
- Reverse String (two-pointer)
- Valid Palindrome
- Remove Duplicates (sorted array)
- Range Sum Query (prefix sum)
- Maximum Average Subarray (fixed window)
- Linked List Cycle (detection)

**Medium (15-20 problems):** 20-30 min each
- Container with Most Water (two-pointer)
- Sliding Window Maximum
- Minimum Window Substring (variable)
- Longest Substring Without Repeating
- Subarray Sum Equals K (prefix)
- Find Duplicate Number (cycle)
- 3Sum, 4Sum variants
- Subarrays with Product Less than K

**Hard (5-8 problems):** 30-40 min each
- Trapping Rainwater (two-pointer optimization)
- Sliding Window Maximum (advanced)
- Subarrays with K Different Integers
- Circular Array Loop (cycle)
- Hard variant of each pattern

### By Category

**Two-Pointer Problems:** 8 problems
1. Two Sum II (LeetCode 167) [Easy]
2. Valid Palindrome (LeetCode 125) [Easy]
3. Container with Most Water (LeetCode 11) [Medium]
4. Remove Duplicates (LeetCode 26) [Easy]
5. 3Sum (LeetCode 15) [Medium]
6. Trapping Rain Water (LeetCode 42) [Hard]
7. Reverse String (LeetCode 344) [Easy]
8. Merge Two Sorted Arrays [Medium]

**Sliding Window Problems:** 12 problems
- **Fixed:** Maximum average, max/min in window, duplicate detection
- **Variable:** Min window substring, longest substring, character count

**Prefix Sum Problems:** 8 problems
1. Range Sum Query (LeetCode 303) [Easy]
2. Subarray Sum Equals K (LeetCode 560) [Medium]
3. Contiguous Array (LeetCode 485) [Medium]
4. Maximum Subarray (LeetCode 53) [Medium]
5. 2D Range Sum (LeetCode 304) [Medium]
6. Binary Subarray with Sum (LeetCode 930) [Medium]

**Cycle Detection Problems:** 6 problems
1. Linked List Cycle (LeetCode 141) [Easy]
2. Linked List Cycle II (LeetCode 142) [Medium]
3. Find Duplicate Number (LeetCode 287) [Medium]
4. Happy Number (LeetCode 202) [Easy]
5. Circular Array Loop (LeetCode 457) [Medium]
6. Cycle in Functional Iteration [Medium]

---

## 💼 Interview Preparation

### Coverage by Week 4
**Problem-Solving Patterns:** 12-15% additional interview coverage (cumulative: 35-45%)

Most common interview questions by pattern:
- **Two-pointers:** 3-4% (pair finding, removal)
- **Fixed Sliding Window:** 2-3% (max/min in range)
- **Variable Sliding Window:** 3-4% (constraint satisfaction)
- **Prefix Sums:** 2-3% (range queries, subarray)
- **Cycle Detection:** 1-2% (linked lists, graphs)

### Mock Interview Strategy
1. **Identify pattern:** 2-3 min (use decision tree from roadmap)
2. **Explain approach:** 1-2 min (state complexity)
3. **Code solution:** 10-15 min (trace example while coding)
4. **Test edge cases:** 5 min (empty, single element, no solution)
5. **Optimize if time:** 2-5 min (can we do better?)

**Total per problem:** 20-30 minutes (typical interview pace)

---

## ❓ Frequently Asked Questions

**Q: What's the difference between two-pointer and sliding window?**
A: Two-pointer finds pairs/relationships. Sliding window processes contiguous subarrays. Different use cases.

**Q: Can I use two-pointer on unsorted arrays?**
A: Not reliably (sorting first defeats the purpose). Use other approaches (hash table, different pattern).

**Q: Does sliding window only work on arrays?**
A: Works on strings, arrays, any linear sequence. Key: contiguous elements.

**Q: Why is prefix sum O(1) space if I need to store prefix array?**
A: "O(1) space" for queries means no extra space per query. Preprocessing O(n) space is acceptable.

**Q: Can Floyd's algorithm work with speeds other than 2x?**
A: Yes, any speed > 1 works. Speed 2 is simplest and most common.

**Q: How do I choose between patterns for a problem?**
A: Use decision trees in problem-solving roadmap. Identify: are you finding pairs (two-pointer), processing ranges (sliding), or solving on subarrays (prefix sum)?

---

## ✅ Before Proceeding to Week 5

**Checklist before moving on:**

**Knowledge:**
- [ ] Understand WHY each pattern exists (5 real-world systems minimum)
- [ ] Can explain each algorithm without looking at code
- [ ] Know complexity tradeoffs for each
- [ ] Understand when to use each pattern

**Coding:**
- [ ] Implement all 5 patterns from scratch (no looking at solutions)
- [ ] Solve 30+ practice problems (minimum)
- [ ] Handle edge cases confidently
- [ ] Code in under 15 minutes for easy, under 25 for medium

**Interview Ready:**
- [ ] Answer 50+ interview Q&A pairs fluently
- [ ] Explain real-world applications
- [ ] Trace algorithms step-by-step
- [ ] Time yourself (20-30 min per medium problem)

**Confidence Assessment:**
- [ ] Two-pointers: 4/5+
- [ ] Fixed sliding window: 4/5+
- [ ] Variable sliding window: 4/5+
- [ ] Prefix sums: 4/5+
- [ ] Cycle detection: 4/5+

If any below 4/5, spend extra time on that pattern before Week 5.

---

## 🚀 Next Steps

1. **This Week:** Complete 5 daily instructional files + 30+ problems
2. **Before Week 5:** Achieve 4/5+ confidence on all patterns
3. **Week 5:** Trees, heaps, BSTs (builds on pattern thinking)
4. **Weeks 6+:** Graphs, specialized algorithms (use patterns extensively)

---

**Status:** Week 4 Guidelines Complete  
**Your focus:** Deep understanding > speed. Master patterns first.

