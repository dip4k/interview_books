# 📘 WEEK 4 DAY 2: SLIDING WINDOW (FIXED) - Complete Learning Package

**Week 4, Day 2: Problem-Solving Pattern - Sliding Window with Fixed Size**

Generated: 2025-12-26 | Duration: 90 minutes | Difficulty: 🟡 Medium | Target: 4-5/5

---

## PART 1: MAIN CONTENT (11 Sections)

### 1️⃣ The Why: Engineering Motivation

**Problem:** Given an array, find the maximum sum of any subarray with exactly k elements.

Real-world:
- **Network traffic:** Find busiest k-minute window in network logs
- **Stock trading:** Find k-day period with highest average price
- **Video streaming:** Calculate quality over k-second buffering window
- **Temperature monitoring:** Find hottest k-hour period in sensor data
- **Website analytics:** Peak traffic in k-minute intervals

**Naive approach:** Recalculate sum for each window O(n·k)
```python
max_sum = float('-inf')
for i in range(len(arr) - k + 1):
    window_sum = sum(arr[i:i+k])  # O(k) operation
    max_sum = max(max_sum, window_sum)
```

**Sliding window approach:** Calculate once, slide O(n)
```python
window_sum = sum(arr[:k])  # O(k) setup
max_sum = window_sum

for i in range(1, len(arr) - k + 1):
    window_sum = window_sum - arr[i-1] + arr[i+k-1]  # O(1) update
    max_sum = max(max_sum, window_sum)
```

**Performance difference:** 10,000 items, k=100: 1M ops vs 10K ops (100x faster!)

---

### 2️⃣ The What: Mental Model

**Core Insight:** Instead of recalculating, maintain window value and slide it forward by removing left element and adding right element.

**Why this works:**
- Window always size k (fixed)
- Move forward one position per iteration
- Remove element leaving window, add element entering
- Recalculation is O(1) instead of O(k)

**Visual:**
```
Array: [1, 2, 3, 4, 5, 6, 7, 8, 9], k=3

Initial window (i=0):
[1, 2, 3] 4  5  6  7  8  9
sum=6

Slide right (i=1):
1 [2, 3, 4] 5  6  7  8  9
remove 1, add 4
sum = 6 - 1 + 4 = 9

Slide right (i=2):
1  2 [3, 4, 5] 6  7  8  9
remove 2, add 5
sum = 9 - 2 + 5 = 12

And so on...
```

**Key Property:** Slide window forward, update value in O(1) by removing left and adding right.

---

### 3️⃣ The How: Mechanics

**Algorithm Template:**
```python
def sliding_window_fixed(arr, k, operation):
    # Initialize window with first k elements
    window_value = operation(arr[:k])
    result = [window_value]  # or track max/min
    
    # Slide window forward
    for i in range(k, len(arr)):
        # Remove leftmost element of previous window
        # Add new rightmost element
        window_value = update(window_value, arr[i-k], arr[i])
        result.append(window_value)
        # or: result = max(result, window_value)
    
    return result
```

**Step-by-step for max sum subarray:**
1. Calculate sum of first k elements: O(k)
2. Store as initial max_sum
3. For each remaining element:
   - Remove leftmost element from window (subtract)
   - Add rightmost element to window (add)
   - Update max_sum if window_sum larger
4. Return max_sum

**Why O(n)?**
- Initial calculation: O(k)
- Sliding loop: n - k iterations
- Each iteration: O(1) update
- Total: O(k) + O(n - k) = O(n)

---

### 4️⃣ Visualization: Examples

**Example 1: Maximum Sum Subarray**
```
Array: [1, 3, 2, 6, -1, 4, 1, 8, 2], k=3

Window 0: [1, 3, 2], sum=6, max=6
Window 1: [3, 2, 6], sum=11, max=11
Window 2: [2, 6, -1], sum=7, max=11
Window 3: [6, -1, 4], sum=9, max=11
Window 4: [-1, 4, 1], sum=4, max=11
Window 5: [4, 1, 8], sum=13, max=13
Window 6: [1, 8, 2], sum=11, max=13

Result: max_sum = 13 (window [4, 1, 8])
```

**Example 2: Moving Average**
```
Array: [1, 3, 2, 6, 5], k=3

Window 0: [1, 3, 2], avg=2.0
Window 1: [3, 2, 6], avg=3.67
Window 2: [2, 6, 5], avg=4.33

Moving averages: [2.0, 3.67, 4.33]
```

**Example 3: Find Max in Each Window**
```
Array: [1, 3, -1, -3, 5, 3, 6, 7], k=3

Window 0: [1, 3, -1], max=3
Window 1: [3, -1, -3], max=3
Window 2: [-1, -3, 5], max=5
Window 3: [-3, 5, 3], max=5
Window 4: [5, 3, 6], max=6
Window 5: [3, 6, 7], max=7

Result: [3, 3, 5, 5, 6, 7]
```

---

### 5️⃣ Critical Analysis

**Time Complexity:**
- Setup (first k elements): O(k)
- Sliding loop: O(n - k)
- Per iteration: O(1) update
- Total: O(n)

**Space Complexity:**
- O(1) for sum/max tracking
- O(m) for result array if storing all window values (m = number of windows)

**Comparison to Naive:**

| Approach | Time | Space | Notes |
|----------|------|-------|-------|
| Naive | O(n·k) | O(1) | Recalculate each window |
| Sliding (sum) | O(n) | O(1) | Track running sum |
| Sliding (max) | O(n·k) worst | O(1) | Need deque for O(n) |

**Key Insight:** Fixed size is simpler than variable size. Both are one-pass algorithms.

---

### 6️⃣ Real System Integration

**Moving Average in Finance:**
Stock prices smoothed with 20-day moving average using sliding window.

**Network Monitoring:**
Sliding window of k packets to detect abnormal traffic patterns.

**Streaming Data Processing:**
Real-time calculation of statistics (mean, std dev) over fixed windows.

**Database Index Design:**
Range queries use sliding window concepts internally.

**Cache Eviction:**
LRU cache uses window-like structure to track access patterns.

---

### 7️⃣ Concept Crossovers

**Builds On:**
- Week 1: Big-O analysis
- Week 2: Array operations
- Week 3: Why sorting enables efficiency
- Week 4 Day 1: Two pointers concept

**Enables:**
- Week 4 Day 3: Variable window (extension)
- Week 4 Day 4: Prefix sums (related optimization)
- Week 5: Tree problems with windows
- Week 12: Sliding window variants in hard problems

**Related Techniques:**
- Two pointers (Day 1): both move, different directions
- Sliding window variable (Day 3): both move, same direction
- Prefix sums (Day 4): precompute for O(1) range queries

---

### 8️⃣ Mathematical Perspective

**Mathematical Property:**

For window [i, i+1, ..., i+k-1]:
```
sum[i+1, i+k] = sum[i, i+k-1] - arr[i] + arr[i+k]
```

This is exact, no approximation. We're just reorganizing addition:
```
sum[i, i+k-1] = arr[i] + arr[i+1] + ... + arr[i+k-1]
sum[i+1, i+k] = arr[i+1] + ... + arr[i+k-1] + arr[i+k]
              = sum[i, i+k-1] - arr[i] + arr[i+k]
```

**Proof of Correctness:**
The algorithm finds correct max because:
1. We evaluate every possible window of size k
2. We track the maximum value seen
3. We never miss a window (one-pass guarantee)
4. Therefore we find the true maximum

---

### 9️⃣ Algorithmic Design Intuition

**When to Use Fixed Sliding Window:**
1. Fixed window size k
2. Need some aggregation (sum, max, min, average)
3. Calculate for all windows in array
4. Want O(n) time

**When NOT to Use:**
- Window size varies (use variable window)
- Need individual elements in window (use regular loop)
- k very large relative to n (overhead not worth it)

**Design Decision Framework:**
```
Need to process windows?
  ├─ Fixed size k? → Fixed sliding window (O(n))
  ├─ Variable size? → Variable sliding window (Day 3)
  └─ All subarrays? → Nested loop or DP
```

---

### 🔟 Knowledge Check

1. Why is fixed sliding window O(n) not O(n·k)?
2. Trace max sum subarray on [2, 1, 5, 1, 3, 2] with k=2
3. Can you extend to find index of max window?
4. How would you find minimum instead of maximum?
5. What if you need both min AND max in each window?
6. How does fixed window compare to two pointers?
7. What happens if k > array length?

---

### 1️⃣1️⃣ Retention Hooks

**One-liner:** "Fixed sliding window slides forward, removing left element and adding right element each iteration, maintaining O(1) per slide."

**Mnemonic - "SLIDE FORWARD":**
- **S**lide: window moves forward by one position
- **L**eft: remove element leaving window
- **I**ncrement: move window position forward
- **D**omain: fixed size k throughout
- **E**: add element entering window

**F**orward: direction of movement
- **O**ne: k is fixed throughout
- **R**emove-Add: update pattern
- **W**indow: size k stays constant
- **A**ggregation: track max/min/sum
- **R**ecalculate: O(1) update, not O(k)
- **D**one: one pass through array

**Visual Memory:**
```
Think: "Moving box of size k"
┌──────────────────────────────┐
1  2  3  4  5  6  7  8  9
[1][2][3]    ← window size 3
    [2][3][4]   ← slides right
        [3][4][5]   ← keeps sliding
```

**Story:** "Imagine sliding a rectangular window across a graph. The window stays same size, just moves forward. Calculate once, update with remove/add."

---

## PART 2: QUICK SUMMARY

**Fixed Sliding Window Essence:**

Window of fixed size k slides across array. Each position, remove leftmost and add rightmost for O(1) update.

**When to Use:**
- Fixed window size ✓
- Need aggregation (sum/max/min) ✓
- Want O(n) time ✓
- Calculating for all windows ✓

**Template:**
```python
def sliding_window_fixed(arr, k):
    # Setup: calculate value for first window
    window_value = initial_calc(arr[:k])
    best = window_value
    
    # Slide: move window forward
    for i in range(k, len(arr)):
        # Remove left, add right
        window_value = window_value - arr[i-k] + arr[i]
        best = max(best, window_value)
    
    return best
```

**Real Problems:**
- Max sum subarray of size k
- Moving average over k elements
- Find maximum element in k windows
- Smallest window with sum ≥ target (use variable)

---

## PART 3: SOCRATIC QUESTIONS & ANSWERS

**Q1:** Why is fixed sliding window O(n) instead of O(n·k)?

**A:** Initial setup is O(k). Then slide n-k times, each O(1). Total: O(k) + O(n-k) = O(n). NOT n iterations of k work each (that would be n·k).

---

**Q2:** Trace max sum subarray on [3, 1, 4, 1, 5, 9] with k=2

**A:**
```
Window 0: [3, 1], sum=4, max=4
Window 1: [1, 4], sum=5, max=5
Window 2: [4, 1], sum=5, max=5
Window 3: [1, 5], sum=6, max=6
Window 4: [5, 9], sum=14, max=14
Result: 14
```

---

**Q3:** Can you find the INDEX of max window, not just the value?

**A:**
```python
def max_sum_window_index(arr, k):
    window_sum = sum(arr[:k])
    max_sum = window_sum
    max_index = 0
    
    for i in range(k, len(arr)):
        window_sum = window_sum - arr[i-k] + arr[i]
        if window_sum > max_sum:
            max_sum = window_sum
            max_index = i - k + 1  # Start of this window
    
    return max_index, max_sum
```

---

**Q4:** How to find MINIMUM instead of maximum in each window?

**A:** Same algorithm, just compare with min instead of max:
```python
min_in_window = window_sum
# ...
for i in range(k, len(arr)):
    window_sum = window_sum - arr[i-k] + arr[i]
    min_in_window = min(min_in_window, window_sum)
```

---

**Q5:** What if you need both min AND max in each window?

**A:** Track both separately:
```python
for i in range(k, len(arr)):
    window_sum = window_sum - arr[i-k] + arr[i]
    max_sum = max(max_sum, window_sum)
    min_sum = min(min_sum, window_sum)
```
Still O(n), just two variables instead of one.

---

**Q6:** How does fixed window compare to two pointers from Day 1?

**A:**
- Fixed window: both pointers move RIGHT, maintaining distance k
- Two pointers: move from OPPOSITE ends, distance shrinks
- Fixed window: multiple passes (one for each window)
- Two pointers: single pass finding one pair

---

**Q7:** What happens if k > array length?

**A:** No valid windows exist. Handle edge case:
```python
if k > len(arr):
    return None  # or handle appropriately
```

---

## PART 4: README

**90-Minute Study Guide:**
1. The Why (10 min): Understand problem
2. The What (15 min): Mental model clicks
3. The How (15 min): Mechanics and algorithm
4. Visualization (20 min): Trace examples
5. Quick Summary (5 min): Key points
6. Questions (15 min): Test understanding

**Key Skill:** Recognize fixed window opportunities, implement efficiently

**Practice:** Max sum subarray, moving average, find max in windows

**Connection:** Day 1 was two pointers (opposite ends). Day 2 is sliding window (same direction, fixed size). Day 3 extends to variable size.

---

**Status:** ✅ Day 2 Complete | **Next:** Day 3 - Sliding Window (Variable)

