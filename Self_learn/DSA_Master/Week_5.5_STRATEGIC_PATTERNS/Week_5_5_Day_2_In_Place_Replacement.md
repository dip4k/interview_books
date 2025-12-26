# Week 5.5, Day 2: In-Place Replacement Technique

**Week:** 5.5 | **Day:** 2 | **Topic:** In-Place Array Modification  
**Time:** 75 minutes reading | **Difficulty:** 🔴 Hard  
**Prerequisites:** Week 5, Day 5.5-1  

---

## 1️⃣ THE WHY — Engineering Motivation

### The Problem We Solve

**Scenario:** Modify array with O(1) extra space (no new array, no stack).

**Naive approach:**
```python
# Remove duplicates
new_arr = []
for x in arr:
    if x not in new_arr:
        new_arr.append(x)
return new_arr  # O(n) extra space!
```

**Better approach (In-place):**
```python
# Modify arr itself, track "new end" pointer
j = 0
for i in range(len(arr)):
    if arr[i] != arr[i-1]:
        arr[j] = arr[i]
        j += 1
return j  # Return length, array modified in place!
```

### Why Interviews Care

- **Space constraint:** Large data (1 billion elements), limited memory
- **Efficiency preference:** O(1) space > O(n) space, even if slightly slower
- **Skill indicator:** Shows deep understanding of pointers and array manipulation

**Why This Matters:** 8-12% of array problems require/prefer in-place solutions.

---

## 2️⃣ THE WHAT — Mental Model & Intuition

### Core Concept: Two Pointers

```
Pointer i: read position (scan for valid elements)
Pointer j: write position (where to place next valid)

As i scans, valid elements are written to positions starting at j.

Key insight: i always ahead of (or equal to) j
So no read-write collision!
```

### Why It Works

```
Example: Remove value 2 from [1, 2, 3, 2, 4]

Initial:
  i=0, j=0
  arr: [1, 2, 3, 2, 4]

i=0, arr[0]=1 (keep):
  arr[0] = 1, j=1
  arr: [1, 2, 3, 2, 4]

i=1, arr[1]=2 (skip)

i=2, arr[2]=3 (keep):
  arr[1] = 3, j=2
  arr: [1, 3, 3, 2, 4]

i=3, arr[3]=2 (skip)

i=4, arr[4]=4 (keep):
  arr[2] = 4, j=3
  arr: [1, 3, 4, 2, 4]

Result: arr[:3] = [1, 3, 4] ✓
Return j=3 (new length)
```

### The Key Insight

```
i always > j (or equal at start)
So when we write arr[j], we haven't read that position yet
Safe to overwrite!

This is why in-place works.
```

---

## 3️⃣ THE HOW — Mechanical Walkthrough

### Generic Pattern

```python
def inplace_modification(arr, should_keep):
    """
    should_keep: function that returns True if element should stay
    Returns: new length
    """
    j = 0
    for i in range(len(arr)):
        if should_keep(arr[i]):
            arr[j] = arr[i]
            j += 1
    return j
```

### Example 1: Remove Duplicates (Sorted)

```python
def removeDuplicates(arr):
    if not arr:
        return 0
    
    j = 1  # Start from index 1
    for i in range(1, len(arr)):
        if arr[i] != arr[i-1]:  # Different from previous
            arr[j] = arr[i]
            j += 1
    
    return j

# [1,1,2,2,3] → [1,2,3,_,_], return 3
```

### Example 2: Remove Element

```python
def removeElement(arr, val):
    j = 0
    for i in range(len(arr)):
        if arr[i] != val:
            arr[j] = arr[i]
            j += 1
    
    return j

# [3,2,2,3], val=3 → [2,2,_,_], return 2
```

### Example 3: Remove Vowels (Hard variant)

```python
def removeVowels(s):
    vowels = set('aeiou')
    chars = list(s)  # Convert to list for in-place
    
    j = 0
    for i in range(len(chars)):
        if chars[i] not in vowels:
            chars[j] = chars[i]
            j += 1
    
    return ''.join(chars[:j])

# "hello" → "hll"
```

---

## 4️⃣ VISUALIZATION — Traced Examples

### Example 1: Remove Duplicates

```
Array: [1, 1, 2, 2, 3]

i=0: arr[0]=1, first element, skip
i=1, j=1:
  arr[1]=1 == arr[0]=1, skip (duplicate)

i=2, j=1:
  arr[2]=2 != arr[1]=1, keep
  arr[1] = 2, j=2
  [1, 2, 2, 2, 3]

i=3:
  arr[3]=2 == arr[2]=2, skip

i=4, j=2:
  arr[4]=3 != arr[3]=2, keep
  arr[2] = 3, j=3
  [1, 2, 3, 2, 3]

Return j=3, use arr[:3] = [1, 2, 3]
```

### Example 2: Remove Element

```
Array: [3, 2, 2, 3], val=3

i=0, j=0:
  arr[0]=3 == val, skip

i=1, j=0:
  arr[1]=2 != val, keep
  arr[0] = 2, j=1
  [2, 2, 2, 3]

i=2, j=1:
  arr[2]=2 != val, keep
  arr[1] = 2, j=2
  [2, 2, 2, 3]

i=3:
  arr[3]=3 == val, skip

Return j=2, use arr[:2] = [2, 2]
```

---

## 5️⃣ CRITICAL ANALYSIS — Performance & Robustness

### Complexity Analysis

| Approach | Time | Space | Notes |
|----------|------|-------|-------|
| **New Array** | O(n) | O(n) | Simple, extra memory |
| **In-Place** | O(n) | O(1) | Slightly tricky, preferred |
| **With Frequency Map** | O(n) | O(k) | k = unique elements |

### Space Savings

```
Remove duplicates from 1 billion element array:

New array approach:
  Space: 4 GB (storing 1B integers)
  
In-place:
  Space: O(1) stack variables only
  
The difference: Not storing the result array!
```

### Edge Cases

**All elements removed:**
```python
# [3, 3, 3], remove 3
# Return 0 (empty array)
```

**No elements removed:**
```python
# [1, 2, 3], remove 4
# Return 3 (unchanged)
```

**Empty array:**
```python
# [], remove anything
# Return 0 immediately
```

---

## 6️⃣ REAL SYSTEM INTEGRATION — Production Applications

### Memory-Constrained Environments

```
Embedded systems, IoT devices
Limited RAM, need to process large datasets
In-place algorithms critical

Example: Sensor reading cleanup
  Remove outliers without extra memory
```

### Data Pipeline Processing

```
Stream processing:
  Read chunk of data
  Filter/clean in-place
  Write result
  
With in-place: single pass, minimal memory
```

### Database Query Optimization

```
Remove duplicates from query result
Option 1: Create new result array
Option 2: Modify result in-place (in-place with j pointer)

Option 2 better for large result sets
```

---

## 7️⃣ CONCEPT CROSSOVERS — Connections

### Two-Pointer Technique Returns

```
Week 4.5: Two-pointer for binary search
Week 5.5 Day 2: Two-pointer for in-place modification

Same tool, different problem:
- Day 1: Different pointers for search space
- Day 2: Different pointers for read/write positions
```

### Array Fundamentals

```
Index manipulation
Pointer arithmetic
Understanding O(1) space

All core array skills
```

---

## 8️⃣ MATHEMATICAL & THEORETICAL — Formal Foundations

### Proof: Safety of In-Place Modification

**Claim:** When i > j, writing arr[j] doesn't affect future reads at positions i+.

**Proof:**
```
At any iteration:
  i: current read position
  j: current write position
  
Since j only advances when we write, and i advances every iteration:
  We have: j <= i

When we write arr[j]:
  j <= i < i+1 < i+2 < ...
  
So the write at arr[j] happens before we read arr[j+1]
Therefore safe to overwrite!
```

### Two-Pointer Invariant

**Invariant:** After each iteration, arr[0..j-1] contains valid elements in order.

**Maintenance:** 
- If arr[i] is valid, write to arr[j], increment j
- If arr[i] is invalid, skip it
- Result: valid elements accumulate at start of array ✓

---

## 9️⃣ ALGORITHMIC DESIGN INTUITION — Why Design Works

### Why Two Pointers?

```
Need to distinguish:
- Elements we've decided to keep (arr[0..j-1])
- Elements we haven't processed (arr[i..n-1])
- Elements we haven't decided on (arr[j..i])

i pointer: current element under inspection
j pointer: boundary between "decided" and "pending"
```

### Why i > j is Safe

```
If we read and write at same position, we lose data.
But i > j ensures we write behind where we read.

Example:
  Write position: index 2
  Read position: index 5
  
Writing at 2 doesn't affect reading at 5!
```

---

## 🔟 KNOWLEDGE CHECK — Socratic Reasoning

1. **Why must i advance every iteration but j only when we keep?** What's the invariant?

2. **Can i ever catch up to j?** Why or why not? What would that mean?

3. **For sorted array duplicates, why compare arr[i] to arr[i-1]?** Not arr[i] to previous kept element?

4. **What happens if the array is empty?** Where are edge cases?

5. **Why is in-place preferred in interviews?** What skill does it test?

---

## 1️⃣1️⃣ RETENTION HOOK — Memory Anchors

### **Read-Write Pointers**
```
i: read (moves every iteration)
j: write (moves only when keeping)

i > j always (or equal)
Safe to overwrite at j
```

### **Two Pointers, One Pass**
```
Single loop, both pointers advance
O(n) time, O(1) space
The optimization trick
```

---

## 📊 SUPPLEMENTARY: Common Patterns

```python
# Pattern 1: Remove element
def remove(arr, val):
    j = 0
    for i in range(len(arr)):
        if arr[i] != val:
            arr[j] = arr[i]
            j += 1
    return j

# Pattern 2: Remove duplicates (sorted)
def remove_dups(arr):
    j = 1
    for i in range(1, len(arr)):
        if arr[i] != arr[i-1]:
            arr[j] = arr[i]
            j += 1
    return j

# Pattern 3: Remove by condition
def remove_if(arr, condition):
    j = 0
    for i in range(len(arr)):
        if not condition(arr[i]):
            arr[j] = arr[i]
            j += 1
    return j
```

---

## 🔗 EXTERNAL RESOURCES

**LeetCode Problems:**
- Remove Duplicates from Sorted Array (LeetCode 26)
- Remove Element (LeetCode 27)
- Remove Vowels from String (LeetCode 1119)

---

## 📝 KEY TAKEAWAYS

✅ **In-place modification uses O(1) extra space**  
✅ **Two pointers: i (read) > j (write)**  
✅ **Single pass, O(n) time**  
✅ **Interview preferred for space optimization**  
✅ **Safe because i always ahead of j**

**Next:** Day 3 — Deque Operations (sliding window optimization)

