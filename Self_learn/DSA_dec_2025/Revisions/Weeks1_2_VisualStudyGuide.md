# 📊 WEEKS 1-2: VISUAL STUDY GUIDE & QUICK REFERENCE
## For Quick Lookup While Studying

---

## 🎯 QUICK FACTS TO MEMORIZE

### Memory & Stack
```
Linux Stack Size:        8 MB = 8,388,608 bytes
Windows Stack Size:      1 MB = 1,048,576 bytes
Average Frame Size:      24 bytes (base) to 28KB (with locals)

Max Recursion Depth = Stack Size / Frame Size
Example: 8MB / 24 bytes = 349,525 frames
Practical Limit:  ~10,000 (when frame size is larger)

Call Stack Growth Per Function: +24 bytes minimum
```

---

## 📈 BIG O CLASSES (MEMORIZE IN ORDER)

```
O(1)      Constant        ████████████████ (flat line)
O(log n)  Logarithmic     ████████░░░░░░░░ (gentle curve)
O(n)      Linear          ████░░░░░░░░░░░░ (straight line)
O(n log n) Linearithmic   ███░░░░░░░░░░░░░ (rising)
O(n²)     Quadratic       █░░░░░░░░░░░░░░░ (steep)
O(n³)     Cubic           ░░░░░░░░░░░░░░░░ (steeper)
O(2^n)    Exponential     ░░░░░░░░░░░░░░░░ (vertical)
O(n!)     Factorial       ░░░░░░░░░░░░░░░░ (impossible)
```

### Growth at Different Sizes
```
          n=10    n=100    n=1K      n=1M        n=1B
O(1)      1       1        1         1           1
O(log n)  3       7        10        20          30
O(n)      10      100      1K        1M          1B
O(n²)     100     10K      1M        1T          10^18
O(2^n)    1K      10^30    ✗         ✗           ✗
```

---

## 💾 MEMORY LAYOUT COMPARISON

### Arrays (Contiguous)
```
Memory: 0x1000  0x1008  0x1010  0x1018
Data:   [10]    [20]    [30]    [40]
        └─ Sequential! Cache-friendly

Access Pattern:
arr[0] → 0x1000 (HIT - cache line loaded)
arr[1] → 0x1008 (HIT - already in cache)
arr[2] → 0x1010 (HIT - already in cache)
arr[3] → 0x1018 (HIT - still same cache line)

Cache Hit Rate: ~87.5%
Real Speed: 4 ns per access
```

### Linked Lists (Fragmented)
```
Memory: 0x1000  0x3000  0x2000  0x4000
Data:   [10]    [20]    [30]    [40]
        └─ Scattered! Cache-unfriendly

Access Pattern:
node[0] → 0x1000 (LOAD cache line)
node[1] → 0x3000 (MISS - 40KB away!)
node[2] → 0x2000 (MISS - different cache line)
node[3] → 0x4000 (MISS - different cache line)

Cache Hit Rate: ~0%
Real Speed: 100 ns per access

Difference: 25x slower!
```

---

## ⏱️ OPERATION COMPLEXITY CHEAT SHEET

### Array
```
Access:     O(1)     ████████████████
Insert:     O(n)     ░░░░░░░░░░░░░░░░
Delete:     O(n)     ░░░░░░░░░░░░░░░░
Search:     O(n)     ░░░░░░░░░░░░░░░░

Best For:   Read-heavy workloads
Worst For:  Frequent insertions
```

### Dynamic Array
```
Append:     O(1) amortized  ████████████████
Insert:     O(n)            ░░░░░░░░░░░░░░░░
Delete:     O(n)            ░░░░░░░░░░░░░░░░
Access:     O(1)            ████████████████

Best For:   Unknown size, build incrementally
Worst For:  Frequent deletions in middle
```

### Linked List
```
Access:     O(n)            ░░░░░░░░░░░░░░░░
Insert:     O(1) [if pointed] ████████████████
Delete:     O(1) [if pointed] ████████████████
Search:     O(n)            ░░░░░░░░░░░░░░░░

Best For:   Frequent insertions/deletions
Worst For:  Random access
```

### Hash Table
```
Insert:     O(1) avg        ████████████████
Delete:     O(1) avg        ████████████████
Access:     O(1) avg        ████████████████
Search:     O(1) avg        ████████████████

Best For:   Everything! (if good hash function)
Worst For:  Ordering, range queries
```

### Stack & Queue
```
Push/Pop:   O(1)            ████████████████
Peek:       O(1)            ████████████████
Search:     O(n)            ░░░░░░░░░░░░░░░░

Best For:   LIFO/FIFO semantics
Worst For:  Random access
```

### Binary Search (sorted array)
```
Search:     O(log n)        ████████░░░░░░░░
            1B → 30 comparisons!

Best For:   Huge sorted datasets
Worst For:  Unsorted, requires pre-sort
```

---

## 📐 DECISION TREE: WHICH DATA STRUCTURE?

```
                        ┌─ Start ─┐
                        │          │
                        └──────────┘
                             │
              ┌──────────────┴──────────────┐
              │                             │
        Need fast             Need fast
        access?               insertion?
              │                             │
              Yes                           Yes
              │                             │
         Array? ──────────────┐      Linked List
              │                │           │
           Cache              Yes         Good?
           matters?                        │
              │                            │
             Yes                          Yes
             │                             │
         Hash Table                   Keep it
         (if keyed)
             │
            Good

       For Ordering?
             │
            Yes
             │
         Sorted Array
         (with binary search)
             │
            No
             │
         Hash Table
         (or linked list)
```

---

## 🔍 RECURSION ANALYSIS AT A GLANCE

### Stack Depth Calculator
```
Safe Recursion Depth = Stack Size / Frame Size
                    = 8,388,608 / 24
                    = 349,525 frames

Rule of Thumb:
- Tree traversal:   Depth = O(log n) → ALWAYS safe
- Linked list:      Depth = O(n)     → RISKY >10K
- File system:      Depth = 30-50    → SAFE
- Unknown depth:    >1,000           → USE ITERATION
```

### Recursion vs Iteration
```
✓ Use Recursion When:
  - Tree/graph (depth = log n)
  - Code clarity matters
  - Depth < 10,000
  
✗ Avoid Recursion When:
  - Linear depth = n
  - Real-time (call overhead)
  - Unknown depth
  - Can't predict
```

---

## 💰 AMORTIZED ANALYSIS FORMULA

### Dynamic Array with k-factor Growth
```
Growth Factor 2x (doubling):
  Resizes for n appends:      log₂(n)
  Total copies:                2n
  Per-operation cost:           O(1) amortized
  Memory waste:                 ~50%

Growth Factor 1.5x:
  Resizes for n appends:      log₁.₅(n)
  Total copies:                3n
  Per-operation cost:           O(1) amortized
  Memory waste:                 ~33%

Growth Factor 1.1x (bad):
  Resizes for n appends:      log₁.₁(n)
  Total copies:                ~10n
  Per-operation cost:           O(1) amortized (barely)
  Memory waste:                 ~10%
```

---

## 🎯 BINARY SEARCH SPEEDUP

```
Array Size    Linear    Binary    Speedup
10            10        4         2.5x
100           100       7         14x
1,000         1K        10        100x
1,000,000     1M        20        50,000x
1,000,000,000 1B        30        33,000,000x

Key insight: As n grows, log n advantage explodes!
```

---

## 📊 CACHE PERFORMANCE NUMBERS

```
L1 Cache (32KB):          4 nanoseconds
L2 Cache (256KB):         10 nanoseconds
L3 Cache (8MB):           40 nanoseconds
Main Memory (8-64GB):     100 nanoseconds

Cache Line Size:          64 bytes = 8 integers

Sequential Access:        87.5% hit rate = ~16 ns
Random Access:            ~0% hit rate = ~100 ns

Real Difference:          6-25x slower for random!
```

---

## 🎮 COMPLEXITY EXAMPLES AT A GLANCE

### Finding Duplicate in Array
```
Brute force (2 loops):        O(n²)
Sort then scan:               O(n log n)
Hash set:                     O(n)

Winner: Hash set
```

### Reverse a Linked List
```
With extra array:             O(n) space
In-place pointer swap:        O(1) space

Winner: In-place
```

### Validate Binary Search Tree
```
Compare each node to min/max:  O(n)
In-order traversal check:      O(n)

Same complexity, different approaches
```

### Find Kth Largest Element
```
Sort then index:              O(n log n)
Min heap of size k:           O(n log k)
Quick select:                 O(n) average

Winner: Quick select (if you know it)
```

---

## 🏆 PERFORMANCE RULES OF THUMB

### Time Complexity at Different Sizes
```
n=10:       O(n²) is OK (100 ops)
n=100:      O(n log n) is needed (700 ops)
n=1,000:    O(n log n) is required (10K ops)
n=1,000,000: O(n) or O(n log n) only (20M ops)
n=1,000,000,000: O(log n) or O(1) only (30 ops)
```

### Space Limits
```
Single variable:          8 bytes
Small array (1K items):   8 KB
Medium array (1M items):  8 MB
Large array (1B items):   8 GB (unavailable!)

Linked list overhead:     3x array space
Hash table overhead:      1.5x array space
```

### Real-World Latency Targets
```
Instant (<1ms):           <10,000 operations
Fast (<100ms):            <1,000,000 operations
Acceptable (<1s):         <1,000,000,000 operations
Batch (<1h):              Anything goes
```

---

## 🎯 DECISION CHECKLIST

### Before Coding, Ask:
```
[ ] What's the data size (n=10? n=1M? n=1B?)
[ ] What operations are frequent?
[ ] Do I need ordering?
[ ] Do I need random access?
[ ] Is memory constrained?
[ ] Is it real-time?
[ ] Can I use recursion? (check depth)
[ ] Should I sort first?
[ ] Which data structure fits best?
```

---

## 📚 QUICK REFERENCE: WHEN TO USE WHAT

```
Fast Access?              → Array
Fast Insert/Delete?       → Linked List
Key-Value Lookup?         → Hash Table
Ordered, range queries?   → Sorted Array/Tree
LIFO semantics?           → Stack
FIFO semantics?           → Queue
Frequent front insert?    → Deque/Linked List
Most recent first?        → LRU (Hash+Link)
Top K elements?           → Heap
Unique elements?          → Hash Set
```

---

## 🚀 STUDY TIMELINE

```
Day 1-2:   Memory & complexity     (read + exercise)
Day 3-4:   Recursion               (deep dive)
Day 5-6:   Week 2 materials        (read + practice)
Day 7-8:   Real-world problems     (apply concepts)
Day 9-10:  Interview prep          (explain clearly)
Week 3:    Verify mastery          (teach others)
```

---

## ✅ FINAL CHECKLIST BEFORE MOVING FORWARD

### Can You Answer These Without Looking?

```
[ ] Stack size on Linux?                    Answer: 8MB
[ ] Frame size?                             Answer: 24 bytes base
[ ] Max recursion depth?                    Answer: 349,525
[ ] Cache speedup?                          Answer: 10-25x
[ ] Binary search speedup on 1B elements?   Answer: 33 billion times
[ ] Array indexing time?                    Answer: O(1)
[ ] Linked list insert time (with pointer)? Answer: O(1)
[ ] Dynamic array append (amortized)?       Answer: O(1)
[ ] Linear search vs binary on sorted?      Answer: O(n) vs O(log n)
[ ] When does 2x growth help?               Answer: O(log n) resizes
```

If you can answer 8+ of these, **you're ready for Week 3!**

---

**Use this guide for quick reference while studying and practicing!**

Good luck! 🎓🚀
