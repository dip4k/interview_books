# 🧠 DSA Deep-Dive: Week 1, Day 3
## Recursion I: The Call Stack, Base Cases, and Stack Overflow Mechanics

---

## 1. The "Why" (Engineering Motivation)

You're debugging a Python application that crashes with:
```
RecursionError: maximum recursion depth exceeded
```

But the code looks simple:
```python
def process_file(filename):
    file = read_file(filename)
    if not file.is_empty():
        # Process the file...
        next_filename = file.get_next()
        return process_file(next_filename)  # Recursive call
    return None
```

You test with 100 files—works fine. You deploy to production with 500,000 files—**crashes instantly**.

**Why?** The function calls itself recursively. Each call adds a "frame" to the **call stack**. With 500,000 files, you need 500,000 frames. The call stack has a size limit (typically 8MB on Linux). Each frame is ~24 bytes.

**The math:** 8MB / 24 bytes per frame = ~349,525 frames maximum.

At 500,000 files, you exceed this limit. **Stack overflow.**

This is not a bug in your code. It's a **fundamental property of how computers work**. Understanding the call stack is the difference between code that works and code that crashes at scale.

---

## 2. The Mental Model (The "What")

Imagine a **stack of dinner plates** at a restaurant.

**A regular function call:**
```
Initial state (empty stack):
(nothing)

Call function_A():
┌─────────────┐
│ function_A  │ ← New plate added (frame pushed)
└─────────────┘

Call function_B() from inside function_A():
┌─────────────┐
│ function_B  │ ← New plate added
├─────────────┤
│ function_A  │
└─────────────┘

Call function_C() from inside function_B():
┌─────────────┐
│ function_C  │ ← New plate added
├─────────────┤
│ function_B  │
├─────────────┤
│ function_A  │
└─────────────┘

Return from function_C():
┌─────────────┐
│ function_B  │ ← function_C plate removed
├─────────────┤
│ function_A  │
└─────────────┘
```

**Recursion is the same stack, but the same function appears multiple times:**
```
Call factorial(5):
┌─────────────────────┐
│ factorial(5)        │
└─────────────────────┘

Calls factorial(4):
┌─────────────────────┐
│ factorial(4)        │
├─────────────────────┤
│ factorial(5)        │
└─────────────────────┘

Calls factorial(3):
┌─────────────────────┐
│ factorial(3)        │
├─────────────────────┤
│ factorial(4)        │
├─────────────────────┤
│ factorial(5)        │
└─────────────────────┘

Calls factorial(2):
┌─────────────────────┐
│ factorial(2)        │
├─────────────────────┤
│ factorial(3)        │
├─────────────────────┤
│ factorial(4)        │
├─────────────────────┤
│ factorial(5)        │
└─────────────────────┘

Calls factorial(1):
┌─────────────────────┐
│ factorial(1)        │
├─────────────────────┤
│ factorial(2)        │
├─────────────────────┤
│ factorial(3)        │
├─────────────────────┤
│ factorial(4)        │
├─────────────────────┤
│ factorial(5)        │
└─────────────────────┘

Base case reached! factorial(1) = 1
Now unwind: remove plates one by one until stack is empty
```

**The key insight:** Each function call is a "plate" (frame). The stack can only hold so many plates before running out of space. Recursion is just adding many frames of the same function.

---

## 3. Under the Hood (The "How")

### 3.1 What is a Stack Frame?

When a function is called, the CPU does the following:

1. **Allocate space on the stack** - Typically ~24 bytes (varies by architecture)
2. **Store the return address** - "Where do I go after this function finishes?"
3. **Store local variables** - All variables declared in the function
4. **Store function parameters** - Arguments passed to the function
5. **Save CPU registers** - Preserve state so we can restore it later

**Example: Stack frame for `int factorial(int n)`**

```
┌──────────────────────────────────────┐
│ Stack Frame for factorial(5)         │
├──────────────────────────────────────┤
│ Return address:    0x7FFF1234 (addr) │ 8 bytes
│ n (parameter):     5 (int)           │ 4 bytes
│ local_result (var):uninitialized     │ 4 bytes
│ Saved RBP (frame): 0x7FFF5678        │ 8 bytes
├──────────────────────────────────────┤
│ TOTAL:             ~24 bytes         │
└──────────────────────────────────────┘
```

### 3.2 The Call Stack in Memory

The **call stack is a contiguous region of memory** managed by the operating system.

```
High Memory Address (0x7FFFFFFF):
┌─────────────────────────────────────┐
│ factorial(1) frame                  │ ← Top of stack
│ └─ return addr, n=1, local_result   │   (most recent call)
├─────────────────────────────────────┤
│ factorial(2) frame                  │
│ └─ return addr, n=2, local_result   │
├─────────────────────────────────────┤
│ factorial(3) frame                  │
│ └─ return addr, n=3, local_result   │
├─────────────────────────────────────┤
│ factorial(4) frame                  │
│ └─ return addr, n=4, local_result   │
├─────────────────────────────────────┤
│ factorial(5) frame                  │
│ └─ return addr, n=5, local_result   │ ← Base of recursion
├─────────────────────────────────────┤
│ main() frame                        │
│ └─ return addr, local variables     │ ← Original call
├─────────────────────────────────────┤
│ ... more stack space ...            │
├─────────────────────────────────────┤
│ STACK LIMIT (8MB on Linux)          │
└─────────────────────────────────────┘

Low Memory Address (0x00000000):
(Unused)
```

**The stack pointer (RSP on x64) always points to the top of the stack.**

When you call a function:
- RSP moves UP (to higher addresses)
- New frame is allocated

When a function returns:
- RSP moves DOWN (to lower addresses)
- Frame is deallocated (no explicit free needed!)

### 3.3 The Base Case: The Only Way Out

**Without a base case, recursion is infinite:**

```python
def infinite():
    return infinite()  # Calls itself forever!
```

Every call adds a frame. No frames are removed. Eventually, you run out of stack space.

**With a base case, recursion terminates:**

```python
def factorial(n):
    if n == 1:           # BASE CASE
        return 1         # Return a value, don't call recursively
    else:                # RECURSIVE CASE
        return n * factorial(n - 1)  # Call with simpler problem
```

**The base case must be:**
1. **Reachable** - Not `if n < -100: return 1` when n is always positive
2. **Correct** - Return the right value for the simplest case
3. **Terminating** - Guarantee that each recursive call gets closer to the base case

---

## 4. Visual Walkthrough (The Simulation)

Let's trace `factorial(4)` step-by-step.

### Step 1: Call factorial(4)
```
Code: factorial(4)

Call Stack:
┌─────────────────────────┐
│ factorial(4)            │
│ n = 4                   │
│ (not yet computed)      │
└─────────────────────────┘

Current PC (Program Counter): Start of factorial function
Next: Check if n == 1?
```

### Step 2: Check base case
```
Code: if n == 1:
      Is 4 == 1? NO

Action: Execute recursive case
Next: Call factorial(n-1) = factorial(3)
```

### Step 3: Call factorial(3) (recursive)
```
Code: return 4 * factorial(3)

Call Stack (factorial(4) is paused, waiting):
┌─────────────────────────┐
│ factorial(3)            │
│ n = 3                   │ ← New frame pushed
│ (not yet computed)      │
├─────────────────────────┤
│ factorial(4)            │
│ n = 4                   │
│ waiting for: 4 * result │
└─────────────────────────┘

Current PC: Start of factorial function
Next: Check if n == 1?
```

### Step 4: Check base case
```
Code: if n == 1:
      Is 3 == 1? NO

Action: Execute recursive case
Next: Call factorial(2)
```

### Step 5: Call factorial(2) (recursive)
```
Call Stack:
┌─────────────────────────┐
│ factorial(2)            │
│ n = 2                   │
├─────────────────────────┤
│ factorial(3)            │
│ n = 3                   │
│ waiting for: 3 * result │
├─────────────────────────┤
│ factorial(4)            │
│ n = 4                   │
│ waiting for: 4 * result │
└─────────────────────────┘

Next: Check if n == 1?
```

### Step 6: Check base case
```
Code: if n == 1:
      Is 2 == 1? NO

Action: Execute recursive case
Next: Call factorial(1)
```

### Step 7: Call factorial(1) (recursive)
```
Call Stack:
┌─────────────────────────┐
│ factorial(1)            │
│ n = 1                   │
├─────────────────────────┤
│ factorial(2)            │
│ n = 2                   │
│ waiting for: 2 * result │
├─────────────────────────┤
│ factorial(3)            │
│ n = 3                   │
│ waiting for: 3 * result │
├─────────────────────────┤
│ factorial(4)            │
│ n = 4                   │
│ waiting for: 4 * result │
└─────────────────────────┘

Next: Check if n == 1?
```

### Step 8: BASE CASE REACHED!
```
Code: if n == 1:
      Is 1 == 1? YES!

Action: return 1
Result: factorial(1) = 1

Call Stack (factorial(1) frame removed):
┌─────────────────────────┐
│ factorial(2)            │
│ n = 2                   │
│ waiting for: 2 * ?      │ ← Got ? = 1
│ Computing: 2 * 1 = 2    │
├─────────────────────────┤
│ factorial(3)            │
│ n = 3                   │
│ waiting for: 3 * result │
├─────────────────────────┤
│ factorial(4)            │
│ n = 4                   │
│ waiting for: 4 * result │
└─────────────────────────┘

Next: Return 2 from factorial(2)
```

### Step 9: Unwind - factorial(2) returns
```
Code: return 2 * 1
Result: factorial(2) = 2

Call Stack (factorial(2) frame removed):
┌─────────────────────────┐
│ factorial(3)            │
│ n = 3                   │
│ waiting for: 3 * ?      │ ← Got ? = 2
│ Computing: 3 * 2 = 6    │
├─────────────────────────┤
│ factorial(4)            │
│ n = 4                   │
│ waiting for: 4 * result │
└─────────────────────────┘

Next: Return 6 from factorial(3)
```

### Step 10: Unwind - factorial(3) returns
```
Code: return 3 * 2
Result: factorial(3) = 6

Call Stack (factorial(3) frame removed):
┌─────────────────────────┐
│ factorial(4)            │
│ n = 4                   │
│ waiting for: 4 * ?      │ ← Got ? = 6
│ Computing: 4 * 6 = 24   │
└─────────────────────────┘

Next: Return 24 from factorial(4)
```

### Step 11: Final return - factorial(4) returns
```
Code: return 4 * 6
Result: factorial(4) = 24

Call Stack (all frames removed):
(empty)

FINAL ANSWER: factorial(4) = 24
```

**Key observations from the walkthrough:**

1. **Call phase (going down):** Each call adds a frame. We keep going until we hit the base case.
2. **Return phase (coming back up):** Each return removes a frame. We compute the result using the value from the deeper call.
3. **Stack grows then shrinks:** The maximum stack depth is reached at the base case (deepest recursion).
4. **No explicit cleanup:** Frames are automatically removed when functions return.

---

## 5. Critical Analysis

### 5.1 Stack Overflow: When Recursion Fails

**Maximum recursion depth calculation:**

```
Stack size:      8MB = 8,388,608 bytes (Linux default)
Frame size:      24 bytes (typical)
Max depth:       8,388,608 / 24 = 349,525 frames

If recursion depth > 349,525: STACK OVERFLOW
```

**Real examples:**

Example 1: Processing a linked list
```python
def process_list(node):
    if node is None:
        return
    process_node(node)
    process_list(node.next)  # Linear recursion

# With 1 million nodes:
# Depth = 1,000,000
# Max safe = 349,525
# Result: STACK OVERFLOW!
```

Example 2: Tree traversal
```python
def traverse_tree(node):
    if node is None:
        return
    traverse_tree(node.left)
    traverse_tree(node.right)

# With a balanced tree of 1M nodes:
# Depth = log₂(1M) ≈ 20
# Max safe = 349,525
# Result: SAFE! Tree recursion is fine.
```

Example 3: Pathological input
```python
def process_list(node):
    if node is None:
        return
    process_list(node.next)

# With a degenerate linked list (1M nodes):
# Worst case depth = 1,000,000
# This will overflow!

# Solution: Use iteration instead
def process_list_iterative(head):
    node = head
    while node is not None:
        process_node(node)
        node = node.next
    # Stack depth = 0 (constant!)
```

### 5.2 Time Complexity of Recursion

**Time depends on two factors:**
1. **Number of function calls** - How many times is the function called?
2. **Work per call** - How much work is done in each call?

**Total time = (Number of calls) × (Work per call)**

**Example: Linear recursion**
```python
def sum_list(arr, i):
    if i == len(arr):
        return 0
    return arr[i] + sum_list(arr, i+1)

# Number of calls: n (one per element)
# Work per call: O(1)
# Total: O(n) × O(1) = O(n)
```

**Example: Binary recursion**
```python
def fibonacci(n):
    if n <= 1:
        return n
    return fibonacci(n-1) + fibonacci(n-2)

# Number of calls: 2^n (exponential!)
#   fibonacci(5) calls:
#   - fibonacci(4) + fibonacci(3)
#   - fibonacci(4) calls fibonacci(3) + fibonacci(2)
#   - fibonacci(3) is called multiple times!
#
# Work per call: O(1)
# Total: O(2^n)
```

---

## 6. System Connection

### How the OS Manages Call Stacks

**Linux/Unix implementation:**

```
Process Memory Layout:
┌─────────────────────────────────┐
│ Text (executable code)          │ Read-only
├─────────────────────────────────┤
│ Data (global variables)         │ Read-write
├─────────────────────────────────┤
│ Heap (malloc'd memory)          │ ↓ growing down
├─────────────────────────────────┤
│       (unused space)            │
├─────────────────────────────────┤
│ Stack (local variables)         │ ↑ growing up
└─────────────────────────────────┘

Stack grows UP as you make function calls.
Heap grows DOWN as you malloc.

When stack meets heap: CRASH (rarely happens in practice)
When stack exceeds limit: STACK OVERFLOW
```

**Thread stacks in Linux:**

Each thread gets its own stack (default 8MB on 64-bit Linux):
```bash
$ ulimit -s
8192
# This is in KB, so 8192 * 1024 = 8,388,608 bytes = 8MB
```

You can increase it:
```bash
$ ulimit -s 16384  # 16MB stack
```

**But this is a band-aid, not a solution.**

### Real-World System: Python's Recursion Limit

Python has a built-in recursion limit to prevent stack overflow:

```python
import sys
print(sys.getrecursionlimit())  # Usually 1000

# Don't do this in production!
sys.setrecursionlimit(10000)
```

**Why 1000 instead of 349,525?**
- Python frames are larger than C frames (~300 bytes vs 24 bytes)
- Python reserves some stack space
- 1000 is a reasonable default that rarely causes issues

---

## 7. Knowledge Check

**Question:** You have a recursive function that needs to process 1 million items in a linked list (depth = 1 million). The default stack size is 8MB. Assume each frame is 24 bytes.

**Your tasks:**

1. **Calculate:** How many frames fit in 8MB?
   - Answer: _______________

2. **Predict:** Will the function stack overflow?
   - Answer: YES / NO
   - Reasoning: _______________

3. **Calculate:** How much stack space would you need?
   - Answer: _______________

4. **Solution:** What are three ways to fix this?
   - Solution 1: _______________
   - Solution 2: _______________
   - Solution 3: _______________

5. **Deep thinking:** Why does tree recursion (depth ≈ 20) work fine but linked list recursion (depth = 1M) fails? What's the fundamental difference?
   - Answer: _______________

---

## Summary: Day 3 Core Concepts

**The Call Stack:**
- Each function call adds a "frame" to the stack
- Frames are ~24 bytes (varies by architecture)
- Stack is LIFO (Last In, First Out)
- Stack has a size limit (8MB typical)

**Recursion Requirements:**
1. **Base case** - When to stop recursing
2. **Recursive case** - How to break the problem down
3. **Progress toward base case** - Each call must get closer to base case

**Recursion Mechanics:**
1. **Call phase** - Add frames to stack (recursive calls)
2. **Return phase** - Remove frames from stack (unwinding)
3. **Stack grows then shrinks** - Maximum depth matters

**Recursion Limitations:**
- **Depth limit** - Maximum concurrent frames on stack
- **Time complexity** - Can be exponential if not careful
- **Space complexity** - O(recursion depth), which can be O(n)

**When to Use Recursion:**
- ✅ Trees and graphs (depth usually log n or similar)
- ✅ Divide-and-conquer (depth grows logarithmically)
- ✅ Natural recursive structures
- ✅ Code is much clearer than iterative alternative

**When to Avoid Recursion:**
- ❌ Linear data structures (arrays, linked lists)
- ❌ When depth could exceed stack limit
- ❌ When simpler iterative solution exists
- ❌ Performance is critical (function call overhead)

---

**End of Day 3: Recursion I Deep-Dive**
