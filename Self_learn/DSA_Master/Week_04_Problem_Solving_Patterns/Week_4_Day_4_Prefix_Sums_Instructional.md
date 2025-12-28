# Week 4, Day 4: Prefix Sums

## 🗓 Metadata
**Week:** 4 | **Day:** 4 of 5 | **Topic:** Prefix Sum Arrays  
**Category:** Problem-Solving Patterns | **Difficulty:** 🟡 Medium  
**Prerequisites:** Week 1-3 (arrays), Day 3 (sliding window)  
**Time:** 120-150 minutes | **Status:** 🔍 In Study

---

## 1️⃣ THE WHY — Engineering Motivation

### Real-World Problem
Range sum queries: "What's the sum of elements from index i to j?" Naive recomputation O(n) per query. Prefix sum trades O(n) space for O(1) query time, enabling O(n + q) total for n elements + q queries.

### Design Problems Solved
- **Range sum queries** (between two indices)
- **Subarray sum problems** (target sum matching)
- **Cumulative statistics** (running totals)
- **2D matrix queries** (sum rectangle)
- **Difference arrays** (range updates O(1))
- **Equilibrium checking** (left sum = right sum)
- **Optimization problems** (find best k-element prefix)

### Real System Usage
- **Time-series databases:** Cumulative sum enables fast range queries on metrics
- **Graphics:** Integral images enable fast feature detection in image processing
- **Finance:** Running balance in transaction processing
- **Analytics:** Aggregation queries benefit from cumulative data
- **Game development:** Mipmap generation uses hierarchical prefix sums
- **Statistics:** Cumulative distribution function (CDF) computation
- **Networking:** Checksum computation accumulates prefix state

### Why Prefix Sums Matter
**Decouples query time from array size through preprocessing**. Fundamental technique for range query optimization, enabling O(1) lookups after O(n) preprocessing.

---

## 2️⃣ THE WHAT — Mental Model & Intuition

### Core Analogy
Imagine **cumulative page numbers** in book. "What's total pages 1-5?" Look at page 5's cumulative number. "Difference between pages 10-5?" Subtract cumulative at 5 from cumulative at 10. No need to count all pages.

### Key Invariants
1. **Monotonic Invariant:** prefix[i] ≥ prefix[i-1] (for non-negative arrays)
2. **Decomposition Invariant:** sum(i, j) = prefix[j] - prefix[i-1]
3. **Prefix Invariant:** prefix[i] = sum of all elements from 0 to i

### Visual Representation

```
Original Array:
[1, 2, 3, 4, 5]
 0  1  2  3  4

Prefix Sum Array:
[0, 1, 3, 6, 10, 15]
 ↑  ↑  ↑  ↑   ↑   ↑
 0  1  1+2 1+2+3 ... 1+2+3+4+5

Range Query: sum(1 to 3) = 2+3+4 = 9
Using prefix: prefix[4] - prefix[1] = 10 - 1 = 9 ✓
```

---

## 3️⃣ THE HOW — Mechanical Walkthrough

### Operation 1: Build Prefix Sum Array

```
Algorithm: Create prefix sum array from original

Input: array of n elements
Output: prefix array of size n+1

Initialize:
  prefix[0] = 0  // Empty prefix is 0

For i = 1 to n:
  prefix[i] = prefix[i-1] + array[i-1]

Time: O(n) — linear pass
Space: O(n) — new array

Example: [1, 2, 3, 4, 5]
prefix[0] = 0
prefix[1] = 0 + 1 = 1
prefix[2] = 1 + 2 = 3
prefix[3] = 3 + 3 = 6
prefix[4] = 6 + 4 = 10
prefix[5] = 10 + 5 = 15
Result: [0, 1, 3, 6, 10, 15]
```

### Operation 2: Query Range Sum

```
Algorithm: Find sum from index left to right (inclusive)

Requires: prefix array already built

sum(left, right) = prefix[right + 1] - prefix[left]

Time: O(1) — constant time lookup
Space: O(1) — no extra space

Example: sum(1, 3) in [1, 2, 3, 4, 5]
sum = prefix[4] - prefix[1] = 10 - 1 = 9
(equals 2 + 3 + 4 = 9 ✓)
```

### Operation 3: Find Subarrays with Target Sum

```
Algorithm: Count subarrays summing to target

Use: Hash map of prefix sums seen
For each position, check if (current_sum - target) exists

Initialize:
  prefix_count = {0: 1}  // Empty prefix
  current_sum = 0
  count = 0

For i = 0 to n-1:
  current_sum += array[i]
  
  complement = current_sum - target
  if complement in prefix_count:
    count += prefix_count[complement]
  
  prefix_count[current_sum]++

return count

Time: O(n) — single pass with hash table
Space: O(n) — hash map storage
```

---

## 4️⃣ VISUALIZATION — Simulation & Examples

### Example 1: Range Sum Queries

**Problem:** Given [1, 2, 3, 4, 5], answer queries: sum(1,2)? sum(2,4)?

```
Array:      [1,  2,  3,  4,  5]
Indices:     0   1   2   3   4

Build prefix:
prefix[0] = 0
prefix[1] = 0+1 = 1
prefix[2] = 1+2 = 3
prefix[3] = 3+3 = 6
prefix[4] = 6+4 = 10
prefix[5] = 10+5 = 15

Query: sum(1, 2) = elements at indices 1,2 = 2+3 = 5
Using prefix: prefix[3] - prefix[1] = 6 - 1 = 5 ✓

Query: sum(2, 4) = elements at indices 2,3,4 = 3+4+5 = 12
Using prefix: prefix[5] - prefix[2] = 15 - 3 = 12 ✓

Without prefix: Each query requires summing elements O(n)
With prefix: Each query is O(1) lookup
For 1000 queries: 1000n → n (1000× speedup!)
```

---

### Example 2: Subarray Sum Equals K

**Problem:** Count subarrays in [1,2,3,1,2,1,3] summing to 3

```
Array: [1, 2, 3, 1, 2, 1, 3]
Target: 3

current_sum = 0, count = 0
prefix_count = {0: 1}

i=0: array[0]=1
  current_sum = 1
  complement = 1-3 = -2 (not in map)
  prefix_count = {0:1, 1:1}

i=1: array[1]=2
  current_sum = 3
  complement = 3-3 = 0 (in map! count += 1)
  Explanation: subarray [1,2] sums to 3
  prefix_count = {0:1, 1:1, 3:1}, count = 1

i=2: array[2]=3
  current_sum = 6
  complement = 6-3 = 3 (in map! count += 1)
  Explanation: subarray [3] sums to 3
  prefix_count = {0:1, 1:1, 3:1, 6:1}, count = 2

i=3: array[3]=1
  current_sum = 7
  complement = 7-3 = 4 (not in map)
  prefix_count = {0:1, 1:2, 3:1, 6:1, 7:1}

i=4: array[4]=2
  current_sum = 9
  complement = 9-3 = 6 (in map! count += 1)
  Explanation: subarray from after index 2 to here
  prefix_count = {0:1, 1:2, 3:1, 6:1, 7:1, 9:1}, count = 3

i=5: array[5]=1
  current_sum = 10
  complement = 10-3 = 7 (in map! count += 1)
  prefix_count = {0:1, 1:3, 3:1, 6:1, 7:1, 9:1, 10:1}, count = 4

i=6: array[6]=3
  current_sum = 13
  complement = 13-3 = 10 (in map! count += 1)
  prefix_count = {0:1, 1:3, 3:1, 6:1, 7:1, 9:1, 10:1, 13:1}, count = 5

Answer: 5 subarrays sum to 3
They are: [1,2], [3], [1,2], [1,1,1], [3]
```

---

## 5️⃣ CRITICAL ANALYSIS — Performance & Robustness

### Complexity Analysis

| Operation | Time | Space | Conditions |
|-----------|------|-------|-----------|
| **Build prefix** | O(n) | O(n) | Initial preprocessing |
| **Range query** | O(1) | O(1) | After building |
| **Subarray count** | O(n) | O(n) | Hash map with prefix sums |
| **2D prefix** | O(mn) | O(mn) | 2D array preprocessing |

### Edge Cases & Failure Modes

1. **Zero elements:** Empty prefix valid
   - ✅ **Solution:** prefix[0] = 0 handles naturally

2. **Single element:** Array of size 1
   - ✅ **Solution:** prefix = [0, element]

3. **Negative numbers:** Prefix not monotonic
   - ✅ **Solution:** Still works, just may decrease

4. **Integer overflow:** Large sums exceed int range
   - ❌ **Risk:** Wraparound on large datasets
   - ✅ **Solution:** Use 64-bit integer or check overflow

---

## 6️⃣ REAL SYSTEM INTEGRATION

### System 1: Time-Series Database Range Queries (InfluxDB)
Cumulative sum enables fast aggregation:
```
Store: [1M data points of daily revenue]
Query: "Total revenue Q3?" (92 days)
Naive: Sum 92 values = 92 operations
With prefix: prefix[day92] - prefix[day1] = 1 operation
```

### System 2: Image Integral Images (OpenCV)
Fast feature detection in computer vision:
```
integral[x][y] = sum of all pixels(0,0) to (x,y)
Helps: Haar Cascade face detection
Speed: O(1) rectangle area queries
Used: Real-time video processing
```

### System 3-7: Finance, Analytics, Networking, Graphics, Statistics
Similar cumulative computation patterns across systems

---

## 7️⃣ CONCEPT CROSSOVERS

### Builds On
- Arrays (Week 2): Linear data structure
- Hashing (Week 3): Count occurrences in prefix_count
- Sliding window: Range queries solved differently

### Built Upon By
- 2D prefix sums (matrix problems)
- Segment trees (range updates + queries)
- Week 11 DP: Cumulative states

---

## 8️⃣ MATHEMATICAL & THEORETICAL PERSPECTIVE

### Theorem: Prefix Sum Correctness
**Claim:** sum(i, j) = prefix[j+1] - prefix[i]

**Proof:**
```
Let prefix[k] = sum of elements 0 to k-1
sum(i, j) = element[i] + element[i+1] + ... + element[j]
          = (element[0] + ... + element[j]) - (element[0] + ... + element[i-1])
          = prefix[j+1] - prefix[i]
```

---

## 9️⃣ ALGORITHMIC DESIGN INTUITION

### When to Use Prefix Sums

✅ **Use when:**
- Multiple range sum queries (q queries)
- Need to optimize from O(nq) to O(n+q)
- Range aggregate operations (sum, XOR, etc.)

✅ **Examples:**
- Subarray sum equals k
- Range sum query mutable/immutable
- Maximum sum rectangle in 2D matrix

---

## 🔟 KNOWLEDGE CHECK — Socratic Reasoning

**Q1: Why is prefix array size n+1 instead of n?**
- Hint: What happens if you query sum starting at index 0?
- Deep: How does prefix[0]=0 solve the problem?

**Q2: Can prefix sums handle range updates?**
- Hint: If you change array[i], what happens to prefix?
- Deep: How is this different from simple queries?

---

## 1️⃣1️⃣ RETENTION HOOK — Memory Anchors

**One-Liner:**
> **Prefix sum trades O(n) space to transform O(n) queries into O(1): range[i,j] = prefix[j+1] - prefix[i].**

**Mnemonic:** **CUMULATIVE** (running total) or **PAGE COUNTER**

### 5 Cognitive Lenses

| **Computational** | Single array pass O(n) preprocessing. O(1) lookup per query uses cache efficiency. |
| **Psychological** | "Don't recompute what you've seen": store running total, reuse it. |
| **Design Trade-off** | Space O(n) up front to save time O(1) per query. Worth it for many queries. |
| **AI/ML Analogy** | CDF (cumulative distribution): answers "probability ≤ x" in O(1) after building CDF. |
| **Historical Context** | Known since 1960s. Fundamental in any system doing repeated range queries. |

---

## Supplementary Outcomes

### Practice Problems (8+)

1. **Range Sum Query - Immutable** (LeetCode 303)
   - Class with constructor and sum range method
   - [Easy] 15 min

2. **Subarray Sum Equals K** (LeetCode 560)
   - Count subarrays summing to target
   - Hash map + prefix sums
   - [Medium] 20 min

3. **Contiguous Array** (LeetCode 485)
   - Find longest contiguous subarray with equal 0s and 1s
   - Replace 0→-1, find sum=0
   - [Medium] 20 min

4. **Maximum Subarray** (LeetCode 53)
   - Kadane's algorithm variant
   - Uses cumulative concepts
   - [Medium] 15 min

5. **2D Sum Matrix Queries** (LeetCode 304)
   - 2D version of range sum
   - 2D prefix array
   - [Medium] 25 min

6. **Matrix Block Sum** (LeetCode 1314)
   - Block sum queries on 2D matrix
   - 2D prefix with block size
   - [Medium] 25 min

7. **Binary Subarray with Sum** (LeetCode 930)
   - Subarrays in binary array with sum k
   - Prefix sums on binary data
   - [Medium] 20 min

8. **Cumulative Sum of Divisors** (LeetCode variant)
   - Range queries on divisor counts
   - Prefix on mathematical sequence
   - [Hard] 30 min

---

**Status:** ✅ Complete  
**Next:** Day 5 (Cycle Detection using Floyd's Algorithm)

