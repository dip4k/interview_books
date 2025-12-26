# Week 4.5 Day 1: Binary Search Fundamentals - Logarithmic Search

## 🗓 Metadata
**Topic:** Binary Search Fundamentals  
**Week:** Week 4.5  
**Day:** Day 1 of 3  
**Category:** Search & Optimization  
**Difficulty:** 🟢 Easy / 🟡 Medium  
**Status:** 🔍 In Study  
**Last Reviewed:** —  
**Confidence Level (1–5):** —/5  

---

## 1️⃣ The Why — Engineering Motivation

### Real-World Problem

**You have 1 billion sorted numbers. Find a target. Can't do linear search (O(n)).**

```
Array: [1, 3, 5, 7, 9, 11, 13, 15, 17, 19]
Target: 13
Linear search: Check 1, 3, 5, 7, 9, 11, 13 ← 7 comparisons

Binary search: 
Check middle (9)
13 > 9, search right half
Check middle (15)
13 < 15, search left half
Check middle (11)
13 > 11, search right half
Found 13 ← 4 comparisons
```

**The power:** O(log n) vs O(n)

For 1 billion items:
```
Linear: 1,000,000,000 operations
Binary: log₂(1B) ≈ 30 operations
~33 million× faster!
```

### Why This Matters

**Binary search:**
1. **Reduces O(n) to O(log n)** - Exponential speedup
2. **Foundation for advanced searches** - Answers, search space reduction
3. **Works with sorted data** - Complements Week 4 sorting
4. **Extends beyond arrays** - Answer space, floating point

---

## 2️⃣ The What — Mental Model & Intuition

### Core Analogy: Guessing Game with Hints

**Game:** Guess a number 1-100. Feedback: "too high" or "too low"

```
Guess 50: "too low"
Range narrows: 51-100

Guess 75: "too high"
Range narrows: 51-74

Guess 62: "too low"
Range narrows: 63-74

Guess 68: "too high"
Range narrows: 63-67

Guess 65: "too low"
Range narrows: 66-67

Guess 66: "correct!" ← Found in log₂(100) ≈ 7 guesses
```

**Key insight:** Each guess cuts search space in half.

### Mental Model: Divide and Conquer Search

```
Sorted Array:
[1, 3, 5, 7, 9, 11, 13, 15, 17, 19]

Step 1: Check middle (9)
  Divide: [1,3,5,7] | 9 | [11,13,15,17,19]

If target > 9: Search right half
If target < 9: Search left half
If target == 9: Found!

Each step eliminates half of remaining elements
```

### Why Sorted Property is Essential

**Sorted array guarantees:**
```
All elements to left of middle: SMALLER
All elements to right of middle: LARGER

If target > middle: Know to go right (skip left half safely)
If target < middle: Know to go left (skip right half safely)

Without sorting, can't make directional decision.
```

---

## 3️⃣ The How — Mechanical Walkthrough

### Binary Search Template

```python
def binary_search(arr, target):
    left = 0
    right = len(arr) - 1
    
    while left <= right:
        mid = (left + right) // 2
        
        if arr[mid] == target:
            return mid  ← Found!
        elif arr[mid] < target:
            left = mid + 1  ← Search right
        else:
            right = mid - 1  ← Search left
    
    return -1  ← Not found

# Time: O(log n)
# Space: O(1)
```

### Example 1: Basic Binary Search

**Problem:** Find target in sorted array

```python
# Trace
arr = [1, 3, 5, 7, 9, 11, 13, 15, 17, 19]
target = 13

Iteration 1:
  left=0, right=9, mid=4
  arr[4]=9, 9 < 13
  left=5

Iteration 2:
  left=5, right=9, mid=7
  arr[7]=15, 15 > 13
  right=6

Iteration 3:
  left=5, right=6, mid=5
  arr[5]=11, 11 < 13
  left=6

Iteration 4:
  left=6, right=6, mid=6
  arr[6]=13, 13 == 13
  return 6 ✓
```

### Example 2: Find First Occurrence (Duplicates)

**Problem:** Array has duplicates, find first occurrence

```python
def binary_search_first(arr, target):
    left, right = 0, len(arr) - 1
    result = -1
    
    while left <= right:
        mid = (left + right) // 2
        
        if arr[mid] == target:
            result = mid  ← Remember position
            right = mid - 1  ← Keep searching left
        elif arr[mid] < target:
            left = mid + 1
        else:
            right = mid - 1
    
    return result

# Trace
arr = [1, 3, 5, 5, 5, 7, 9]
target = 5

Found at index 2, continue searching left
Reach index 2 (first occurrence)
return 2 ✓
```

### Example 3: Search in Rotated Array

**Problem:** Array is sorted but rotated. Find target.

```
Original: [1, 3, 5, 7, 9, 11, 13]
Rotated:  [7, 9, 11, 13, 1, 3, 5]
                         ↑ Pivot

Key insight: One half is always sorted
Find which half, then decide which to search
```

```python
def search_rotated(arr, target):
    left, right = 0, len(arr) - 1
    
    while left <= right:
        mid = (left + right) // 2
        
        if arr[mid] == target:
            return mid
        
        # Which half is sorted?
        if arr[left] <= arr[mid]:  # Left half sorted
            if arr[left] <= target < arr[mid]:
                right = mid - 1  # Target in left sorted half
            else:
                left = mid + 1  # Target in right (maybe rotated)
        else:  # Right half sorted
            if arr[mid] < target <= arr[right]:
                left = mid + 1  # Target in right sorted half
            else:
                right = mid - 1  # Target in left (maybe rotated)
    
    return -1
```

---

## 4️⃣ Visualization — Examples & Trace

### Visual Trace: Basic Binary Search

```
Array: [1, 3, 5, 7, 9, 11, 13, 15, 17, 19]
Target: 13

Step 1: Check middle (index 4, value 9)
[1, 3, 5, 7, 9 | 11, 13, 15, 17, 19]
       ↑ mid
9 < 13, search right

Step 2: Check middle of right half (index 7, value 15)
[11, 13, 15 | 17, 19]
    ↑ mid
15 > 13, search left

Step 3: Check middle (index 6, value 13)
[11, 13]
    ↑ mid
13 == 13 → FOUND! ✓

Iterations: 3
Compare to linear: Would need 7 checks
```

### Visual Trace: Find First Occurrence

```
Array: [1, 3, 5, 5, 5, 7, 9]
Target: 5

Step 1: Check middle (index 3, value 5)
[1, 3, 5 | 5, 5 | 7, 9]
    ↑ mid
5 == 5, but search left for first

Step 2: Check middle of left (index 1, value 3)
[1, 3 | 5]
  ↑ mid
3 < 5, search right

Step 3: Check middle (index 2, value 5)
[5]
↑ mid
5 == 5, no more left
→ First occurrence at index 2 ✓
```

---

## 5️⃣ Critical Analysis — Performance & Robustness

### Time Complexity Analysis

**Binary Search:** O(log n)

```
Array size 10:     log₂(10) ≈ 4 checks
Array size 100:    log₂(100) ≈ 7 checks
Array size 1000:   log₂(1000) ≈ 10 checks
Array size 1M:     log₂(1M) ≈ 20 checks
Array size 1B:     log₂(1B) ≈ 30 checks

Compare to linear O(n):
n=1B: 1,000,000,000 checks (timeout)
Binary: 30 checks (instant!)
```

### Space Complexity

**Iterative:** O(1) - Just left, right, mid pointers

**Recursive:** O(log n) - Call stack depth

### When Binary Search Works

**Condition 1: Data MUST be sorted**
```
Sorted: [1, 3, 5, 7, 9] ✓
Unsorted: [5, 1, 9, 3, 7] ✗ (must sort first, adds O(n log n))
```

**Condition 2: Random access required**
```
Arrays: O(1) access ✓
Linked lists: O(n) access ✗ (can't use binary search)
```

**Condition 3: Not dynamic (mostly)**
```
Static array: Perfect ✓
Frequent insertions: Expensive (breaks sort) ✗
```

### Edge Cases

**Edge Case 1: Single element**
```
arr = [5]
left=0, right=0, mid=0
arr[0]=5, compare with target
Works fine ✓
```

**Edge Case 2: Empty array**
```
arr = []
left=0, right=-1
left > right, exit loop
return -1 ✓
```

**Edge Case 3: Target not in array**
```
arr = [1, 3, 5, 7]
target = 6
Binary search will narrow to empty range
return -1 ✓
```

---

## 6️⃣ Real System Integration

### Where Binary Search Appears

**Database indexes:**
```
B-tree indexes use binary search concepts
Find leaf nodes quickly
```

**Version control (Git bisect):**
```
Find commit that introduced bug
Binary search through commits
```

**AutoComplete systems:**
```
Dictionary of 1M words
Binary search to find matches
```

**Competitive programming:**
```
Judge systems use binary search on answer space
Find minimum cost, maximum efficiency, etc.
```

---

## 7️⃣ Concept Crossovers

### Builds On (Week 3-4)

**Sorting:** Binary search requires sorted data (use Week 3 sorts)

**Two Pointers:** Similar divide-and-conquer on arrays

### Builds Toward (Week 5+)

**Answer Space Search:** Binary search on value space, not array

**Greedy + Binary Search:** Find optimal solution

---

## 8️⃣ Mathematical & Theoretical Perspective

### Proof: Binary Search Correctness

**Claim:** Binary search finds target if it exists.

**Proof by invariant:**

```
Invariant: If target exists in array, it exists in [left, right]

Initially: left=0, right=n-1
Target (if exists) is in [0, n-1] ✓

Each iteration:
- Check mid
- If arr[mid]==target, found ✓
- If arr[mid]<target, target must be in (mid, right]
  Update left=mid+1, invariant preserved ✓
- If arr[mid]>target, target must be in [left, mid)
  Update right=mid-1, invariant preserved ✓

Eventually: left > right (empty range)
If we haven't found target, it doesn't exist ✓

Therefore: Either finds target or correctly returns -1
```

### Why O(log n) Not O(1)?

```
O(1): Instant lookup (impossible without perfect hashing)
O(log n): Reduce problem by half each step
O(n): Linear scan

Binary search: Optimal for comparison-based search
Can't do better without special structure (hash table)
```

---

## 9️⃣ Algorithmic Design Intuition

### When to Use Binary Search

```
Do you need to find something in sorted data?
  ├─ YES → Consider binary search ✓
  ├─ Is data sorted?
  │   ├─ YES → Use directly O(log n)
  │   └─ NO → Sort first O(n log n) then search
  └─ NO → Linear search or hash table

Need exact match?
  ├─ YES → Binary search (or hash table)
  ├─ NO → May still help (answer space)
  
Multiple queries?
  ├─ YES → Sort once, binary search each
  ├─ NO → Linear might be simpler
```

---

## 🔟 Knowledge Check — Socratic Reasoning

**Question 1: Why can't you use binary search on unsorted arrays?**

Think: What assumption does binary search make about left and right halves?

**Question 2: Why is mid = (left + right) // 2?**

Think: What's wrong with mid = (left + right) / 2? (Hint: overflow, truncation)

**Question 3: When you find the target, why return immediately?**

Think: What if array has duplicates? When do you need to keep searching?

**Question 4: How would you find ALL occurrences of a duplicate element?**

Think: Find first, find last, count in between.

**Question 5: Why is space O(1) for iterative but O(log n) for recursive?**

Think: Call stack depth.

---

## 1️⃣1️⃣ Retention Hook — Memory Anchors

### One-Line Essence

> **Binary Search: Divide search space in half each iteration on sorted data. O(log n) time, O(1) space. Requires sorted input and random access.**

### Mnemonic: "BINARY"

- **B**y halving search space
- **I**terative or recursive
- **N**eed sorted data
- **A**rray or answer space
- **R**andom access required
- **Y**ield O(log n) magic

---

## 📚 Supplementary Data

### Binary Search Variations

| Type | Use Case | Complexity |
|------|----------|-----------|
| Exact match | Find target | O(log n) |
| First occurrence | Find first duplicate | O(log n) |
| Last occurrence | Find last duplicate | O(log n) |
| Answer space | Find min/max meeting condition | O(log n) |
| Rotated array | Handle pivot point | O(log n) |

---

## 🔗 External References

1. **LeetCode Problems:**
   - Binary Search: https://leetcode.com/problems/binary-search/
   - Search Insert Position: https://leetcode.com/problems/search-insert-position/
   - First Bad Version: https://leetcode.com/problems/first-bad-version/
   - Search in Rotated Array: https://leetcode.com/problems/search-in-rotated-sorted-array/

2. **Visualization:**
   - VisuAlgo Binary Search: https://www.cs.usfca.edu/~galles/visualization/BinarySearch.html

---

## 📋 Summary

**Binary Search Key Facts:**
✅ O(log n) on sorted arrays  
✅ O(1) space (iterative)  
✅ Requires sorted input  
✅ Requires random access  
✅ Foundation for answer space search  

**When to use:**
- Find element in sorted array ✓
- Multiple queries on sorted data ✓
- Space is premium ✓
- Need logarithmic time ✓

**When NOT to use:**
- Unsorted array (sort first) ✗
- Linked lists (no random access) ✗
- Hash table faster (O(1) vs O(log n)) ✗

---

**Word Count:** ~2,500 words  
**Reading Time:** 70-80 minutes  
**Status:** ✅ Complete with all 11 sections + supplementary material

