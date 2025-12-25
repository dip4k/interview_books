# 🎓 Week 1, Days 3-4: Recursion Deep-Dive
## Practice Exercises, Cheat Sheets, and Socratic Questions

---

## PART 1: RECURSION I - CORE EXERCISES

### Exercise 1.1: Call Stack Mechanics

**Problem:** Trace the call stack for this function:

```python
def countdown(n):
    if n == 0:           # BASE CASE
        return "Blastoff!"
    print(n)
    return countdown(n - 1)
```

**Your task:** Assume each frame is 24 bytes. Stack size is 8MB.

A. **Trace the call stack for countdown(3)**
   - Show the stack state at each step (before/after each call)
   - Show maximum stack depth
   - Answer: _______________

B. **Calculate maximum recursion depth before overflow**
   - Formula: Stack size / Frame size
   - Answer: _______________

C. **For countdown(500,000), will this overflow?**
   - Answer: YES / NO
   - Reasoning: _______________

D. **What's the time complexity?**
   - Answer: _______________
   - Reasoning: _______________

E. **What's the space complexity?**
   - Answer: _______________
   - Reasoning: _______________

---

**Solution 1.1:**

**Part A: Call Stack Trace for countdown(3)**

```
Step 1: Call countdown(3)
┌──────────────────┐
│ countdown(3)     │
└──────────────────┘

Step 2: Check base case (3 == 0? NO) → Call countdown(2)
┌──────────────────┐
│ countdown(2)     │
├──────────────────┤
│ countdown(3)     │
└──────────────────┘

Step 3: Check base case (2 == 0? NO) → Call countdown(1)
┌──────────────────┐
│ countdown(1)     │
├──────────────────┤
│ countdown(2)     │
├──────────────────┤
│ countdown(3)     │
└──────────────────┘

Step 4: Check base case (1 == 0? NO) → Call countdown(0)
┌──────────────────┐
│ countdown(0)     │
├──────────────────┤
│ countdown(1)     │
├──────────────────┤
│ countdown(2)     │
├──────────────────┤
│ countdown(3)     │
└──────────────────┘

Step 5: BASE CASE! (0 == 0? YES) → return "Blastoff!"
┌──────────────────┐
│ countdown(1)     │ ← countdown(0) removed
├──────────────────┤
│ countdown(2)     │
├──────────────────┤
│ countdown(3)     │
└──────────────────┘

Step 6: Unwinding
┌──────────────────┐
│ countdown(2)     │ ← countdown(1) removed
├──────────────────┤
│ countdown(3)     │
└──────────────────┘

Step 7: Final unwind
┌──────────────────┐ (empty)
```

Maximum stack depth: 4 frames (when at countdown(0))
Total space used: 4 × 24 = 96 bytes

---

**Part B: Maximum Recursion Depth**

```
Stack size:     8MB = 8,388,608 bytes
Frame size:     24 bytes
Max depth:      8,388,608 / 24 = 349,525 frames

Answer: 349,525 frames maximum
```

---

**Part C: Will countdown(500,000) overflow?**

```
Required depth: 500,000
Max safe depth: 349,525

Answer: YES, this will overflow
Reasoning: 500,000 > 349,525, so the stack fills completely
```

---

**Part D: Time Complexity**

```
Function is called once per number from n to 0
Total calls: n + 1 (for n, n-1, ..., 1, 0)
Work per call: O(1) (just a print statement)
Total time: O(n)
```

---

**Part E: Space Complexity**

```
Stack depth: n (maximum concurrent frames)
Each frame: 24 bytes
Total stack space: n × 24 bytes = O(n)

Space complexity: O(n)
```

---

### Exercise 1.2: Base Case Identification

**Problem:** Identify the base case and recursive case for each function:

```python
# Function A
def factorial(n):
    if n == 0 or n == 1:
        return 1
    return n * factorial(n - 1)

# Function B
def print_array(arr, i):
    if i == len(arr):
        return
    print(arr[i])
    print_array(arr, i + 1)

# Function C
def sum_digits(n):
    if n == 0:
        return 0
    return (n % 10) + sum_digits(n // 10)
```

**Your task:**

For each function, identify:

A. **Base case:** _______________
B. **Recursive case:** _______________
C. **What problem are we solving?** _______________
D. **Is the function correct?** YES / NO (explain why or why not)
E. **What's the recursion depth for this input?** _______________

---

**Solution 1.2:**

**Function A: factorial(n)**
- Base case: `if n == 0 or n == 1: return 1`
- Recursive case: `return n * factorial(n - 1)`
- Problem: Calculate n! (n factorial)
- Correct: YES (base case properly handled, progress toward base case)
- Depth for n=5: 5 levels (5, 4, 3, 2, 1, 0)

**Function B: print_array(arr, i)**
- Base case: `if i == len(arr): return`
- Recursive case: Print element, then call with i+1
- Problem: Print all array elements
- Correct: YES (terminates when i reaches array length)
- Depth for array of size 10: 10 levels

**Function C: sum_digits(n)**
- Base case: `if n == 0: return 0`
- Recursive case: `return (n % 10) + sum_digits(n // 10)`
- Problem: Sum all digits in a number (e.g., 123 → 1+2+3=6)
- Correct: YES (n //= 10 each call, eventually reaches 0)
- Depth for n=12345: 5 levels (5 digits)

---

### Exercise 1.3: Stack Overflow Detection

**Problem:** You have a function that processes a linked list recursively:

```python
class Node:
    def __init__(self, val, next=None):
        self.val = val
        self.next = next

def process_list(node):
    if node is None:
        return
    process_node(node)
    process_list(node.next)
```

**Your task:**

A. **What's the recursion depth for a linked list of 1,000,000 nodes?**
   - Answer: _______________

B. **Max safe recursion depth (from previous calculation)?**
   - Answer: _______________

C. **Will this overflow?**
   - Answer: YES / NO

D. **Fix this problem WITHOUT using recursion (write pseudocode)**
   - Answer: _______________

E. **Fix this problem WHILE KEEPING recursion (what technique?)**
   - Answer: _______________

---

**Solution 1.3:**

A. **Recursion depth for linked list of 1,000,000 nodes?**
   - Answer: 1,000,000 (one frame per node)

B. **Max safe depth?**
   - Answer: 349,525 frames

C. **Will this overflow?**
   - Answer: YES (1,000,000 > 349,525)

D. **Non-recursive solution (iteration):**
   ```
   node = head
   while node != null:
       process_node(node)
       node = node.next
   
   Stack depth: O(1) constant
   This avoids the problem entirely!
   ```

E. **Keep recursion, fix the overflow:**
   - **Tail call optimization:** Some languages (not Python) optimize this
   - **Increase stack size:** `ulimit -s 16384` (temporary fix)
   - **Hybrid approach:** Process 1000 nodes iteratively, then recurse
   
   But the real answer: **Use iteration instead. Recursion is the wrong tool here.**

---

## PART 2: RECURSION II - RECURSION TREES

### Exercise 2.1: Drawing Recursion Trees

**Problem:** Draw the recursion tree for this function with the given input:

```python
def multiply(a, b):
    if b == 0:
        return 0
    return a + multiply(a, b - 1)
```

**Input:** multiply(3, 4)

**Your task:**

A. **Draw the complete recursion tree**
   - Show each node (function call)
   - Show return values at each node
   - Show height and width

B. **Count total function calls**
   - Answer: _______________

C. **Trace the execution:**
   - Show the order calls are made (call sequence)
   - Show the order results come back (return sequence)

D. **Time complexity:**
   - Answer: _______________
   - Reasoning: _______________

E. **Space complexity:**
   - Answer: _______________
   - Reasoning: _______________

---

**Solution 2.1:**

A. **Recursion tree for multiply(3, 4):**

```
                    multiply(3, 4)
                          │
                    3 + multiply(3, 3)
                          │
                    3 + multiply(3, 2)
                          │
                    3 + multiply(3, 1)
                          │
                    3 + multiply(3, 0)
                          │
                        [BASE]
                       return 0

Reading upward (unwinding):
multiply(3, 0) = 0
multiply(3, 1) = 3 + 0 = 3
multiply(3, 2) = 3 + 3 = 6
multiply(3, 3) = 3 + 6 = 9
multiply(3, 4) = 3 + 9 = 12
```

Height: 5 (linear)
Width: 1 (linear)

B. **Total function calls:**
   - Answer: 5 calls (one per number from 4 to 0)

C. **Call and return sequences:**

   **Call sequence (downward):**
   - multiply(3, 4)
   - multiply(3, 3)
   - multiply(3, 2)
   - multiply(3, 1)
   - multiply(3, 0) [base case]

   **Return sequence (upward):**
   - multiply(3, 0) → 0
   - multiply(3, 1) → 3
   - multiply(3, 2) → 6
   - multiply(3, 3) → 9
   - multiply(3, 4) → 12

D. **Time complexity:**
   - Answer: O(b) where b is the second parameter
   - Reasoning: Called once for each decrement from b to 0

E. **Space complexity:**
   - Answer: O(b)
   - Reasoning: Maximum stack depth is b frames

---

### Exercise 2.2: Overlapping Subproblems

**Problem:** Count function calls for fibonacci(6):

```python
def fibonacci(n):
    if n <= 1:
        return n
    return fibonacci(n-1) + fibonacci(n-2)
```

**Your task:**

A. **Draw the recursion tree for fibonacci(6)**
   - Show all nodes
   - Label duplicate calculations

B. **Count total calls:**
   - Answer: _______________

C. **Count unique subproblems:**
   - Answer: _______________

D. **With memoization, how many calls would you make?**
   - Answer: _______________

E. **Speedup from memoization?**
   - Answer: _______________x faster

---

**Solution 2.2:**

A. **Recursion tree for fibonacci(6):**

```
                        fib(6)
                       /      \
                    fib(5)    fib(4)
                   /    \     /    \
                fib(4) fib(3) fib(3) fib(2)
               /  \    / \    / \    / \
            fib(3) fib(2) ... (many more)
```

Notice fib(4) appears twice, fib(3) appears multiple times, etc.

B. **Total calls:**
   - fib(6): 1 call
   - fib(5), fib(4): 2 calls
   - fib(4), fib(3), fib(3): 3 calls (fib(4) again!)
   - More branches...
   
   Without drawing completely: ~25 total calls
   (This is approximately 2^n / sqrt(n) ≈ 2^5 ≈ 25)

C. **Unique subproblems:**
   - {0, 1, 2, 3, 4, 5, 6}
   - Answer: 7 unique values

D. **With memoization:**
   - One call per unique subproblem
   - Answer: 7 calls

E. **Speedup:**
   - Answer: ~3.5x faster (25 → 7 calls)
   - For fib(20): 10,946 calls → 21 calls (521x faster!)

---

### Exercise 2.3: Time vs. Space Trade-offs

**Problem:** Compare these two approaches:

```python
# Approach 1: Naive recursion
def power(base, exp):
    if exp == 0:
        return 1
    return base * power(base, exp - 1)

# Approach 2: Optimized recursion
def power_optimized(base, exp):
    if exp == 0:
        return 1
    if exp % 2 == 0:
        half = power_optimized(base, exp // 2)
        return half * half
    else:
        return base * power_optimized(base, exp - 1)
```

**Your task:**

A. **Time complexity of Approach 1:**
   - Answer: _______________
   - For base=2, exp=64: _____ calls

B. **Time complexity of Approach 2:**
   - Answer: _______________
   - For base=2, exp=64: _____ calls

C. **Space complexity of both:**
   - Approach 1: _______________
   - Approach 2: _______________

D. **When is Approach 2 worth the added complexity?**
   - Answer: _______________

E. **What's the underlying optimization technique?**
   - Answer: _______________

---

**Solution 2.3:**

A. **Approach 1 time complexity:**
   - Answer: O(exp)
   - For exp=64: 64 calls

B. **Approach 2 time complexity:**
   - Answer: O(log exp) - divides exp by 2 each time
   - For exp=64: log₂(64) = 6 calls

C. **Space complexity:**
   - Approach 1: O(exp) - stack depth = exp
   - Approach 2: O(log exp) - stack depth = log exp

D. **When is Approach 2 worth it?**
   - When exp is large (>1000)
   - When performance matters (banking, cryptography)
   - The added complexity is worth it for exponential speedup

E. **Underlying technique:**
   - Answer: **Exponentiation by squaring** (also called fast exponentiation)
   - Key insight: 2^64 = (2^32)^2 = ((2^16)^2)^2 = ... (only 6 squarings!)

---

## PART 3: SOCRATIC QUESTIONS (Deep Understanding)

### Socratic Question 1: "Why does recursion work?"

**Prompt:** Explain why recursion works at all. Why doesn't the function get confused calling itself?

**Expected answer components:**
- The call stack maintains separate frames for each call
- Each frame has its own local variables
- Return addresses allow the CPU to know where to go after each return
- The OS manages the stack automatically (no manual cleanup needed)

**Follow-up:** "If each call is independent, how does the result from a recursive call affect the current call?"

**Expected answer:** The return value from the recursive call is used in the current call's computation. The key is that we wait for the recursive call to return before using its value.

---

### Socratic Question 2: "When should you use recursion instead of iteration?"

**Prompt:** You need to process all files in a directory tree. Should you use recursion or iteration? Defend your choice.

**Expected answer framework:**
1. **Natural fit:** Directory trees are naturally recursive
2. **Depth is safe:** Directory depth is typically < 20 (well under 349,525 limit)
3. **Code clarity:** Recursive code is cleaner and more maintainable
4. **Performance:** Modern compilers optimize both equally

**Conclusion:** Use recursion here.

**Follow-up:** "Now you need to process 1 million items in a linked list. Should you use recursion or iteration?"

**Expected answer:**
- Linear structure → iteration is better
- Depth would be 1M > 349,525 → iteration is necessary
- Code is simpler with iteration anyway
- Use iteration.

**Key insight:** Recursion is best when depth is small (log n) or code clarity is paramount. Iteration is better for linear structures or deep recursion.

---

### Socratic Question 3: "Can you always convert recursion to iteration?"

**Prompt:** Is it possible to rewrite ANY recursive function as an iterative function? If yes, how? If no, why not?

**Expected answer:** YES, any recursion can be converted to iteration by:
1. Simulating the call stack manually (using an explicit stack data structure)
2. Using a while loop instead of recursion

**Example:**

```
Recursive:
def factorial(n):
    if n <= 1:
        return 1
    return n * factorial(n-1)

Iterative (manual stack):
def factorial_iter(n):
    stack = [n]
    result = 1
    
    while stack:
        current = stack.pop()
        if current <= 1:
            continue
        result *= current
        stack.push(current - 1)
    
    return result
```

**Follow-up:** "If we can always convert to iteration, should we?"

**Expected answer:** NO. Consider:
- Code clarity: Recursion is often clearer
- Performance: Tree traversal is faster with recursion
- Maintainability: Explicit stack management is error-prone
- Only convert to iteration if you're hitting stack limits

---

## PART 4: QUICK REFERENCE - RECURSION CHEAT SHEET

### Maximum Recursion Depth

```
Memory Model:
Stack size: 8MB (typical Linux)
Frame size: 24 bytes (typical x64)

Max depth = 8MB / 24 bytes = 349,525 frames

Data Type: Maximum depth (single element)
- int (4 bytes): 2M elements
- double (8 bytes): 1M elements
- object (24+ bytes): 349K elements
```

### Time Complexity Patterns

```
Pattern              | Complexity | Example
─────────────────────┼────────────┼──────────────
Linear recursion     | O(n)       | factorial(n)
Binary recursion     | O(2^n)     | naive fibonacci
Balanced binary      | O(n)       | tree traversal
Tail recursion       | O(n) space | can optimize to O(1)
Divide-and-conquer   | O(n log n) | merge sort
```

### Recursion vs Iteration Decision Tree

```
Is the problem naturally recursive? (tree, graph, divide-and-conquer)
├─ YES: Will depth exceed 349,525?
│   ├─ NO: Use recursion (cleaner code)
│   └─ YES: Use iteration (safer)
│
└─ NO: Is code much simpler with recursion?
    ├─ YES: Use recursion if depth is safe
    └─ NO: Use iteration
```

---

## Summary: Days 3-4 Core Takeaways

**The Call Stack (Day 3):**
- Each function call adds a frame (24 bytes typical)
- Stack is limited (8MB typical = 349,525 frames max)
- Frames are automatically deallocated on return
- Base case must terminate recursion

**Recursion Trees (Day 4):**
- Visualize all function calls in a tree structure
- Identify overlapping subproblems
- Count total calls and maximum depth
- Analyze time and space complexity

**When to Use Recursion:**
- ✅ Trees, graphs, hierarchical structures
- ✅ Natural recursive problems
- ✅ Code is much clearer
- ✅ Depth is safe (< 349,525)

**When to Avoid Recursion:**
- ❌ Linear data structures (use iteration)
- ❌ Very deep recursion (> 10,000 levels)
- ❌ Exponential subproblems (use memoization or DP)
- ❌ Performance-critical code

**Key Insights:**
1. Stack overflow is **predictable**, not random
2. Recursion depth is limited by **physical memory**
3. Recursion trees reveal **overlapping subproblems**
4. Memoization trades **space for exponential time savings**

---

**End of Days 3-4 Practice & Reference**
