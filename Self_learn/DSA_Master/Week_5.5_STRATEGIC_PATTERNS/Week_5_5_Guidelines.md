# Week 5.5 Enhanced Guidelines - Master Overview

**Week:** 5.5 | **Focus:** Optimization Techniques Mastery  
**Difficulty:** 🔴 Hard | **Time:** 15-20 hours | **Interview Weight:** 38-57%

---

## 1️⃣ WEEK 5.5 MISSION

Master four optimization techniques that cover **38-57% of advanced array interview problems**.

From foundation (Week 5) → optimization (Week 5.5) → generalization (Week 6).

---

## 2️⃣ THE FOUR TECHNIQUES AT A GLANCE

| Technique | Problem | Solution | Complexity | Interview % |
|-----------|---------|----------|-----------|------------|
| **Difference Array** | Range updates | Mark boundaries | O(m+n) | 10-15% |
| **In-Place** | Space constraint | Two-pointer i,j | O(n) time, O(1) space | 8-12% |
| **Deque** | Window max/min | Monotonic queue | O(n) | 5-10% |
| **Combinations** | Complex | Chain techniques | Varies | 15-20% |

---

## 3️⃣ DAILY BREAKDOWN & TIME ALLOCATION

**Phase 1: Core (Days 1-3)** - 7.5 hours
- Day 1 Diff Array: 2.5 hrs
- Day 2 In-Place: 2.5 hrs
- Day 3 Deque: 2.5 hrs

**Phase 2: Advanced (Days 4-5)** - 5 hours
- Day 4 Combinations: 2.5 hrs
- Day 5 Integration: 2.5 hrs

**Phase 3: Mastery (2.5-5 hours)**
- Problem solving sprint
- 15+ problems total
- Interview simulation

---

## 4️⃣ LEARNING OBJECTIVES

### Knowledge (Understanding)
- [ ] Difference array = inverse of prefix sum
- [ ] In-place = safe because i > j always
- [ ] Deque = monotonic for O(1) access
- [ ] When to combine techniques
- [ ] Why each technique works

### Skills (Can Do)
- [ ] Code difference array from scratch
- [ ] Code in-place removal from scratch
- [ ] Code deque sliding window from scratch
- [ ] Combine 2+ techniques
- [ ] Handle all edge cases

### Application (Where to Use)
- [ ] Recognize pattern from problem statement
- [ ] Choose optimal technique(s)
- [ ] Implement efficiently
- [ ] Verify with test cases
- [ ] Discuss trade-offs

---

## 5️⃣ PATTERN RECOGNITION FRAMEWORK

### Decision Tree

```
Problem mentions:
├─ "Update range" OR "add to [L,R]"
│  └─ Difference Array
├─ "In-place" OR "O(1) space"
│  └─ In-Place Two-Pointer
├─ "Sliding window" OR "window of size k"
│  └─ Deque Monotonic
├─ Multiple of above
│  └─ Combination Approach
└─ Not sure?
   └─ Reference Decision Matrix
```

### Keywords Trigger

**Difference Array:**
- Range updates, range additions, shifts, batch operations

**In-Place:**
- Modify in-place, O(1) space, no extra array, remove elements

**Deque:**
- Sliding window, maximum, minimum, every window

**Combinations:**
- After updates, then query; filter then analyze; multiple operations

---

## 6️⃣ COMMON MISTAKES & HOW TO AVOID

| Mistake | Why Wrong | Prevention |
|---------|-----------|-----------|
| Diff array size = n | Index out of bounds | Always: size = n+1 |
| In-place: i ≤ j | Read-write collision | Verify: i > j always |
| Deque: store values | Can't check window | Store indices instead |
| Update while query | Wrong results | Query AFTER updates |
| Forget to reconstruct | Using wrong array | Reconstruct = required step |
| Heap for window max | O(n log n) not O(n) | Use deque for monotonic |

---

## 7️⃣ INTERVIEW PREPARATION

### 30-Second Explanations

**Difference Array:**
> "For range updates, I use a difference array. Mark start with +val, end+1 with -val. Then reconstruct with prefix sum. Time: O(m+n)."

**In-Place:**
> "For space optimization, I use two pointers. i scans for valid elements, j marks write position. Since i > j always, no collision. Time: O(n), Space: O(1)."

**Deque:**
> "For sliding window max, monotonic deque. Maintain indices in decreasing value order. Front is always max. Time: O(n)."

**Combinations:**
> "This problem combines techniques. I'll apply difference array for updates, reconstruct, then use deque for window queries."

### Code in 5 Minutes

- Difference array template: 5 lines
- In-place template: 4 lines
- Deque template: 8 lines

### Solve in 20-25 Minutes

- Easy problems: 15-20 min
- Medium problems: 25-35 min
- Hard problems: 40-60 min

---

## 8️⃣ PRACTICE PROGRESSION

### Week 5.5 Problem Target: 15+ Total

**By Technique:**
- Difference Array: 3-4 problems
- In-Place: 3-4 problems
- Deque: 3-4 problems
- Combinations: 2-3 problems

**By Difficulty:**
- Easy: 5 problems (15-20 min each)
- Medium: 5 problems (25-40 min each)
- Hard: 5 problems (40-60 min each)

**Recommended LeetCode Problems:**
1. Range Addition (370)
2. Remove Element (27)
3. Sliding Window Maximum (239)
4. Hotel Bookings II (1109)
5. Remove Vowels (1119)
6. And 10 more of your choice

---

## 9️⃣ RESOURCES & EXTERNAL LINKS

**Visualization:**
- LeetCode Playground (for coding)
- Draw.io (for diagrams)
- Pen & paper (for tracing)

**Practice:**
- LeetCode (primary source)
- HackerRank (alternative)
- CodeSignal (mock interviews)

**Reference:**
- [73] Summary (quick lookup)
- [67-71] Instructional files
- [75] Q&A with answers

---

## 🔟 ASSESSMENT & SUCCESS CRITERIA

### Knowledge Assessment (Rate 1-5)

| Concept | Rating |
|---------|--------|
| Difference array concept | ___/5 |
| In-place mechanism | ___/5 |
| Deque monotonic | ___/5 |
| Pattern recognition | ___/5 |
| Technique combination | ___/5 |

**Target:** 4/5 on all

### Practical Skills (Can You...)

- [ ] Code difference array from scratch in < 5 min
- [ ] Code in-place from scratch in < 5 min
- [ ] Code deque from scratch in < 8 min
- [ ] Combine techniques correctly
- [ ] Handle all edge cases

### Interview Readiness (Pre-Interview)

- [ ] Explain each technique in 30 sec
- [ ] Solve easy problems in 15 min
- [ ] Solve medium problems in 30 min
- [ ] Recognize which technique(s) apply
- [ ] Write production-quality code

---

## 1️⃣1️⃣ WEEK 5.5 INTEGRATION POINTS

### With Week 5 (Trees)
- Trees used prefix sums
- Week 5.5 uses inverse (difference array)
- Same thinking, different angle

### With Week 6 (Graphs)
- Difference array → edge weight updates
- In-place → vertex coloring
- Deque → BFS optimization

### With Interviews
- Week 5.5 techniques appear in 38-57% of advanced problems
- Essential for Google, Meta, Microsoft
- Tests optimization mindset

---

## 1️⃣2️⃣ WEEK 5.5 TO WEEK 6 TRANSITION

### Before Moving to Week 6, Verify:

✅ **Readiness Checklist:**
- [ ] Understand all 4 techniques conceptually
- [ ] Confidence 4/5 on Days 1-3 (core techniques)
- [ ] Confidence 3/5 on Day 4 (combinations)
- [ ] Solved 15+ problems across all techniques
- [ ] Can recognize technique from problem statement
- [ ] Can code from scratch in 5 minutes
- [ ] Can explain in 30 seconds

✅ **Performance Targets:**
- [ ] Easy problems: 90% success rate
- [ ] Medium problems: 70% success rate
- [ ] Hard problems: 50% success rate
- [ ] Average time: within target range

✅ **Confidence Levels:**
- [ ] Overall confidence: 4/5
- [ ] Ready for advanced problems: YES

### If Not Ready:
1. Identify weak technique(s)
2. Review specific instructional file
3. Solve 5+ problems on weak technique
4. Return to readiness checklist

### If Ready:
→ Proceed to Week 6 (Graph Fundamentals)

---

## 📝 FINAL SUMMARY

| Dimension | Week 5.5 |
|-----------|----------|
| **Topics** | 4 optimization techniques |
| **Time** | 15-20 hours |
| **Problems** | 15+ required |
| **Difficulty** | Hard |
| **Interview %** | 38-57% of advanced arrays |
| **Key Skill** | Pattern recognition |
| **Next Step** | Week 6 (Graphs) |

---

## ✅ SUCCESS DEFINITION

**You've mastered Week 5.5 when:**

1. **Knowledge:** Can explain all 4 techniques in detail
2. **Skills:** Can code all 4 from scratch quickly
3. **Application:** Can recognize which technique(s) apply
4. **Proficiency:** Can solve medium/hard problems consistently
5. **Speed:** Can solve problems within time limits
6. **Confidence:** Feel 4/5 confidence on each technique

---

**Week 5.5 Enhanced Guidelines Complete**  
**Status:** Ready for learning  
**Goal:** Master optimization patterns  
**Outcome:** 38-57% interview coverage  

**Let's optimize!** 🚀

