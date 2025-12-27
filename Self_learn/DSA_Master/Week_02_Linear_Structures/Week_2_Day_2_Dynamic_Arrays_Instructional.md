# Week 2, Day 2: Dynamic Arrays (Vectors)

## 🗓 Metadata
**Week:** 2 | **Day:** 2 of 5 | **Topic:** Dynamic Arrays (Vectors)  
**Category:** Linear Structures | **Difficulty:** 🟢 Easy  
**Prerequisites:** Week 2 Day 1 (Arrays), Week 1 (Amortized Analysis)  
**Time:** 90-120 minutes | **Status:** 🔍 In Study

---

## 1️⃣ THE WHY — Engineering Motivation

**Real-World Problem:**
You're building a spreadsheet. Users don't know the final row count. Preallocating a 1 million-row array wastes memory. Reallocating for every row addition is O(n²).

**Design Problems Solved:**
- Unknown size at compile/runtime
- Grow dynamically without O(n²) total cost
- Maintain O(1) amortized append
- Standard container for most programming (vector in C++, ArrayList in Java, list in Python)

**Real System Usage:**
- **C++ std::vector:** Default container for almost everything
- **Java ArrayList:** Widely used in enterprise code
- **Python lists:** Most common collection type
- **JavaScript arrays:** Dynamic from inception

---

## 2️⃣ THE WHAT — Mental Model & Intuition

**Core Analogy:**
Think of a dynamic array like a theater that grows when full.

```
Theater with 10 seats (capacity):  [occupied, occupied, ..., empty]
User 1-10 arrive: occupy all 10 seats.
User 11 arrives: theater is full!

Solution: Build a NEW theater with 20 seats.
Move all 10 people. User 11 sits in seat 11.

Next growth: 40 seats (double again)
Then: 80 seats
Then: 160 seats
```

**Key Insight:** Exponential growth (2x) means resizes happen O(log n) times for n elements. Total copies: O(n).

---

## 3️⃣ THE HOW — Mechanical Walkthrough

**State:**
```
buffer:    pointer to allocated array
size:      number of elements currently used
capacity:  maximum elements before resize
```

**Append Operation:**
1. If size < capacity: add element, increment size, done (O(1))
2. If size == capacity: 
   - Allocate new array (capacity × 2)
   - Copy all elements from old to new
   - Deallocate old
   - Add new element

**Cost:** O(1) usually, O(n) occasionally (resize)

---

## 4️⃣ VISUALIZATION — Simulation & Examples

```
Append sequence: 1, 2, 3, 4, 5, 6, 7, 8, 9

Initial: size=0, capacity=2
[_, _]

Append 1: [1, _]  size=1, capacity=2
Append 2: [1, 2]  size=2, capacity=2
Append 3: FULL! Resize to capacity=4
          Copy: [1, 2, _, _]
          Place 3: [1, 2, 3, _]  size=3, capacity=4
Append 4: [1, 2, 3, 4]  size=4, capacity=4
Append 5: FULL! Resize to capacity=8
          Copy: [1, 2, 3, 4, _, _, _, _]
          Place 5: [1, 2, 3, 4, 5, _, _, _]  size=5, capacity=8
Append 6-8: Add to remaining capacity
          [1, 2, 3, 4, 5, 6, 7, 8]  size=8, capacity=8
Append 9: FULL! Resize to capacity=16
          [1, 2, 3, 4, 5, 6, 7, 8, 9, _, _, _, _, _, _, _]  size=9

Resize timeline:
- Resizes happened at: n=3, n=5, n=9 (when capacity doubled: 2→4, 4→8, 8→16)
- Total elements copied: (1+2) + (1+2+3+4) + (1+2+...+8) ≈ 3n
- Amortized per append: 3n / n = O(1) with small constant (actually <2)
```

---

## 5️⃣ CRITICAL ANALYSIS — Performance & Robustness

| Operation | Best | Average | Worst | Notes |
|-----------|------|---------|-------|-------|
| **Append** | O(1) | O(1) amortized | O(n) occasionally | Resize every log n appends |
| **Access** | O(1) | O(1) | O(1) | Same as static array |
| **Insert middle** | O(n) | O(n) | O(n) | Still need to shift |
| **Delete end** | O(1) | O(1) | O(1) | Just decrement size |
| **Space** | O(n) | O(n) | O(n) | Capacity ≥ size; ratio: 1 to 2 |

**Real Memory Behavior:**
- Doubling: capacity waste ≈ 25% average (between n and 2n)
- Linear growth (e.g., +10 each time): more frequent resizes, less waste
- Exponential is standard because fewer total copies

---

## 6️⃣ REAL SYSTEM INTEGRATION

**C++ std::vector implementation (libstdc++):**
- Uses exponential growth (capacity = size * 2)
- Deallocates old memory after copy
- Push_back() amortized O(1)

**Java ArrayList:**
- Growth factor: 1.5x (slightly less waste than 2x)
- Used in Collections Framework pervasively

**Python list:**
- Growth factor: ~1.125x (adaptive growth)
- Starts small, grows carefully to minimize waste

---

## 7️⃣ CONCEPT CROSSOVERS

**Builds on:** Arrays, amortized analysis  
**Built by:** Hash tables (arrays with collision chains), stacks/queues implementations

---

## 8️⃣ MATHEMATICAL & THEORETICAL PERSPECTIVE

**Claim:** Appending n elements takes O(n) total time (O(1) amortized per element).

**Proof:**
```
Cost of resizes:
  Resize 1: copy 1 element, allocate 2 capacity
  Resize 2: copy 2 elements, allocate 4 capacity  
  Resize 3: copy 4 elements, allocate 8 capacity
  ...
  Resize k: copy 2^(k-1) elements

Total copies for k resizes: 1 + 2 + 4 + ... + 2^(k-1) = 2^k - 1

For n elements, k = log₂ n resizes
Total cost: O(2^(log₂ n)) = O(n)

Amortized: n insertions cost O(n), so O(1) per insertion
```

---

## 9️⃣ ALGORITHMIC DESIGN INTUITION

**When to use:**
- Unknown size at compile time (almost always!)
- Need O(1) append (streaming data, building result)
- Default choice for any growing collection

**Why exponential > linear growth:**
- Linear (e.g., +k each time): Total resizes = n/k, total cost = k×(n/k)² = O(n²/k)
- Exponential (2x): Total resizes = log n, total cost = O(n)

---

## 🔟 KNOWLEDGE CHECK — Socratic Reasoning

**Q1:** Why double capacity instead of adding a fixed amount like +10?

**Q2:** If capacity is 100 and size is 100, how many copies when appending 1 element? How many when appending the next 50?

**Q3:** Could you use capacity = size × 1.5 instead of 2x? What changes?

**Q4:** A program appends 1 million times. How many resize operations occur (capacity 2x growth starting from 1)?

---

## 1️⃣1️⃣ RETENTION HOOK — Memory Anchors

**One-Liner:**
> **Dynamic arrays: Trade space (waste ≈25%) for time (O(1) amortized append via exponential growth).**

**Mnemonic:** "D.A.B." — Dynamic Arrays By doubling

**Cognitive Lenses:**
| Computational | O(1) amortized hides O(n) resizes; total cost spread over appends |
| Psychological | Counter-intuitive: occasional huge pauses (resize) give O(1) average |
| Design | Buy: flexibility & O(1) append. Sell: 25% memory waste, occasional latency |
| Historical | 1970s: theoretical amortized analysis. Now practical in all languages |

---

## Supplementary: Practice Problems

1. Implement dynamic array from scratch (using malloc/realloc)
2. Analyze growth factor: 1.5x vs 2x vs 1.1x (memory vs resize cost)
3. How many total bytes copied for n=10 million appends?

