# 🧠 DSA Deep-Dive: Week 1, Day 4
## Recursion II: Visualizing Recursion Trees and Time/Space Trade-offs

---

## 1. The "Why" (Engineering Motivation)

You're optimizing a financial system that calculates portfolio values using this approach:

```python
def calculate_value(portfolio_id):
    # Base case: leaf account has a fixed value
    if is_leaf_account(portfolio_id):
        return get_balance(portfolio_id)
    
    # Recursive case: parent = sum of children
    total = 0
    for child_id in get_children(portfolio_id):
        total += calculate_value(child_id)  # Recursive call
    
    return total
```

**The problem:** This same portfolio hierarchy is processed:
- Once per second (1,000 times/second at large scale)
- Repeatedly calculating the same values

A small portfolio (100 accounts) processes fine. A large portfolio (10,000 accounts structured as a binary tree) takes **8 seconds per calculation** instead of 8 milliseconds.

**Why?** The same account's value is calculated **hundreds of times**. Without memoization, you're doing redundant work exponentially.

**The fix:** Add memoization—cache results so each account's value is calculated only once.

**The insight:** Visualizing the **recursion tree** reveals this problem immediately. The same account ID appears multiple times in the tree. Without visualization, you'd spend hours optimizing the wrong thing.

---

## 2. The Mental Model (The "What")

A **recursion tree** is a visualization of every function call made during a recursive execution.

**Simple analogy: A family tree**

```
                     John (root)
                    /          \
                Sarah           Mike
               /      \       /      \
            Emma    David  Katie    Leo
```

Each person is a "node" (function call). Each parent-child relationship is a function calling itself recursively. The tree shows:
- **Height:** How deep the recursion goes (maximum depth)
- **Width:** How many recursive calls branch out
- **Total nodes:** Total number of function calls made

---

## 3. Under the Hood (The "How")

### 3.1 Building a Recursion Tree

When you execute a recursive function, you can draw the **entire call structure** as a tree.

**Example 1: Linear Recursion**

```python
def sum_array(arr, i):
    if i == len(arr):      # Base case
        return 0
    return arr[i] + sum_array(arr, i+1)  # Recursive case
```

**Recursion tree for sum_array([10, 20, 30], 0):**

```
                    sum_array(arr, 0)
                           │
                           │ arr[0]=10
                           │
                    sum_array(arr, 1)
                           │
                           │ arr[1]=20
                           │
                    sum_array(arr, 2)
                           │
                           │ arr[2]=30
                           │
                    sum_array(arr, 3)
                           │
                      [BASE CASE]
                           │
                        return 0
```

**Tree properties:**
- Height (max depth): 4 (including base case)
- Width (max branching): 1 (linear)
- Total nodes (calls): 4
- Time complexity: O(n) - linear depth × 1 work per call
- Space complexity: O(n) - stack depth is n

---

**Example 2: Binary Recursion**

```python
def fibonacci(n):
    if n <= 1:           # Base case
        return n
    return fibonacci(n-1) + fibonacci(n-2)  # Two recursive calls!
```

**Recursion tree for fibonacci(5):**

```
                          fib(5)
                         /      \
                      fib(4)     fib(3)
                     /     \      /    \
                  fib(3)  fib(2) fib(2) fib(1)
                 /    \    /  \   /  \
            fib(2)  fib(1) fib(1) fib(0) fib(1) fib(0)
           /    \
        fib(1) fib(0)
```

**Count the nodes:**
- fib(5): 1 call
- fib(4), fib(3): 2 calls  
- fib(3), fib(2), fib(2): 3 calls (fib(3) appears twice!)
- fib(2), fib(1), fib(1), fib(0), fib(1), fib(0): 6 calls
- fib(1), fib(0): 2 calls

**Total nodes: 1 + 2 + 3 + 6 + 2 = 15 function calls**

**But how many unique values of n?** Only 6: {0, 1, 2, 3, 4, 5}

**Tree properties:**
- Height: 5 (log₂(n) roughly)
- Width: 2^n at worst (exponential branching)
- Total nodes: ~2^n function calls
- Unique subproblems: n
- Time complexity: O(2^n) - exponential!
- Space complexity: O(n) - maximum depth is n

### 3.2 The Critical Insight: Overlapping Subproblems

Look at the fibonacci tree again. Notice what happens:

```
fib(3) is called 2 times (from fib(5) and fib(4))
fib(2) is called 3 times (from fib(4) twice and fib(3))
fib(1) is called 5 times
fib(0) is called 3 times
```

**You're computing the same values multiple times!**

This is called **overlapping subproblems** - the same problem is solved repeatedly.

**Without memoization:**
```
fib(5): 15 function calls

fib(4): 9 function calls
fib(3): 5 function calls
fib(2): 3 function calls
fib(1): 1 function call
fib(0): 1 function call
```

**With memoization (cache results):**
```
fib(5): Solve once, cached
fib(4): Solve once, cached
fib(3): Solve once, cached
fib(2): Solve once, cached
fib(1): Solve once, cached
fib(0): Solve once, cached

Total: 6 function calls (one per unique n)
```

**Speedup: 15 calls → 6 calls (2.5x faster)**

For fib(30): 1,346,269 calls → 31 calls (43,000x faster!)

---

## 4. Visual Walkthrough: Drawing Recursion Trees

Let's trace through a concrete example and build the recursion tree step-by-step.

### Problem: Tree Sum

```python
class TreeNode:
    def __init__(self, val, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right

def tree_sum(node):
    if node is None:        # Base case
        return 0
    # Recursive case: node value + left subtree + right subtree
    return node.val + tree_sum(node.left) + tree_sum(node.right)
```

**Build a simple tree:**
```
        10
       /  \
      5    15
     / \
    3   7
```

### Step-by-Step Execution

**Step 1: Call tree_sum(node=10)**

```
Recursion tree so far:
    tree_sum(10)
```

**Step 2: 10 is not None, so call tree_sum(left child = 5)**

```
    tree_sum(10)
    /
tree_sum(5)   ← Currently executing here
```

**Step 3: 5 is not None, so call tree_sum(left child = 3)**

```
    tree_sum(10)
    /
tree_sum(5)
/
tree_sum(3)  ← Currently executing here
```

**Step 4: 3 is not None, so call tree_sum(left child = None)**

```
    tree_sum(10)
    /
tree_sum(5)
/
tree_sum(3)
/
tree_sum(None)  ← Currently executing here
```

**Step 5: BASE CASE! tree_sum(None) returns 0**

```
    tree_sum(10)
    /
tree_sum(5)
/
tree_sum(3)
/
tree_sum(None) → returns 0
```

**Step 6: Back to tree_sum(3). Call tree_sum(right child = None)**

```
    tree_sum(10)
    /
tree_sum(5)
/
tree_sum(3)
├─ tree_sum(None) → returns 0
└─ tree_sum(None) → returns 0

3 + 0 + 0 = 3
```

**Step 7: Back to tree_sum(5). Call tree_sum(right child = 7)**

```
    tree_sum(10)
    /
tree_sum(5)
├─ tree_sum(3) → returns 3
└─ tree_sum(7)  ← Currently executing
```

**Step 8: tree_sum(7). Call tree_sum(None) for both children**

```
tree_sum(7)
├─ tree_sum(None) → returns 0
└─ tree_sum(None) → returns 0

7 + 0 + 0 = 7
```

**Step 9: Back to tree_sum(5). Now we have both children's results**

```
tree_sum(5)
├─ tree_sum(3) → returns 3
└─ tree_sum(7) → returns 7

5 + 3 + 7 = 15
```

**Step 10: Back to tree_sum(10). Call tree_sum(right child = 15)**

```
    tree_sum(10)
    ├─ tree_sum(5) → returns 15
    └─ tree_sum(15)  ← Currently executing
```

**Step 11: tree_sum(15). Call tree_sum(None) for both children**

```
tree_sum(15)
├─ tree_sum(None) → returns 0
└─ tree_sum(None) → returns 0

15 + 0 + 0 = 15
```

**Step 12: Back to tree_sum(10). Now we have both children's results**

```
tree_sum(10)
├─ tree_sum(5) → returns 15
└─ tree_sum(15) → returns 15

10 + 15 + 15 = 40
```

**Final Recursion Tree (complete):**

```
                    tree_sum(10) → 40
                    /              \
              tree_sum(5) → 15     tree_sum(15) → 15
              /           \           /            \
        tree_sum(3) → 3  tree_sum(7) → 7      tree_sum(None)  tree_sum(None)
        /        \         /        \                  ↓         ↓
    tree_sum(None) tree_sum(None) tree_sum(None) tree_sum(None) 0  0
         ↓             ↓                 ↓             ↓
         0             0                 0             0
```

**Tree Analysis:**
- Height: 3 (three levels deep)
- Width: Max 2 branches per node (binary tree)
- Total nodes: 11 function calls
- Leaf nodes (base case): 6 calls to tree_sum(None)
- Time complexity: O(n) where n = number of nodes
- Space complexity: O(h) where h = height (recursion stack)

---

## 5. Critical Analysis: Time & Space Trade-offs

### 5.1 When Recursion is Efficient

**Good recursion: Balanced binary tree**

```
Tree structure:
        1
       / \
      2   3
     / \ / \
    4 5 6 7

Height: log₂(n)
Calls: n
Stack depth: log₂(n)

Time: O(n) - visit each node once
Space: O(log n) - stack depth

This is GOOD! Recursion is efficient.
```

### 5.2 When Recursion is Inefficient

**Bad recursion 1: Linked list**

```python
def process_list(node):
    if node is None:
        return
    process(node)
    process_list(node.next)

# For a linked list of 1M nodes:
Time: O(n) ← Not bad
Space: O(n) ← BAD! Stack depth = n
                   1M × 24 bytes = 24MB > 8MB stack

Result: STACK OVERFLOW
```

**Bad recursion 2: Fibonacci (overlapping subproblems)**

```
Time: O(2^n) ← TERRIBLE! Exponential growth
Space: O(n) ← Stack depth is linear
```

### 5.3 The Memoization Trade-off

**Memoization: Trade space for time**

```python
def fibonacci_memo(n, memo={}):
    if n in memo:
        return memo[n]
    
    if n <= 1:
        return n
    
    result = fibonacci_memo(n-1, memo) + fibonacci_memo(n-2, memo)
    memo[n] = result
    return result

Before: O(2^n) time, O(n) space
After:  O(n) time, O(n) space
        (Space trade-off: +n for memo, same stack depth)
```

**When to use memoization:**
- ✅ Overlapping subproblems exist (same subproblem solved multiple times)
- ✅ Time complexity would be exponential without it
- ✅ Memory is available (trade space for time)
- ❌ If subproblems are unique, memoization adds overhead

---

## 6. System Connection

### Real-world Recursive Systems

**1. File System Tree Traversal (Linux)**

```c
// Find all files in a directory tree
void traverse_directory(const char* path) {
    DIR* dir = opendir(path);
    struct dirent* entry;
    
    while ((entry = readdir(dir)) != NULL) {
        if (entry->d_type == DT_DIR) {
            // Recursive call for subdirectory
            traverse_directory(entry->d_name);
        } else {
            // Process file
            process_file(entry);
        }
    }
    closedir(dir);
}
```

**Why recursion works here:**
- Directory depth is typically < 20 (safe)
- Each directory has few subdirectories (branching factor < 10)
- Time: O(n) where n = number of files
- Space: O(h) where h = directory depth

---

**2. Compiler Parsing (GCC, LLVM)**

```
Expression: 1 + 2 * (3 + 4)

Parse tree (recursive):
           +
          / \
         1   *
            / \
           2   +
              / \
             3   4
```

The parser **recursively descends** the syntax tree:

```
parse_expression()
├─ parse_term()
│  ├─ parse_factor()
│  │  └─ "1"
│  └─ parse_expression()
│     ├─ parse_term()
│     │  └─ parse_factor()
│     │     └─ "2"
│     └─ ...
```

**Why recursion works here:**
- Expression nesting depth is usually < 50
- Grammar naturally maps to recursion
- Cleaner code than iterative parsing

---

**3. JSON/XML Parsing**

Deeply nested JSON:

```json
{
  "data": {
    "users": [
      {
        "profile": {
          "name": "John"
        }
      }
    ]
  }
}
```

Recursive parser:

```python
def parse_json(tokens, index):
    if tokens[index] == '{':
        # Parse object recursively
        obj = {}
        index = parse_key_value_pairs(tokens, index, obj)
        return obj, index
    elif tokens[index] == '[':
        # Parse array recursively
        arr = []
        index = parse_array_elements(tokens, index, arr)
        return arr, index
    else:
        # Parse primitive value
        return tokens[index], index+1
```

**Why recursion works:**
- Nesting depth is finite
- Recursive structure maps to data structure
- Clean, understandable code

---

## 7. Knowledge Check

**Question 1: Recursion Tree Analysis**

For this function:
```python
def power(x, n):
    if n == 0:
        return 1
    return x * power(x, n-1)
```

A. Draw the recursion tree for `power(2, 4)`
B. Count total function calls
C. What's the maximum depth?
D. What's the time complexity?
E. What's the space complexity?

---

**Question 2: Overlapping Subproblems**

For this function:
```python
def ways_to_climb(n):
    # How many ways to climb n stairs if you can take 1 or 2 steps?
    if n == 0 or n == 1:
        return 1
    return ways_to_climb(n-1) + ways_to_climb(n-2)
```

A. How many times is `ways_to_climb(1)` called for `ways_to_climb(5)`?
B. Without memoization, how many total calls for `ways_to_climb(10)`?
C. With memoization, how many total calls for `ways_to_climb(10)`?
D. What's the speedup (without / with)?

---

**Question 3: Real-World Decision**

You're processing a directory tree with 100,000 files. Average depth: 20.

A. Would you use recursion or iteration? Why?
B. What's the maximum stack depth you'd use?
C. Could you safely use recursion for 1,000,000 files at depth 50?
D. What conditions would make you convert to iteration?

---

## Summary: Day 4 Core Concepts

**Recursion Trees:**
- Visual representation of all function calls
- Shows depth (maximum recursion depth)
- Shows branching (number of recursive calls per function)
- Shows overlapping subproblems (same call appears multiple times)

**Time Complexity:**
- Linear recursion: O(n)
- Binary recursion (balanced): O(2^height)
- Binary recursion (unbalanced): O(2^n)
- With memoization: Depends on number of unique subproblems

**Space Complexity:**
- Stack depth = maximum recursion depth
- Can be O(log n) for balanced, O(n) for linear
- Memoization adds O(unique subproblems) extra space

**When Recursion Excels:**
- ✅ Trees and hierarchical structures (depth is logarithmic)
- ✅ Divide-and-conquer algorithms
- ✅ Code is much clearer than iteration
- ✅ Problem naturally maps to recursive structure

**When Recursion Struggles:**
- ❌ Linear structures (arrays, linked lists)
- ❌ Exponential subproblems without memoization
- ❌ Very deep recursion (>10,000 levels)
- ❌ Performance-critical code (function call overhead)

**Memoization:**
- Cache results of subproblems
- Trade O(k) space for exponential time savings
- Essential for dynamic programming
- Only works with overlapping subproblems

---

**End of Day 4: Recursion II Deep-Dive**
