# Week 4 Day 3: Prefix Sums - Range Query Optimization

## 🗓 Metadata
**Topic:** Prefix Sums Technique  
**Week:** Week 4  
**Day:** Day 3 of 5  
**Category:** Array Optimization  
**Difficulty:** 🟢 Easy / 🟡 Medium  
**Status:** 🔍 In Study  
**Last Reviewed:** —  
**Confidence Level (1–5):** —/5  

---

## 1️⃣ The Why — Engineering Motivation

### Real-World Problem

**Given array, answer multiple range sum queries efficiently.**

```
Array: [3, 2, 5, 1, 4]
Query 1: Sum of elements from index 1 to 3 = 2+5+1 = 8
Query 2: Sum of elements from index 0 to 2 = 3+2+5 = 10
Query 3: Sum of elements from index 2 to 4 = 5+1+4 = 10
```

**Naive approach (O(q×n)):**
```
for each query (left, right):
    sum = 0
    for i in range(left, right+1):
        sum += arr[i]
    return sum
```

**Problem:** q queries × n elements per query = O(q×n). For q=1M, n=1M: 1 trillion ops!

**Better approach (O(n + q)):**
```
Precompute prefix sums once: O(n)
prefix[i] = sum of elements from 0 to i

For query (left, right):
answer = prefix[right] - prefix[left-1]  ← O(1)!

Total: O(n) preprocessing + O(q) queries = O(n+q)
```

### Why This Matters

**Prefix sums:**
1. **Reduces range queries from O(n) to O(1)**
2. **Enables solving problems with multiple passes**
3. **Foundation for advanced techniques** (2D prefix sums, product arrays)
4. **Trade-off:** O(n) space for O(1) query time

---

## 2️⃣ The What — Mental Model & Intuition

### Core Analogy: Cumulative Bank Balance

**Checking account transactions:**

```
Day:    1    2    3    4    5
Trans: +3   +2   +5   +1   +4
       ↓    ↓    ↓    ↓    ↓

Balance evolution:
Day 1: 3
Day 2: 3+2 = 5
Day 3: 5+5 = 10
Day 4: 10+1 = 11
Day 5: 11+4 = 15

To find total spent from day 2-4:
Spend = Balance_day4 - Balance_day1
      = 11 - 3 = 8
(Matches: 2+5+1 = 8) ✓
```

**Key insight:** Cumulative sum lets you query any range instantly.

### Mental Model: Cumulative Array

```
Array:     [3, 2, 5, 1, 4]
Index:      0  1  2  3  4

Prefix sum:
Index 0: 3
Index 1: 3+2 = 5
Index 2: 3+2+5 = 10
Index 3: 3+2+5+1 = 11
Index 4: 3+2+5+1+4 = 15

Range sum [1,3]:
= prefix[3] - prefix[0]
= 11 - 3
= 8 ✓
```

---

## 3️⃣ The How — Mechanical Walkthrough

### Prefix Sum Template

```python
def build_prefix_sum(arr):
    n = len(arr)
    prefix = [0] * (n + 1)  # Extra 0 at start
    
    for i in range(n):
        prefix[i+1] = prefix[i] + arr[i]
    
    return prefix

def range_sum(prefix, left, right):
    # Sum from left to right (inclusive)
    return prefix[right+1] - prefix[left]

# Usage
arr = [3, 2, 5, 1, 4]
prefix = build_prefix_sum(arr)  # [0, 3, 5, 10, 11, 15]

print(range_sum(prefix, 1, 3))  # 8
print(range_sum(prefix, 0, 2))  # 10
print(range_sum(prefix, 2, 4))  # 10
```

### Example 1: Running Sum

**Problem:** Compute running sum (each position is sum up to that index)

```python
def running_sum(arr):
    result = []
    current_sum = 0
    
    for num in arr:
        current_sum += num
        result.append(current_sum)
    
    return result

# Trace
arr = [3, 2, 5, 1, 4]
current_sum = 0
→ 0 + 3 = 3, result = [3]
→ 3 + 2 = 5, result = [3, 5]
→ 5 + 5 = 10, result = [3, 5, 10]
→ 10 + 1 = 11, result = [3, 5, 10, 11]
→ 11 + 4 = 15, result = [3, 5, 10, 11, 15]

Answer: [3, 5, 10, 11, 15] ✓
```

### Example 2: Product Array Except Self

**Problem:** For each index, find product of all other elements (without division)

```python
def product_except_self(arr):
    n = len(arr)
    result = [1] * n
    
    # Left products: result[i] = product of all elements left of i
    left_product = 1
    for i in range(n):
        result[i] *= left_product
        left_product *= arr[i]
    
    # Right products: result[i] *= product of all elements right of i
    right_product = 1
    for i in range(n-1, -1, -1):
        result[i] *= right_product
        right_product *= arr[i]
    
    return result

# Trace
arr = [1, 2, 3, 4]

Left pass:
i=0: result[0] = 1 × 1 = 1, left_product = 1 × 1 = 1
i=1: result[1] = 1 × 1 = 1, left_product = 1 × 2 = 2
i=2: result[2] = 1 × 2 = 2, left_product = 2 × 3 = 6
i=3: result[3] = 1 × 6 = 6, left_product = 6 × 4 = 24

After left: result = [1, 1, 2, 6]

Right pass:
i=3: result[3] = 6 × 1 = 6, right_product = 1 × 4 = 4
i=2: result[2] = 2 × 4 = 8, right_product = 4 × 3 = 12
i=1: result[1] = 1 × 12 = 12, right_product = 12 × 2 = 24
i=0: result[0] = 1 × 24 = 24, right_product = 24 × 1 = 24

Answer: [24, 12, 8, 6] ✓
Verify: [2×3×4, 1×3×4, 1×2×4, 1×2×3] = [24, 12, 8, 6] ✓
```

### Example 3: 2D Prefix Sum

**Problem:** Answer 2D range sum queries in O(1)

```python
def build_2d_prefix(matrix):
    rows, cols = len(matrix), len(matrix[0])
    prefix = [[0] * (cols + 1) for _ in range(rows + 1)]
    
    for i in range(1, rows + 1):
        for j in range(1, cols + 1):
            prefix[i][j] = (prefix[i-1][j] + prefix[i][j-1] 
                          - prefix[i-1][j-1] + matrix[i-1][j-1])
    
    return prefix

def sum_region(prefix, row1, col1, row2, col2):
    # Sum of rectangle from (row1,col1) to (row2,col2)
    return (prefix[row2+1][col2+1] - prefix[row1][col2+1] 
          - prefix[row2+1][col1] + prefix[row1][col1])

# Usage
matrix = [[3, 0, 1],
          [5, 6, 2],
          [1, 2, 4]]

prefix = build_2d_prefix(matrix)
print(sum_region(prefix, 0, 0, 2, 2))  # Sum of entire matrix = 24
print(sum_region(prefix, 1, 1, 2, 2))  # Sum of [6,2,2,4] = 14
```

---

## 4️⃣ Visualization — Examples & Trace

### Visual Trace: Range Sum Queries

```
Array: [3, 2, 5, 1, 4]

Prefix sum array:
prefix[0] = 0
prefix[1] = 3
prefix[2] = 5
prefix[3] = 10
prefix[4] = 11
prefix[5] = 15

Query: Sum from index 1 to 3
  = prefix[4] - prefix[1]
  = 11 - 3
  = 8
  
Visual:
|---3---|--2--|--5--|--1--|--4--|
         ^left         ^right
  Exclude left of index 1, include up to right
  Answer: 2+5+1 = 8 ✓
```

### Visual Trace: Product Except Self

```
Array: [1, 2, 3, 4]

Left product (product of all left):
Index 0: 1 (nothing left)
Index 1: 1 (only 1 left)
Index 2: 1×2 = 2 (1 and 2 left)
Index 3: 1×2×3 = 6 (1,2,3 left)

Right product (product of all right):
Index 0: 2×3×4 = 24
Index 1: 3×4 = 12
Index 2: 4
Index 3: 1 (nothing right)

Result:
Index 0: 1 × 24 = 24 ✓
Index 1: 1 × 12 = 12 ✓
Index 2: 2 × 4 = 8 ✓
Index 3: 6 × 1 = 6 ✓
```

### Visual Trace: 2D Prefix Sum

```
Matrix:
[3, 0, 1]
[5, 6, 2]
[1, 2, 4]

Prefix matrix:
[0,  0,  0,  0]
[0,  3,  3,  4]
[0,  8, 14, 17]
[0,  9, 17, 24]

Query sum_region(0, 0, 2, 2) = entire matrix
  = prefix[3][3] - 0 - 0 + 0
  = 24 ✓

Query sum_region(1, 1, 2, 2):
  = prefix[3][3] - prefix[1][3] - prefix[3][1] + prefix[1][1]
  = 24 - 4 - 9 + 3
  = 14 ✓ (which is 6+2+2+4)
```

---

## 5️⃣ Critical Analysis — Performance & Robustness

### Time Complexity

**Build prefix:** O(n)
```
Single pass through array
Each element processed once
```

**Query range sum:** O(1)
```
Just arithmetic: prefix[right+1] - prefix[left]
Constant time regardless of range size
```

**Total for q queries:** O(n + q)
```
vs Naive: O(n×q)

For n = 1M, q = 1M:
Prefix: 2M operations
Naive: 1 trillion operations
5×10^8× speedup!
```

### Space Complexity

**Prefix sums:** O(n)
```
Store prefix array of size n+1
```

**2D prefix sums:** O(n×m)
```
Store 2D prefix array
```

### When Prefix Sums Work

**Condition 1: Multiple range queries**
```
Single query: Naive O(n) is fine
Multiple queries: Prefix O(1) per query dominates
```

**Condition 2: Static array**
```
If array changes, must rebuild prefix
For dynamic updates: Segment tree better
```

**Condition 3: Linear (or 2D/3D) ranges**
```
✓ 1D range sum [i, j]
✓ 2D rectangle sum
✗ Arbitrary shapes (tree range sums)
```

### Edge Cases

**Edge Case 1: Single element**
```
arr = [5]
prefix = [0, 5]
sum(0, 0) = prefix[1] - prefix[0] = 5 - 0 = 5 ✓
```

**Edge Case 2: Range with negative numbers**
```
arr = [3, -2, 5, -1, 4]
prefix = [0, 3, 1, 6, 5, 9]
Works same way (subtraction handles negatives) ✓
```

**Edge Case 3: Zero in array**
```
arr = [1, 0, 2, 0, 3]
prefix = [0, 1, 1, 3, 3, 6]
Works fine ✓
```

---

## 6️⃣ Real System Integration

### Where Prefix Sums Appears

**Image processing (2D prefix sums):**
```
Integral images for fast rectangle feature computation
Used in face detection (Viola-Jones algorithm)
Allows O(1) average brightness of any rectangle
```

**Data warehouse queries:**
```
Fast aggregation queries over time ranges
Stock price statistics, website analytics
```

**Competitive programming:**
```
Many problems require fast range queries
Segment trees often built on prefix concepts
```

---

## 7️⃣ Concept Crossovers

### Builds On (Weeks 3-4)

**Arrays:** Fundamental structure for prefix sums

**Sorting:** Some problems need pre-sorting before prefix sums

### Builds Toward (Advanced)

**Segment Trees:** Build on prefix sum concepts for updates

**Dynamic Programming:** Prefix sums optimize many DP solutions

---

## 8️⃣ Mathematical & Theoretical Perspective

### Proof: Correctness of Range Sum Formula

**Claim:** For prefix array, sum(left, right) = prefix[right+1] - prefix[left]

**Proof:**

```
Let S(i) = sum of elements from 0 to i

prefix[i] = sum of arr[0] to arr[i-1]
prefix[i+1] = sum of arr[0] to arr[i]

We want: sum from arr[left] to arr[right]
       = S(right) - S(left-1)
       = prefix[right+1] - prefix[left]

Example:
arr = [a, b, c, d, e]
left=1, right=3

Sum = b + c + d
    = (a+b+c+d) - (a)
    = S(3) - S(0)
    = prefix[4] - prefix[1]
```

---

## 9️⃣ Algorithmic Design Intuition

### Decision Framework

**When to use prefix sums:**

```
Are there multiple range queries?
  ├─ YES → Use prefix sums ✓
  ├─ NO  → Might not help
  └─ More queries → more benefit

Is array static?
  ├─ YES → Prefix sums work ✓
  ├─ NO  → Use segment tree
  └─ Updates require rebuild

Is dimension small (1D, 2D)?
  ├─ YES → Prefix sums efficient
  ├─ NO  → Might need different structure
  └─ 3D still works but O(n³) space
```

---

## 🔟 Knowledge Check — Socratic Reasoning

**Question 1: Why is prefix sum construction O(n) and not O(n²)?**

Think: Do you need to recalculate all previous elements?

**Question 2: Why does 2D prefix use the formula: prefix[i-1][j] + prefix[i][j-1] - prefix[i-1][j-1]?**

Think: What double-counting happens? Why subtract overlap?

**Question 3: When would naive range sum be better than prefix sums?**

Think: What's the break-even point for number of queries?

**Question 4: Can prefix sums help with updates to array?**

Think: What happens to prefix array when you change one element?

**Question 5: How would you handle 3D range queries?**

Think: Generalize 2D formula to 3D with inclusion-exclusion principle.

---

## 1️⃣1️⃣ Retention Hook — Memory Anchors

### One-Line Essence

> **Prefix sums: Precompute cumulative sums in O(n) to enable O(1) range queries. Trade space for query speed.**

### Mnemonic: "CUMULATIVE"

- **C**umulative sum at each index
- **U**pdate once (during preprocessing)
- **M**ultiple queries answered fast
- **U**se subtraction for ranges
- **L**inear space O(n)
- **A**rray must be static
- **T**ime: O(n + q) total
- **I**nclusion-exclusion (2D)
- **V**ery fast queries O(1)
- **E**xcel at aggregation problems

---

## 📚 Supplementary Data

### Prefix Sums Variations

| Type | Space | Build | Query | Use Case |
|------|-------|-------|-------|----------|
| 1D | O(n) | O(n) | O(1) | Range sums |
| 2D | O(n²) | O(n²) | O(1) | Rectangle sums |
| 3D | O(n³) | O(n³) | O(1) | Box sums |
| 1D updates | O(n) | O(n) | O(n) | Segment tree needed |

---

## 🔗 External References

1. **LeetCode Problems:**
   - Running Sum: https://leetcode.com/problems/running-sum-of-1d-array/
   - Product Array Except Self: https://leetcode.com/problems/product-of-array-except-self/
   - 2D Sum Query: https://leetcode.com/problems/range-sum-query-2d-immutable/

---

## 📋 Summary

**Prefix Sums Key Facts:**
✅ O(n) preprocessing, O(1) queries  
✅ Trade space O(n) for query speed  
✅ Works for 1D, 2D, 3D ranges  
✅ Array must be static  
✅ Fundamental for many optimization problems  

---

**Word Count:** ~2,500 words  
**Reading Time:** 70-80 minutes  
**Status:** ✅ Complete with all 11 sections + supplementary material

