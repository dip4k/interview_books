# Week 1: Foundations - Daily Progress Checklist

**Week:** 1 | **Focus:** Daily learning outcomes, practice, and mastery verification  
**Date:** December 27, 2025

---

## DAY 1: RAM Model & Pointers

**Morning Objectives**
- [ ] Understand RAM model: memory is linear, addressable
- [ ] Know what pointers are and how to dereference them
- [ ] Understand pointer arithmetic on arrays
- [ ] Recognize cache locality importance

**Core Learning**
- [ ] Read: Week_1_Day_1_Instructional.md (Sections 1-4)
- [ ] Study: Real-world examples (Linux, Redis, graphics)
- [ ] Watch: Call stack visualization in memory

**Practice Problems** (Choose 3-5)
- [ ] Simple pointer dereferencing
- [ ] Pointer arithmetic (arr[i] vs *(arr+i))
- [ ] Identifying sequential vs random access
- [ ] Predicting cache hits vs misses
- [ ] Stack/heap allocation scenarios

**Afternoon Deep Dive**
- [ ] Read: Day 1 Sections 5-9 (Analysis, Real Systems, Math)
- [ ] Work through: 5 pointer arithmetic examples
- [ ] Trace: Memory layout with pointers
- [ ] Understand: Why cache locality is 100x important

**Knowledge Check** (Try without looking)
- [ ] Explain dereferencing in one sentence
- [ ] Draw memory layout for: int x=5; int* p=&x; int* q=p+1;
- [ ] Why is sequential access faster?
- [ ] What's the difference between address and value?

**Evening Synthesis**
- [ ] Read: Day 1 Sections 10-11 (Knowledge Check, Cognitive Lenses)
- [ ] Answer all 5 Socratic questions (Retention Hook)
- [ ] Explain 5 cognitive lenses (computational, psychological, design, AI/ML, historical)
- [ ] Review: 3 production system examples

**Mastery Checklist**
- [ ] Can explain RAM model without notes
- [ ] Can derive pointer arithmetic mentally
- [ ] Understand cache impact on performance
- [ ] Know when to care about memory layout
- [ ] Can explain in interview

**Confidence Rating**: ___ / 5

---

## DAY 2: Asymptotic Analysis (Big-O)

**Morning Objectives**
- [ ] Understand Big-O notation and why it matters
- [ ] Know complexity hierarchy: O(1) < O(log n) < O(n) < O(n²) < O(2^n)
- [ ] Count operations to derive complexity
- [ ] Distinguish Big-O, Big-Omega, Big-Theta

**Core Learning**
- [ ] Read: Week_1_Day_2_Instructional.md (Sections 1-4)
- [ ] Study: Real-world complexity examples (Netflix, Google, databases)
- [ ] Practice: Counting operations in code snippets

**Practice Problems** (Choose 5-7)
- [ ] Simple loop: O(n)
- [ ] Nested loops: O(n²)
- [ ] Binary search: O(log n)
- [ ] Two sequential loops: O(n)
- [ ] Logarithmic operations
- [ ] Complexity comparisons at different input sizes

**Afternoon Deep Dive**
- [ ] Read: Day 2 Sections 5-9 (Analysis, Real Systems, Math)
- [ ] Master Theorem: T(n) = aT(n/b) + f(n)
- [ ] Prove complexity from code (recurrence relations)
- [ ] Compare algorithms at scale (n=1M, n=1B)

**Knowledge Check** (Try without looking)
- [ ] Rank: O(1), O(n), O(n²), O(log n), O(2^n)
- [ ] For n=1,000,000: which is feasible?
- [ ] Why do constants not matter in Big-O?
- [ ] What's the recurrence for binary search?

**Evening Synthesis**
- [ ] Read: Day 2 Sections 10-11 (Knowledge Check, Cognitive Lenses)
- [ ] Answer all 5 Socratic questions
- [ ] Explain 5 cognitive lenses
- [ ] Create a Big-O cheat sheet

**Mastery Checklist**
- [ ] Can count operations to derive O(n²)
- [ ] Understand why O(2^n) is infeasible
- [ ] Know complexity hierarchy by heart
- [ ] Can compare algorithms intelligently
- [ ] Can pass Big-O interview questions

**Confidence Rating**: ___ / 5

---

## DAY 3: Space Complexity

**Morning Objectives**
- [ ] Understand space complexity = measure memory like Big-O measures time
- [ ] Distinguish stack (recursion) from heap (allocation)
- [ ] Analyze space usage in algorithms
- [ ] Recognize space-time tradeoffs

**Core Learning**
- [ ] Read: Week_1_Day_3_Instructional.md (Sections 1-4)
- [ ] Study: Real-world constraints (mobile OOM, cloud costs, embedded)
- [ ] Visualize: Stack growing with recursion depth

**Practice Problems** (Choose 4-6)
- [ ] Simple algorithm space: O(1)
- [ ] Temporary array space: O(n)
- [ ] Recursion depth space: O(depth)
- [ ] Stack overflow predictions
- [ ] Memoization space tradeoff
- [ ] In-place vs extra-space algorithms

**Afternoon Deep Dive**
- [ ] Read: Day 3 Sections 5-9 (Analysis, Real Systems, Math)
- [ ] Identify stack vs heap allocations
- [ ] Predict stack overflow (depth > 100K)
- [ ] Evaluate space-time tradeoffs practically

**Knowledge Check** (Try without looking)
- [ ] What's the space of factorial(n)?
- [ ] Stack size typical: ___ MB
- [ ] Memoization: costs ___ space for ___ speedup
- [ ] When should you optimize for space?

**Evening Synthesis**
- [ ] Read: Day 3 Sections 10-11 (Knowledge Check, Cognitive Lenses)
- [ ] Answer all 5 Socratic questions
- [ ] Explain 5 cognitive lenses
- [ ] Real-world example: mobile app with 512MB RAM

**Mastery Checklist**
- [ ] Analyze space complexity of any algorithm
- [ ] Understand stack vs heap
- [ ] Predict stack overflow
- [ ] Reason about space constraints
- [ ] Can explain space-time tradeoff

**Confidence Rating**: ___ / 5

---

## DAY 4: Recursion I

**Morning Objectives**
- [ ] Understand recursion: function calls itself on smaller problem
- [ ] Know base case is mandatory
- [ ] Understand call stack and recursion depth
- [ ] Analyze recursive time and space

**Core Learning**
- [ ] Read: Week_1_Day_4_Instructional.md (Sections 1-4)
- [ ] Study: Real-world recursion (file systems, DOM, parsing)
- [ ] Trace: Recursive calls by hand (draw call tree)

**Practice Problems** (Choose 5-8)
- [ ] Factorial recursively
- [ ] Array sum recursively
- [ ] Binary search recursively
- [ ] Write base case correctly
- [ ] Prevent infinite recursion
- [ ] Analyze recursion depth
- [ ] Derive recurrence relations
- [ ] Trace execution by hand

**Afternoon Deep Dive**
- [ ] Read: Day 4 Sections 5-9 (Analysis, Real Systems, Math)
- [ ] Master recurrence relations: T(n) = T(n-1) + O(1) = O(n)
- [ ] Understand mutual recursion (parsing)
- [ ] Identify when recursion is natural

**Knowledge Check** (Try without looking)
- [ ] What happens without base case?
- [ ] Recursion depth of factorial(5)?
- [ ] Recurrence for binary search?
- [ ] Is recursion better or worse than iteration?

**Evening Synthesis**
- [ ] Read: Day 4 Sections 10-11 (Knowledge Check, Cognitive Lenses)
- [ ] Answer all 5 Socratic questions
- [ ] Explain 5 cognitive lenses
- [ ] Trace fib(4) completely by hand

**Mastery Checklist**
- [ ] Write recursive solutions
- [ ] Trace recursion by hand
- [ ] Understand call stack growth
- [ ] Derive recursion complexity
- [ ] Prevent stack overflow
- [ ] Know when recursion is appropriate

**Confidence Rating**: ___ / 5

---

## DAY 5: Recursion II

**Morning Objectives**
- [ ] Understand tail recursion and compiler optimization
- [ ] Apply memoization to eliminate recomputation
- [ ] Recognize mutual recursion patterns
- [ ] Optimize exponential-time algorithms

**Core Learning**
- [ ] Read: Week_1_Day_5_Instructional.md (Sections 1-4)
- [ ] Study: Tail recursion vs iteration
- [ ] Practice: Adding memoization to recursive functions

**Practice Problems** (Choose 6-9)
- [ ] Convert to tail-recursive form
- [ ] Add memoization to Fibonacci
- [ ] Identify mutual recursion
- [ ] Analyze factorial (tail vs non-tail)
- [ ] Optimize O(2^n) to O(n)
- [ ] Recognize when memoization helps
- [ ] Predict speedup from caching
- [ ] Implement parsing recursion
- [ ] Advanced: backtracking with pruning

**Afternoon Deep Dive**
- [ ] Read: Day 5 Sections 5-9 (Analysis, Real Systems, Math)
- [ ] Understand compiler tail-call optimization
- [ ] Master memoization technique
- [ ] Design recursive solution with caching
- [ ] Prove Fibonacci optimization mathematically

**Knowledge Check** (Try without looking)
- [ ] What makes recursion "tail-recursive"?
- [ ] Will Python optimize tail calls?
- [ ] Fibonacci: 2^n → ___ with memoization
- [ ] Memoization cost/benefit?

**Evening Synthesis**
- [ ] Read: Day 5 Sections 10-11 (Knowledge Check, Cognitive Lenses)
- [ ] Answer all 5 Socratic questions
- [ ] Explain 5 cognitive lenses
- [ ] Implement optimized Fibonacci from scratch

**Mastery Checklist**
- [ ] Convert to tail-recursive form
- [ ] Add memoization correctly
- [ ] Analyze time/space tradeoff
- [ ] Recognize optimization opportunities
- [ ] Implement mutual recursion
- [ ] Know language compiler behavior

**Confidence Rating**: ___ / 5

---

## WEEKLY INTEGRATION & VERIFICATION

### **Weekend Synthesis (3-5 hours)**

**Step 1: Concept Integration** (60 min)
- [ ] Read: Week_1_Summary_Key_Concepts.md (all sections)
- [ ] Review: Mental models for each day
- [ ] Create: One-page cheat sheet with formulas

**Step 2: Interview Preparation** (60 min)
- [ ] Read: Week_1_Interview_QA_Reference.md
- [ ] Answer: 10-15 Q&A pairs (mixed topics)
- [ ] Review: Answers you got wrong
- [ ] Understand: Why you were wrong

**Step 3: Problem-Solving Practice** (90 min)
- [ ] Read: Week_1_Problem_Solving_Roadmap.md
- [ ] Solve: 5 mixed problems (1 per topic)
- [ ] Trace: Each solution completely
- [ ] Verify: Complexity is correct

**Step 4: Knowledge Verification** (45 min)
- [ ] Rate confidence on each day (1-5 scale)
- [ ] Identify weak areas
- [ ] Revisit lowest-confidence topics
- [ ] Answer Socratic questions from each day

**Step 5: Application to Real Code** (60 min)
- [ ] Find: Real algorithm in production (sort, search, etc.)
- [ ] Analyze: Complexity and space
- [ ] Identify: Cache behavior
- [ ] Predict: Performance on large inputs

---

## MASTERY ASSESSMENT

### **Self-Assessment (Rate 1-5 on each)**

| Competency | Day 1 | Day 2 | Day 3 | Day 4 | Day 5 |
|------------|-------|-------|-------|-------|-------|
| **Understanding** | ___ | ___ | ___ | ___ | ___ |
| **Skill Application** | ___ | ___ | ___ | ___ | ___ |
| **Problem Solving** | ___ | ___ | ___ | ___ | ___ |
| **Explanation** | ___ | ___ | ___ | ___ | ___ |
| **Confidence** | ___ | ___ | ___ | ___ | ___ |

**Target:** 4/5 on all before Week 2

### **Practical Skills Verification**

Check each skill:
- [ ] Day 1: Trace pointer arithmetic mentally
- [ ] Day 2: Derive O(n²) from nested loops
- [ ] Day 3: Calculate stack depth for recursion
- [ ] Day 4: Write and trace recursive function
- [ ] Day 5: Add memoization to exponential function

### **Interview Readiness**

Can you answer without notes:
- [ ] "Explain pointers in one sentence" ✓ / ❌
- [ ] "What's the complexity hierarchy?" ✓ / ❌
- [ ] "Why does space matter?" ✓ / ❌
- [ ] "How does recursion work?" ✓ / ❌
- [ ] "What is memoization?" ✓ / ❌

---

## BEFORE MOVING TO WEEK 2

### **Critical Checklist**

- [ ] Completed all 5 daily instructional files
- [ ] Answered all Socratic questions correctly
- [ ] Solved 5+ practice problems per day
- [ ] Understand all 5 cognitive lenses
- [ ] Can explain each concept in interview
- [ ] Rate 4/5 or higher on all competencies

### **Red Flags (Get Help If Present)**

- ❌ "I don't understand what a pointer is"
- ❌ "I can't derive Big-O from code"
- ❌ "Recursion still confuses me"
- ❌ "I don't see why space complexity matters"
- ❌ "I can't trace recursion by hand"

**If any red flag present:** Revisit that day before moving on.

### **Resources for Weak Areas**

**Weak on Pointers?**
- Revisit Day 1 Section 3 (Mechanical Walkthrough)
- Watch: MIT OCW lecture on pointers
- Practice: 10 pointer arithmetic problems

**Weak on Big-O?**
- Revisit Day 2 Section 3 (Mechanical Walkthrough)
- Abdul Bari YouTube: Asymptotic analysis
- Practice: Derive complexity for 20 different snippets

**Weak on Recursion?**
- Revisit Day 4-5 Section 3 (Mechanical Walkthrough)
- Visualizer: https://www.recursionvisualizer.com/
- Practice: Trace 20 different recursive functions

**Weak on Space?**
- Revisit Day 3 Section 3 (Mechanical Walkthrough)
- Practice: Analyze space for 15 algorithms

---

## WEEK 1 COMPLETION SIGN-OFF

### **Final Verification**

**Knowledge:** I understand the core concepts
- [ ] RAM Model & Pointers (Day 1)
- [ ] Asymptotic Analysis (Day 2)
- [ ] Space Complexity (Day 3)
- [ ] Recursion I (Day 4)
- [ ] Recursion II (Day 5)

**Skills:** I can apply these concepts
- [ ] Predict algorithm performance
- [ ] Analyze space usage
- [ ] Write and optimize recursive code
- [ ] Count operations correctly
- [ ] Make intelligent algorithm choices

**Confidence:** I can discuss with experts
- [ ] Explain in interviews
- [ ] Teach others
- [ ] Debug performance issues
- [ ] Optimize for constraints
- [ ] Reason about real systems

**Readiness for Week 2:** YES / NO

If YES: Proceed to Week 2 (Linear Structures)
If NO: Spend 1-2 more days on weak areas, then re-assess

---

## WEEK 1 SUMMARY

**Time Invested:** ~15 hours (5 days × 3 hrs)
**Topics Mastered:** 5 foundational concepts
**Problems Solved:** 25-40 practice problems
**Interview Prep:** 60 Q&A pairs reviewed
**Real-world Examples:** 25+ production systems

**Result:** Ready for Week 2, with strong theoretical foundation

**Next:** Week 2 (Linear Structures) - Apply these concepts to arrays, lists, stacks, queues, binary search

---

## PROGRESS TRACKING GRAPH

```
Mastery Level Over Week 1:

Day 1:  ███░░░░░░  30% (Just learning concepts)
Day 2:  █████░░░░  50% (Understanding relationships)
Day 3:  ███████░░  70% (Applying concepts)
Day 4:  █████████░ 90% (Deep mastery)
Day 5:  ██████████ 100% (Integration complete)
```

---

## Congratulations! 🎉

**You've completed Week 1: Foundations**

You now understand:
- How computers work (RAM Model)
- How to measure algorithms (Big-O)
- How to optimize memory (Space Complexity)
- How to solve recursively (Recursion I & II)

**You're ready for Week 2: Linear Structures**

