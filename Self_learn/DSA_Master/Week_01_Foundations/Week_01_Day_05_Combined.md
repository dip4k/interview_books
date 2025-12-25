# 📘 WEEK 1 DAY 5: SPACE COMPLEXITY - Complete Learning Package

**Week 1, Day 5: Understanding Memory Usage**

Generated: 2025-12-26 | Duration: 90 minutes | Difficulty: 🟡 Medium | Target: 4-5/5

---

## PART 1: MAIN CONTENT

### 1️⃣ The Why

**Problem:** We've analyzed TIME. What about MEMORY?

Real-world constraints:
- **Embedded systems:** 64 MB of RAM total
- **Mobile apps:** Limited battery (memory allocation = power)
- **Data centers:** Memory is expensive (cost per GB)
- **Datasets:** 1 billion users = need smart memory usage

**Trade-off:** We often trade space to save time
- **Memoization:** Store results to avoid recomputation (space vs time)
- **Indexing:** Build data structure to search faster (space vs time)
- **Hashing:** Store table for O(1) lookup (space vs time)

---

### 2️⃣ The What: Mental Model

**Where Programs Use Memory:**

```
Program Memory Layout:
┌─────────────────────────┐
│ Code (read-only)        │ ~1-100 MB
├─────────────────────────┤
│ Global variables        │ ~1 KB
├─────────────────────────┤
│ Heap (dynamic alloc)    │ Used for arrays, objects
│ ↓ grows down            │ (can be GB)
├─────────────────────────┤
│ Free space              │ Unallocated
├─────────────────────────┤
│ ↑ grows up              │ (stack frames, locals)
│ Stack (function calls)  │ ~1-10 MB typically
├─────────────────────────┤
│ Environment/OS          │
└─────────────────────────┘
```

**Stack Memory:**
- Automatically freed when function returns
- Limited size (~1-10 MB on most systems)
- Fast allocation (just increment pointer)
- Used for: Local variables, function arguments, return addresses

**Heap Memory:**
- Manually freed (or garbage collected)
- Large size (GB available)
- Slower allocation (complex bookkeeping)
- Used for: Dynamic arrays, objects, memoization caches

**Example: Function Locals vs Heap**

```c
// Stack: All local, freed automatically
void stack_example(int n) {
    int arr[10];        // 40 bytes on stack
    int x = 5;          // 4 bytes on stack
    char name[100];     // 100 bytes on stack
    // Total: ~150 bytes on stack
    // Freed automatically when function returns
}

// Heap: Persistent, must free
void heap_example(int n) {
    int* arr = malloc(n * sizeof(int));  // n*4 bytes on heap
    // Must remember to free(arr) later!
    // If forgotten: memory leak
}
```

---

### 3️⃣ The How: Analysis

**Space Complexity (Big-O for Memory):**

```python
def example(n):
    arr = [0] * n           # O(n) space (array of size n)
    for i in range(n):      # Loop doesn't add space
        x = i               # Single variable, O(1)
    return sum(arr)         # Still O(n) total
```

**Counting Space:**

| Code | Space |
|------|-------|
| Single variable | O(1) |
| Array of size n | O(n) |
| 2D array n×m | O(n·m) |
| Recursive depth d | O(d) for stack |
| Hash table with n items | O(n) |
| Memoization cache for n items | O(n) |

**Recursive Space:**

```python
def sum_array(arr, index):
    if index == len(arr):
        return 0
    else:
        return arr[index] + sum_array(arr, index+1)

# Space: O(n)
# Why: Recursive call stack grows to depth n
# Each frame consumes constant space, n frames total
```

**Exponential Recursion Space:**

```python
def fib(n):
    if n <= 1: return n
    return fib(n-1) + fib(n-2)

# Space: O(n) (depth of recursion tree, not breadth)
# Max simultaneous frames: O(n) along one path
# Compare: Time is O(2^n) (total number of calls)
```

---

### 4️⃣ Visualization

**Stack Growing with Recursion:**

```
factorial(5) space usage:

Call 1: factorial(5)
  [frame: n=5]
  Space: 1 frame

Call 2: factorial(4) (from factorial(5))
  [frame: n=4]
  [frame: n=5]
  Space: 2 frames

Call 5: factorial(1)
  [frame: n=1]
  [frame: n=2]
  [frame: n=3]
  [frame: n=4]
  [frame: n=5]
  Space: 5 frames (O(n))

Returning:
  Return from fib(1): pop frame, space = 4
  Return from fib(2): pop frame, space = 3
  ...
  Done: space = 0
```

**Memory Over Time:**

```
Recursion depth vs space:

Space
  |
5 |    ╱╲
  |   ╱  ╲
4 |  ╱    ╲
  | ╱      ╲
3 |╱        ╲
  |          ╲
2 |           ╲
  |            ╲
1 |             ╲
  |_________________
    Time →
```

---

### 5️⃣ Critical Analysis

**Space-Time Trade-offs:**

| Technique | Time | Space | Useful When |
|-----------|------|-------|------------|
| Naive | O(2^n) | O(n) | n ≤ 20 |
| Memoization | O(n) | O(n) | n ≤ 10^6 |
| DP table | O(n) | O(n) | n ≤ 10^9 |
| Space-optimized DP | O(n) | O(1) | n ≤ 10^18 |

**Example: Fibonacci**

```python
# Naive: O(2^n) time, O(n) space
def fib_naive(n):
    if n <= 1: return n
    return fib_naive(n-1) + fib_naive(n-2)

# Memoized: O(n) time, O(n) space
def fib_memo(n, memo={}):
    if n in memo: return memo[n]
    if n <= 1: return n
    memo[n] = fib_memo(n-1, memo) + fib_memo(n-2, memo)
    return memo[n]

# DP: O(n) time, O(n) space
def fib_dp(n):
    dp = [0] * (n+1)
    dp[1] = 1
    for i in range(2, n+1):
        dp[i] = dp[i-1] + dp[i-2]
    return dp[n]

# Space-optimized: O(n) time, O(1) space
def fib_optimized(n):
    if n <= 1: return n
    a, b = 0, 1
    for _ in range(2, n+1):
        a, b = b, a+b
    return b
```

---

### 6️⃣ Real Systems

**Database Indexing:**

```
Option 1: Sequential scan
  Time: O(n) read every row
  Space: O(1) don't store anything
  
Option 2: Index on column
  Time: O(log n) use index to find
  Space: O(n) store index copy of data
  
Use option 2 if data accessed frequently!
```

**Web Cache:**

```
Option 1: Fetch from server every time
  Time: 100ms per request
  Space: 0
  
Option 2: Cache in browser
  Time: 1ms from cache (100x faster)
  Space: Cache storage used
  
Use cache if storage available!
```

---

### 7️⃣ Connections

Builds on: Days 1-4 (all use memory)
Enables: Week 11 (dynamic programming), optimization techniques

---

### 8️⃣ Mathematics

**Recurrence for Space:**

S(n) = S(n-1) + O(1) = O(n) (linear recursion)
S(n) = O(n) (depth of recursion tree)

Note: S(n) ≠ time complexity!
- Fib time: O(2^n), space: O(n)
- Very different!

---

### 9️⃣ Design Intuition

**Use More Space When:**
- Time is critical (trading space for speed)
- Space is available (plenty of RAM)
- Problem is compute-bound (not memory-bound)

**Use Less Space When:**
- Embedded system (limited RAM)
- Data is huge (10^9 items, need O(1) space)
- Memory cost high (cloud VMs charged per MB)

**Example Decisions:**

```
Problem: Find if number exists in 1M integers

Option A: Linear search O(n) time, O(1) space
  Scan all integers, check each
  1M comparisons, instant

Option B: Hash set O(n) preprocessing, O(1) lookup, O(n) space
  Build hash table (1M items)
  Lookup instant
  Use if you search many times!

Option C: Sorted + binary search O(n log n) sort, O(log n) lookup, O(1) space
  Sort array, then binary search
  Efficient time and space
  Balanced choice!
```

---

### 🔟 Knowledge Check

1. Stack vs heap: When is each used?
2. Space complexity of recursive factorial?
3. Memoization trades what for what?
4. Compare space: naive vs memo vs DP?
5. When would you optimize space to O(1)?
6. Recursive depth of binary_search(10^9)?
7. Memory leak scenario and how to prevent?

### 1️⃣1️⃣ Hooks

**One-liner:** "Space complexity measures memory usage like time complexity measures duration."

**Memory aid:** "Stack = automatic. Heap = manual. Heap = flexible, larger."

**Real impact:** "Facebook optimized cache to use 30% less RAM, saving millions in hardware costs!"

---

## PART 2: QUICK SUMMARY

**Stack Memory:**
- Automatic deallocation
- Limited (~10 MB)
- Fast allocation
- Use for: Local variables

**Heap Memory:**
- Manual deallocation (or GC)
- Large (GB)
- Slower allocation
- Use for: Dynamic arrays, objects

**Space Complexity:**
- Recursive depth = O(depth)
- Arrays = O(n)
- Memoization cache = O(subproblems)

**Space-Time Trade-offs:**
- More time, less space: Naive recursion, recompute
- Less time, more space: Memoization, precompute
- Balanced: DP with space optimization

---

## PART 3: QUESTIONS & ANSWERS

**Q1:** factorial(1000) uses how much stack space?
**A:** 1000 frames × ~100 bytes = ~100 KB (usually safe)

**Q2:** What's a memory leak?
**A:** Allocate on heap, forget to free. Memory stays allocated even after need.

**Q3:** Memoization stores what?
**A:** Results of function calls. If called with same input, return cached result.

**Q4:** Space: naive fib(50) vs memoized?
**A:** Naive: O(50) stack. Memoized: O(50) stack + O(50) cache = O(50) total.

**Q5:** Stack overflow happens when?
**A:** Recursion depth exceeds stack size (~10K frames). Each frame consumes ~100-200 bytes.

**Q6:** Recursive binary_search(1 billion) space?
**A:** O(log 1000000000) ≈ O(30) frames. Safe!

**Q7:** When is space more important than time?
**A:** Embedded systems, mobile (battery), when problem is memory-bound.

---

## PART 4: README

**90-Minute Study:**
- Why (15 min): Memory constraints and trade-offs
- What (15 min): Stack vs heap, space complexity
- How (15 min): Analyze space in code
- Visualization (15 min): Trace memory allocation
- Analysis (10 min): Complexity, trade-offs

**Key Insight:** Space can be as critical as time in real systems

**This Week Integration:**
- Day 1: RAM model (memory hierarchy)
- Day 2: Time complexity (Big-O)
- Day 3-4: Recursion (creates stack frames)
- Day 5: Space complexity (memory usage)

**Together:** Understand both time AND space of algorithms

---

**Status:** ✅ Complete | **Ready:** For Week 2 (Linear Structures)

