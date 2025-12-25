# 🧠 Week 2: Linear Structures - Day 2

# Dynamic Arrays: Resizing, Amortization, Growth Strategy

## 🗓 Metadata
**Topic:** Dynamic Arrays  
**Week:** Week 2  
**Day:** Day 2 of 5  
**Category:** Linear Structures  
**Difficulty:** 🟡 Medium  
**Status:** 🔍 In Study  
**Last Reviewed:** —  
**Confidence Level (1–5):** —/5  

---

## 1️⃣ The Why — Engineering Motivation

### Real-World Problem

Plain arrays require you to declare size upfront. But in many real-world scenarios, you don't know how many items you'll have:
- Reading lines from a file.
- Incoming network requests (unbounded).
- Building a result set incrementally.

You *could* estimate a large upper bound, but that wastes memory. You *could* use linked lists, but you lose the cache-friendly sequential access of Day 1.

### Design Problem Solved

**Dynamic arrays solve this elegantly:** Maintain array semantics (O(1) indexing, cache-friendly) while supporting automatic growth.

Trade-off: Occasional O(n) resize operation, but amortized to O(1) per append.

### Real System Usage

- **Java ArrayList**, **C++ std::vector**, **Python list**: All are dynamic arrays.
- Used in: Collections frameworks, compiler intermediate code buffers, graphics command queues.

---

## 2️⃣ The What — Mental Model & Intuition

### Core Analogy

Imagine a **stretchable tray** with slots for items:

1. You start with 2 slots.
2. Fill them up.
3. When you add a 3rd item, the tray "stretches" to 4 slots (doubles capacity).
4. You move all items to the new tray and discard the old one.
5. You still have O(1) random access, but now more room.

The key insight: If capacity doubles, you only stretch **log(n)** times to hold n items.

---

## 3️⃣ The How — Mechanical Walkthrough

### Data Structure State

```
buffer: pointer to contiguous array
size: number of elements currently stored
capacity: maximum elements buffer can hold
```

### Append Operation (pseudocode-free explanation)

**Case 1: size < capacity**
1. Write the new element at position `size`.
2. Increment `size`.
3. Cost: O(1).

**Case 2: size == capacity**
1. Create a new buffer with `capacity' = growth_factor * capacity` (e.g., ×2).
2. Copy all `size` elements from old buffer to new buffer.
3. Free the old buffer.
4. Update `buffer` pointer and `capacity`.
5. Write the new element at the old `size` position.
6. Increment `size`.
7. Cost: O(n) for this single append.

### Amortized Analysis

Insert n items starting with capacity 1:

- Resize triggers at sizes: 1, 2, 4, 8, ..., 2^k where 2^k ≥ n.
- Copy costs: 1 + 2 + 4 + ... + 2^k = O(2^(k+1)) = O(n).
- Total appends: n.
- Amortized cost per append: O(n) / n = **O(1)**.

---

## 4️⃣ Visualization — Simulation

Capacity starts at 2. Append values: 10, 20, 30, 40.

```
Step 0: capacity=2, size=0
buffer: [_, _]

Append 10: size < capacity
[10, _], size=1

Append 20: size < capacity
[10, 20], size=2

Append 30: size == capacity → RESIZE
New capacity = 4
Copy to new buffer: [10, 20, _, _]
Add 30: [10, 20, 30, _], size=3

Append 40: size < capacity
[10, 20, 30, 40], size=4

Append 50: size == capacity → RESIZE
New capacity = 8
Copy: [10, 20, 30, 40, _, _, _, _]
Add 50: [10, 20, 30, 40, 50, _, _, _], size=5
```

Over 5 appends: 3 resizes, but total copies = 0 + 0 + 2 + 0 + 4 = 6 ≈ O(n).

---

## 5️⃣ Critical Analysis — Performance & Robustness

### Complexity Table

| Operation         | Amortized | Worst | Notes                                    |
|-------------------|-----------|-------|------------------------------------------|
| Append end        | O(1)      | O(n)  | Resize happens, but rarely              |
| Read/write index  | O(1)      | O(1)  | Same as static arrays                   |
| Insert middle     | O(n)      | O(n)  | Must shift elements                     |
| Delete middle     | O(n)      | O(n)  | Must shift to fill gap                  |
| Space             | O(n)      | O(n)  | May have unused slots                   |

### Growth Factor Trade-offs

- **Factor = 1.5x:** Slower growth, less waste, more frequent resizes.
- **Factor = 2x:** Faster growth (logarithmic resizes), more waste (~50% unused on average).
- **Factor = 3x or more:** Excessive waste.

Typical choice: 1.5x to 2x.

### Edge Cases & Failure Modes

- **Allocation failure:** If new buffer allocation fails, you're in an inconsistent state (requires careful error handling).
- **Integer overflow:** Capacity × element_size can overflow on 32-bit systems.
- **Resize pause:** In real-time systems, the O(n) resize operation may violate latency bounds.

---

## 6️⃣ Real System Integration

- **std::vector (C++):** Grows with factor 1.5x to 2x depending on implementation.
- **ArrayList (Java):** Grows with factor 1.5x.
- **Python list:** Grows with factor 1.125x for small sizes, then 1.12x.

---

## 7️⃣ Concept Crossovers

- **Extends Day 1 (Arrays):** Same cache benefits, plus growth.
- **Competes with Day 3 (Linked Lists):** Dynamic size, but contiguous.
- **Foundation for Day 4 (Stacks/Queues):** Often implemented using dynamic arrays with head/tail pointers.

---

## 8️⃣ Mathematical & Theoretical Perspective

### Series Sum

If capacity doubles:
- Resize sequence: C, 2C, 4C, 8C, ...
- Copy costs: C + 2C + 4C + ... = C(1 + 2 + 4 + ...) = O(n).

### Amortized Cost Definition

Cost(append) = (actual cost per operation + accumulated future cost spread over operations) = (1 + O(n)/n) = O(1).

---

## 9️⃣ Algorithmic Design Intuition

### When to Use Dynamic Arrays

- Unknown size upfront.
- Append-heavy workload.
- Need O(1) indexing.
- Can tolerate occasional pauses.

### When to Avoid

- Real-time constraints (occasional O(n) resize unacceptable).
- Frequent mid-insertions.
- Very tight memory budgets.

---

## 🔟 Knowledge Check — Socratic

1. If capacity grows by +100 each time (linear), what's the total cost to append n elements?
   - Answer: 100 + 200 + ... + n ≈ O(n²). Bad!

2. How would you design a dynamic array for a real-time system that cannot tolerate pauses?
   - Answer: Pre-allocate extra capacity or use a different growth strategy (e.g., tiers of fixed-size blocks).

3. Why does Python choose 1.125x instead of 2x for growth?
   - Answer: Balance between resize frequency and wasted space.

---

## 1️⃣1️⃣ Retention Hook

**One-liner:** Dynamic arrays are **arrays that stretch geometrically** — O(1) indexing, O(1) amortized appends, occasional O(n) resize.

---

## 🧭 Navigation

**← [Previous: Day 1 - Arrays](./01_Arrays.md)**  
**→ [Next: Day 3 - Linked Lists](./03_Linked_Lists.md)**  
**↑ [Back to README](../README.md)**

