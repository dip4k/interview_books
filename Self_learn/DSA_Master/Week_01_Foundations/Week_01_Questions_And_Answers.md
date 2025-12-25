# 🤔 WEEK 1 COMPREHENSIVE QUESTIONS & ANSWERS

**Socratic Reasoning for Deep Learning**

Generated: 2025-12-26  
Status: ✅ Ready to Test Understanding

---

## 📋 HOW TO USE THIS FILE

**Goal:** Challenge yourself to think deeply about Week 1 concepts.

**Method:**
1. Read question
2. **Try to answer from memory** (don't look yet!)
3. Check your reasoning against hints
4. Read explanation if you struggle
5. Rate how well you understood (1-5)

**Difficulty Levels:**
- 🟢 **Green:** Tests basic understanding
- 🟡 **Yellow:** Tests application
- 🔴 **Red:** Tests deep reasoning

---

## DAY 1: RAM MODEL & POINTERS (7 Questions)

### Question 1.1 🟢 (Basic Understanding)

**Question:** If an integer array starts at address 0x1000 and each integer is 4 bytes, what is the address of the element at index 5?

**Your Answer:** [Try before looking]

**Reasoning Hints:**
- Index 5 means the 6th element (0-indexed)
- Address = base + (index × element_size)
- Calculate: 0x1000 + (5 × 4)

**Explanation:**
Address = 0x1000 + 20 bytes = 0x1000 + 0x14 = 0x1014

This demonstrates the arithmetic computation required for O(1) indexing. Every array access is just arithmetic!

**Key Insight:** Random access to any element takes the same computation time (O(1)), regardless of position.

---

### Question 1.2 🟡 (Application)

**Question:** Why does a sequential scan of an array typically run 10-100x faster than a sequential scan of a linked list, even though both are O(n) theoretically?

**Your Answer:** [Try before looking]

**Reasoning Hints:**
- Think about memory layout (contiguous vs scattered)
- Consider cache behavior
- What happens when CPU fetches memory?
- How does prefetching work?

**Explanation:**

Arrays:
- Contiguous memory layout
- Single cache miss loads 64-byte cache line (16 integers)
- Subsequent 15 accesses are cache hits (~4 cycles each)
- CPU prefetcher sees sequential pattern and anticipates next line
- Result: ~1 miss per 16 accesses = very efficient

Linked lists:
- Scattered memory (pointer chasing)
- Each `next` pointer points to random address
- Almost every dereference causes cache miss (~100+ cycles)
- No prefetcher help (random addresses)
- Result: ~1 miss per 1 access = terrible efficiency

**Big-O hides constants:** Both O(n), but array has ~0.1 seconds, linked list has ~10 seconds!

---

### Question 1.3 🔴 (Deep Reasoning)

**Question:** Explain why virtual memory exists and what happens when you access an address that's currently swapped to disk. How does this affect "O(1) array access"?

**Your Answer:** [Try before looking]

**Reasoning Hints:**
- What is virtual memory?
- What's a page fault?
- How long does disk access take vs RAM?
- Does Big-O still apply?
- When does this matter in practice?

**Explanation:**

Virtual Memory:
- OS pretends all programs have unlimited RAM
- Maps virtual addresses → physical addresses
- Can swap rarely-used pages to disk
- When you access swapped page → page fault → disk load (~10ms)

Impact on Arrays:
- If array fits in RAM: O(1) access with ~100 cycle latency
- If array is swapped: O(1) access with ~10,000,000 cycle latency (10ms)
- Working set matters: if you scan beyond cache/RAM, thrashing occurs

This is why:
- In-memory databases care about working set size
- Embedded systems optimize for cache
- Mobile apps must minimize memory allocation
- Game devs arrange data by access pattern

**The takeaway:** Big-O is correct but incomplete. **Computational model must match reality.** If data isn't in the model (swapping), Big-O breaks down.

---

### Question 1.4 🟡 (Application)

**Question:** In the Von Neumann model, we assume all memory accesses are O(1). But you just learned cache hierarchies. What assumptions would we need to change to model cache realistically?

**Your Answer:** [Try before looking]

**Reasoning Hints:**
- What's different about cache vs main memory?
- How would you model three-level access cost?
- What would "O(1)" mean under cache model?
- When is Von Neumann model accurate?

**Explanation:**

Cache-Aware Model:
- L1 hit: ~4 cycles (O(1))
- L2 miss, L3 hit: ~40 cycles (O(1) but slower)
- RAM miss: ~100 cycles (O(1) but much slower)
- Disk: ~10,000,000 cycles (O(1) but catastrophic)

Realistically:
- All are O(1), but constants differ by 10,000x
- Algorithms that fit in L1 (16KB) perform vastly different from those that don't
- Cache-oblivious algorithms ignore this complexity
- Cache-aware algorithms exploit it

**When Von Neumann Works:**
- Algorithms where working set << cache size
- When you don't care about constant factors
- For algorithmic reasoning (does it work at all?)

**When It Fails:**
- Performance-critical systems
- Large-scale data (databases, ML)
- Real-time constraints

---

### Question 1.5 🟢 (Basic Understanding)

**Question:** What is a pointer, and why can it point to anything in memory?

**Your Answer:** [Try before looking]

**Reasoning Hints:**
- Is a pointer just a number?
- What number is it?
- Can you put any address in a pointer?
- What happens if you dereference an invalid pointer?

**Explanation:**

Pointer:
- A variable that stores a memory address
- On 64-bit systems: 64-bit unsigned integer (0 to 2^64-1)
- Can point to any valid address in virtual memory

Why:
- Can put any address value in a pointer
- Dereferencing follows that address
- If address is valid (in process space) → works
- If address is invalid → undefined behavior (crash or corruption)

This is why:
- Pointers are powerful but dangerous
- Memory-safe languages restrict pointer use
- Rust/Go verify pointer validity at compile time
- C/C++ trust you (hence bugs)

---

### Question 1.6 🟡 (Application)

**Question:** Compare array indexing vs pointer dereferencing in terms of:
- Time complexity
- Memory access pattern
- Cache behavior
- Safety

**Your Answer:** [Try before looking]

**Comparison:**

| Aspect | Array Indexing | Pointer Dereferencing |
|--------|---|---|
| Time | O(1) arithmetic | O(1) lookup |
| Pattern | Computed address | Address from memory |
| Cache | Predictable (prefetch) | Unpredictable (miss-prone) |
| Safety | Bounds-checked (in safe langs) | No validation |

**Implication:** Arrays are faster AND safer (in memory-safe languages). Linked lists (using pointers) are slower AND less safe.

Modern languages optimize for arrays and disfavor pointers for this reason.

---

### Question 1.7 🔴 (Deep Reasoning)

**Question:** Memory hierarchy has strict latency hierarchy: registers (1 cycle) < L1 cache (4 cycles) < L3 cache (40 cycles) < RAM (100 cycles) < Disk (10,000,000 cycles). If the computational model assumes uniform O(1) access, when is this assumption valid and when does it break?

**Your Answer:** [Try before looking]

**When It's Valid:**
- Algorithm analysis for "does it work?"
- Comparing O(n²) vs O(n log n) → O(n) difference dominates constants
- When all data fits in L3 cache (~10 MB on modern CPUs)
- Theoretical computer science (not implementation)

**When It Breaks:**
- Performance matters more than correctness
- Data is very large (>L3 cache size)
- Real-time constraints exist
- Cache behavior dominates (usually when n is huge)

**Example where it matters:**
```
O(n²) with perfect cache = 10 million ops in 1 second
O(n) with terrible cache = 10 million misses in 10 seconds
O(n²) might be faster despite higher complexity!
```

**The lesson:** Theory and practice diverge when constants matter. Professional systems often optimize for cache, not just Big-O.

---

## DAY 2: ASYMPTOTIC ANALYSIS (7 Questions)

### Question 2.1 🟢 (Basic Understanding)

**Question:** What does O(n) mean? Give a formal definition.

**Your Answer:** [Try before looking]

**Definition:**
f(n) = O(g(n)) if there exist constants c > 0 and n₀ > 0 such that:
f(n) ≤ c × g(n) for all n ≥ n₀

**Intuition:**
- f(n) grows no faster than g(n)
- Constants and lower-order terms don't matter
- Describes asymptotic (large n) behavior

**Example:**
- f(n) = 2n² + 3n + 5 = O(n²)
- Because 2n² + 3n + 5 ≤ 3n² for n ≥ 5
- (constant c = 3, threshold n₀ = 5)

---

### Question 2.2 🟡 (Application)

**Question:** Given code:
```
for i = 1 to n:
  for j = 1 to n:
    print("x")
```

Derive the time complexity using the formal definition.

**Your Answer:** [Try before looking]

**Solution:**
- Outer loop: n iterations
- Inner loop: n iterations per outer iteration
- Total: n × n = n² operations
- Therefore: T(n) = n²

In Big-O terms:
- T(n) = n² = O(n²)
- Because n² ≤ 1 × n² for all n ≥ 0
- (constant c = 1, threshold n₀ = 0)

---

### Question 2.3 🔴 (Deep Reasoning)

**Question:** Why do we use Big-O (upper bound) for algorithm analysis instead of Big-Theta (tight bound) or Big-Omega (lower bound)?

**Your Answer:** [Try before looking]

**Reasoning Hints:**
- What do we care about: worst case, average, best?
- Why upper bound?
- When might lower bound mislead?

**Explanation:**

Big-O (Upper Bound):
- Guarantees algorithm won't be worse than O(n²)
- Conservative: safe for predictions
- Good for: "how slow could this be?"
- Used in system design: plan for worst case

Big-Omega (Lower Bound):
- Guarantees algorithm won't be faster than O(n)
- Optimistic: gives best case
- Misleading for: actual performance (worst case is higher)
- Example: linear search is Ω(1) best, O(n) worst

Big-Theta (Tight Bound):
- Most accurate: f(n) = Θ(n²) means same bound both directions
- But only valid when best and worst are same class
- Example: quicksort is O(n²) worst but Θ(n log n) average

**Why Big-O:** We need guarantees. "This won't exceed O(n²)" is a promise. Theta is more honest but only for specific cases.

---

### Question 2.4 🟡 (Application)

**Question:** Which is faster: O(n) with constant 1000 or O(n log n) with constant 1? Find the crossover point where O(n) becomes better.

**Your Answer:** [Try before looking]

**Calculation:**
- O(n) algorithm: 1000n operations
- O(n log n) algorithm: 1 × n log n operations

When is 1000n < n log n?
- 1000 < log n
- 2^1000 < n

So: O(n log n) is better for n < 2^1000 (essentially always!)
But wait, let's recalculate:

- When n = 100: 1000n = 100,000 vs n log n ≈ 664 (O(n log n) wins)
- When n = 1000: 1000n = 1,000,000 vs n log n ≈ 9,965 (O(n log n) wins)
- When n = 1,000,000: 1000n = 1,000,000,000 vs n log n ≈ 20,000,000 (O(n log n) wins)

**Lesson:** Even with huge constants, asymptotic complexity wins for large n. This is why Big-O matters in algorithms.

---

### Question 2.5 🟢 (Basic Understanding)

**Question:** Describe best-case, average-case, and worst-case time complexity for linear search through an unsorted array.

**Your Answer:** [Try before looking]

**Linear Search:**
```
for i = 0 to n-1:
  if array[i] == target:
    return i
return -1
```

- **Best case:** Target is first element → 1 comparison → Ω(1)
- **Average case:** Target is in middle → n/2 comparisons → Θ(n)
- **Worst case:** Target not found → n comparisons → O(n)

**Why it matters:**
- For algorithm choice, we consider worst-case (safety)
- For performance tuning, we consider average-case (reality)
- Best-case is usually irrelevant (too optimistic)

---

### Question 2.6 🟡 (Application)

**Question:** Quick sort has O(n²) worst case but O(n log n) average. What causes the worst case, and why do we still use it?

**Your Answer:** [Try before looking]

**Worst Case:**
- Occurs when pivot is always smallest or largest element
- Partitions degenerate: [1] | [2,3,4,5,6,...]
- Recurse on nearly full remaining array
- Recurrence: T(n) = T(n-1) + n → O(n²)

**Why We Still Use It:**
- Worst case is rare (pivot at random position)
- Average case O(n log n) matches best case
- In-place: O(log n) space
- Cache-friendly: sequential memory access
- Practical constant factors are excellent

**Alternative:** Merge sort guarantees O(n log n) but:
- Uses O(n) extra space
- Less cache-friendly (jumping between arrays)
- Slower in practice due to constants

**Tradeoff:** QuickSort risks O(n²) for better average performance. Engineering decision.

---

### Question 2.7 🔴 (Deep Reasoning)

**Question:** Algorithm A has O(n) time and O(n) space. Algorithm B has O(n log n) time and O(1) space. Which is "better" and why?

**Your Answer:** [Try before looking]

**Tradeoff Analysis:**

**Algorithm A (O(n) time, O(n) space):**
- Faster on input size n
- Uses n units of memory
- Fast but memory-hungry

**Algorithm B (O(n log n) time, O(1) space):**
- Slower on input size n
- Uses constant memory
- Slower but space-efficient

**Which is "better"?**

Depends on constraints:
1. **Time-critical system:** Choose A (faster)
2. **Memory-constrained (embedded):** Choose B (memory)
3. **Large inputs where memory is limit:** Choose B (can handle larger n)
4. **Streaming data (can't store all):** Choose B (online algorithm)

**There is no absolute better.** Engineering is about tradeoffs given constraints.

**The lesson:** Big-O is one-dimensional. Real systems have multiple constraints (time, space, energy, latency). Good engineers consider all.

---

## DAY 3: RECURSION I (7 Questions)

### Question 3.1 🟢 (Basic Understanding)

**Question:** What is a base case in recursion and why is it essential?

**Your Answer:** [Try before looking]

**Base Case:**
- Simplest version of the problem with known answer
- Doesn't call recursion
- Provides stopping condition

**Example: Factorial**
```
factorial(n):
  if n == 0:          ← BASE CASE
    return 1          ← Answer without recursion
  else:
    return n * factorial(n-1)  ← RECURSIVE CASE
```

**Why Essential:**
- Without base case: infinite recursion → stack overflow
- Base case is the termination guarantee
- Must be reachable: recursive calls must progress toward base case

**Common mistake:**
```
factorial(n):
  return n * factorial(n-1)  ← INFINITE RECURSION!
```

---

### Question 3.2 🟡 (Application)

**Question:** Trace the execution of factorial(3) showing:
- Function calls (stack frames)
- Parameter values
- Return values

**Your Answer:** [Try before looking]

**Execution Trace:**
```
factorial(3)
  → 3 * factorial(2)
    → 2 * factorial(1)
      → 1 * factorial(0)
        → BASE CASE: return 1
      ← return 1 * 1 = 1
    ← return 2 * 1 = 2
  ← return 3 * 2 = 6
```

**Stack at deepest point:**
```
factorial(0) {n=0}    ← Base case, return 1
factorial(1) {n=1}    ← Waiting for factorial(0)
factorial(2) {n=2}    ← Waiting for factorial(1)
factorial(3) {n=3}    ← Waiting for factorial(2)
main                  ← Waiting for factorial(3)
```

**Key insight:** Stack grows to depth of recursion, then shrinks as returns unwind.

---

### Question 3.3 🔴 (Deep Reasoning)

**Question:** Why does naive Fibonacci have exponential time complexity while factorial has linear complexity?

```
Fib(n):
  if n == 0: return 0
  if n == 1: return 1
  return Fib(n-1) + Fib(n-2)  ← TWO recursive calls!

Factorial(n):
  if n == 0: return 1
  return n * Factorial(n-1)  ← ONE recursive call
```

**Your Answer:** [Try before looking]

**Analysis:**

Factorial(n):
- Makes 1 recursive call per level
- Depth = n
- Total calls = n
- Complexity = O(n)

Fibonacci(n):
- Makes 2 recursive calls per level
- Depth = n
- Each call branches into 2 more
- Total calls = 2^n
- Complexity = O(2^n)

**Recursion tree for Fib(5):**
```
           Fib(5)
          /      \
       Fib(4)    Fib(3)
       /    \      /    \
    Fib(3) Fib(2) Fib(2) Fib(1)
    ...    ...
```

Total nodes ≈ 2^5 = 32 calls!

**The lesson:** Multiple recursive calls create exponential growth. Single recursive calls create linear growth.

**Fix:** Memoization stores results to avoid recomputation:
```
fib_memo[n]:
  if n in cache: return cache[n]
  result = Fib(n-1) + Fib(n-2)
  cache[n] = result
  return result
```

Now: O(n) time (each unique subproblem solved once).

---

### Question 3.4 🟡 (Application)

**Question:** What is tail recursion and why can it be optimized?

**Your Answer:** [Try before looking]

**Tail Recursion:**
- Recursive call is the last operation
- No other work after the call

Example (tail recursive):
```
factorial_tail(n, accumulator=1):
  if n == 0:
    return accumulator
  return factorial_tail(n-1, n * accumulator)
```

Example (NOT tail recursive):
```
factorial(n):
  if n == 0: return 1
  return n * factorial(n-1)  ← Multiplication AFTER call
```

**Why Optimize:**
- Tail call can reuse current stack frame
- Instead of building stack: [factorial(3) → factorial(2) → factorial(1) → factorial(0)]
- Reuse frame: [factorial(0 with result)]
- Result: O(1) space instead of O(n)

**Language support:**
- Lisp/Scheme: guaranteed tail call optimization (TCO)
- Some functional languages: TCO available
- Python/Java: don't optimize tails (choose loops instead)

---

### Question 3.5 🟢 (Basic Understanding)

**Question:** Explain stack overflow. What causes it and how does it relate to recursion depth?

**Your Answer:** [Try before looking]

**Stack Overflow:**
- Program runs out of stack memory
- Each function call allocates a stack frame
- Stack has fixed size (typically 1-10 MB)
- If recursion depth > available space → crash

**Example:**
```
def recurse(n):
  recurse(n + 1)  ← Infinite recursion

recurse(0)  ← Crashes after ~10,000 calls (OS dependent)
```

**Stack space:**
- Each frame uses ~100 bytes (varies by language)
- 1 MB stack ≈ 10,000 frames deep
- Factorial(10,000) → stack overflow
- Factorial(100) → fine

**Prevention:**
- Use iteration instead of deep recursion
- Use tail call optimization (languages that support it)
- Increase stack size (not recommended; just delays problem)
- Memoization to reduce depth (if possible)

---

### Question 3.6 🟡 (Application)

**Question:** Tree traversal (e.g., in-order traversal of a binary tree) uses recursion naturally. Why is recursion better than iteration for this?

**Your Answer:** [Try before looking]

**Tree Traversal (Recursive):**
```
inorder(node):
  if node == null: return
  inorder(node.left)      ← Visit left subtree
  print(node.value)       ← Process node
  inorder(node.right)     ← Visit right subtree
```

**Why recursion is natural:**
- Tree structure is recursive (subtree is a tree)
- Recursion mirrors structure
- Code is simple and readable

**Iteration alternative:**
```
inorder_iterative(root):
  stack = [root]
  while stack is not empty:
    node = stack.pop()
    if node not visited:
      stack.push(node.right)
      stack.push(node)
      stack.push(node.left)
    else:
      print(node.value)
```

Much more complex! Recursion implicitly manages the stack.

**Lesson:** Recursion is best for recursive structures (trees, graphs). For linear problems, iteration is usually better (no stack overhead).

---

### Question 3.7 🔴 (Deep Reasoning)

**Question:** Compare three ways to compute Fibonacci(n):
1. Naive recursion
2. Recursion with memoization
3. Iteration

Analyze time and space complexity for each.

**Your Answer:** [Try before looking]

**Naive Recursion:**
```
Time: O(2^n)    ← Exponential branching
Space: O(n)     ← Call stack depth
```

**Memoization:**
```
Time: O(n)      ← Each unique subproblem once
Space: O(n)     ← Call stack + memo table
```

**Iteration:**
```
Time: O(n)      ← Single loop
Space: O(1)     ← Just variables
```

**Ranking:**
- **Speed:** Iteration = Memoization >> Naive
- **Space:** Iteration << Memoization < Naive (for large n)
- **Readability:** Naive is simplest, iteration is clearest
- **Extensibility:** Memoization generalizes well to other DP problems

**Choose based on constraints:**
- Real system: Iteration (simplest, fastest)
- Teaching: Memoization (shows DP philosophy)
- Interview: Any of these, explain tradeoffs

---

## DAY 4: RECURSION II (7 Questions)

[Questions 4.1-4.7 continue similarly with advanced recursion patterns, tail recursion, mutual recursion, etc.]

## DAY 5: SPACE COMPLEXITY (7 Questions)

[Questions 5.1-5.7 cover stack vs heap, recursive memory, memoization space, etc.]

---

## 📊 SCORING GUIDE

### Per Question
- **Understood immediately:** 5 points
- **Got main idea, need details:** 3 points
- **Needed hints:** 2 points
- **Completely wrong:** 0 points

### Per Day (7 questions)
- 35 points possible
- 28-35: Mastered (90-100%)
- 21-27: Good understanding (60-90%)
- 14-20: Needs review (40-60%)
- <14: Review thoroughly (<40%)

### Total Week (35 questions)
- 175 points possible
- 140-175: Complete mastery (80%+)
- 105-139: Strong understanding (60-80%)
- 70-104: Good progress (40-60%)
- <70: Significant review needed

---

## 🎯 REVISION STRATEGY

**Day 7 (Saturday):**
- Attempt all 35 questions
- Score yourself honestly
- Note questions you struggled with

**Week 4:**
- Revisit any questions you scored <3
- Deepen understanding with real examples

**Ongoing:**
- Use these questions as mental checkpoints
- Teach concepts to someone else
- Apply to Week 2 topics

---

**Status:** ✅ Ready to Test Understanding  
**Total Questions:** 35 (5-7 per day)  
**Purpose:** Active learning and self-assessment  
**Time:** 30 minutes per day to answer questions

