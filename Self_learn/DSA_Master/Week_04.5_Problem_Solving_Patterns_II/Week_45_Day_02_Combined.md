# 📘 WEEK 4.5 DAY 2: MONOTONIC STACK - Complete Learning Package

**Week 4.5, Day 2: Stack Pattern - Finding Next/Previous Greater or Smaller Elements**

Generated: 2025-12-26 | Duration: 90 minutes | Difficulty: 🟡 Medium | Target: 4-5/5

---

## PART 1: MAIN CONTENT (11 Sections)

### 1️⃣ The Why: Engineering Motivation

**Problem:** For each element, find the next greater element to the right.

Real-world:
- **Stock trading:** Find next higher price for selling decision
- **Temperature analysis:** Find next warmer day for forecasting
- **Building heights:** Find next taller building for visibility analysis
- **Task scheduling:** Find next higher priority task
- **Histogram:** Find building heights for area calculation

**Naive approach:** Nested loop O(n²)
```python
def next_greater_naive(arr):
    result = [-1] * len(arr)
    for i in range(len(arr)):
        for j in range(i+1, len(arr)):
            if arr[j] > arr[i]:
                result[i] = arr[j]
                break
    return result
```

**Monotonic Stack approach:** O(n) time
```python
def next_greater_stack(arr):
    result = [-1] * len(arr)
    stack = []  # Stores indices
    
    for i in range(len(arr)):
        # Pop elements smaller than current
        while stack and arr[stack[-1]] < arr[i]:
            idx = stack.pop()
            result[idx] = arr[i]
        stack.append(i)
    
    return result
```

**Performance difference:** 1000 items: 1M ops vs 1K ops (1000x faster!)

---

### 2️⃣ The What: Mental Model

**Core Insight:** Maintain stack in monotonic order. When new element breaks order, popped elements found their answer.

**Key Property:**
- Stack stores indices in decreasing order of values
- New element greater than top → top found its answer
- Pop until stack empty or new element smaller than top
- Add new element

**Why this works:**
- Elements to right of popped element are checked
- First greater element found (due to monotonicity)
- O(1) amortized time per element (each pushed/popped once)

**Visual:**
```
Array: [2, 1, 2, 4, 3]

Index 0 (value 2):
  Stack: []
  Push 0
  Stack: [0]

Index 1 (value 1):
  1 < 2, no pop
  Push 1
  Stack: [0, 1]

Index 2 (value 2):
  2 > 1, pop 1 → result[1] = 2
  2 = 2, no pop
  Push 2
  Stack: [0, 2]

Index 3 (value 4):
  4 > 2, pop 2 → result[2] = 4
  4 > 0, pop 0 → result[0] = 4
  Push 3
  Stack: [3]

Index 4 (value 3):
  3 < 4, no pop
  Push 4
  Stack: [3, 4]

Result: [4, 2, 4, -1, -1]
```

---

### 3️⃣ The How: Mechanics

**Monotonic Increasing Stack Template:**
```python
def monotonic_stack(arr):
    result = [-1] * len(arr)
    stack = []  # Stores indices
    
    for i in range(len(arr)):
        # Pop while stack not empty AND top is less than current
        while stack and arr[stack[-1]] < arr[i]:
            idx = stack.pop()
            result[idx] = arr[i]
        stack.append(i)
    
    return result
```

**Monotonic Decreasing Stack:**
```python
def monotonic_decreasing(arr):
    result = [-1] * len(arr)
    stack = []
    
    for i in range(len(arr)):
        # Pop while stack not empty AND top is greater than current
        while stack and arr[stack[-1]] > arr[i]:
            idx = stack.pop()
            result[idx] = arr[i]
        stack.append(i)
    
    return result
```

**Step-by-step:**
1. Initialize result array and empty stack
2. For each element:
   - While stack not empty AND top violates monotonicity:
     - Pop element, record answer
   - Add current element to stack
3. Remaining stack elements have no answer (-1)

**Why O(n)?**
- Each element pushed once
- Each element popped at most once
- Total operations = 2n
- Therefore O(n)

---

### 4️⃣ Visualization: Examples

**Example 1: Next Greater Element**
```
Array: [1, 3, 2, 4]

Step 0: Process 1
  Stack empty, push 0
  Stack: [0]

Step 1: Process 3
  arr[0]=1 < 3, pop 0 → result[0]=3
  Stack empty, push 1
  Stack: [1]

Step 2: Process 2
  arr[1]=3 > 2, no pop
  Push 2
  Stack: [1, 2]

Step 3: Process 4
  arr[2]=2 < 4, pop 2 → result[2]=4
  arr[1]=3 < 4, pop 1 → result[1]=4
  Stack empty, push 3
  Stack: [3]

Final: result = [3, 4, 4, -1]
```

**Example 2: Previous Greater Element (right-to-left)**
```
Array: [1, 6, 4, 10, 2, 5]

Process right-to-left:
Index 5 (5): Stack: [5], result[5] = -1
Index 4 (2): 2 < 5, pop 5 → result[4] = 5, Stack: [4]
Index 3 (10): 10 > 4, no pop, Stack: [10, 4]
Index 2 (4): 4 < 10, no pop, Stack: [10, 2]
Index 1 (6): 6 < 10, no pop, Stack: [10, 1]
Index 0 (1): 1 < 6, no pop, Stack: [10, 1, 0]

Result: [-1, 10, 10, -1, 5, -1]
```

**Example 3: Trapping Rain Water (visual)**
```
Heights: [0, 1, 0, 2, 1, 0, 1, 3, 2, 1, 2, 1]
Trapped:  0 0 1 0 1 3 2 0 1 1 0 0

Use monotonic decreasing stack to find matching heights.
```

---

### 5️⃣ Critical Analysis

**Time Complexity:**
- Building stack: O(n)
- Each element pushed: 1 time
- Each element popped: at most 1 time
- Total: 2n operations = O(n)

**Space Complexity:**
- Stack stores at most n indices: O(n)
- Result array: O(n)
- Total: O(n)

**Why Monotonic Stack Better than Naive?**

| Approach | Time | Space |
|----------|------|-------|
| Naive nested loop | O(n²) | O(1) |
| Monotonic stack | O(n) | O(n) |

Monotonic stack **100x faster** for 1000 elements!

**When to Use:**
- Need next/previous greater/smaller
- Linear time critical
- Don't need sorted order

---

### 6️⃣ Real System Integration

**Stock Analysis:**
Find next higher stock price for optimal selling.

**Temperature Tracking:**
Find next warmer day for daily forecast changes.

**Building Visibility:**
Determine which buildings visible from each building.

**Histogram Area:**
Calculate largest rectangle in histogram efficiently.

---

### 7️⃣ Concept Crossovers

**Builds On:**
- Week 1: Stack data structure
- Week 2: Monotonicity concept
- Week 4: Pointer patterns

**Enables:**
- Trapping rain water (medium/hard)
- Largest rectangle histogram (medium)
- Daily temperatures (easy/medium)
- Stock problems (medium)

**Related Techniques:**
- Binary search (for similar problems)
- Dynamic programming (for histogram variants)

---

### 8️⃣ Mathematical Perspective

**Amortized Analysis:**
- Each element pushed once: n operations
- Each element popped once: n operations
- Total: 2n operations
- Amortized O(n)

**Proof of Correctness:**
When element at index i popped by element at index j:
- All elements between i and j are smaller than arr[j]
- So arr[j] is first greater element to right of i

---

### 9️⃣ Algorithmic Design Intuition

**When to Use Monotonic Stack:**
1. Find next/previous greater/smaller
2. Linear time required
3. Structure naturally maintains monotonicity
4. Can process left-to-right or right-to-left

**When NOT to Use:**
1. Need exact sorted order (use sort)
2. Need range queries (use segment tree)
3. Multiple queries (preprocess differently)

---

### 🔟 Knowledge Check

1. Why is monotonic stack O(n) instead of O(n²)?
2. What does "monotonic" mean in this context?
3. Trace next greater element example
4. What's the difference between increasing and decreasing stack?
5. How to find previous greater instead of next?
6. What problems use monotonic stack?
7. How is stack order maintained?

---

### 1️⃣1️⃣ Retention Hooks

**One-liner:** "Monotonic stack maintains order while processing, enabling O(n) next-greater solutions."

**Mnemonic - "STACK MONO":**
- **S**tack maintains order
- **T**races elements in sequence
- **A**nswers built as we go
- **C**omplexity O(n)
- **K**eeps monotonicity

**M**onotonicDecreasing
- **O**ne pass through array
- **N**o backtracking needed
- **O**(1) amortized per element

**Visual Memory:**
```
Think: "Queue at store"
People line up by height (monotonic).
When taller person comes, shorter people see them (answer found).
```

**Story:** "A stock trader watches prices all day. As new price comes, previous traders instantly know if they should have held (new price is higher) or sold (new price is lower)."

---

## PART 2: QUICK SUMMARY

**Monotonic Stack Essence:**

Maintain stack in monotonic order while processing. When new element breaks order, popped element found its answer. O(n) time for single pass.

**When to Use:**
- Find next/previous greater element ✓
- Find next/previous smaller element ✓
- O(n) time required ✓
- Linear processing acceptable ✓

**Template:**
```python
def next_greater(arr):
    result = [-1] * len(arr)
    stack = []
    
    for i in range(len(arr)):
        while stack and arr[stack[-1]] < arr[i]:
            idx = stack.pop()
            result[idx] = arr[i]
        stack.append(i)
    
    return result
```

**Real Problems:**
- Next Greater Element
- Next Greater Element II (circular)
- Largest Rectangle in Histogram
- Trapping Rain Water
- Daily Temperatures

---

## PART 3: SOCRATIC QUESTIONS & ANSWERS

**Q1:** Why is monotonic stack O(n) and not O(n²)?

**A:** Each element pushed once (n ops) and popped at most once (n ops). Total 2n operations = O(n). Not O(n²) because we don't compare to every previous element.

---

**Q2:** What does "monotonic" mean in this context?

**A:** Stack indices are maintained in monotonic order (increasing or decreasing order of their values). When new element violates order, we pop until restored.

---

**Q3:** Trace [2, 1, 2, 4, 3] for next greater

**A:** Already traced in visualization section above.

---

**Q4:** What's difference between increasing and decreasing stack?

**A:** Increasing: pop when new element > top (finds next greater). Decreasing: pop when new element < top (finds next smaller). Opposite logic.

---

**Q5:** How to find previous greater instead of next?

**A:** Process array right-to-left instead of left-to-right. Same logic, opposite direction.

---

**Q6:** What problems use monotonic stack pattern?

**A:** Next greater/smaller, largest rectangle histogram, trapping rain water, stock span, daily temperatures, etc.

---

**Q7:** How is stack monotonicity maintained?

**A:** Before adding new element, pop all elements that violate monotonicity. Then add new element. This maintains property.

---

## PART 4: README

**90-Minute Study Guide:**
1. The Why (10 min): Understand next greater problem
2. The What (15 min): Monotonic stack concept
3. The How (15 min): Stack mechanics
4. Visualization (20 min): Trace examples
5. Quick Summary (5 min): Key points
6. Questions (15 min): Test understanding

**Key Skill:** Recognize next-greater problems, implement monotonic stack

**Practice:** Next greater element, trapping rain water, histogram

**Connection:** Unique pattern not in Week 4. Enables many medium/hard problems!

---

**Status:** ✅ Day 2 Complete | **Next:** Day 3 - Merge Operations

