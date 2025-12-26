# Week 5.5, Day 1: Difference Array Technique

**Week:** 5.5 | **Day:** 1 | **Topic:** Difference Array (Range Updates)  
**Time:** 75 minutes reading | **Difficulty:** 🔴 Hard  
**Prerequisites:** Week 5 (Arrays comfortable)  

---

## 1️⃣ THE WHY — Engineering Motivation

### The Problem We Solve

**Scenario:** Update ranges in an array repeatedly, then query final values.

**Naive approach:**
```
Update range [2,5]: add 10 to indices 2,3,4,5
Update range [1,3]: add 5 to indices 1,2,3
Update range [4,6]: add 3 to indices 4,5,6

Each update: O(k) where k = range length
m updates: O(m × k)
```

**Better approach (Difference Array):**
```
Same operations in O(m + n) total!
O(1) per update, O(n) final computation
```

### Real Interview Problems

- **Hotel Bookings:** n hotels, m bookings, find if any hotel double-booked (LeetCode 1109)
- **Range Addition:** m range additions, return final array (LeetCode 370)
- **Range Update Queries:** millions of updates, single query at end

**Why This Matters:** Difference arrays appear in 10-15% of array/range update interviews.

---

## 2️⃣ THE WHAT — Mental Model & Intuition

### Core Concept: Inverse of Prefix Sum

**Prefix Sum:** Cumulative totals from left  
**Difference Array:** Inverse operation

```
Original array:     [3, 5, 2, 8, 9]

Prefix sum:         [3, 8, 10, 18, 27]
(Each element = cumulative)

Difference array:   [3, 2, -3, 6, 1]
(Differences between consecutive elements)

Why inverse? 
  Original[i] = Difference[0] + Difference[1] + ... + Difference[i]
  (Same as prefix sum reconstruction!)
```

### How It Optimizes Range Updates

```
Update range [1,3] with +5:

❌ Naive:
for i in range(1, 4):
    arr[i] += 5
O(k) per update

✅ Difference Array:
diff[1] += 5      # Mark range start
diff[4] -= 5      # Mark range end (one past)
O(1) per update!

At end: reconstruct from difference array O(n)
```

### Visual Example

```
Original:  [0, 0, 0, 0, 0]

Update [1,3] with +5:
Diff:      [0, 5, 0, 0, -5, 0]
           mark  mark end

Update [0,2] with +3:
Diff:      [3, 5, 0, -3, -5, 0]

Reconstruct (prefix sum on diff):
           [3, 8, 8, 5, 0, 0]
           ↓  ↓  ↓  ↓
Final:     [3, 8, 8, 5, 0]
```

---

## 3️⃣ THE HOW — Mechanical Walkthrough

### Implementation Pattern

```python
class RangeUpdater:
    def __init__(self, n):
        self.diff = [0] * (n + 1)  # Extra slot for boundaries
    
    def update_range(self, left, right, val):
        """Update [left, right] (inclusive) by val"""
        self.diff[left] += val
        self.diff[right + 1] -= val
    
    def get_final_array(self):
        """Reconstruct actual array from diff"""
        result = []
        current = 0
        for i in range(len(self.diff) - 1):  # Exclude boundary
            current += self.diff[i]
            result.append(current)
        return result

# Usage
updater = RangeUpdater(5)
updater.update_range(1, 3, 5)   # O(1)
updater.update_range(0, 2, 3)   # O(1)
final = updater.get_final_array()  # O(n)
# Result: [3, 8, 8, 5, 0]
```

### Step-by-Step Trace

```
Array size: 5, indices 0-4
Diff array size: 6 (with boundary)

Initial diff: [0, 0, 0, 0, 0, 0]

Update [1,3] += 5:
  diff[1] += 5  → [0, 5, 0, 0, 0, 0]
  diff[4] -= 5  → [0, 5, 0, 0, -5, 0]

Update [0,2] += 3:
  diff[0] += 3  → [3, 5, 0, 0, -5, 0]
  diff[3] -= 3  → [3, 5, 0, -3, -5, 0]

Reconstruct:
  Prefix sum of diff array:
  i=0: curr = 0 + 3 = 3     → result[0] = 3
  i=1: curr = 3 + 5 = 8     → result[1] = 8
  i=2: curr = 8 + 0 = 8     → result[2] = 8
  i=3: curr = 8 + (-3) = 5  → result[3] = 5
  i=4: curr = 5 + (-5) = 0  → result[4] = 0

Final: [3, 8, 8, 5, 0]
```

---

## 4️⃣ VISUALIZATION — Traced Examples

### Example 1: Hotel Bookings

```
3 hotels, bookings: [1,2], [2,3], [2,3]

Create diff array:
Initial: [0, 0, 0, 0]

Booking [1,2]:
  diff[1] += 1, diff[3] -= 1
  diff: [0, 1, 0, -1]

Booking [2,3]:
  diff[2] += 1, diff[4] -= 1
  diff: [0, 1, 1, -1, -1]
  (boundary extended)

Booking [2,3]:
  diff[2] += 1, diff[4] -= 1
  diff: [0, 1, 2, -1, -2]

Reconstruct:
  Hotel 0: 0 (no bookings)
  Hotel 1: 1 (one booking)
  Hotel 2: 1 + 2 = 3 (three bookings)
  Hotel 3: 3 - 1 = 2 (decline after booking ends)

Answer: Hotel 2 has 3 bookings? Check limit.
```

### Example 2: Range Addition

```
Array: [0, 0, 0, 0, 0, 0]
Operations: [[2,4,3], [5,6,10], [2,3,2]]

Update [2,4] += 3:
  diff: [0, 0, 3, 0, 0, -3, 0]

Update [5,6] += 10:
  diff: [0, 0, 3, 0, 0, -3+10, -10, 0]
  diff: [0, 0, 3, 0, 0, 7, -10, 0]

Update [2,3] += 2:
  diff: [0, 0, 3+2, 0, -2, 7, -10, 0]
  diff: [0, 0, 5, 0, -2, 7, -10, 0]

Reconstruct (prefix sum):
  [0, 0+5, 5+0, 5-2, 3+7, 10-10, 0]
  [0, 5, 5, 3, 10, 0]
```

---

## 5️⃣ CRITICAL ANALYSIS — Performance & Robustness

### Complexity Analysis

| Operation | Time | Space | Why |
|-----------|------|-------|-----|
| **Update range** | O(1) | O(1) | Just 2 assignments |
| **Get final** | O(n) | O(n) | Prefix sum reconstruction |
| **Total (m updates, n size)** | O(m+n) | O(n) | Best possible for this problem |

### Comparison with Naive

```
Naive approach (update each element):
  m updates × k average length = O(m×k)
  Worst: O(m×n) if all updates cover entire array

Difference array:
  m updates × O(1) = O(m)
  1 reconstruction × O(n) = O(n)
  Total: O(m+n) ✓ Much better!

Example: 1 million updates, 10,000 element array
  Naive: ~10 billion operations
  Diff: ~10 million operations (1000x faster!)
```

### Edge Cases

**Boundary handling:**
```python
# Need diff size = n+1 to avoid index out of bounds
self.diff = [0] * (n + 1)
self.diff[right + 1] -= val  # Safe because size is n+1
```

**Overlapping ranges:**
```
Ranges can overlap, difference array handles naturally
[1,3] += 5
[2,4] += 3

diff[1] += 5, diff[4] -= 5
diff[2] += 3, diff[5] -= 3

Overlapping region (2,3) gets both: 5+3=8 ✓
```

---

## 6️⃣ REAL SYSTEM INTEGRATION — Production Applications

### Database Range Updates

```
Update all prices in region A by +10%
Update all salaries for department B by +1000

Difference array pattern:
  Mark start of range
  Mark end of range
  Process batch efficiently
```

### Shift Operators

```
Array operations: shift elements in range
  Shift [2,5] left by 2 positions
  
Traditional: Move each element (O(k) per operation)
Difference array: Mark with shift amounts, reconstruct once
```

### Event Processing

```
Events: start_time, end_time, value

Line sweep algorithm:
  1. Create diff array
  2. Mark events with difference array
  3. Sweep once, maintaining current value
  
Used in: calendar apps, room booking, traffic analysis
```

---

## 7️⃣ CONCEPT CROSSOVERS — Connections

### Week 4: Prefix Sum Returns

```
Prefix Sum: cumulative left-to-right
Difference Array: inverse of prefix sum

If diff array = [a, b, c, d]
Prefix sum of diff = [a, a+b, a+b+c, a+b+c+d]

This IS the original array!
One direction: array → diff (subtraction)
Other direction: diff → array (prefix sum)
```

### Week 2: Arrays Fundamentals

```
Array modification in place
Range queries
Batch operations

All rely on understanding index manipulation
```

### Sliding Window Connection

```
Difference array helps with:
- Range-based problems
- Batch updates
- O(1) update time

Next: Deque for sliding window max/min
```

---

## 8️⃣ MATHEMATICAL & THEORETICAL — Formal Foundations

### Proof: Difference Array Reconstruction

**Theorem:** If diff[i] = arr[i] - arr[i-1], then arr[i] = sum(diff[0..i])

**Proof:**
```
diff[0] = arr[0]
diff[1] = arr[1] - arr[0]
diff[2] = arr[2] - arr[1]
...
diff[i] = arr[i] - arr[i-1]

Sum: diff[0] + diff[1] + ... + diff[i]
   = arr[0] + (arr[1]-arr[0]) + (arr[2]-arr[1]) + ... + (arr[i]-arr[i-1])
   = arr[i]  (telescoping sum)
✓ Proven ∎
```

### Range Update Invariant

**Claim:** Adding v to diff[L] and -v to diff[R+1] adds v to arr[L..R]

**Proof:**
```
When we reconstruct arr, we compute prefix sums of diff.
At index L: sum includes the +v from diff[L]
At indices L+1 to R: sum includes the +v (accumulated from L)
At index R+1: sum includes -v, canceling the +v
So arr[L..R] all increase by v, arr[R+1..] unchanged ✓
```

---

## 9️⃣ ALGORITHMIC DESIGN INTUITION — Why Design Works

### Why O(1) Update Works

```
Without marking endpoints, we'd need to update every element.
By marking start (+v) and end (-v), the reconstruction 
process (prefix sum) handles the "spreading" of the value.

Key insight: Defer computation, batch process
```

### Why Reconstruction Works

```
Prefix sum of difference array recovers original values
because differences collapse in telescoping sum.

This is the mathematical foundation of the technique.
```

---

## 🔟 KNOWLEDGE CHECK — Socratic Reasoning

1. **Why add val to diff[left] and subtract from diff[right+1]?** What happens during reconstruction?

2. **Can overlapping updates interfere with each other?** Test with 2 ranges: [1,3] and [2,4].

3. **Why must diff array size be n+1, not n?** What breaks if we use n?

4. **How does this compare to segment trees for range updates?** Which is simpler? When use each?

5. **Can you use difference array for multiplicative updates (e.g., *2)?** Why or why not?

---

## 1️⃣1️⃣ RETENTION HOOK — Memory Anchors

### **Mark Start & End**
```
+val at left
-val at right+1
Reconstruction handles the rest
```

### **Defer, Then Process**
```
All updates: O(1) each
Reconstruction: O(n) once
Total: O(m+n)
```

### **Difference = Inverse**
```
Diff[i] = Arr[i] - Arr[i-1]
Arr[i] = sum(Diff[0..i])
```

---

## 📊 SUPPLEMENTARY: Implementation Checklist

```python
# Key points to remember:
✓ diff array size = n + 1 (boundary)
✓ diff[right + 1] -= val (not diff[right])
✓ Reconstruct with prefix sum
✓ Time: O(m+n) for m updates, n elements
✓ Space: O(n) for diff array
```

---

## 🔗 EXTERNAL RESOURCES

**LeetCode Problems:**
- Range Addition (LeetCode 370)
- Hotel Bookings II (LeetCode 1109)
- Shift Queries (multiple variations)

**Visualization:**
- Prefix sum vs difference: https://cp-algorithms.com/data_structures/sparse_table.html

---

## 📝 KEY TAKEAWAYS

✅ **Difference array optimizes range updates to O(1) each**  
✅ **Reconstruction via prefix sum O(n)**  
✅ **Total complexity O(m+n) vs O(m×k) naive**  
✅ **Works for any range-based batch updates**  
✅ **Interview staple for optimization**

**Next:** Day 2 — In-Place Replacement (space optimization)

