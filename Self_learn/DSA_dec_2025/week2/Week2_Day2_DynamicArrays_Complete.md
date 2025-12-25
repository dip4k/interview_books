# 🧠 DSA Deep-Dive: Week 2, Day 2
## Dynamic Arrays: Amortized Analysis and Geometric Resizing Logic

---

## 1. The "Why" (Engineering Motivation)

You're implementing a log collection system for a massive web application. Logs come in at 10,000 per second.

**Three implementation options:**

**Option A: Fixed-size array**
```python
logs = [None] * 100_000  # Pre-allocated

for log in incoming_logs:
    logs[index] = log
    index += 1
    if index >= len(logs):
        # CATASTROPHIC! Lost all new logs!
        break
```

**Problem:** Fixed size fails when data exceeds capacity.

**Option B: Allocate more space as needed**
```python
logs = []
for log in incoming_logs:
    logs.append(log)
```

**But wait... append is O(n)?**

If we add 10,000 logs/second, and each append copies all previous elements, we'd do:
- Append 1: 1 copy
- Append 2: 2 copies
- ...
- Append 1,000,000: 1,000,000 copies

**Total copies:** 1 + 2 + 3 + ... + 1,000,000 = 500 billion copies!

**That's way slower than it should be.**

**Option C: Geometric resizing**
```python
logs = []
capacity = 10
for log in incoming_logs:
    if len(logs) == capacity:
        capacity *= 2  # Double capacity
        reallocate(logs, new_capacity)
    logs.append(log)
```

**Result:** Efficient growth with minimal reallocation.

**The question:** How much does doubling actually help? Is it really O(1) amortized? What about 1.5x growth vs. 2x growth?

**The insight:** Dynamic arrays are everywhere (Python lists, JavaScript arrays, Java ArrayLists, C++ vectors), but most people don't understand WHY they're so efficient. Understanding amortized analysis changes how you think about performance.

---

## 2. The Mental Model (The "What")

Imagine a **parking lot that grows as needed**.

**Static array:**
```
Parking lot (capacity 5):
┌─────┬─────┬─────┬─────┬─────┐
│  1  │  2  │  3  │  4  │  5  │
└─────┴─────┴─────┴─────┴─────┘

6th car arrives: NOWHERE TO PARK! Crash!
```

**Dynamic array with doubling:**
```
Initial: Capacity 2
┌─────┬─────┐
│  1  │  2  │
└─────┴─────┘

3rd car arrives: FULL!
  Build new lot (capacity 4)
  Move cars: 1, 2 → new lot
  Add car 3
  
┌─────┬─────┬─────┬─────┐
│  1  │  2  │  3  │  ?  │
└─────┴─────┴─────┴─────┘

4th car: Fits!
┌─────┬─────┬─────┬─────┐
│  1  │  2  │  3  │  4  │
└─────┴─────┴─────┴─────┘

5th car: FULL again!
  Build new lot (capacity 8)
  Move cars: 1, 2, 3, 4 → new lot
  Add car 5
  
┌─────┬─────┬─────┬─────┬─────┬─────┬─────┬─────┐
│  1  │  2  │  3  │  4  │  5  │  ?  │  ?  │  ?  │
└─────┴─────┴─────┴─────┴─────┴─────┴─────┴─────┘

Continue...
```

**The key insight:**
- Each car moves fewer and fewer times
- Car 1: Moves 3 times (sizes 2 → 4, 4 → 8, 8 → 16)
- Car 100: Moves maybe 1 time total (added late)
- Car 1,000,000: Never moves (we stop resizing)

---

## 3. Under the Hood (The "How")

### 3.1 Geometric Resizing Mechanics

**When capacity is exceeded:**

```python
# Current state
size = 8      # Elements currently stored
capacity = 8  # Space allocated

# 9th element arrives
append(9):
    if size == capacity:
        old_capacity = capacity           # 8
        new_capacity = capacity * 2       # 16
        
        # Step 1: Allocate new memory
        new_array = allocate(16 bytes * element_size)
        
        # Step 2: Copy all old elements
        for i in range(size):
            new_array[i] = array[i]   # Copy 8 elements
        
        # Step 3: Deallocate old memory
        deallocate(array)
        
        # Step 4: Update pointer
        array = new_array
        capacity = new_capacity
    
    # Now add the new element
    array[size] = 9
    size += 1
```

**Memory layout before and after:**

```
Before resize:
Old array (8 slots):
┌─────┬─────┬─────┬─────┬─────┬─────┬─────┬─────┐
│  1  │  2  │  3  │  4  │  5  │  6  │  7  │  8  │ (address: 0x1000)
└─────┴─────┴─────┴─────┴─────┴─────┴─────┴─────┘
size = 8, capacity = 8

Append 9 (capacity exceeded!):
1. Allocate new memory (16 slots)
┌──────────────────────────────────────────────────────────┐
│ New array (16 slots) - address: 0x2000                   │
└──────────────────────────────────────────────────────────┘

2. Copy all 8 old elements
┌──────┬──────┬──────┬──────┬──────┬──────┬──────┬──────┬─────┬─────┬─────┐
│  1   │  2   │  3   │  4   │  5   │  6   │  7   │  8   │  ?  │  ?  │  ?  │
└──────┴──────┴──────┴──────┴──────┴──────┴──────┴──────┴─────┴─────┴─────┘

3. Add new element
┌──────┬──────┬──────┬──────┬──────┬──────┬──────┬──────┬──────┬─────┬─────┐
│  1   │  2   │  3   │  4   │  5   │  6   │  7   │  8   │  9   │  ?  │  ?  │
└──────┴──────┴──────┴──────┴──────┴──────┴──────┴──────┴──────┴─────┴─────┘
size = 9, capacity = 16

4. Deallocate old memory at 0x1000
```

### 3.2 Amortized Analysis: Why It's O(1)

**The question:** If we resize multiple times, what's the total cost?

**Naive analysis (WRONG):**
```
Append 1: O(1)
Append 2: O(1)
...
Append 1000000: O(1) at each step

But some appends trigger resize, costing O(n)!
Those resizes are O(n), making total O(n log n)?
```

**Correct analysis (amortized):**

Let's track total work over n appends:

```
Append 1 (size=1):  No resize, work = 1
Append 2 (size=2):  RESIZE (copy 1 element), work = 1 + 1 = 2
Append 3 (size=3):  No resize, work = 1
Append 4 (size=4):  RESIZE (copy 3 elements), work = 1 + 3 = 4
Append 5 (size=5):  No resize, work = 1
Append 6 (size=6):  No resize, work = 1
Append 7 (size=7):  No resize, work = 1
Append 8 (size=8):  RESIZE (copy 7 elements), work = 1 + 7 = 8
Append 9 (size=9):  No resize, work = 1
...
Append 16 (16):     RESIZE (copy 15), work = 1 + 15 = 16
```

**Pattern: Resizes happen at sizes 2, 4, 8, 16, 32, ...**

```
Resize costs:    1 + 3 + 7 + 15 + 31 + ... + (n-1)
                = (2-1) + (4-1) + (8-1) + (16-1) + ...
                = 1 + 1 + 1 + ... + 1  (for 2, 4, 8, 16...)
                + (1 + 3 + 7 + 15 + ...)
                = (number of resizes) + (sum of elements copied)

Number of resizes: log₂(n)  (capacity doubles each time)
Total copies: 1 + 2 + 4 + 8 + ... + (n/2)
            = (geometric series)
            = 2n - 1
            ≈ 2n
```

**Total work for n appends:**

```
Regular appends: n × O(1) = O(n)
Copy operations: O(2n) = O(n)
─────────────────────────
Total: O(n)

Amortized per append: O(n) / n = O(1)
```

**Key insight:** Even though some individual appends cost O(n), the average cost per append over n appends is O(1).

### 3.3 Growth Factor Comparison

**Different growth strategies:**

**2x growth (doubling):**
```
Capacity: 1 → 2 → 4 → 8 → 16 → 32 → ... → 2^k
Number of resizes: log₂(n)
Total copies: O(n)
Amortized: O(1) per append
Space overhead: Worst case ~50% unused (when capacity doubled but not filled)
```

**1.5x growth:**
```
Capacity: 1 → 1.5 → 2.25 → 3.375 → 5.06 → ... → 1.5^k
Number of resizes: log₁.₅(n) ≈ 1.71 × log₂(n) (more resizes)
Total copies: Still O(n) (geometric series still sums to O(n))
Amortized: O(1) per append (same!)
Space overhead: Worst case ~33% unused (closer fit than 2x)
```

**Linear growth (add constant):**
```
Capacity: 1 → 11 → 21 → 31 → ... (adding 10 each time)
Number of resizes: O(n) (linear!)
Total copies: 1 + 11 + 21 + 31 + ... 
            = O(1) + O(2) + O(3) + ... + O(n)
            = O(n²) (quadratic!)
Amortized: O(n) per append (TERRIBLE!)
```

**Comparison:**
```
Growth Factor │ Resizes    │ Total Copies │ Amortized/Append
──────────────┼────────────┼──────────────┼─────────────
2x            │ log n      │ O(n)         │ O(1) ✓
1.5x          │ 1.71×log n │ O(n)         │ O(1) ✓
1.1x          │ 7.3×log n  │ O(n)         │ O(1) ✓
+10           │ n/10       │ O(n²)        │ O(n) ✗
```

---

## 4. Visual Walkthrough: Building a Dynamic Array

**Scenario:** Create dynamic array starting with capacity 2, then append [10, 20, 30, 40, 50]

### Step 1: Initialize

```
Array created:
array = []
size = 0
capacity = 2

Memory:
┌─────┬─────┐
│ ?   │ ?   │
└─────┴─────┘
Address: 0x1000
```

### Step 2: Append 10

```
Action: array.append(10)

Check: size (0) < capacity (2)? YES
  Add element: array[0] = 10
  size = 1

State:
┌─────┬─────┐
│ 10  │ ?   │
└─────┴─────┘
size = 1, capacity = 2
```

### Step 3: Append 20

```
Action: array.append(20)

Check: size (1) < capacity (2)? YES
  Add element: array[1] = 20
  size = 2

State:
┌─────┬─────┐
│ 10  │ 20  │
└─────┴─────┘
size = 2, capacity = 2
```

### Step 4: Append 30 (FIRST RESIZE!)

```
Action: array.append(30)

Check: size (2) < capacity (2)? NO! RESIZE!

Step 1: Create new array (capacity = 4)
┌─────┬─────┬─────┬─────┐
│ ?   │ ?   │ ?   │ ?   │
└─────┴─────┬─────┴─────┘
Address: 0x2000

Step 2: Copy old elements
Copy 10: array[0] = 10
Copy 20: array[1] = 20
┌─────┬─────┬─────┬─────┐
│ 10  │ 20  │ ?   │ ?   │
└─────┴─────┴─────┴─────┘

Step 3: Deallocate old array at 0x1000

Step 4: Add new element
array[2] = 30
size = 3

Final state:
┌─────┬─────┬─────┬─────┐
│ 10  │ 20  │ 30  │ ?   │
└─────┴─────┴─────┴─────┘
size = 3, capacity = 4

Work done: 1 (append) + 2 (copies) = 3 operations
```

### Step 5: Append 40

```
Action: array.append(40)

Check: size (3) < capacity (4)? YES
  Add element: array[3] = 40
  size = 4

State:
┌─────┬─────┬─────┬─────┐
│ 10  │ 20  │ 30  │ 40  │
└─────┴─────┴─────┴─────┘
size = 4, capacity = 4

Work done: 1 operation (append only, no resize)
```

### Step 6: Append 50 (SECOND RESIZE!)

```
Action: array.append(50)

Check: size (4) < capacity (4)? NO! RESIZE!

Step 1: Create new array (capacity = 8)
┌─────┬─────┬─────┬─────┬─────┬─────┬─────┬─────┐
│ ?   │ ?   │ ?   │ ?   │ ?   │ ?   │ ?   │ ?   │
└─────┴─────┴─────┴─────┴─────┴─────┴─────┴─────┘
Address: 0x3000

Step 2: Copy old elements (4 copies)
10, 20, 30, 40
┌─────┬─────┬─────┬─────┬─────┬─────┬─────┬─────┐
│ 10  │ 20  │ 30  │ 40  │ ?   │ ?   │ ?   │ ?   │
└─────┴─────┴─────┴─────┴─────┴─────┴─────┴─────┘

Step 3: Deallocate old array

Step 4: Add new element
array[4] = 50
size = 5

Final state:
┌─────┬─────┬─────┬─────┬─────┬─────┬─────┬─────┐
│ 10  │ 20  │ 30  │ 40  │ 50  │ ?   │ ?   │ ?   │
└─────┴─────┴─────┴─────┴─────┴─────┴─────┴─────┘
size = 5, capacity = 8

Work done: 1 (append) + 4 (copies) = 5 operations
```

### Cost Summary

```
Append 10: 1 operation
Append 20: 1 operation
Append 30: 3 operations (resize)
Append 40: 1 operation
Append 50: 5 operations (resize)

Total: 1 + 1 + 3 + 1 + 5 = 11 operations
Average per append: 11 / 5 = 2.2 ≈ O(1)

As n grows:
Total work: O(n)
Amortized: O(1) per append
```

---

## 5. Critical Analysis

### 5.1 Time Complexity: Append

**Best case: O(1)**
```
array.append(x) when size < capacity
  - No resize needed
  - Just place element at array[size]
  - Time: O(1)
```

**Worst case (single append): O(n)**
```
array.append(x) when size == capacity
  - Must resize
  - Copy all n elements
  - Time: O(n)
```

**Amortized: O(1)**
```
Over n appends:
  - Total work: O(n) (proven above)
  - Per append: O(n) / n = O(1)
```

### 5.2 Space Complexity

**Auxiliary space: O(1)**
```
Resize operation copies to new array:
  - Old array: discarded
  - New array: becomes the data structure
  - Extra space during resize: O(1) (pointers only)
```

**Total space: O(n + wasted)**
```
If size = n:
  - Used space: n × element_size
  - Capacity = 2^⌈log₂(n)⌉ (next power of 2)
  - Wasted space: capacity - size
  
Worst case (just after doubling):
  - Capacity = 2n
  - Size = n + 1
  - Wasted = n - 1 ≈ n
  
Percentage wasted: (n-1) / (2n) ≈ 50%
Average wasted: 25% (over time, not just at resize)
```

### 5.3 Edge Cases

**1. Out of memory**
```python
array = []
try:
    while True:
        array.append(huge_object)  # Eventually, allocate fails
except MemoryError:
    # Can't grow anymore
```

**2. Memory fragmentation**
```
First allocation: 1000 bytes at 0x1000-0x3E8
Resize to 2000: Need contiguous 2000 bytes

Memory map:
0x0000 - 0x0FFF: Free (4KB)
0x1000 - 0x3E8:  Array (1000 bytes) ← Can't expand here
0x3E9 - 0x5000:  Other data (allocated)
0x5001 onwards:  Free but scattered

Solution: Allocate 2000 bytes from free space, copy, deallocate old
Cost: O(n) per resize (normal)
```

**3. Very small growth factor**
```
Growth factor = 1.01 (1% per resize)

Number of resizes to reach 1 million:
log₁.₀₁(1,000,000) ≈ 1,380 resizes!

This makes many small allocations, fragmenting memory.
Better: Use 2x growth (only 20 resizes to 1 million)
```

---

## 6. System Connection

### C++ std::vector

```cpp
std::vector<int> v;
v.push_back(10);  // append in C++

// Real implementation (simplified):
template <typename T>
class vector {
    T* data;
    size_t size;
    size_t capacity;
    
public:
    void push_back(const T& value) {
        if (size == capacity) {
            // Resize with growth factor
            capacity = (capacity == 0) ? 1 : capacity * 2;
            T* new_data = new T[capacity];
            for (size_t i = 0; i < size; i++) {
                new_data[i] = data[i];
            }
            delete[] data;
            data = new_data;
        }
        data[size++] = value;
    }
};
```

**C++ vector growth:**
- Growth factor: 1.5x or 2x (implementation dependent)
- std::capacity() shows allocated size
- std::reserve() pre-allocate to avoid resizes

### Python list

```python
# Python list growth (CPython implementation)
# Growth factor: 1.125x (12.5% increase)
# This balances memory usage with resize frequency

lst = []
lst.append(x)  # Triggers internal dynamics

# Under the hood:
# size = 0, capacity = 0
# append: capacity = 4
# append: capacity = 8  (4 + 4 = 8, not 8)
# append: capacity = 12 (8 + 4, growth factor ≈ 1.125x)
# ...
```

### Java ArrayList

```java
ArrayList<Integer> list = new ArrayList<>();
list.add(10);  // append

// Java's implementation:
// Initial capacity: 10
// Growth factor: 1.5x
private int newCapacity(int minCapacity) {
    int oldCapacity = this.capacity;
    int newCapacity = oldCapacity + (oldCapacity >> 1);  // 1.5x
    return newCapacity;
}
```

---

## 7. Knowledge Check

**Question 1: Amortized Analysis**

You repeatedly append to a dynamic array with 2x growth. Starting with capacity 2:

A. How many resizes occur for the first 1000 appends?
B. What's the total work (number of copies)?
C. What's the amortized cost per append?
D. Why is this better than 1.1x growth?

---

**Question 2: Space Efficiency**

After appending 1 million elements with 2x growth:

A. What's the capacity of the array?
B. How much space is wasted?
C. What percentage is wasted?
D. Is this acceptable?

---

**Question 3: Real-world Decision**

You're implementing a log system that appends 100,000 logs/second. Each log is 1KB.

A. With 2x growth, how many resizes in 1 second?
B. How much time is spent copying (estimate)?
C. Is this acceptable for a real-time system?
D. What growth factor would you use instead?

---

## Summary: Day 2 Core Concepts

**Dynamic Arrays:**
- **Append:** O(1) amortized (not O(n)!)
- **Resize:** O(n) worst case, but rare
- **Growth factor:** 2x is standard (1.5x for memory efficiency)
- **Space:** ~25% wasted on average (50% worst case)

**Amortized Analysis:**
- Spread cost of expensive operations over many cheap operations
- Total work for n operations is O(n), so per-operation is O(1)
- Important for understanding real performance (not just Big O)

**When to use dynamic arrays:**
- ✅ Size unknown at declaration
- ✅ Need to append frequently
- ✅ Random access matters
- ✅ Most general-purpose use case

**When to avoid:**
- ❌ Frequent insertions in middle (use linked list)
- ❌ Frequent deletions from middle (use linked list)
- ❌ Memory is extremely tight (use fixed arrays)

---

**End of Day 2: Dynamic Arrays Deep-Dive**
