# 🧠 Week 2: Linear Structures - Day 5

# Binary Search: Logarithmic Reduction, Invariants, Boundaries

## 🗓 Metadata
**Topic:** Binary Search  
**Week:** Week 2  
**Day:** Day 5 of 5  
**Category:** Linear Structures  
**Difficulty:** 🟡 Medium  
**Status:** 🔍 In Study  
**Last Reviewed:** —  
**Confidence Level (1–5):** —/5  

---

## 1️⃣ The Why — Engineering Motivation

### Real-World Problem

You need to find an element in a **sorted array** quickly. Linear scan is O(n), which is slow for large n (millions of records).

Binary search reduces the search space by half each step, achieving **O(log n)** time.

Examples:
- Searching a sorted customer database.
- Finding a threshold (e.g., first value ≥ threshold).
- Disk-based index lookups.

### Design Problem Solved

- **Logarithmic search time:** 20 comparisons for 1 million elements.
- **Predictable performance:** Always O(log n), unlike hash tables (which can degrade).
- **Works on sorted data:** No preprocessing cost if already sorted.

Trade-off: Data must be sorted; binary search only works on sorted structures.

### Real System Usage

- **Standard library:** Java Collections.binarySearch, C++ std::lower_bound, Python bisect.
- **Databases:** B-trees use binary search internally for key lookups.
- **Hardware:** CPU branch prediction uses similar bisection concepts.

---

## 2️⃣ The What — Mental Model & Intuition

### Core Analogy

Imagine **guessing a number from 1 to 1024** where you get feedback: "too high", "too low", or "correct".

```
Guess 512 → too high
Guess 256 → too low
Guess 384 → too high
Guess 320 → too low
Guess 352 → correct

Takes ~10 steps to narrow 1024 possibilities to 1.
```

Each guess halves the remaining range → logarithmic convergence.

---

## 3️⃣ The How — Mechanical Walkthrough

### Loop Invariant

Maintain indices `low` and `high` such that:

> **If the target exists in the array, it is somewhere in [low, high].**

### The Algorithm

```
low = 0
high = n - 1

while low <= high:
    mid = (low + high) / 2
    
    if A[mid] == target:
        return mid
    
    else if A[mid] < target:
        low = mid + 1    (target is to the right)
    
    else:
        high = mid - 1   (target is to the left)

return -1 (not found)
```

### Step-by-Step Execution

1. Compute `mid` as the middle of [low, high].
2. Compare `A[mid]` with target.
3. If equal, found!
4. If target > A[mid], eliminate [low, mid] and search [mid+1, high].
5. If target < A[mid], eliminate [mid, high] and search [low, mid-1].
6. Repeat until interval collapses.

### Why It Works

- **Invariant maintenance:** At each step, we eliminate half the remaining interval while keeping invariant true.
- **Termination:** Interval shrinks; eventually high < low (not found) or we find the target.
- **Correctness:** We never eliminate the target (if it exists) from [low, high].

---

## 4️⃣ Visualization — The Simulation

Sorted array:

```
Index:  0  1  2  3  4  5  6
Values: 2  5  7 10 13 15 20
Target: 13
```

**Iteration 1:**
```
low=0, high=6
mid = (0+6)/2 = 3
A[3] = 10
10 < 13 → low = 4
Interval narrows to [4, 6]
```

**Iteration 2:**
```
low=4, high=6
mid = (4+6)/2 = 5
A[5] = 15
15 > 13 → high = 4
Interval narrows to [4, 4]
```

**Iteration 3:**
```
low=4, high=4
mid = (4+4)/2 = 4
A[4] = 13
13 == 13 → FOUND at index 4
```

Search space: 7 → 3 → 1 elements. **3 comparisons to find among 7 elements.**

For 1 million elements: ≤ 20 comparisons.

---

## 5️⃣ Critical Analysis — Performance & Robustness

### Complexity Table

| Operation | Time    | Notes                    |
|-----------|---------|--------------------------|
| Search    | O(log n) | Halves range per iteration |
| Space     | O(1)    | Iterative version        |

### Comparisons Count

For array size n:
- Each iteration eliminates ~n/2 elements.
- After k iterations: ~n / 2^k elements remain.
- To reduce to 1: n / 2^k ≤ 1 → 2^k ≥ n → **k ≥ log₂(n)**.

Example: n = 1,000,000 → k ≈ 20 comparisons.

### Robustness & Edge Cases

**Off-by-one errors (very common):**
- `mid = (low + high) / 2` can overflow if low + high > 2^31.
  - Fix: `mid = low + (high - low) / 2`.
- Loop condition: `while low <= high` (vs `<`) affects termination.
- Boundary updates: `low = mid + 1` (not `mid`), `high = mid - 1` (not `mid`).

**Precondition:**
- Array must be **sorted**.
- Violating this silently returns wrong answers.

**Edge cases:**
- Empty array: Should return -1 (not found).
- Single element: Works correctly.
- All elements the same: Finds one occurrence (not necessarily the first/last).

---

## 6️⃣ Real System Integration

### Standard Libraries

- **C++ std::lower_bound, std::upper_bound:** Binary search for range queries.
- **Java Collections.binarySearch():** Standard binary search.
- **Python bisect.bisect_left, bisect_right:** For maintaining sorted lists.

### Database Indexes

- **B-trees:** Internal nodes use binary search (or interpolation search) to find child pointers.
- **Log-structured merge trees (LSM):** Binary search across levels.

### Numerical Algorithms

- **Bisection method:** Finding roots of functions (continuous version of binary search).
- **Root-finding in sorted sequences:** First element satisfying a property.

---

## 7️⃣ Concept Crossovers

### Predecessors
- **Arrays (Day 1):** Binary search requires contiguous, indexable storage.
- **Asymptotic analysis (Week 1, Day 2):** O(log n) is the fundamental speedup.

### Successors
- **Balanced BSTs (Week 5, Day 5):** Maintain sorted order while allowing insertions.
- **Segment trees (Week 8, Day 2):** Range queries using binary search on tree structure.
- **Greedy algorithms (Week 10, Day 1):** Often binary-search the answer space.

---

## 8️⃣ Mathematical & Theoretical Perspective

### Recurrence Relation

Let T(n) = number of comparisons for array of size n.

```
T(n) = T(n/2) + 1    (search half, plus one comparison)
T(1) = 1             (base case)
```

Solving:
```
T(n) = log₂(n) + 1 = O(log n)
```

### Proof Sketch (Invariant-Based)

1. Maintain invariant: target in [low, high].
2. Each step: eliminate at least half.
3. Interval size shrinks exponentially.
4. After log n steps, interval is 1 element.
5. Either found or not found.

---

## 9️⃣ Algorithmic Design Intuition

### When to Use Binary Search

1. **Data is sorted** (or can be sorted once).
2. You need **many searches** (amortizes sort cost O(n log n) over many O(log n) queries).
3. You want **predictable O(log n)** performance (unlike hash tables which can degrade).

### When to Avoid

1. **Unsorted data:** Must sort first (O(n log n)).
2. **Single search on unsorted:** Linear scan is O(n) vs O(n log n) sort + O(log n) search.
3. **Frequent insertions:** Maintaining sorted order is expensive; use balanced trees instead.

### Decision Framework

```
Is the data sorted?
  → YES: Binary search is viable.
     Do you search often?
       → YES: Binary search (total cost = O(n log n) sort + many O(log n) searches).
       → NO: Linear scan might be faster.
  
  → NO: Must sort first.
     Then same analysis as above.
```

---

## 🔟 Knowledge Check — Socratic Reasoning

**Question 1: How would you adapt binary search to find the FIRST element ≥ target (not exact match)?**

Your reasoning:
```
Classic binary search returns an exact match.
For "first ≥ target":
- If A[mid] >= target: might be the answer, but check left (high = mid - 1).
- If A[mid] < target: answer is to the right (low = mid + 1).
Keep track of the best candidate found so far.
This is std::lower_bound.
```

**Question 2: Why are off-by-one errors so common in binary search?**

Your reasoning:
- Many subtle edge cases: empty array, single element, target at boundaries.
- Multiple ways to write the loop, each with different invariants.
- Off-by-one survives testing if test cases don't cover boundaries.
- Example: `mid = (low + high) / 2` can overflow; must use `mid = low + (high - low) / 2`.

**Question 3: When does it make sense to pay O(n log n) to sort, then do many binary searches?**

Your reasoning:
```
Upfront cost: O(n log n) sort.
Per search: O(log n).
If you do k searches:
  Total = O(n log n + k log n)

Breakeven vs linear search:
  O(n log n + k log n) vs O(kn)
  → k log n ≈ kn → log n ≈ n (never, for reasonable n).

So binary search is almost always better for sorted data, even single searches on large n.
```

**Question 4: Why does binary search work on sorted arrays but not on hash tables?**

Your reasoning:
- Binary search relies on order: A[mid] < target → search right.
- Hash tables destroy order (hash function scrambles keys).
- Hash tables use different strategies (chaining, probing) for O(1) average lookup.

---

## 11️⃣ Retention Hook — Memory Anchors

### One-Line Essence

> **Binary search is controlled bisection on a sorted array, using comparisons to shrink the search interval to the target.**

### Mnemonic

**"BINARY = Bisect, Interval Narrowing, Accurate Result, Yet Logarithmic"**

- **Bisect:** Cut the interval in half.
- **Interval Narrowing:** Shrink based on comparison.
- **Accurate Result:** Find exact match or boundary.
- **Yet Logarithmic:** Despite large n, very fast.

### Geometric Cue

```
Sorted array: [2, 5, 7, 10, 13, 15, 20]
              [0, 1, 2,  3,  4,  5,  6]
              
Search space shrinks:
[0-6] → [4-6] → [4-4] → found

Visual: \ shape, converging to target.
```

---

## 🧩 Cognitive & Meta Layers

| Lens | Insight |
|------|---------|
| **Computational** | Eliminates half the search space per comparison; O(log n) fundamental speedup |
| **Psychological** | Beginners think "binary search is hard"; reality: just maintain invariant [low, high] |
| **Design Trade-off** | Sort cost O(n log n) vs search cost O(log n); tradeoff depends on k (number of searches) |
| **Historical** | One of the oldest algorithms; fundamental to computer science (divide and conquer) |

---

## 🔁 Revision & Spaced Repetition

Track your understanding:

| Review Date | Confidence (1–5) | Strengths | Areas to Deepen | Next Review |
|---|---|---|---|---|
| 2025-12-26 (Today) | — | — | — | 2025-12-28 |
| | | | | |

---

## 📚 Reference Pointers

### Textbooks
- **CLRS:** Chapter 12 (Binary Search Trees) and Chapter 2 (Merge Sort, which uses binary search concepts).
- **Skiena:** Chapter 3 (Data Structures).

### Online
- **LeetCode:** Binary Search tag (704, 34, 153, 162 are classic problems).
- **Cracking the Coding Interview:** Chapter 8 (Sorting and Searching).

### Real System Code
- **std::lower_bound:** C++ Standard Library (algorithm header).
- **Python bisect:** Built-in module for binary search operations.

---

## 🧭 Navigation

**← [Previous: Day 4 - Stacks & Queues](./04_Stacks_Queues.md)**  
**→ [Week 3: Start Sorting & Hashing](../Week_03_Sorting_Hashing/01_Elementary_Sorts.md)**  
**↑ [Back to README](../README.md)**  

---

**Status:** 🔍 In Study  
**Time Spent:** — minutes  
**Last Updated:** 2025-12-26  
**Week 2 Complete:** Ready to move to Week 3!

