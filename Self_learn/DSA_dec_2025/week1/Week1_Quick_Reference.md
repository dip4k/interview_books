# 🧠 DSA Week 1: Quick Reference Guide
## One-Page Lookup for Key Concepts, Decision Trees & Interview Prep

---

## PART 1: COMPLEXITY CHEAT SHEET

### **The 11 Complexity Classes (Ordered Fastest to Slowest)**

```
Rank | Notation  | Name        | At n=1K  | At n=1M    | Verdict
─────┼───────────┼─────────────┼──────────┼────────────┼──────────
1    | O(1)      | Constant    | 1        | 1          | ✓ Always
2    | O(log n)  | Log         | 10       | 20         | ✓ Always
3    | O(n)      | Linear      | 1K       | 1M         | ✓ Feasible
4    | O(n log n)| Linearithm  | 10K      | 20M        | ✓ Good sort
5    | O(n²)     | Quadratic   | 1M       | 1T         | ⚠ Slow
6    | O(n³)     | Cubic       | 1B       | huge       | ✗ Very slow
7    | O(2ⁿ)     | Exponential | huge     | impossible | ✗ Infeasible
8    | O(n!)     | Factorial   | huge     | impossible | ✗ Never
```

---

## PART 2: TIME COMPLEXITY QUICK REFERENCE

### **Common Algorithms at a Glance**

```
Algorithm              | Best      | Average   | Worst      | Space
───────────────────────┼───────────┼───────────┼────────────┼─────────
Linear Search          | O(1)      | O(n)      | O(n)       | O(1)
Binary Search          | O(1)      | O(log n)  | O(log n)   | O(log n)
Bubble Sort            | O(n)      | O(n²)     | O(n²)      | O(1)
Insertion Sort         | O(n)      | O(n²)     | O(n²)      | O(1)
Selection Sort         | O(n²)     | O(n²)     | O(n²)      | O(1)
Merge Sort             | O(n log n)| O(n log n)| O(n log n) | O(n)
Quick Sort             | O(n log n)| O(n log n)| O(n²)      | O(log n)
Heap Sort              | O(n log n)| O(n log n)| O(n log n) | O(1)
Hash Table Insert      | O(1)      | O(1)      | O(n)       | O(n)
Hash Table Lookup      | O(1)      | O(1)      | O(n)       | O(n)
BST Insert             | O(log n)  | O(log n)  | O(n)       | O(n)
BST Search             | O(log n)  | O(log n)  | O(n)       | O(n)
Balanced Tree          | O(log n)  | O(log n)  | O(log n)   | O(n)
DFS/BFS                | O(V+E)    | O(V+E)    | O(V+E)     | O(V)
Dijkstra's Algorithm   | O((V+E) log V) for heap implementation
Floyd-Warshall        | O(V³)     | O(V³)     | O(V³)      | O(V²)
```

---

## PART 3: SPACE COMPLEXITY QUICK REFERENCE

```
Data Structure      | Search | Insert | Delete | Space  | Best Used For
────────────────────┼────────┼────────┼────────┼────────┼───────────────
Array               | O(n)   | O(n)   | O(n)   | O(n)   | Random access
Linked List         | O(n)   | O(1)*  | O(1)*  | O(n)   | Fast insertion
Stack               | O(n)   | O(1)   | O(1)   | O(n)   | LIFO
Queue               | O(n)   | O(1)   | O(1)   | O(n)   | FIFO
Hash Table          | O(1)** | O(1)** | O(1)** | O(n)   | Fast lookup
Binary Search Tree  | O(log n)***| O(log n)***| O(log n)***| O(n) | Sorted data
AVL Tree            | O(log n)| O(log n)| O(log n)| O(n)  | Balanced tree
Heap                | O(n)   | O(log n)| O(log n)| O(n)  | Priority queue
Trie                | O(m)   | O(m)   | O(m)   | O(m)   | Prefix search
Graph (Matrix)      | O(V)   | O(1)   | O(1)   | O(V²)  | Dense graphs
Graph (List)        | O(V+E) | O(1)   | O(1)   | O(V+E) | Sparse graphs

* If you have a reference to the node
** Average case; O(n) worst case with poor hash function
*** Assuming balanced tree; O(n) if unbalanced
```

---

## PART 4: MEMORY REFERENCE

### **How Much Space Does This Use?**

```
Data Type           | Size (Bytes)
────────────────────┼──────────────
char                | 1
short               | 2
int                 | 4
float               | 4
long                | 8
double              | 8
pointer             | 8 (64-bit) / 4 (32-bit)
bool                | 1

Quick Calculation:
Array of 1M ints: 1,000,000 × 4 = 4,000,000 bytes = 4 MB
Array of 1M doubles: 1,000,000 × 8 = 8,000,000 bytes = 8 MB
Array of 1M strings (avg 100 bytes): 100 MB
```

### **Real-World Memory Constraints**

```
Device              | RAM Available | Typical Max Array
────────────────────┼───────────────┼──────────────────
Arduino Uno         | 2KB           | 500 ints
IoT Device          | 256KB-2MB     | 50K-500K ints
Mobile Phone        | 512MB-8GB     | 100M-2B ints
Desktop             | 8GB-32GB      | 2B-8B ints
Server              | 32GB-256GB    | 8B-64B ints
```

---

## PART 5: QUICK DECISION TREES

### **Decision Tree: Which Sorting Algorithm?**

```
Do you need a stable sort?
├─ YES → Do you have O(n) extra space?
│   ├─ YES → Merge Sort (guaranteed O(n log n))
│   └─ NO  → Insertion Sort (if small) or convert to in-place
├─ NO  → Do you want guaranteed O(n log n)?
    ├─ YES → Heap Sort
    └─ NO  → Quick Sort (average case, faster in practice)

Special cases:
- Data is nearly sorted? → Insertion Sort (O(n))
- Must work in-place? → Quick Sort or Heap Sort
- Maximum predictability needed? → Merge Sort
- Hybrid (best of both worlds)? → Timsort (Python) or Introsort (C++)
```

### **Decision Tree: Which Data Structure?**

```
Do you need fast lookups?
├─ YES → Do you have a key (searching by ID/name)?
│   ├─ YES → Use Hash Table (O(1) lookup)
│   └─ NO  → Use Sorted Array + Binary Search (O(log n))
│
├─ NO  → Do you need sorted data?
    ├─ YES → Use Balanced Tree (BST) (O(log n) insert/search)
    └─ NO  → Do you need fast insertions/deletions at ends?
        ├─ YES → Use Deque or Linked List
        └─ NO  → Use Array (simplest)
```

### **Decision Tree: Recursion or Iteration?**

```
Is the problem naturally recursive?
├─ YES → Use Recursion (clearer code)
│   ├─ Check: Is recursion depth safe?
│   │   ├─ YES → OK
│   │   └─ NO  → Convert to iteration or increase stack
│   └─ Does it have overlapping subproblems?
│       ├─ YES → Add memoization
│       └─ NO  → Pure recursion is fine
│
└─ NO → Use Iteration (more explicit control)
```

---

## PART 6: INTERVIEW PREPARATION CHECKLIST

### **When You See a Problem, Ask Yourself:**

**Complexity Analysis:**
- [ ] What's the time complexity (best, avg, worst)?
- [ ] What's the space complexity?
- [ ] At scale (n = 1M, 1B), is this feasible?
- [ ] Can I optimize? (Can I reduce a complexity class?)

**Algorithm Selection:**
- [ ] Which algorithm/data structure fits?
- [ ] What are the trade-offs?
- [ ] Have I considered edge cases?
- [ ] Is there a more elegant solution?

**Implementation:**
- [ ] Can I code this clearly in 10 minutes?
- [ ] What can go wrong? (Off-by-one, null pointers, stack overflow)
- [ ] Should I use built-in functions or implement from scratch?

**Real-World Context:**
- [ ] What constraints exist? (Mobile? Embedded? Distributed?)
- [ ] Does performance matter at scale?
- [ ] Can I accept trade-offs? (Space for time, stability for performance)

---

## PART 7: RED FLAGS & OPTIMIZATION OPPORTUNITIES

### **Red Flags (Probably Too Slow)**

```
Pattern                  | Time      | Red Flag
─────────────────────────┼───────────┼──────────────────────
Nested loops over same   | O(n²)     | ⚠ Often avoidable
Triple nested loops      | O(n³)     | ✗ Very slow
Exponential recursion    | O(2ⁿ)     | ✗ Infeasible
Factorial-like recursion | O(n!)     | ✗ Never acceptable
```

### **Optimization Opportunities (Look for These)**

```
Situation                          | Optimization           | Result
───────────────────────────────────┼────────────────────────┼─────────
Sorted array lookups               | Use binary search      | O(n) → O(log n)
Finding duplicates in array        | Use hash table         | O(n²) → O(n)
Finding paths in graph             | Use BFS/DFS            | Varies
Selecting k min/max                | Use heap               | O(n log k)
Computing multiple range queries   | Use prefix sums        | O(1) per query
Overlapping subproblems            | Use memoization        | Exponential → Polynomial
```

---

## PART 8: COMMON MISCONCEPTIONS

**Misconception 1:** "O(1) is always better than O(log n)"
- **Truth:** O(1) means constant time regardless of n, but actual times differ. At n=1M, both are negligible. Constants matter!

**Misconception 2:** "Recursion is always inefficient"
- **Truth:** Modern compilers optimize recursion. Recursion is often clearer and equally fast.

**Misconception 3:** "Stack overflow is random"
- **Truth:** Stack overflow is deterministic. If depth × frame size > stack limit, you overflow.

**Misconception 4:** "Big O is the only thing that matters"
- **Truth:** Big O predicts large-scale behavior, but constants determine practical speed at small scales.

**Misconception 5:** "Memory is unlimited"
- **Truth:** Every system has memory constraints. Mobile: 512MB-8GB. Embedded: KB-MB.

---

## PART 9: ONE-MINUTE EXPLANATIONS

### **Big O Notation in 60 seconds:**
"Big O describes how an algorithm's time/space grows as input size n increases, ignoring constants. It answers: 'As n doubles, does runtime double (O(n)), quadruple (O(n²)), or barely change (O(log n))?'"

### **Recursion in 60 seconds:**
"Recursion is a function calling itself with a simpler problem until reaching a base case. Each call creates a stack frame. Maximum concurrent frames = recursion depth. If depth > stack limit, overflow."

### **Time vs. Space Trade-off in 60 seconds:**
"You often can spend memory to save time or vice versa. Example: Memoization trades O(n) space for exponential time savings. The question is always: What resource is more precious? (Usually, time in production.)"

---

## PART 10: FORMULAS YOU SHOULD KNOW

```
Sum of first n integers:           n(n+1)/2
Sum of geometric series:            a(1-r^n)/(1-r)
Log₂(n) for n=1 million:            ~20
Log₂(n) for n=1 billion:            ~30
n log n at n=1 million:             ~20 million
n² at n=1 million:                  1 trillion
2^n at n=50:                        10^15 (infeasible)
Fibonacci(n) unoptimized:           O(2^n)
Fibonacci(n) with memoization:      O(n)
```

---

## PART 11: QUICK LOOKUP TABLE

### **"I have n items and need to _____"**

```
Do this...                  | Use this structure/algorithm    | Complexity
────────────────────────────┼────────────────────────────────┼─────────────
Find item by ID             | Hash Table                     | O(1)
Find item by range          | Sorted Array + Binary Search   | O(log n)
Keep items sorted           | Balanced BST or sorted list    | O(log n) insert
Find min/max repeatedly     | Heap                           | O(log n) each
Find duplicates             | Hash Set                       | O(n)
Group similar items         | Hash Map                       | O(n)
Traverse in order           | In-order DFS or sorted list    | O(n)
Store hierarchical data     | Tree                           | O(n) space
Find shortest path          | BFS or Dijkstra               | O(V + E) or O((V+E)log V)
Sort items                  | Merge Sort, Quick Sort         | O(n log n)
Need LIFO behavior          | Stack                          | O(1) push/pop
Need FIFO behavior          | Queue                          | O(1) enqueue/dequeue
```

---

## PART 12: MEMORY LAYOUT QUICK REFERENCE

```
Stack (LIFO, automatic cleanup):
├─ Fast allocation (1 cycle)
├─ Limited size (~8MB typical)
├─ Automatic deallocation on function return
├─ Good for: Local variables, function parameters, recursion
└─ Risk: Stack overflow with deep recursion

Heap (Free-form, manual cleanup):
├─ Slower allocation (100+ cycles)
├─ Huge size (GB available)
├─ Manual deallocation (must free())
├─ Good for: Large data structures, dynamic sizes
└─ Risk: Memory leaks if forget to free()

CPU Caches:
├─ L1: Fast (4 cycles), small (32KB)
├─ L2: Medium (10 cycles), medium (256KB)
├─ L3: Slower (40 cycles), large (8MB)
└─ RAM: Slowest (100+ cycles), huge (GB)
    → Lesson: Locality matters! Sequential > Random access
```

---

## END NOTES

**The Five Questions You Must Answer for ANY Algorithm:**

1. **What's the time complexity?** (Best, average, worst)
2. **What's the space complexity?** (Input + auxiliary + stack)
3. **At production scale (n = millions/billions), is it feasible?**
4. **What are the trade-offs?** (Time vs. space, simplicity vs. performance)
5. **Can I do better?** (Can I reduce a complexity class?)

**Master these, and you've mastered Week 1.** ✓

---

**End of Week 1 Quick Reference Guide**
