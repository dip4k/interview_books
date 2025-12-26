# Recursion II: Advanced Recursion & Optimization

## 🗓 Metadata
**Topic:** Recursion II  
**Week:** Week 1  
**Day:** Day 5 of 5  
**Category:** Foundations  
**Difficulty:** 🔴 Hard  
**Status:** 🔍 In Study  
**Last Reviewed:** —  
**Confidence Level (1–5):** —/5

---

## 1️⃣ The Why — Engineering Motivation

### Real-World Problem

Yesterday you learned basic recursion. Now: **How do you make recursion fast enough for production?**

Consider the classic Fibonacci sequence: `fib(5) = 5`. The naive recursive definition is:
```
fib(n) = fib(n-1) + fib(n-2)
```

This recomputes the same values thousands of times. `fib(40)` requires ~2 billion recursive calls! That's unusable.

Real systems can't afford such waste. They need optimization techniques:

**Real Examples:**
- **JavaScript engines:** Optimize recursive functions with memoization caching
- **Database query optimization:** Convert recursive CTEs to iterative execution plans
- **Compiler tail-call optimization:** Recognize patterns like `return f(x)` and convert to jumps (not calls)
- **JVM (Java Virtual Machine):** Some languages (Scala) use trampolines to optimize recursion
- **Python generators:** Convert recursion to lazy iterators (generator pattern)

### Design Problem Solved

1. **Eliminate redundant computation:** Cache results of subproblems (memoization)
2. **Convert to iteration:** Transform recursion to loops (tail-call optimization, trampolines)
3. **Reduce memory:** Stack space reduction via optimization
4. **Handle mutual recursion:** Multiple functions calling each other
5. **Lazy evaluation:** Compute only needed values (generators)

### Trade-offs Introduced

- **Cache memory:** Memoization trades computation time for memory usage
- **Code complexity:** Optimization techniques add complexity
- **Debuggability:** Optimized code is harder to trace mentally

### Real System Usage

- **Dynamic programming:** Memoized recursion is the foundation (Week 11)
- **Functional programming languages:** Scheme, Haskell have tail-call optimization built-in
- **Compiler back-ends:** Tail recursion → loops conversion in code generation
- **Graphics rendering:** Recursive ray-tracing optimized with memoization and iterative approaches
- **Graph algorithms:** DFS implemented recursively, optimized with memoization for DP

---

## 2️⃣ The What — Mental Model & Intuition

### Core Analogy

**Think of memoization like taking notes in a test.**

Without notes (naive recursion): When you're asked "What's 5×3?", you compute it. Later, you're asked "What's 5×3?" again, and you recompute it (wasteful!).

With notes (memoization): You write "5×3=15" after first computation. Next time, you look it up (instant!).

**Tail recursion** is different: It's like a letter carrier making deliveries. Instead of returning home after each delivery, each carrier **hands off to the next carrier**, who continues the route. No backtracking needed.

### Visual Representation

**Naive Fibonacci recursion tree:**
```
                    fib(5)
                   /      \
              fib(4)        fib(3)
             /      \       /     \
        fib(3)   fib(2)  fib(2)  fib(1)
       /     \    /   \   /   \
    fib(2) fib(1) fib(1) f(0) f(1) f(0)
    /  \
fib(1) fib(0)

Notice: fib(3) computed twice, fib(2) computed 3 times!
```

**With memoization:** Each node computed once, then looked up in cache.

```
                    fib(5) → cache[5]
                   /      \
              fib(4)        fib(3)
              (cache)       (cache)
```

### Core Invariants

1. **Memoization invariant:** If `memo[n]` exists, return it immediately (no recomputation)
2. **Tail recursion invariant:** The recursive call's result is directly returned (no combining needed)
3. **Mutual recursion invariant:** All mutually recursive functions exist and are defined

### Key Concepts

- **Memoization:** Caching results of expensive function calls (top-down DP)
- **Tail recursion:** Last operation is a recursive call; enables stack reuse
- **Tail-call optimization (TCO):** Compiler converts tail recursion to loop
- **Trampolines:** Indirect recursion via functions returning functions (functional pattern)
- **Mutual recursion:** Functions calling each other in cycles

---

## 3️⃣ The How — Mechanical Walkthrough

### State/Data Structure

**For Memoization:**
```
Cache structure:
  memo = { n → result }
  
Example for Fibonacci:
  memo[0] = 0
  memo[1] = 1
  memo[2] = 1
  memo[3] = 2
  memo[4] = 3
  memo[5] = 5
```

**For Tail Recursion:**
```
State tracking:
  accumulator = current_result
  n = remaining_work
```

### Operation 1: Memoized Recursive Call

**Step-by-step:**

1. Check if `memo[n]` exists
2. If yes, **return immediately** without recursion
3. If no, compute recursively and **store in memo** before returning
4. Recursive call also checks memo, finding previously computed values

**Cost:** O(1) for cache lookup + O(1) for cache store

### Operation 2: Tail-Call Conversion

**Before (tail recursion):**
```
sum_tail(n, acc=0):
  if n == 0: return acc
  return sum_tail(n-1, acc+n)  ← Tail call (last operation)
```

**After (compiler optimization → loop):**
```
sum_loop(n):
  acc = 0
  while n > 0:
    acc += n
    n -= 1
  return acc
```

The compiler recognizes the tail call and converts it to loop:
1. Save current state in variables
2. Update state for next iteration
3. Jump back to function start (not new call)
4. No new stack frame created

### Operation 3: Mutual Recursion

**Example:** Is a number even/odd?

```
is_even(n):
  if n == 0: return True
  return is_odd(n-1)

is_odd(n):
  if n == 0: return False
  return is_even(n-1)
```

**Mechanical execution:**
1. `is_even(4)` calls `is_odd(3)`
2. `is_odd(3)` calls `is_even(2)`
3. `is_even(2)` calls `is_odd(1)`
4. `is_odd(1)` calls `is_even(0)` → returns True

Stack shows interleaving calls:
```
[is_even(4) → waiting]
  [is_odd(3) → waiting]
    [is_even(2) → waiting]
      [is_odd(1) → waiting]
        [is_even(0) → returns True]
```

### Memory Behavior

**Memoization memory:**
- Cache grows with each new subproblem solved
- O(unique subproblems) space
- Subsequent lookups are O(1) cache hit

**Tail recursion memory:**
- Stack frame reused (single frame for entire computation)
- O(1) stack space (when optimized)
- Without optimization: O(n) stack space (each call creates frame)

---

## 4️⃣ Visualization — Simulation & Examples

### Example 1: Fibonacci with Memoization

**Initial state:**
```
Input: fib(5)
Cache: {} (empty)
Goal: Compute F(5) = 5 with caching
```

**Step-by-step execution:**

```
fib(5):
  Cache miss. Compute:
    fib(4):
      Cache miss. Compute:
        fib(3):
          Cache miss. Compute:
            fib(2):
              Cache miss. Compute:
                fib(1):
                  Cache hit! Return 1
                fib(0):
                  Cache hit! Return 0
              Result: 1+0=1
              Store cache[2]=1
              Return 1
            fib(1):
              Cache hit! Return 1
          Result: 1+1=2
          Store cache[3]=2
          Return 2
        fib(2):
          Cache hit! Return 1 ← Avoided recomputation!
      Result: 2+1=3
      Store cache[4]=3
      Return 3
    fib(3):
      Cache hit! Return 2 ← Avoided recomputation!
  Result: 3+2=5
  Store cache[5]=5
  Return 5

Final cache:
  {0:0, 1:1, 2:1, 3:2, 4:3, 5:5}
```

**Complexity comparison:**

| Calls | Naive | Memoized |
|-------|-------|----------|
| fib(5) | 15 calls | 5 calls + 5 lookups |
| fib(10) | 177 calls | 10 calls + lookups |
| fib(20) | 21,891 calls | 20 calls |

### Example 2: Tail Recursion — Sum

**Tail recursive version:**
```
sum_tail(arr, index=0, accumulator=0):
  if index == len(arr): return accumulator
  return sum_tail(arr, index+1, accumulator+arr[index])
```

**Execution trace:**

```
sum_tail([1,2,3,4], 0, 0):
  index < 4, so:
  return sum_tail([1,2,3,4], 1, 0+1)
         sum_tail([1,2,3,4], 1, 1):
           index < 4, so:
           return sum_tail([1,2,3,4], 2, 1+2)
                  sum_tail([1,2,3,4], 2, 3):
                    index < 4, so:
                    return sum_tail([1,2,3,4], 3, 3+3)
                           sum_tail([1,2,3,4], 3, 6):
                             index < 4, so:
                             return sum_tail([1,2,3,4], 4, 6+4)
                                    sum_tail([1,2,3,4], 4, 10):
                                      index == 4
                                      return 10
```

**With tail-call optimization (compiler converts to loop):**

```
Stack state (optimized):
index | accumulator
-----|-------------
0    | 0
1    | 1
2    | 3
3    | 6
4    | 10 → return

Only 1 stack frame reused 5 times, not 5 nested frames!
```

### Example 3: Mutual Recursion — Even/Odd

**Initial state:**
```
Input: is_even(4)
Goal: Determine if 4 is even using mutual recursion
```

**Execution:**

```
is_even(4):
  4 == 0? No
  Call is_odd(3)
    is_odd(3):
      3 == 0? No
      Call is_even(2)
        is_even(2):
          2 == 0? No
          Call is_odd(1)
            is_odd(1):
              1 == 0? No
              Call is_even(0)
                is_even(0):
                  0 == 0? Yes
                  Return True
              is_odd returns: True
            is_even returns: True
          is_odd returns: True
        is_even returns: True
      is_odd returns: True
    is_even returns: True

Result: True (4 is even) ✓
```

**Stack at deepest point:**
```
[is_even(0)]
[is_odd(1)]
[is_even(2)]
[is_odd(3)]
[is_even(4)]
```

---

## 5️⃣ Critical Analysis — Performance & Robustness

### Complexity Table

| Technique | Time | Space | Notes |
|-----------|------|-------|-------|
| **Naive recursion** (fib) | O(2^n) | O(n) stack | Exponential calls |
| **Memoized recursion** (fib) | O(n) | O(n) cache + O(n) stack | Linear calls |
| **Tail recursion (optimized)** | O(n) | O(1) stack | Compiler converts to loop |
| **Tail recursion (unoptimized)** | O(n) | O(n) stack | Each call creates frame |
| **Mutual recursion** | O(n) | O(n) stack | Stack grows with depth |

### Memory Access Patterns

**Memoization:**
- Cache miss on new subproblems (main memory access)
- Cache hit on repeated lookups (L1/L2 cache hit, ~1 cycle)
- Memory allocation for cache (hash map grows dynamically)

**Tail recursion (optimized):**
- Same memory access as loop
- Stack frame reused (excellent cache locality)
- No new allocations

**Tail recursion (unoptimized):**
- New frame per call
- Stack memory allocation/deallocation overhead
- Stack access is cache-friendly but repeated allocation isn't

### Edge Cases & Failure Modes

| Failure | Cause | Example |
|---------|-------|---------|
| **Stack overflow in memoization** | Cache grows too large | memoizing fib(100,000) needs huge cache |
| **Cache memory exhausted** | Too many unique subproblems | Some DP problems have O(n²) subproblems |
| **No tail-call optimization** | Python, Java don't optimize tail calls | Deep tail recursion still overflows |
| **Incorrect memoization** | Forgetting to cache, or caching wrong value | Returns computed but doesn't store |
| **Mutual recursion infinite loop** | Base cases unreachable | `even(n) ↔ odd(n)` with no base cases |

### When Complexity Analysis Breaks Down

1. **Cache effects:** TCO reduces stack space, but actual speed depends on loop overhead
2. **Memoization overhead:** For small n, lookup might be slower than recomputation
3. **Hash table collision:** Cache lookup isn't always O(1) (hash collisions cause O(log n) or worse)
4. **Memory fragmentation:** Memoization cache can fragment memory (practical issue in C/C++)

---

## 6️⃣ Real System Integration

### Databases

**Recursive CTEs (Common Table Expressions):**

Modern databases execute recursive CTEs by:
1. Iterative evaluation (not true recursion)
2. Memoization of intermediate results
3. Efficient union operations

**Example:** Finding all organizational hierarchy
```
WITH RECURSIVE org_tree AS (
  SELECT id, name, manager_id FROM employees WHERE manager_id IS NULL
  UNION
  SELECT e.id, e.name, e.manager_id FROM employees e 
  JOIN org_tree ON e.manager_id = org_tree.id
)
SELECT * FROM org_tree;
```

The database:
1. Starts with managers (base case)
2. Memoizes results
3. Iteratively joins with subordinates

### Compilers & Language Runtimes

**Tail-call optimization (TCO):**

Languages like Scheme, Scala, and modern JavaScript (strict mode) apply TCO:
```
Scheme: (define (sum n acc) (if (= n 0) acc (sum (- n 1) (+ acc n))))
→ Compiler detects tail call, converts to loop
→ No stack overflow for large n
```

**Python:** Notably **does NOT** optimize tail calls (by design; for debuggability)
```
Python: def sum(n, acc=0): 
          if n == 0: return acc
          return sum(n-1, acc+n)  ← Still creates new frame!
```

### Graphics Engines

**Ray tracing with memoization:**

Ray-tracing recursively bounces rays:
```
trace_ray(ray, depth):
  if depth > MAX_DEPTH: return base_color
  intersection = find_nearest_hit(ray)
  local_color = compute_lighting(intersection)
  reflected = trace_ray(reflect(ray, intersection), depth+1)
  refracted = trace_ray(refract(ray, intersection), depth+1)
  return combine(local, reflected, refracted)
```

Optimization: Memoize by ray direction (approximate, probabilistic caching).

### JavaScript Engine Optimizations

**V8 (Chrome's JavaScript engine):**

1. Detects tail calls in strict mode
2. Optimizes with "jump" instead of "call"
3. Stack remains flat

**Example:**
```javascript
'use strict';
function sum(n, acc = 0) {
  if (n === 0) return acc;
  return sum(n - 1, acc + n);  // Tail call optimized in V8
}
```

---

## 7️⃣ Concept Crossovers

### What It Builds On (Prerequisites)

- **Day 4 (Recursion I):** Basic recursive structure, stack frames
- **Week 2: Arrays/Lists:** Memoization cache often uses hash maps or arrays
- **Week 3: Hash Tables:** Memoization relies on fast caching
- **Asymptotic analysis (Week 1):** Understanding O(2^n) → O(n) improvement

### What Builds On It (Successors)

- **Dynamic Programming (Week 11):** Memoization is the core technique
- **Backtracking (Week 10):** Pruning with memoization
- **Graph algorithms (Weeks 6-7):** DFS with memoization for shortest paths
- **Functional programming patterns:** Memoization, recursion schemes

### Applications in Algorithms

- **Fibonacci:** O(2^n) naive → O(n) memoized
- **Longest Common Subsequence:** Recursive with memoization
- **Tree recursion with caching:** Optimal substructure problems
- **Graph traversal:** DFS with memoization for strong components
- **Compiler optimization:** Tail-call recognition in code generation

### Combinations with Other Techniques

- **Recursion + Memoization:** Top-down DP (Week 11)
- **Recursion + Trampolines:** Avoiding stack issues (advanced)
- **Tail recursion + Accumulator:** Tail-call patterns
- **Mutual recursion + Memoization:** Efficient mutual dependencies

---

## 8️⃣ Mathematical & Theoretical Perspective

### Formal Definition

**Memoized recursion (top-down DP):**
```
memo = {}

f(n):
  if n in memo:
    return memo[n]
  
  if base_case(n):
    result = base_value(n)
  else:
    result = combine(f(n-1), f(n-2), ...)
  
  memo[n] = result
  return result
```

**Tail recursion:**
```
f(n, accumulator):
  if terminal_condition(n):
    return accumulator
  return f(n-1, accumulator ⊕ operation(n))
```

### Proof Sketch

**Why memoization preserves correctness:**

1. **Correctness invariant:** `memo[n]` stores correct result for f(n)
2. **Base case:** memo initialized with correct base case values
3. **Recursive case:** If memo lookup succeeds, value is correct (by invariant)
4. **Recomputation:** If not in memo, we recompute (recursive call) and store
5. **Conclusion:** memoized function returns same result as non-memoized, but faster

**Why tail recursion optimization is correct:**

Tail recursion: `return f(x)` (last operation is returning recursive call)

Optimization: Reuse stack frame (jump, don't call)

- No state to preserve (nothing after the recursive call)
- Jump destination is same function
- Local variables go out of scope
- Therefore: Safe to reuse frame (semantically equivalent to jump)

### Recurrence Relation

**Naive Fibonacci:**
```
T(n) = T(n-1) + T(n-2) + O(1)
T(0) = T(1) = O(1)

Solution: T(n) = O(φ^n) ≈ O(1.618^n)
```

**Memoized Fibonacci:**
```
T(n) = T(n-1) + O(1)  [Each subproblem solved once]
T(0) = T(1) = O(1)

Solution: T(n) = O(n)
```

**Space complexity with memoization:** O(number of unique subproblems)

### Theoretical Models

**Master Theorem (recurrence analysis):**

For `T(n) = aT(n/b) + f(n)`:
- **a = 1, b = 1:** Linear recursion (unbranched), O(n)
- **a = 2, b = 2:** Binary tree recursion, O(2^n) without memoization, O(n) with
- **a = 2, b = 2, f(n) = O(n):** T(n) = O(n log n) (merge sort)

---

## 9️⃣ Algorithmic Design Intuition

### When to Use Memoization

1. **Overlapping subproblems:** Same subproblem solved multiple times
2. **Optimal substructure:** Solution to problem built from optimal solutions to subproblems
3. **Bounded subproblem space:** Number of unique subproblems is tractable

**Examples:** Fibonacci, coin change, LCS (longest common subsequence)

### When to Use Tail Recursion

1. **Linear accumulation:** Computing sum, product, count in a loop
2. **Avoiding stack overflow:** With TCO, same efficiency as iteration
3. **Functional style:** Language supports TCO (Scheme, Scala, JavaScript strict mode)

**Examples:** Summing array, factorial (with accumulator), list reduction

### When to Use Mutual Recursion

1. **Two or more interdependent concepts:** Even/odd, male/female trees
2. **Deferred decisions:** Don't know which function to call until runtime
3. **Logical clarity:** Two functions are conceptually separate

**Examples:** Even/odd checking, grammar parsing (mutually recursive rules)

### Decision Framework

```
Problem has overlapping subproblems?
  ├─ YES: Use memoization (top-down DP)
  │  └─ Space for cache? Use it; else convert to bottom-up DP
  │
  └─ NO: Is last operation a recursive call?
     ├─ YES: Use tail recursion (compiler will optimize)
     │  └─ Does language support TCO? If no, convert to iteration
     │
     └─ NO: Use basic recursion (OK if depth < 1000)
```

### Trade-off Scenarios

| Scenario | Naive | Memoized | Tail-Recursive | Iteration |
|----------|-------|----------|----------------|-----------|
| Fibonacci(40) | ~2B calls | ~40 calls | N/A | O(n) loop |
| Computing sum(arr) | O(n) stack | Unnecessary | O(1) stack (opt) | O(1) stack |
| Even/odd(1M) | Stack overflow | No help | TCO needed | O(n) loop |
| DFS tree traversal | O(depth) stack | Helps if revisit | Not applicable | O(n) with stack |

---

## 🔟 Knowledge Check — Socratic Reasoning

**Question 1: Memoization Trade-off**

Memoization trades computation time for memory. When is this trade-off **not worth it**? Provide a specific example.

*Your reasoning:*
- What's the cost of cache lookup vs recomputation?
- When is an O(1) calculation so cheap that caching is wasteful?
- Consider cache memory pressure on systems with limited RAM

---

**Question 2: Tail Recursion Without Optimization**

You write tail-recursive code in Python (which doesn't support TCO). What happens? Why doesn't Python optimize tail calls like other languages?

*Your reasoning:*
- What's the stack behavior without TCO?
- Why might Python designers choose not to optimize?
- What's the trade-off between stack overflow risk and debuggability?

---

**Question 3: Mutual Recursion Termination**

In mutual recursion, how do you ensure termination? What happens if both functions call each other without reaching a base case?

*Your reasoning:*
- What defines a "base case" in mutual recursion?
- Can you have a cycle without infinite recursion?
- How would you design base cases for even/odd checking?

---

**Question 4: Memoization Space Complexity**

In dynamic programming, cache space is O(number of subproblems). When does this become problematic?

*Your reasoning:*
- How many subproblems exist for fib(n)?
- How many for edit distance on two strings of length n and m?
- When is O(n²) cache memory acceptable? When is it too much?

---

**Question 5: Comparing Approaches**

You need to compute factorial(1000000). Should you use:
A) Naive recursion
B) Memoized recursion
C) Tail recursion
D) Iteration

Justify your choice and explain why the others fail.

*Your reasoning:*
- What's the stack depth limit?
- Does memoization help here?
- Does the language support TCO?

---

## 1️⃣1️⃣ Retention Hook — Memory Anchors

### One-Line Essence

> **Memoization = Caching subproblem results to convert exponential recursion to polynomial. Tail recursion = Function calls that return immediately, enabling stack reuse (TCO).**

### Mnemonic Device

**"MEMO-TAIL"** — **MEMO**ization, **TAIL** recursion

Explanation:
- **M — Memoization:** Cache results of expensive subproblems
- **E — Exponential avoidance:** Prevent recomputing same subproblem
- **M — Memory trade-off:** Use cache memory to save computation time
- **O — Overlapping subproblems:** Only useful if subproblems repeat
- **T — Tail call:** Last operation is a recursive call
- **A — Accumulator:** Tail recursion uses accumulator to avoid combining
- **I — Iteration-like:** Tail recursion acts like a loop (with TCO)
- **L — Language support:** Not all languages optimize tail calls

### Geometric/Visual Cue

**Memoization as a pyramid (top to bottom avoids recomputation):**
```
           fib(5)
          /      \
      fib(4)    fib(3) ← Would be recomputed without cache
      /    \     /    \
  fib(3)  fib(2) ← Cache hit! Avoid recomputation
  /    \   /  \
fib(2) fib(1)  ...
  
With memo: fib(3) computed once, fib(2) computed once, etc.
Without: fib(3) computed twice, fib(2) computed three times!
```

**Tail recursion as a loop unwinding (stack reuse):**
```
Without TCO:
[sum(4, 0)]     ← Stack grows
[sum(3, 1)]
[sum(2, 3)]
[sum(1, 6)]
[sum(0, 10)] → return 10

With TCO (jump, not call):
sum(4, 0) → sum(3, 1) → sum(2, 3) → sum(1, 6) → sum(0, 10)
All using SAME stack frame, just update state
```

### Cognitive Lenses

| Lens | Insight |
|------|---------|
| **Computational** | Memoization trades time for space; TCO trades clarity for efficiency |
| **Psychological** | Memoization = laziness (avoid repeat work); TCO = recognition (compiler sees pattern) |
| **Design** | Both optimize recursion; different techniques for different problems |
| **Historical** | Memoization formalized by Bellman (dynamic programming); TCO from lambda calculus |

---

## 🧩 Cognitive & Meta Layers

### Understanding Memoization Deeply

The key insight: **Exponential blowup is caused by recomputation, not recursion itself.**

Example: `fib(5)` calls `fib(3)` twice, `fib(2)` three times, etc.
- With memoization: Each unique input computed **exactly once**
- This converts O(2^n) to O(n)

This is the foundation of dynamic programming (Week 11).

### Understanding Tail Recursion Deeply

The insight: **Tail recursion looks recursive, but acts like iteration.**

When the last operation is `return f(x)`, there's nothing to do after `f(x)` returns:
- No combining results
- No using returned value in further computation
- So the stack frame can be reused (jump, not call)

Different languages make different choices:
- Functional languages (Haskell, Scheme): TCO is guaranteed
- Imperative languages (C, Java): Compiler may or may not optimize
- Python: Intentionally doesn't optimize (for debugging)

### Common Misconceptions

1. **"Memoization means storing everything"** — No; only cache needed subproblems
2. **"Tail recursion is slower than iteration"** — No; with TCO, they're equivalent
3. **"Tail recursion is the same as normal recursion"** — No; only the *form* of tail recursion enables TCO
4. **"Mutual recursion is always inefficient"** — No; if base cases are reachable and functions are simple, it's fine

---

## 🔁 Revision & Spaced Repetition

Track your understanding over time:

| Review Date | Confidence (1–5) | Strengths | Areas to Deepen | Next Review |
|---|---|---|---|---|
| 2025-12-26 | — | — | — | 2025-12-28 |
| | | | | |
| | | | | |
| | | | | |

---

## 📚 Reference Pointers

### Textbooks

- **CLRS (Intro to Algorithms):** Chapter 15 (Dynamic Programming) — memoization formalized
- **Structure and Interpretation of Computer Programs (SICP):** Chapter 1 — tail recursion and TCO explained beautifully
- **Grokking Algorithms:** Chapter 9 (Dynamic Programming) — memoization examples

### Online Resources

- **MIT OpenCourseWare:** "Lecture 20: Dynamic Programming" — recursive formulation
- **V8 Blog:** "TurboFan" engine — how modern JS optimizes tail calls
- **Compiler Explorer (Godbolt):** View TCO in compiled code

### Real System Code

- **Python CPython:** `ceval.c` shows why Python doesn't implement TCO
- **V8 JavaScript engine:** `code-generator.cc` — TCO optimization code
- **GCC compiler:** Tree-level tail-call elimination

### Personal Insights & Notes

[Space for you to write discoveries and aha moments]

---

## 🧭 Navigation

**← [Week 1, Day 4: Recursion I]**  
**→ [Week 2, Day 1: Arrays]**  
**↑ [Back to Week 1 Summary]**  
**⬆ [Back to Master Prompt]**

---

**Version:** 1.0  
**Status:** ✅ Complete  
**Created:** 2025-12-26  
**Reading Time:** ~90 minutes  
**Prerequisite:** Week 1 Day 4 (Recursion I)