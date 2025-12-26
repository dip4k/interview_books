# Week 5.5, Day 4: Advanced Pattern Combinations

**Week:** 5.5 | **Day:** 4 | **Topic:** Combining Techniques for Complex Problems  
**Time:** 90 minutes reading | **Difficulty:** 🔴🔴 Very Hard  
**Prerequisites:** Week 5.5 Days 1-3  

---

## 1️⃣ THE WHY — Engineering Motivation

### Multi-Technique Problems

**Scenario:** Real interview problems combine multiple techniques.

**Example Problem:** Range Updates + Query for Maximum in Ranges

```python
# Not just updates, but also: what's max after all updates?
# Requires: Difference Array (updates) + Deque (querying)
```

**Why This Matters:** Advanced interviews (Google, Meta) combine 2-3 techniques. 15-20% of hard problems.

---

## 2️⃣ THE WHAT — Combined Approaches

### Combination 1: Difference Array + Range Max Query

```
Problem: n range updates, then k range max queries

Naive:
  - Update array O(n) per update
  - Query max O(k) per query
  - Total: O(n×updates + k×queries)

Smart:
  - Use difference array for updates: O(1) each
  - Reconstruct once: O(n)
  - Use segment tree for queries: O(log n) each
  - Total: O(m + n + k log n)

For large m, k: massive savings!
```

### Combination 2: In-Place + Difference Array

```
Problem: Remove elements AND update ranges

Example:
  Array: [1,2,3,2,4]
  Remove all 2s
  Update remaining: [1,_,3,_,4]
  Then apply range update [0,2] += 10
  Result: [11,_,13,_,4]

Approach:
  1. In-place removal: O(n)
  2. Map to new positions
  3. Apply difference array: O(1) per update
  4. Reconstruct: O(n)
```

### Combination 3: Deque + In-Place

```
Problem: Sliding window max on filtered array

Example:
  Array: [1,2,3,4,5]
  Filter: keep if value > 2
  Filtered: [3,4,5]
  Window max (size 2): [4,5]

Approach:
  1. In-place filtering (or mark indices)
  2. Apply deque on filtered indices
  3. Record results
```

---

## 3️⃣ THE HOW — Implementation Patterns

### Pattern 1: Difference Array + Reconstruction + Query

```python
def range_update_then_query(arr, updates, queries):
    n = len(arr)
    diff = [0] * (n + 1)
    
    # Step 1: Apply all updates in O(m)
    for left, right, val in updates:
        diff[left] += val
        diff[right + 1] -= val
    
    # Step 2: Reconstruct array in O(n)
    current = 0
    for i in range(n):
        current += diff[i]
        arr[i] += current  # Add accumulated change
    
    # Step 3: Answer queries (simple array lookup now)
    results = []
    for left, right in queries:
        max_val = max(arr[left:right+1])
        results.append(max_val)
    
    return results
```

### Pattern 2: In-Place Filter + Deque Window

```python
def filter_then_sliding_window(arr, k, condition):
    # Step 1: Filter in-place
    j = 0
    for i in range(len(arr)):
        if condition(arr[i]):
            arr[j] = arr[i]
            j += 1
    
    filtered_len = j
    filtered_arr = arr[:filtered_len]
    
    # Step 2: Apply deque sliding window max
    from collections import deque
    dq = deque()
    result = []
    
    for i in range(len(filtered_arr)):
        if dq and dq[0] < i - k + 1:
            dq.popleft()
        
        while dq and filtered_arr[dq[-1]] < filtered_arr[i]:
            dq.pop()
        
        dq.append(i)
        
        if i >= k - 1:
            result.append(filtered_arr[dq[0]])
    
    return result
```

---

## 4️⃣ VISUALIZATION — Complex Example

### Problem: Hotel with Cancellations & Peak Period

```
Problem:
  n=5 hotels
  Bookings: [1,3], [2,4], [3,5]
  Cancellations: [1,2]
  Find: current occupancy, max occupancy in range [1,4]

Solution:

Step 1: Difference array for bookings
  diff: [0, 1, 1, 0, -1, -1, 0]

Step 2: Difference array for cancellations
  diff: [0, -1, -1, 0, -1, -1, 0]

Step 3: Combine (add both)
  diff: [0, 0, 0, 0, -2, -2, 0]

Step 4: Reconstruct
  Hotel 0: 0 occupancy
  Hotel 1: 0 occupancy
  Hotel 2: 0 occupancy
  Hotel 3: -2 occupancy??? 

Wait, we need to track bookings separately!

Correct approach:
  diff_book: [0, 1, 1, 0, -1, -1, 0]
  Reconstruct bookings first: [0, 1, 2, 2, 1, 0]
  
  diff_cancel: [0, -1, -1, 0, 0, 0, 0]
  Reconstruct: [0, -1, -2, -2, -2, -2]
  
  Final: [0, 0, 0, 0, -1, -2]
  
  Query max in [1,4]: max(0,0,0,-1) = 0
```

---

## 5️⃣ CRITICAL ANALYSIS — When to Combine

### Decision Tree

```
Problem has:
├─ Range updates?
│  └─ Yes → Use difference array
├─ Sliding window queries?
│  └─ Max/min? → Use deque
│  └─ Sum/average? → Use prefix sum
├─ In-place space constraint?
│  └─ Yes → Use two-pointer in-place
└─ Multiple conditions?
   └─ Chain techniques together
```

---

## 6️⃣ REAL SYSTEM INTEGRATION

### Database Optimization

```
Scenario: Hotel booking system
  - Millions of bookings (range updates)
  - Check if room double-booked (range query)
  - Mark cancellations (remove/update)
  - Peak analysis (sliding window)

Solution: Combine all three techniques!
```

---

## 7️⃣ KNOWLEDGE CHECK

1. **When would you use combination vs individual techniques?** What's the trade-off?

2. **How do you handle conflicts?** (e.g., both update and query on same range)

3. **What's the failure mode?** What happens if you forget one technique?

---

## 📝 KEY TAKEAWAYS

✅ **Combine techniques for complex problems**  
✅ **Order matters: updates before queries usually**  
✅ **Each technique handles one aspect optimally**  
✅ **Practice recognizing pattern combinations**

**Next:** Day 5 — Week Integration & Mastery

