# 📘 WEEK 1 DAY 3: RECURSION I - Complete Learning Package

**Week 1, Day 3: Understanding Recursion Fundamentals**

Generated: 2025-12-26 | Duration: 90 minutes | Difficulty: 🟡 Medium | Target: 4-5/5

---

## PART 1: MAIN CONTENT

### 1️⃣ The Why

**Problem:** How do you solve a problem that's defined in terms of itself?

Real-world:
- **File systems:** A folder contains folders (recursive structure)
- **Tree traversal:** Visit root, then recursively visit children
- **Parsing:** Expressions contain expressions (JSON, code)
- **Backtracking:** Try option, recurse, undo if fails
- **Divide-and-conquer:** Break problem in half, solve each half

**Without recursion:** Manually manage stack with loops (verbose, error-prone)

**With recursion:** Elegant solution that mirrors problem structure

---

### 2️⃣ The What: Mental Model

**Core Idea:** Function calls itself to solve smaller version of problem

**Example: Factorial**
```
5! = 5 × 4!
4! = 4 × 3!
3! = 3 × 2!
2! = 2 × 1!
1! = 1 (base case - stop!)
```

**Required Elements:**

1. **Base case:** Simplest version with known answer (MUST have!)
2. **Recursive case:** Call self on smaller problem
3. **Progress:** Each call must get closer to base case

**Memory Model: Call Stack**

```
factorial(5)
  → 5 * factorial(4)
    → 4 * factorial(3)
      → 3 * factorial(2)
        → 2 * factorial(1)
          → 1 (base case)
        ← return 1
      ← return 2*1=2
    ← return 3*2=6
  ← return 4*6=24
← return 5*24=120

Stack at deepest:
[factorial(5), factorial(4), factorial(3), factorial(2), factorial(1)]
```

---

### 3️⃣ The How: Mechanics

**Execution Model:**

```
1. Call function with argument n
2. Check base case: Is this the simplest version?
   YES → Return known answer
   NO → Continue
3. Call function recursively on smaller problem
4. Wait for recursive call to return
5. Use returned value in computation
6. Return result to caller
```

**Stack Frame Details:**

```
Each function call creates a frame:
┌─────────────────────┐
│ Function name       │
│ Local variables     │
│ Return address      │
│ Arguments           │
└─────────────────────┘

For factorial(3):
Frame: factorial(3)
  n = 3
  return address = statement after call
  local: result of factorial(2)
  
Frame: factorial(2)
  n = 2
  return address = statement after call
  local: result of factorial(1)
  
Frame: factorial(1)
  n = 1
  return address = statement after call
  BASE CASE: return 1
```

---

### 4️⃣ Visualization: Examples

**Example 1: Sum of Array**

```python
def sum_array(arr, index):
    if index == len(arr):          # Base case
        return 0
    else:
        return arr[index] + sum_array(arr, index+1)

# Trace: sum_array([2, 3, 4], 0)
#   2 + sum_array([2,3,4], 1)
#     3 + sum_array([2,3,4], 2)
#       4 + sum_array([2,3,4], 3)
#         0 (base case)
#       = 4 + 0 = 4
#     = 3 + 4 = 7
#   = 2 + 7 = 9
```

**Example 2: Counting Down**

```python
def countdown(n):
    if n <= 0:                    # Base case
        print("Blastoff!")
    else:
        print(n)
        countdown(n-1)            # Recursive call with n-1

# countdown(3):
#   Print 3
#   countdown(2):
#     Print 2
#     countdown(1):
#       Print 1
#       countdown(0):
#         Print "Blastoff!"
```

---

### 5️⃣ Critical Analysis

| Aspect | Value |
|--------|-------|
| Time | Depends on recursion depth × work per call |
| Space | O(depth) for call stack |
| Best for | Recursive structures (trees, lists) |
| Worst for | Exponential branching (naive fibonacci) |

**Complexity Analysis:**

```
Linear recursion: T(n) = T(n-1) + 1 = O(n)
  Example: countdown, array sum

Multiple recursion: T(n) = 2·T(n-1) = O(2^n)
  Example: naive fibonacci, all subsets
  
Logarithmic recursion: T(n) = T(n/2) + 1 = O(log n)
  Example: binary search
```

---

### 6️⃣ Real Systems

**Tree Traversal:**
```
File system: List all files in directory recursively
  def list_files(path):
      if is_file(path): return [path]
      else:
          results = []
          for child in list_directory(path):
              results.extend(list_files(child))
          return results
```

**JSON Parsing:**
```
Parse nested JSON: Value can be string, number, or object/array containing values
  def parse_value():
      if see_string(): return parse_string()
      if see_number(): return parse_number()
      if see_object(): return parse_object()
        # parse_object() calls parse_value() recursively!
```

---

### 7️⃣ Connections

**Builds on:** Day 1 (RAM model explains stack), Day 2 (complexity analysis)

**Enables:** Days 4 (advanced recursion), Week 5+ (tree/graph algorithms)

---

### 8️⃣ Mathematics

**Recurrence Relation:** T(n) = a·T(n-k) + f(n)

Solve using:
- Substitution method
- Recursion tree
- Master theorem (Day 2)

---

### 9️⃣ Design Intuition

**Use recursion when:**
- Problem is recursive (trees, graphs, parsing)
- Problem requires backtracking
- Divide-and-conquer structure

**Avoid when:**
- Problem is naturally iterative
- Deep recursion (> 10,000 levels) risks stack overflow

---

### 🔟 Knowledge Check

1. What's a base case and why is it required?
2. Trace recursive fibonacci(4)
3. What's stack overflow and when does it occur?
4. Derive Big-O for T(n) = T(n-1) + n

### 1️⃣1️⃣ Hooks

**One-liner:** "Recursion breaks problem into smaller versions until reaching base case."

**Story:** "Every recursive call is one step down mountain. Base case is mountain bottom. Return is climbing back up."

---

## PART 2: QUICK SUMMARY

**Recursion Essentials:**
- Base case: Simplest version, known answer
- Recursive case: Call self on smaller problem
- Stack: Each call allocates frame, returns from deepest first

**Common Patterns:**
- Linear: T(n) = T(n-1) + O(1) = O(n)
- Exponential: T(n) = k·T(n-1) = O(k^n)
- Logarithmic: T(n) = T(n/2) = O(log n)

**Debugging:** Print when entering and exiting to see call stack

---

## PART 3: QUESTIONS & ANSWERS

**Q1:** What happens if you forget the base case?
**A:** Infinite recursion → Stack overflow → Crash

**Q2:** Trace sum([1,2,3]) with recursion
**A:** 1+sum([2,3]) → 1+2+sum([3]) → 1+2+3+sum([]) → 1+2+3+0 = 6

**Q3:** Compare recursive vs iterative sum
**A:** Recursion: O(n) time, O(n) space. Iterative: O(n) time, O(1) space. Iterative better!

**Q4:** What's stack depth for factorial(100)?
**A:** 100 frames (one per call). Safe (typically 10K+ stack depth available)

**Q5:** Why do programmers avoid deep recursion?
**A:** Limited stack size. n > 10,000 risks stack overflow on most systems.

**Q6:** Derive T(n) for: T(n) = 2·T(n-1) + 1
**A:** Unwinds to sum of powers of 2 = O(2^n) (exponential!)

**Q7:** When is recursion actually faster than iteration?
**A:** Rarely. Same big-O but recursion has function call overhead. Use for clarity, not speed.

---

## PART 4: README

**Study Plan (90 min):**
- Why (15 min): Understand motivation
- What (15 min): Mental model of stack
- How (15 min): Trace execution by hand
- Visualization (15 min): Deeply trace examples
- Rest (10 min): Analysis + concepts

**Key Skill:** Trace recursion by hand multiple times

**Confidence Check:** Can you trace any recursive function on paper?

---

**Status:** ✅ Complete | **Next:** Day 4 - Recursion II

