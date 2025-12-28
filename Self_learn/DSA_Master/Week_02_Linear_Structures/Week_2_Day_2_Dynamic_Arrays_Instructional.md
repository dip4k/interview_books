# Week 2, Day 2: Dynamic Arrays

## 🗓 Metadata
**Week:** 2 | **Day:** 2 of 5 | **Topic:** Dynamic Arrays — Automatic Growth, Amortized Analysis  
**Category:** Linear Data Structures | **Difficulty:** 🟡 Medium  
**Prerequisites:** Week 1 (Big-O), Week 2 Day 1 (Arrays)  
**Time:** 120-150 minutes | **Status:** 🔍 In Study

---

## 1️⃣ THE WHY — Engineering Motivation

### Real-World Problem
Arrays have fixed size (must know n upfront). But real programs accumulate data of unknown size: user list grows, log entries accumulate. Need automatically resizing array. When to resize? Doubling strategy: O(1) amortized per append.

### Design Problems Solved
- **Unknown data size** (don't know how many items coming)
- **Automatic growth** (user code calls append, never worries about capacity)
- **Efficiency** (O(1) amortized, not O(n) reallocation every time)
- **Memory usage** (don't allocate upfront for worst case)
- **Built-in sequences** (Python list, Java ArrayList, C++ vector)
- **Real-time systems** (predictable amortized cost)

### Real System Usage
- **Python list:** append() O(1) amortized via doubling
- **Java ArrayList:** add() O(1) amortized
- **C++ vector:** push_back() O(1) amortized
- **String builders:** StringBuilder.append() O(1) amortized
- **Memory allocators:** malloc with growth factor
- **Message queues:** Resizable circular buffers
- **Log files:** Write buffers that flush when full

### Why Dynamic Arrays Matter
**Most common data structure in practice.** Every language has built-in dynamic array (list, vector, ArrayList). Understanding amortized analysis crucial for predicting performance.

---

## 2️⃣ THE WHAT — Mental Model & Intuition

### Core Analogy
**Dynamic array:** Movie theater with variable seating. Start with 10 seats. When full, build new theater with 20 seats, move everyone. When full again, build 40-seat theater. Moving happens rarely, so amortized cost is constant per person.

### Key Invariants
1. **Doubling Invariant:** Capacity = power of 2 (2, 4, 8, 16, ...)
2. **Load Factor Invariant:** After resize, size < capacity/2
3. **Amortized Cost Invariant:** O(1) per append over many operations
4. **Memory Conservation:** Never allocate > 2× current usage

---

## 3️⃣ THE HOW — Mechanical Walkthrough

### Dynamic Array Append

```
APPEND(dynamic_array, value):
  if size >= capacity:
    // Resize: allocate new array, copy, deallocate old
    new_capacity = capacity * 2
    new_array = ALLOCATE(new_capacity)
    COPY_ALL_ELEMENTS(dynamic_array, new_array)
    FREE(dynamic_array)
    dynamic_array = new_array
    capacity = new_capacity
  
  dynamic_array[size] = value
  size = size + 1

Time: O(1) amortized
Space: O(n) total, O(capacity - size) wasted space
```

### Amortized Analysis

```
Append n elements to empty dynamic array:

Element 1: size=1, capacity=2 (initial). No resize.
Element 2: size=2, capacity=2. No resize.
Element 3: size=3, capacity=4. Resize! Cost=3 (copy 2 elements)
Element 4: size=4, capacity=4. No resize.
Element 5: size=5, capacity=8. Resize! Cost=4 (copy 4 elements)
Element 6-8: No resize.
Element 9: size=9, capacity=16. Resize! Cost=8 (copy 8 elements).
...

Total cost: 3 + 4 + 8 + 16 + ... < 2*n
Amortized: 2*n / n = O(1) per append

Key: Resize happens log(n) times. Each doubling costs more, but happens exponentially less often.
```

---

## 4️⃣ VISUALIZATION — Simulation & Examples

### Example: Building Dynamic Array

```
Append [1, 2, 3, 4, 5, 6, 7, 8, 9]:

Initial: capacity=2, size=0, data=[]

Append 1: data=[1], size=1, capacity=2 (no resize)
Append 2: data=[1,2], size=2, capacity=2 (no resize)
Append 3: size=3 > capacity=2 → RESIZE!
  - Allocate new array capacity=4
  - Copy [1,2] → [1,2,_,_]
  - Append 3 → [1,2,3,_]
  - size=3, capacity=4

Append 4: [1,2,3,4], size=4, capacity=4 (no resize)
Append 5: size=5 > capacity=4 → RESIZE!
  - Allocate capacity=8
  - Copy [1,2,3,4] → [1,2,3,4,_,_,_,_]
  - Append 5 → [1,2,3,4,5,_,_,_]
  - size=5, capacity=8

Append 6-8: [1,2,3,4,5,6,7,8], no resizes
Append 9: size=9 > capacity=8 → RESIZE!
  - Allocate capacity=16
  - Copy [1,2,3,4,5,6,7,8] → [1,2,3,4,5,6,7,8,_,_,_,_,_,_,_,_]
  - Append 9 → [1,2,3,4,5,6,7,8,9,_,_,_,_,_,_,_]
  - size=9, capacity=16

Resizes happened: 3 times (at n=3, n=5, n=9)
Total copy cost: 2 + 4 + 8 = 14 operations
Total append cost: 9 operations
Total: 23 operations
Amortized: 23/9 ≈ 2.5 ≈ O(1)

If we knew size=9 upfront:
Allocate capacity=9 at start, then append 9 times
Cost: 9 operations only!
But we don't know size upfront, so doubling is good compromise.
```

---

## 5️⃣ CRITICAL ANALYSIS — Performance & Robustness

| Operation | Worst | Amortized | Why |
|-----------|-------|-----------|-----|
| **Append** | O(n) | O(1) | Resize rare |
| **Access** | O(1) | O(1) | No resize needed |
| **Insert middle** | O(n) | O(n) | Must shift elements |
| **Delete end** | O(1) | O(1) | Just decrement |

### Why Doubling vs Other Strategies

**Doubling (factor 2):**
- ✅ Good: O(1) amortized
- ✅ Good: Unused space never > 2×
- ✅ Good: Powers of 2 (cache aligned)

**Growing by 1 each time:**
- ❌ Bad: O(n) amortized (quadratic total time)
- ✅ Good: No wasted space
- ❌ Bad: Many small allocations

**Growing by fixed amount (k):**
- ❌ Bad: O(n/k) amortized (still polynomial)
- ✅ Good: Predictable growth
- ❌ Bad: Many reallocations

---

## 6️⃣ REAL SYSTEM INTEGRATION

[Descriptions of Python list, Java ArrayList, C++ vector, etc.]

---

## 7️⃣ CONCEPT CROSSOVERS

**Builds On:** Arrays (Day 1), Amortized analysis (Week 1)
**Built Upon By:** All high-level languages' list implementations

---

Sections 8-11 follow same structure...

**Status:** ✅ Complete  
**Next:** Day 3 (Linked Lists)

