# 📋 WEEK 4: PROBLEM-SOLVING PATTERNS - OVERVIEW

**Pattern Recognition & Technique Mastery**

Generated: 2025-12-26 | Status: Ready for Learning

---

## 🎯 WEEK 4 AT A GLANCE

**Theme:** Problem-Solving Patterns

**Duration:** 10 hours (90 minutes per day × 5 days + review)

**Difficulty:** 🟡 Medium (Shift from data structures to patterns)

**Learning Outcomes:**
- ✅ Recognize two-pointer pattern
- ✅ Understand sliding window (fixed and variable)
- ✅ Master prefix sum optimization
- ✅ Detect cycles using Floyd's algorithm
- ✅ Solve 60% of LeetCode medium problems

---

## 📚 DAILY BREAKDOWN

### **Monday (Day 1): Two Pointers**
**File:** code_file:88 (Week_04_Day_01_Combined.md)

**Topics:**
- Two pointers from opposite ends
- Why it works on sorted arrays
- Time O(n), Space O(1)

**Key Problems:**
- Two sum (sorted array)
- Valid palindrome
- Remove duplicates
- Container with most water

**Difficulty:** 🟡 Medium

**Key Insight:** "Pointers move from opposite ends toward middle, exploring all pairs in O(n) time."

---

### **Tuesday (Day 2): Sliding Window (Fixed)**
**File:** Will create code_file:89

**Topics:**
- Fixed-size window over array
- One pass algorithm
- Applications: max/min in window, averages

**Key Problems:**
- Max sum subarray of size k
- Moving average
- Find all anagrams

**Difficulty:** 🟡 Medium

**Key Insight:** "Slide window forward, recalculate value by removing left, adding right."

---

### **Wednesday (Day 3): Sliding Window (Variable)**
**File:** Will create code_file:90

**Topics:**
- Variable window size
- Expand/contract based on condition
- Optimization problems

**Key Problems:**
- Longest substring without duplicates
- Minimum window substring
- Maximum length subarray with sum

**Difficulty:** 🔴 Hard

**Key Insight:** "Expand window when condition not met, contract when met, track best."

---

### **Thursday (Day 4): Prefix Sums**
**File:** Will create code_file:91

**Topics:**
- Trade space for time
- Range sum queries O(1)
- 2D prefix sums

**Key Problems:**
- Range sum query
- Subarray sum equals k
- Maximum subarray sum

**Difficulty:** 🟡 Medium

**Key Insight:** "Precompute prefix sums to answer range queries in O(1)."

---

### **Friday (Day 5): Cycle Detection**
**File:** Will create code_file:92

**Topics:**
- Floyd's tortoise and hare
- Linked list cycles
- Array cycles

**Key Problems:**
- Find cycle in linked list
- Find cycle start position
- Happy number problem

**Difficulty:** 🟡 Medium

**Key Insight:** "Slow and fast pointers: if cycle exists, they'll meet."

---

## 📊 PATTERN MAP

```
Week 4: Problem-Solving Patterns
│
├── Day 1: Two Pointers
│   └── Sorted arrays, pairs, O(n) linear
│
├── Day 2: Sliding Window (Fixed)
│   └── Moving window, aggregation
│
├── Day 3: Sliding Window (Variable)
│   └── Dynamic window, optimization
│
├── Day 4: Prefix Sums
│   └── Space-time trade-off
│
└── Day 5: Cycle Detection
    └── Pointer mathematics
```

---

## 🔗 CONNECTION TO OTHER WEEKS

**Prerequisites (Week 1-3):**
- Big-O analysis (Week 1)
- Array operations (Week 2)
- Sorting (Week 3)
- Hash sets (Week 3)

**This Week Enables (Week 5+):**
- Tree patterns (Week 5)
- Graph traversal (Week 6)
- DP problems (Week 11)
- Interview mastery (Week 12)

**Why This Week:**
After learning data structures (Weeks 2-3), learn common patterns that apply them.
These 5 patterns solve 40% of LeetCode problems.

---

## ✨ KEY CONCEPTS

### **Pattern 1: Two Pointers**
- Start at opposite ends
- Move toward middle
- Use sorted property
- Time: O(n), Space: O(1)

### **Pattern 2: Sliding Window (Fixed)**
- Fixed window size k
- Slide one position at a time
- Recompute value incrementally
- Time: O(n), Space: O(1)

### **Pattern 3: Sliding Window (Variable)**
- Expand/contract window
- Track condition
- Maintain best found
- Time: O(n), Space: O(n) worst case

### **Pattern 4: Prefix Sums**
- Precompute cumulative sums
- Answer range queries instantly
- Trade O(n) space for O(1) query
- Time: O(n) setup, O(1) query

### **Pattern 5: Cycle Detection**
- Two pointers (slow, fast)
- Slow moves 1, fast moves 2
- If cycle, they meet
- Find cycle entry point with math

---

## 🎓 SKILLS YOU'LL GAIN

**By End of Day 1:**
- Recognize two-pointer situations
- Implement two-pointer algorithm
- Understand why O(n) works

**By End of Day 2:**
- Implement fixed-size sliding window
- Know when to use vs two pointers
- Solve moving average problems

**By End of Day 3:**
- Implement variable sliding window
- Use two-pointer technique in window
- Solve optimization problems

**By End of Day 4:**
- Understand prefix sum concept
- Build prefix sum arrays
- Answer range queries in O(1)

**By End of Day 5:**
- Understand Floyd's algorithm
- Detect cycles in structures
- Find cycle start position

**By End of Week:**
- Recognize pattern in new problems
- Choose right pattern for problem
- Implement confidently
- Solve 60% of LeetCode medium

---

## 📈 DIFFICULTY PROGRESSION

```
Difficulty
    |
🔴 |        Day 3 (Variable Window)
    |       ╱
🟡 |   D1  ╱  D2  D4  D5
    |  ╱   D2   ╲  ╱  ╱
🟢 | ╱─────────╲─╱──╱
    |
    └──────────────────→ Days
```

- **Day 1 (🟡):** Foundation, two pointers
- **Day 2 (🟡):** Fixed window, simpler
- **Day 3 (🔴):** Variable window, hardest
- **Day 4 (🟡):** Space-time trade-off
- **Day 5 (🟡):** Pointer math, clever

---

## 💡 COMMON PITFALLS

**Pitfall 1: Forgetting requirement**
"Two pointers only work if array is sorted!" ← WRONG for sliding window.
Lesson: Understand when each pattern applies.

**Pitfall 2: Not updating window correctly**
Sliding window: forgot to remove from left? Incorrect answer.
Lesson: Debug by tracing window changes.

**Pitfall 3: Prefix sum off-by-one**
sum[i] = prefix sum up to index i. Index confusion leads to bugs.
Lesson: Be careful with 0-indexing vs 1-indexing.

**Pitfall 4: Cycle detection not understanding math**
Why do slow and fast pointers meet if cycle exists?
Lesson: Understand the mathematical proof.

**Pitfall 5: Applying wrong pattern**
Using two pointers when variable window better.
Lesson: Know characteristics of each pattern.

---

## 🎯 LEARNING PATH

**Conservative (Deep):**
Read all 11 sections per topic
Do hand-tracing
Implement code
Return after 2 days for review
Time: 12-14 hours

**Moderate (Balanced):**
Read sections 1-6 per topic
Trace key examples
Practice problems
Return after 3 days
Time: 10 hours

**Aggressive (Quick):**
Read sections 1-3 per topic
Light tracing
Focus on when to use
Return after week
Time: 6-7 hours

**Recommendation:** Moderate. Pattern recognition requires practice.

---

## 🔧 PRACTICAL APPLICATIONS

**Real-World Use:**

| Pattern | Application | Example |
|---------|-------------|---------|
| Two Pointers | Palindrome check | "racecar" |
| Fixed Window | Moving average | Stock price smoothing |
| Variable Window | Substring search | Find longest without duplicates |
| Prefix Sum | Range queries | Sum of range in O(1) |
| Cycle Detection | Loop detection | Memory leak detection |

---

## 📚 TOPICS BY PROBLEM TYPE

**Array/String Problems:**
- Two pointers (Day 1)
- Sliding window (Days 2-3)
- Prefix sum (Day 4)

**Linked List Problems:**
- Cycle detection (Day 5)
- Two pointers (Day 1)

**Optimization Problems:**
- Sliding window variable (Day 3)
- Prefix sum (Day 4)

---

## ✅ SUCCESS CRITERIA

**Daily (Mon-Fri):**
- ✅ 90-minute study completed
- ✅ Pattern understood conceptually
- ✅ Can implement from scratch
- ✅ 5+ problems solved
- ✅ Confidence 4-5

**Weekly (By Sunday):**
- ✅ All 5 patterns mastered
- ✅ Can recognize pattern in new problem
- ✅ Solve 30+ LeetCode medium problems
- ✅ Ready for Week 5 (Trees)

---

## 📞 KEY REFERENCES

**Two Pointers:**
- Problems: Two sum, valid palindrome, remove duplicates
- Complexity: O(n) time, O(1) space
- Requirement: Sorted array or specific structure

**Sliding Window:**
- Fixed: Moving aggregation, constant space
- Variable: Optimization, O(n) time
- Complexity: O(n) time, O(1) or O(n) space

**Prefix Sum:**
- Setup: O(n) time, O(n) space
- Query: O(1) time
- Use: Range sum queries

**Cycle Detection:**
- Algorithm: Floyd's tortoise and hare
- Time: O(n)
- Space: O(1)

---

**Status:** Week 4 Ready | Quality: Professional Grade

