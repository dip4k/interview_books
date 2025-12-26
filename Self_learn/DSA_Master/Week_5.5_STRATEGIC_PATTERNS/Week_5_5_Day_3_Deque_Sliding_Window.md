# Week 5.5, Day 3: Deque Operations & Sliding Window

**Week:** 5.5 | **Day:** 3 | **Topic:** Deque for Optimal Sliding Window  
**Time:** 80 minutes reading | **Difficulty:** 🔴 Hard  
**Prerequisites:** Week 5, Week 5.5 Days 1-2  

---

## 1️⃣ THE WHY — Engineering Motivation

### The Problem We Solve

**Scenario:** Find maximum/minimum in every sliding window efficiently.

**Naive approach:**
```python
# Window size k, slide across array
for i in range(len(arr) - k + 1):
    window = arr[i:i+k]
    result.append(max(window))  # O(k) per window
# Total: O(n × k)
```

**Better approach (Deque):**
```python
# Deque stores indices of potential maximums
from collections import deque

dq = deque()
for i in range(len(arr)):
    # Remove indices outside window
    if dq and dq[0] < i - k + 1:
        dq.popleft()
    
    # Remove smaller elements (monotonic)
    while dq and arr[dq[-1]] < arr[i]:
        dq.pop()
    
    dq.append(i)
    
    if i >= k - 1:
        result.append(arr[dq[0]])  # Max is at front
# Total: O(n) amortized
```

### Why This Matters

- **Sliding window maximum:** 5-10% of interview problems
- **Optimization:** O(n log n) with heap → O(n) with deque
- **Practical:** Real-time streaming data, market analysis

**Why This Matters:** Deque optimization appears in 5-10% of advanced array problems.

---

## 2️⃣ THE WHAT — Mental Model & Intuition

### Core Concept: Monotonic Deque

```
Goal: Maintain potential max/min candidates
Key: Only keep indices we might need later

For max problem:
- Deque stores indices in DECREASING order of values
- Front index always points to max in window
```

### Why It Works

```
Example: [1, 3, 1, 2, 0, 5], window size 3

Iteration by iteration:

i=0 (arr=1):
  dq: [0]
  (window not full)

i=1 (arr=3):
  3 > 1, remove 0
  dq: [1]

i=2 (arr=1):
  1 < 3, keep 1
  dq: [1, 2]
  max in window [1,3,1]: 3 ✓

i=3 (arr=2):
  2 > 1, remove 2
  2 < 3, keep 1
  dq: [1, 3]
  max in window [3,1,2]: 3 ✓

i=4 (arr=0):
  0 < 2, keep 3
  0 < 3, keep 1
  dq: [1, 3, 4]
  max in window [1,2,0]: 2 ✓

i=5 (arr=5):
  5 > 0, remove 4
  5 > 2, remove 3
  5 > 3, remove 1
  dq: [5]
  max in window [2,0,5]: 5 ✓

Result: [3, 3, 2, 5]
```

### The Key Insight

```
We don't need all elements in window.
We only need indices that COULD be future max.

When we see larger element, all smaller elements
to its left are useless (will never be max).

Remove them! Keep only candidates.
```

---

## 3️⃣ THE HOW — Mechanical Walkthrough

### Sliding Window Maximum

```python
from collections import deque

def sliding_window_maximum(arr, k):
    if not arr or k == 0:
        return []
    
    dq = deque()  # Store indices
    result = []
    
    for i in range(len(arr)):
        # Remove indices outside current window
        while dq and dq[0] < i - k + 1:
            dq.popleft()
        
        # Remove indices of smaller elements
        # (they can never be max while this larger exists)
        while dq and arr[dq[-1]] < arr[i]:
            dq.pop()
        
        # Add current index
        dq.append(i)
        
        # When window is full, add max to result
        if i >= k - 1:
            result.append(arr[dq[0]])
    
    return result

# [1,3,1,2,0,5], k=3 → [3,3,2,5]
```

### Sliding Window Minimum

```python
def sliding_window_minimum(arr, k):
    dq = deque()
    result = []
    
    for i in range(len(arr)):
        # Remove outside window
        while dq and dq[0] < i - k + 1:
            dq.popleft()
        
        # Remove larger elements (for min, we keep increasing)
        while dq and arr[dq[-1]] > arr[i]:  # CHANGE: > instead of <
            dq.pop()
        
        dq.append(i)
        
        if i >= k - 1:
            result.append(arr[dq[0]])  # Min is at front
    
    return result
```

---

## 4️⃣ VISUALIZATION — Traced Examples

### Example 1: Detailed Trace

```
Array: [1, 3, 1, 2, 0, 5]
Window: 3

Initial state:
  dq: empty
  result: empty

i=0, arr[0]=1, window not ready:
  Append 0 to dq
  dq: [0]

i=1, arr[1]=3, window not ready:
  3 > arr[0]=1, remove 0
  Append 1
  dq: [1]

i=2, arr[2]=1, window ready:
  Window: [1,3,1], dq[0]=1 (inside)
  1 < arr[1]=3, keep 1
  Append 2
  dq: [1, 2]
  result: [3]  (arr[dq[0]]=arr[1]=3)

i=3, arr[3]=2, window ready:
  Window: [3,1,2], dq[0]=1 (inside)
  2 > arr[2]=1, remove 2
  2 < arr[1]=3, keep 1
  Append 3
  dq: [1, 3]
  result: [3, 3]

i=4, arr[4]=0, window ready:
  Window: [1,2,0], dq[0]=1 (outside!)
  Remove dq[0]=1
  dq: [3]
  0 < arr[3]=2, keep 3
  Append 4
  dq: [3, 4]
  result: [3, 3, 2]

i=5, arr[5]=5, window ready:
  Window: [2,0,5], dq[0]=3 (inside)
  5 > arr[4]=0, remove 4
  5 > arr[3]=2, remove 3
  dq: []
  Append 5
  dq: [5]
  result: [3, 3, 2, 5]

Final: [3, 3, 2, 5]
```

---

## 5️⃣ CRITICAL ANALYSIS — Performance & Robustness

### Complexity Analysis

| Approach | Time | Space | Why |
|----------|------|-------|-----|
| **Naive (per window max)** | O(n×k) | O(1) | k operations per window |
| **Heap (binary search)** | O(n log n) | O(k) | log n per insertion |
| **Deque (monotonic)** | O(n) | O(k) | Each element in/out once |

### Why O(n)?

```
Each element:
- Enters deque once: O(1)
- Leaves deque once: O(1)

Total operations: 2n = O(n)
(Not O(n×k) because removals distributed)
```

### Edge Cases

**Small window:**
```python
# k=1: Every element is max of its window
# Deque always has 1 element
```

**Larger elements at end:**
```python
# [1,2,3,4,5] with k=3
# Each window max: [3,4,5]
# Deque: [2], [3], [4], [5]
# Multiple removals, but still O(n) total
```

---

## 6️⃣ REAL SYSTEM INTEGRATION — Production Applications

### Streaming Data Analysis

```
Real-time stock prices:
  Find max in last k minutes
  Deque tracks potential maximums
  O(1) access to current max
  
Without deque: O(k) per query
With deque: O(1) per query
```

### Network Traffic Analysis

```
Sliding window over time:
  Max requests per second in last minute
  Min latency in last 10 seconds
  
Deque-based approach optimal
```

### Database Aggregation

```
Time-windowed aggregates:
  SELECT MAX(value) 
  FROM metrics 
  WHERE timestamp >= now - 1hour
  
Deque-based window handling
```

---

## 7️⃣ CONCEPT CROSSOVERS — Connections

### Week 2: Deque Data Structure Returns

```
Week 2: Learned deque (double-ended queue)
Week 5.5 Day 3: Deque application
  
Deque = efficient implementation for this pattern
```

### Sliding Window Technique

```
Week 4: Two-pointer sliding window
Week 5.5 Day 3: Deque-enhanced sliding window

Same principle, different data structure
For max/min queries: deque wins
```

### Monotonic Structure

```
Deque maintains monotonic order
Same idea as monotonic stacks (Week 6)
Different data structure, similar principle
```

---

## 8️⃣ MATHEMATICAL & THEORETICAL — Formal Foundations

### Monotonic Invariant

**Invariant:** Deque maintains indices in decreasing order of their values.

**Maintenance:**
- Remove right if arr[last] < arr[current]
- This preserves decreasing order
- Ensures dq[0] is always maximum ✓

### Why Remove Smaller

**Claim:** If arr[i] < arr[j] and i < j, we never need arr[i] as max.

**Proof:**
```
When arr[i] is in the window, arr[j] is also in window
(since j > i and both in same window).

max(window) = max(arr[i], arr[j], others) = max(arr[j], others)
(since arr[j] >= arr[i])

So arr[i] never contributes to max after arr[j] enters.
Therefore safe to remove arr[i].
```

---

## 9️⃣ ALGORITHMIC DESIGN INTUITION — Why Design Works

### Why Deque, Not Heap?

```
Heap:
  Insert: O(log n)
  Remove arbitrary: O(log n) (need to find it)
  Total: O(n log n)

Deque:
  Insert/remove: O(1)
  Total: O(n)

Deque better because:
1. We remove by position (always oldest), not by value
2. Monotonic property ensures dq[0] is max
3. No searching needed
```

### Why Monotonic?

```
Monotonic deque allows us to:
1. Keep only useful candidates
2. Instantly know max is at front
3. Remove candidates in order

Without monotonic: would need to search for max in deque
With monotonic: max guaranteed at dq[0]
```

---

## 🔟 KNOWLEDGE CHECK — Socratic Reasoning

1. **Why do we remove indices smaller than i-k+1?** What does it mean for an index to be outside the window?

2. **Why remove elements from back (arr[dq[-1]] < arr[i])?** What does it mean for them to be "useless"?

3. **Could we use regular queue instead of deque?** Why or why not?

4. **For minimum instead of maximum, what changes?** Why only one comparison changes?

5. **How is this different from heap-based solution?** What's the key advantage of deque?

---

## 1️⃣1️⃣ RETENTION HOOK — Memory Anchors

### **Monotonic Deque**
```
Indices in DECREASING order of values
Front = maximum of current window
O(n) total, not O(n log n)
```

### **Two Removal Steps**
```
1. Remove old (outside window): popleft
2. Remove small (useless): pop from back
3. Add current: append
```

### **Why Deque Beats Heap**
```
Deque: O(n)
Heap: O(n log n)
Key: Monotonic lets us avoid searching
```

---

## 📊 SUPPLEMENTARY: Implementation Template

```python
from collections import deque

def sliding_window_maximum(arr, k):
    dq = deque()
    result = []
    
    for i in range(len(arr)):
        # Step 1: Remove outside window
        if dq and dq[0] < i - k + 1:
            dq.popleft()
        
        # Step 2: Remove smaller elements (monotonic property)
        while dq and arr[dq[-1]] < arr[i]:
            dq.pop()
        
        # Step 3: Add current
        dq.append(i)
        
        # Step 4: Record max when window full
        if i >= k - 1:
            result.append(arr[dq[0]])
    
    return result
```

---

## 🔗 EXTERNAL RESOURCES

**LeetCode Problems:**
- Sliding Window Maximum (LeetCode 239)
- Sliding Window Median (LeetCode 295)
- Jump Game VI (LeetCode 1696)

---

## 📝 KEY TAKEAWAYS

✅ **Deque maintains monotonic order for O(n) efficiency**  
✅ **Front of deque always = maximum of window**  
✅ **Remove outside indices and dominated candidates**  
✅ **O(n) time vs O(n log n) heap approach**  
✅ **Perfect for streaming/real-time data**

**Next:** Days 4-5 (Integration & Advanced Patterns)

