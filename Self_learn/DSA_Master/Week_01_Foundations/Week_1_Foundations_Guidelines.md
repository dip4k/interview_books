# Week 1: Foundations - Guidelines

**Week Focus:** Understand how computers work and measure algorithm efficiency  
**Total Time Investment:** 10-12 hours (learning + practice)  
**Difficulty Level:** 🟢 Easy  
**Prerequisites:** None (complete beginner-friendly)

---

## 📅 Daily Breakdown & Time Allocation

| Day | Topic | Time | Key Outcomes |
|-----|-------|------|--------------|
| **1** | RAM Model & Pointers | 100 min | Computational model, memory access, pointer basics |
| **2** | Asymptotic Analysis | 110 min | Big-O notation, time complexity analysis, growth rates |
| **3** | Space Complexity | 100 min | Memory usage, Stack vs Heap, space trade-offs |
| **4** | Recursion I | 110 min | Stack frames, base cases, intuitive understanding |
| **5** | Recursion II | 100 min | Advanced recursion, tail recursion, mutual recursion |

**Total Core Learning:** ~520 minutes (8.7 hours)  
**Practice & Consolidation:** ~2-3 hours  

---

## 🎯 Week 1 Learning Objectives

### By Week End, You Should:

**Knowledge:**
- [ ] Understand RAM model (the computational model all analysis assumes)
- [ ] Know what Big-O notation means and why it matters
- [ ] Understand time complexity vs space complexity distinction
- [ ] Know difference between stack and heap memory
- [ ] Understand recursion and how it works

**Skills:**
- [ ] Analyze time complexity of algorithms (derive Big-O)
- [ ] Analyze space complexity
- [ ] Estimate algorithm runtime
- [ ] Write recursive functions with correct base cases
- [ ] Trace recursive calls by hand

**Application:**
- [ ] Choose data structures based on complexity analysis
- [ ] Identify inefficient algorithms
- [ ] Understand why specific structures are efficient/slow
- [ ] Write efficient recursive solutions
- [ ] Analyze trade-offs between solutions

---

## 📚 Core Concepts Overview

### RAM Model
```
Computational Model:
  - Random Access Memory: O(1) access to any memory address
  - CPU executes instructions sequentially
  - Basic operations (add, compare, assign) = 1 unit time
  
Key Insight:
  - All Big-O analysis assumes RAM model
  - Justifies ignoring constants
  - Why O(n) vs O(n²) matters even for small n
```

### Big-O Notation
```
Definition: Upper bound on growth rate
Examples:
  O(1) - constant time
  O(log n) - logarithmic
  O(n) - linear
  O(n log n) - linearithmic
  O(n²) - quadratic
  O(2^n) - exponential
  O(n!) - factorial

Key: Ignore constants and lower-order terms
  50n + 10 = O(n)
  n² + 50n = O(n²)
```

### Space Complexity
```
Where memory is used:
  - Input storage: unavoidable
  - Auxiliary space: extra we allocate
  
Stack vs Heap:
  - Stack: function calls, local variables (limited, LIFO)
  - Heap: dynamic allocation (large, managed)
  
Examples:
  - Array of n elements: O(n) space
  - Recursive depth d: O(d) stack space
  - Hash table for n items: O(n) space
```

### Recursion
```
Structure:
  1. Base case (when to stop)
  2. Recursive case (reduce problem)
  3. Stack frame (tracks state)
  
Time: Usually O(branches^depth)
Space: Usually O(depth) stack

Examples:
  Factorial: T(n) = O(n), S(n) = O(n)
  Binary search: T(n) = O(log n), S(n) = O(log n)
  Fibonacci: T(n) = O(2^n), S(n) = O(n) memoized
```

---

## 🔄 Recommended Learning Path

**Best Order to Study:**

1. **Day 1:** RAM Model & Pointers
   - Understand computational foundation
   - Learn how memory access works
   - Why Big-O analysis is valid
   - Mental model for algorithms

2. **Day 2:** Asymptotic Analysis
   - Learn Big-O notation deeply
   - Practice deriving complexity
   - Understand growth rates
   - Compare algorithms

3. **Day 3:** Space Complexity
   - Analyze memory usage
   - Understand stack vs heap
   - Know trade-offs
   - Predict memory requirements

4. **Day 4:** Recursion I
   - Understand basic recursion
   - Write simple recursive functions
   - Trace execution by hand
   - Get comfortable with concept

5. **Day 5:** Recursion II
   - Advanced recursion patterns
   - Tail recursion optimization
   - Mutual recursion
   - Complex recursive problems

**Why This Order?**
- RAM model foundation for all analysis
- Big-O builds on RAM understanding
- Space complexity uses both
- Recursion needs understanding of both
- Advanced recursion caps the week

---

## ⚠️ Common Mistakes to Avoid

### Big-O Analysis

| Mistake | Fix |
|---------|-----|
| **Confusing worst, best, average** | State which case you're analyzing |
| **Including constants** | O(2n) = O(n), ignore coefficients |
| **Summing complexities wrong** | Nested loops: multiply, sequential: add |
| **Ignoring lower-order terms** | O(n² + n) = O(n²) |
| **Wrong for this data** | Complexity depends on input structure |

### Space Complexity

| Mistake | Fix |
|---------|-----|
| **Forgetting input space** | Often analyze only auxiliary space |
| **Not counting recursion depth** | Each call adds to stack |
| **Ignoring data structure overhead** | Hash table has O(n) space |

### Recursion

| Mistake | Fix |
|---------|-----|
| **Missing base case** | Always need stopping condition |
| **Base case never reached** | Verify problem reduces toward base |
| **Infinite recursion** | Each recursive call must get closer to base |
| **Stack overflow** | Recursion depth too deep for stack |
| **Wrong return value** | Think about what to return at each level |

---

## 🎓 Practice Problems Guide

### Big-O Analysis

**Easy:**
- Analyze simple loops
- Analyze nested loops
- Identify Big-O of code snippets
- Time: 15-20 min

**Medium:**
- Complex nested loops
- Multiple loops (sequential vs nested)
- Logarithmic patterns
- Time: 20-30 min

### Recursion

**Easy:**
- Factorial (n!)
- Power (x^n)
- Simple list operations
- Time: 15-25 min

**Medium:**
- Fibonacci
- Binary search
- Array problems recursively
- Time: 25-40 min

**Hard:**
- Permutations, combinations
- Backtracking patterns
- Time: 40-60 min

**Sources:** LeetCode (recursion), GeeksforGeeks, InterviewBit

---

## 💼 Interview Preparation

### Common Week 1 Questions

**Big-O Analysis:**
- "What's the time complexity of this algorithm?"
- "Can you optimize this? What's the trade-off?"
- "Why O(n log n) better than O(n²)?"
- "What's the space complexity?"

**Recursion:**
- "Implement factorial recursively"
- "Implement Fibonacci (optimize it)"
- "Trace this recursive function"
- "Convert recursion to iteration"

**Trade-offs:**
- "Why choose this data structure? Time vs space?"
- "When would you use recursion vs iteration?"
- "What if n is very large? What breaks?"

### Interview Tips
1. **Always state assumptions:** "I'll analyze worst case"
2. **Simplify before optimizing:** "First O(n²), then optimize"
3. **Discuss space/time trade-offs:** "Can use space to reduce time"
4. **Verify with examples:** "For n=5, this is..."
5. **Explain reasoning:** "Big-O matters because..."

---

## 🔗 Resources & References

### Online Platforms
- **LeetCode:** Problems to practice complexity analysis
- **GeeksforGeeks:** Big-O tutorials with explanations
- **InterviewBit:** Recursion problems
- **Khan Academy:** CS fundamentals

### Visualization Tools
- **Big-O Complexity Chart:** https://www.bigocheatsheet.com/
- **Recursion Visualizer:** https://www.recursionvisualizer.com/
- **Python Tutor:** https://pythontutor.com (step-by-step execution)

### Recommended Readings
- "Introduction to Algorithms" - CLRS (Chapter 2-3)
- "Cracking the Coding Interview" - Chapter 2
- "The Algorithm Design Manual" - Skiena (Chapter 1-2)

---

## ✅ Assessment & Success Criteria

### Knowledge Check
- [ ] Understand RAM model and why Big-O works
- [ ] Know 8 common time complexities and growth rates
- [ ] Difference between time and space complexity
- [ ] Stack vs heap memory (when to use each)
- [ ] How recursion uses stack memory

### Practical Skills
- [ ] Derive Big-O from simple code
- [ ] Analyze nested loop complexity
- [ ] Write correct base case in recursion
- [ ] Trace recursive function by hand
- [ ] Estimate runtime for given n

### Confidence Targets
| Concept | Target |
|---------|--------|
| RAM Model | 4-5/5 |
| Big-O Analysis | 4/5 |
| Space Complexity | 3-4/5 |
| Basic Recursion | 4/5 |
| Advanced Recursion | 3/5 |
| Overall Week 1 | 4/5 |

---

## 📊 Connection to Future Weeks

### Week 2: Linear Structures
```
Week 1 Big-O Analysis foundation
    ↓
Week 2 Know why arrays O(1) access, linked lists O(n)
    ↓
Understanding complexity essential for choosing structures
```

### Week 3: Sorting & Hashing
```
Week 1 Time complexity analysis
    ↓
Week 3 Compare O(n²) vs O(n log n) sorting
    ↓
Must understand growth rates to see difference
```

### Week 4+: Advanced Algorithms
```
Weeks 1-3 Foundations, Structures, Sorting
    ↓
Weeks 4+ Choose optimal algorithms based on complexity
    ↓
Week 1 analysis skills critical for entire curriculum
```

---

## ❓ Frequently Asked Questions

### Q1: Why spend a week on fundamentals? Can't I just start coding?

**A:** No. Understanding Big-O prevents writing terrible algorithms. Example: O(2^n) looks fine for n=20, breaks at n=30. Foundation prevents mistakes.

### Q2: Is Big-O exact or approximate?

**A:** Approximate (upper bound). O(n) could be 2n or 100n. Constants matter in practice, but Big-O simplifies algorithm comparison.

### Q3: My recursive solution is slow. How to optimize?

**A:** Often memoization (remember previous results). Example: Fibonacci O(2^n) → O(n) with memoization. Understanding is first step.

### Q4: Stack vs heap - which is faster?

**A:** Stack slightly faster (simpler allocation), but limited size. Heap slower but unlimited. Recursion limited by stack depth.

### Q5: Should I always use iteration instead of recursion?

**A:** Recursion cleaner for tree problems. Iteration for simple loops. Choose based on clarity and constraints.

### Q6: What if my code is O(n²) but n ≤ 1000?

**A:** Still might be fast enough (10^6 operations ≈ 0.01s). But O(n) is safer if achievable. Interview: mention both.

---

## 🎯 Before Moving to Week 2

**Checklist:**
- [ ] Understand RAM model conceptually
- [ ] Can derive Big-O from simple code
- [ ] Know 6+ common complexities and growth rates
- [ ] Understand stack vs heap distinction
- [ ] Write 5+ recursive functions correctly
- [ ] Can trace recursion by hand
- [ ] Overall confidence: 4/5 or higher

**If not ready:**
- Review Big-O analysis section
- Practice deriving complexity (10+ problems)
- Write 10+ recursive functions
- Don't rush to Week 2

---

## 📝 Week 1 Quick Summary

| Concept | Definition | Example | Importance |
|---------|-----------|---------|------------|
| **RAM Model** | O(1) memory access | CPU executes sequentially | Foundation for Big-O |
| **Big-O** | Upper bound on growth | O(n) linear, O(n²) quadratic | Compare algorithms |
| **Time Complexity** | Steps as function of n | Factorial O(n), Binary search O(log n) | Predict runtime |
| **Space Complexity** | Memory as function of n | Array O(n), Binary search O(log n) stack | Memory constraints |
| **Recursion** | Function calling itself | Factorial, Fibonacci, Trees | Elegant solutions |

---

**Status:** Week 1 Ready for Study ✓  
**Expected Completion:** 1 week focused study  
**Success Rate:** 90%+ with consistent practice  
**Cumulative Progress:** 10-15% of total curriculum (foundations)

