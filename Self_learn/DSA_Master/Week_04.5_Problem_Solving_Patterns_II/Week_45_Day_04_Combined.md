# 📘 WEEK 4.5 DAY 4: PARTITION & KADANE'S - Complete Learning Package

**Week 4.5, Day 4: Array Manipulation - Partitioning & Maximum Subarray Patterns**

Generated: 2025-12-26 | Duration: 90 minutes | Difficulty: 🟡 Medium | Target: 4-5/5

---

## PART 1: MAIN CONTENT (11 Sections)

### 1️⃣ The Why: Engineering Motivation

**Problem 1: Partition** - Move all zeros to end while maintaining order

Real-world:
- **Quicksort:** Partition arrays around pivot
- **Load balancing:** Separate heavy from light requests
- **Garbage collection:** Separate marked from unmarked objects
- **Data cleaning:** Segregate invalid from valid records

**Problem 2: Kadane's Algorithm** - Find maximum subarray sum

Real-world:
- **Stock trading:** Best buy-sell window (max profit)
- **Traffic analysis:** Peak traffic period
- **Weather data:** Warmest streak
- **Revenue:** Best performing quarter sequence

**Naive approaches:**
```python
# Partition: O(n) space
def move_zeroes_naive(arr):
    non_zero = [x for x in arr if x != 0]
    zeroes = [0] * (len(arr) - len(non_zero))
    return non_zero + zeroes

# Kadane naive: O(n²)
def max_subarray_naive(arr):
    max_sum = float('-inf')
    for i in range(len(arr)):
        for j in range(i+1, len(arr)+1):
            max_sum = max(max_sum, sum(arr[i:j]))
    return max_sum
```

**Efficient approaches:** O(n) and O(1) space

---

### 2️⃣ The What: Mental Model

**Part 1: Partition - Two Pointers**

**Core Insight:** Two pointers separate elements by condition. Left pointer finds element violating condition, right pointer swaps.

**Visual:**
```
Original: [1, 0, 2, 0, 3, 0, 4]
Target:   [1, 2, 3, 4, 0, 0, 0]

Process:
Step 1: left finds 0, swaps with right's 4
        [1, 4, 2, 0, 3, 0, 0] (simplified)
        Continue until left ≥ right
```

**Part 2: Kadane's Algorithm - Dynamic Programming**

**Core Insight:** At each position, decide: extend current sum or start fresh?

**Why this works:**
- Current best: max sum ending here
- For next element: extend previous or restart
- Track overall maximum
- O(n) single pass

**Visual:**
```
Array: [-2, 1, -3, 4, -1, 2, 1, -5, 4]

Position 0 (-2):
  current_max = -2, global_max = -2

Position 1 (1):
  current_max = max(1, -2+1) = 1
  global_max = 1

Position 2 (-3):
  current_max = max(-3, 1-3) = -2
  global_max = 1

Position 3 (4):
  current_max = max(4, -2+4) = 4
  global_max = 4

Position 4 (-1):
  current_max = max(-1, 4-1) = 3
  global_max = 4

Continue...
Final: global_max = 6 (subarray [4, -1, 2, 1])
```

---

### 3️⃣ The How: Mechanics

**Partition - Two Pointers Template:**
```python
def moveZeroes(arr):
    # Write pointer position
    write = 0
    
    for read in range(len(arr)):
        if arr[read] != 0:
            # Swap non-zero to write position
            arr[write], arr[read] = arr[read], arr[write]
            write += 1
    
    return arr
```

**Dutch National Flag (3-way partition):**
```python
def sort_colors(arr):  # 0s, 1s, 2s
    low = 0
    mid = 0
    high = len(arr) - 1
    
    while mid <= high:
        if arr[mid] == 0:
            arr[low], arr[mid] = arr[mid], arr[low]
            low += 1
            mid += 1
        elif arr[mid] == 1:
            mid += 1
        else:  # arr[mid] == 2
            arr[mid], arr[high] = arr[high], arr[mid]
            high -= 1
```

**Kadane's Algorithm Template:**
```python
def maxSubArray(arr):
    if not arr:
        return 0
    
    current_max = arr[0]
    global_max = arr[0]
    
    for i in range(1, len(arr)):
        # Decide: extend or restart
        current_max = max(arr[i], current_max + arr[i])
        
        # Update global maximum
        global_max = max(global_max, current_max)
    
    return global_max
```

**Finding Subarray Indices:**
```python
def maxSubArray_with_indices(arr):
    max_sum = arr[0]
    current_sum = arr[0]
    start = 0
    end = 0
    temp_start = 0
    
    for i in range(1, len(arr)):
        if arr[i] > current_sum + arr[i]:
            current_sum = arr[i]
            temp_start = i
        else:
            current_sum += arr[i]
        
        if current_sum > max_sum:
            max_sum = current_sum
            start = temp_start
            end = i
    
    return max_sum, start, end
```

**Step-by-step (Kadane):**
1. Initialize: current_max and global_max to first element
2. For each subsequent element:
   - Choose: extend current sum or start new
   - Update global maximum
3. Return global_max

**Complexity:**
- Time: O(n) single pass
- Space: O(1) only variables

---

### 4️⃣ Visualization: Examples

**Example 1: Partition (Move Zeroes)**
```
Array: [0, 1, 0, 3, 12]

Step 0: read=0 (0), write=0 → skip
Step 1: read=1 (1), write=0 → swap → [1, 0, 0, 3, 12], write=1
Step 2: read=2 (0), write=1 → skip
Step 3: read=3 (3), write=1 → swap → [1, 3, 0, 0, 12], write=2
Step 4: read=4 (12), write=2 → swap → [1, 3, 12, 0, 0], write=3

Result: [1, 3, 12, 0, 0]
```

**Example 2: Kadane's Algorithm**
```
Array: [5, -3, 5]

i=0: current=5, global=5
i=1: current=max(-3, 5-3)=2, global=5
i=2: current=max(5, 2+5)=7, global=7

Result: 7 (entire array [5, -3, 5])
```

**Example 3: Dutch Flag**
```
Array: [2, 0, 2, 1, 1, 0]

Process:
low=0, mid=0, high=5

mid=0 (2): swap with high → [0, 0, 2, 1, 1, 2], high=4
mid=0 (0): low→1, mid→1
mid=1 (0): low→2, mid→2
mid=2 (2): swap with high → [0, 0, 2, 1, 1, 2], high=3
mid=2 (2): swap with high → [0, 0, 1, 1, 2, 2], high=2
...
Result: [0, 0, 1, 1, 2, 2]
```

---

### 5️⃣ Critical Analysis

**Partition:**
- Time: O(n) single pass
- Space: O(1) in-place modification
- Better than collecting non-zero and appending zeros

**Kadane's Algorithm:**
- Time: O(n) single pass
- Space: O(1) only variables (vs O(n) for O(n²) naive)
- 1000x faster than O(n²) approach!

**Comparison:**

| Approach | Time | Space |
|----------|------|-------|
| Partition naive | O(n) | O(n) |
| Partition in-place | O(n) | O(1) |
| Kadane naive | O(n²) | O(1) |
| Kadane DP | O(n) | O(1) |

---

### 6️⃣ Real System Integration

**Partition in Quicksort:**
Critical for divide-and-conquer sorting.

**Kadane in Trading:**
Find best buy-sell window for stock trading.

**Data Segregation:**
Separate valid from invalid records in pipelines.

---

### 7️⃣ Concept Crossovers

**Builds On:**
- Week 1: Array operations
- Week 2: Two pointers
- Week 4: Dynamic thinking

**Enables:**
- Quicksort (partition)
- Dynamic programming (Kadane extends)
- Advanced DP problems

**Related Techniques:**
- Multiway partition (3-way, k-way)
- Sliding window variations
- DP problems

---

### 8️⃣ Mathematical Perspective

**Kadane's Correctness:**
- Optimal subarray ending at position i is either:
  - Starting fresh at i: arr[i]
  - Extending from i-1: max_ending[i-1] + arr[i]
- Maximum subarray is maximum of all max_ending[i]

**Proof by Induction:**
- Base: max_ending[0] = arr[0] ✓
- Step: if true for i-1, then true for i ✓

---

### 9️⃣ Algorithmic Design Intuition

**When to Use Partition:**
1. Need to segregate elements
2. Order within groups not critical
3. Space important
4. Single pass preferred

**When to Use Kadane's:**
1. Maximum/minimum subarray sum
2. O(n) time critical
3. Extensions: product, circular, etc.

---

### 🔟 Knowledge Check

1. Why partition is O(n) instead of O(n²)?
2. Trace move zeroes example
3. What's Dutch National Flag?
4. How Kadane's algorithm works?
5. When to extend vs restart (Kadane)?
6. Why Kadane O(n) vs O(n²) naive?
7. Can find subarray indices with Kadane?

---

### 1️⃣1️⃣ Retention Hooks

**Partition One-liner:** "Two pointers separate elements by condition in single pass."

**Kadane One-liner:** "At each position, extend current sum or restart fresh."

**Mnemonics:**
- **PARTITION:** Two pointers, condition, swap, O(n)
- **KADANE:** Current max, global max, extend or restart

---

## PART 2: QUICK SUMMARY

**Partition Essence:**
Two pointers separate elements by condition. Write pointer tracks position for valid elements.

**Kadane's Essence:**
Dynamic decision: extend current sum or start new. Track global maximum.

**When to Use Partition:**
- Segregate elements ✓
- In-place modification ✓
- Single pass ✓

**When to Use Kadane:**
- Maximum subarray sum ✓
- O(n) time required ✓
- Dynamic extension/restart ✓

---

## PART 3: SOCRATIC QUESTIONS & ANSWERS

**Q1:** Why partition is O(n) instead of O(n²)?

**A:** Two pointers traverse array once each. O(n) total operations. No nested comparison like O(n²) approaches.

**Q2:** Trace move zeroes on [0, 1, 0, 3, 12]

**A:** Already traced above in visualization.

**Q3:** What's Dutch National Flag?

**A:** 3-way partition for 0s, 1s, 2s. Uses low, mid, high pointers to maintain three regions.

**Q4:** How Kadane's algorithm work?

**A:** At each element, decide extend current sum or start fresh. Track global maximum through single pass.

**Q5:** When to extend vs restart (Kadane)?

**A:** Extend if current_sum + arr[i] > arr[i]. Otherwise restart fresh at arr[i].

**Q6:** Why Kadane O(n) vs O(n²) naive?

**A:** Naive checks all subarrays. Kadane uses dynamic programming decision at each step. Single pass = O(n).

**Q7:** Can find subarray indices with Kadane?

**A:** Yes! Track temp_start and when max updates, record start and end indices.

---

## PART 4: README

**90-Minute Study Guide:**
1. Partition Why (5 min)
2. Kadane Why (5 min)
3. Partition What (10 min)
4. Kadane What (10 min)
5. Implementation (15 min)
6. Visualization (20 min)
7. Questions (10 min)

**Key Skills:** Partition arrays, find maximum subarray

**Practice:** Move zeroes, sort colors, max subarray

**Connection:** Foundation for quicksort and advanced DP!

---

**Status:** ✅ Day 4 Complete | **Next:** Week 4.5 Complete, Review, Then Week 5!

