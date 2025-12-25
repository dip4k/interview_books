# 🧠 DSA Week 1: Comprehensive Practice Exercises
## 12 Advanced Exercises with Real-World Trading System Scenario

---

## Scenario: Building a High-Frequency Trading Platform

You're hired as lead engineer for **QuantTrade**, a high-frequency trading (HFT) platform that processes 1 million stock quotes per second. Every microsecond matters. Your Week 1 knowledge will determine whether the system is fast, scalable, and reliable.

---

## Exercise Set 1: Memory Architecture & Pointers (Day 1)

### **Exercise 1.1: Cache-Aware Quote Processing**

**The Problem:**

QuantTrade receives 1 million quotes per second. Each quote is:
```c
struct Quote {
    double price;      // 8 bytes
    int volume;        // 4 bytes
    char symbol[8];    // 8 bytes
    short delta;       // 2 bytes
    char padding[2];   // 2 bytes (alignment)
} // Total: 24 bytes
```

You have two approaches to store quotes:

**Approach A: Sequential (Contiguous Memory)**
```c
Quote quotes[1000000];  // All quotes in one block
// Addresses: 0x1000, 0x1018, 0x1030, 0x1048, ...
```

**Approach B: Scattered (Linked List of Pointers)**
```c
struct Node {
    Quote quote;
    Node* next;
};
// Quotes scattered across memory at random addresses
```

**Your Task:**

```
Question 1: How many quotes fit in one 64-byte cache line?
Answer: 64 / 24 = _____ quotes

Question 2: For sequential storage, how many cache misses to process 1M quotes?
Answer: 1,000,000 / 2.67 ≈ _____ misses

Question 3: For scattered storage, how many cache misses?
Answer: _____ (one miss per quote, essentially)

Question 4: Time per miss on modern CPU: 100 cycles at 2GHz = _____ nanoseconds

Question 5: Total time to process 1M quotes:
- Sequential: _____ × 100ns = _____ milliseconds ✓
- Scattered: _____ × 100ns = _____ milliseconds ✗

Question 6: Which approach do you choose and why?
Answer: _____
```

**[WORK THROUGH THIS YOURSELF FIRST]**

---

### ✅ Exercise 1.1 Solution

**Calculations:**

```
Cache line: 64 bytes
Quote size: 24 bytes
Quotes per cache line: 64 / 24 = 2.67, so 2 quotes fit perfectly

Sequential storage:
- 1,000,000 quotes total
- 2 quotes per cache line
- Cache misses needed: 1,000,000 / 2 = 500,000 misses

Scattered storage:
- Each quote at random address
- Each quote triggers a new cache miss
- Cache misses needed: 1,000,000 misses

Time per cache miss: 100 cycles
At 2GHz: 100 cycles / 2×10^9 = 50 nanoseconds

Wait, let me recalculate:
1 GHz = 10^9 cycles per second = 1 ns per cycle
2 GHz = 2×10^9 cycles per second = 0.5 ns per cycle
100 cycles at 2GHz = 100 × 0.5 ns = 50 ns per cache miss

Sequential approach:
500,000 misses × 50 ns = 25,000,000 ns = 25 milliseconds

Scattered approach:
1,000,000 misses × 50 ns = 50,000,000 ns = 50 milliseconds

Speedup: 50 / 25 = 2x faster with sequential storage
Plus: Better branch prediction, TLB performance, etc.
Real speedup: 3-5x faster
```

**Answer:**

**Use sequential (contiguous) storage.**

**Why:**
- Cache locality: 2 quotes per cache miss vs. 1 quote per cache miss
- 50% fewer cache misses
- 2x faster processing
- For 1M quotes/second: Difference between 25ms and 50ms
- In HFT, this difference affects market competitiveness

**Real-world note:** Modern trading systems use pre-allocated arrays (sequential) rather than dynamic allocations (scattered) for exactly this reason.

---

### **Exercise 1.2: Stack vs. Heap: Which Allocation Strategy?**

**The Problem:**

QuantTrade needs to track:
- Active traders: ~10,000
- Each trader has a portfolio with ~100 positions
- Each position has associated data (price history, margins, risk metrics)

**Approach A: Stack Allocation (Fast but Limited)**
```c
void process_trader(int trader_id) {
    double price_history[1000];  // 8KB per call
    int risk_metrics[500];       // 2KB per call
    // Process...
}

// Called millions of times during the day
```

**Approach B: Heap Allocation (Flexible but Requires Management)**
```c
void process_trader(int trader_id) {
    double* price_history = malloc(1000 * sizeof(double));
    int* risk_metrics = malloc(500 * sizeof(int));
    
    // Process...
    
    free(price_history);
    free(risk_metrics);
}
```

**Your Task:**

```
Question 1: What's the total stack space needed per call in Approach A?
Answer: _____ KB

Question 2: If function is called 100,000 times, is this viable?
- Stack limit: 8MB = 8,192 KB
- 100,000 calls need: _____ KB
- Viable? YES / NO

Question 3: In Approach B, which has faster allocation: malloc or stack?
Answer: _____ (stack is ~1 cycle, malloc is 10+ cycles with fragmentation risk)

Question 4: What's the risk in Approach B if you forget to free?
Answer: _____

Question 5: Which approach for QuantTrade?
Answer: _____ (A for small data structures, B for large ones)
```

**[THINK THROUGH THIS]**

---

### ✅ Exercise 1.2 Solution

```
Space per call (Approach A):
- price_history: 1000 × 8 bytes = 8,000 bytes = 8 KB
- risk_metrics: 500 × 4 bytes = 2,000 bytes = 2 KB
- Total: 10 KB per call

Viability of 100,000 calls:
- Need: 100,000 × 10 KB = 1,000,000 KB = 1 GB
- Stack limit: 8 MB
- 1 GB >> 8 MB
- Result: STACK OVERFLOW ✗

Speed comparison:
- Stack allocation: ~1 CPU cycle (just move stack pointer)
- Malloc: ~100+ cycles (search free list, initialize, etc.)
- Overhead: ~100x slower

Memory management:
- Stack: Automatic deallocation (when function returns)
- Heap: Manual deallocation (easy to leak memory)

For QuantTrade:
```

**RECOMMENDATION: Hybrid Approach**

```c
// Allocate large data structures once during startup
double* price_histories = malloc(10000 * 1000 * sizeof(double));
int* risk_metrics_all = malloc(10000 * 500 * sizeof(int));

// Reuse the same memory for each trader
void process_trader(int trader_id) {
    double* my_history = price_histories + (trader_id * 1000);
    int* my_metrics = risk_metrics_all + (trader_id * 500);
    
    // Process using pre-allocated memory
    // No mallocs/frees during tight loop
}

// Free once at shutdown
free(price_histories);
free(risk_metrics_all);
```

**Why this works:**
- Avoids stack overflow: Large arrays on heap
- Avoids malloc overhead: Allocated once, reused millions of times
- Avoids memory leaks: Single free at shutdown
- Optimized for HFT: No allocation/deallocation in critical path

---

## Exercise Set 2: Time Complexity Analysis (Day 2)

### **Exercise 2.1: Quote Matching Engine Complexity**

**The Problem:**

QuantTrade needs to match buy and sell orders. The naive approach:

```c
void match_orders() {
    for (int i = 0; i < num_buy_orders; i++) {
        for (int j = 0; j < num_sell_orders; j++) {
            if (can_match(buy[i], sell[j])) {
                execute_trade(buy[i], sell[j]);
            }
        }
    }
}

// Processing 100,000 buy orders and 100,000 sell orders
```

**Your Task:**

```
Question 1: What's the time complexity?
Answer: O(_)

Question 2: How many comparisons for 100K buy and 100K sell orders?
Answer: _____ (100,000 × 100,000)

Question 3: At 1 billion comparisons per second, how long does this take?
Answer: _____ seconds

Question 4: Is this acceptable for a trading system?
Answer: YES / NO (trading happens in microseconds!)

Question 5: How can you optimize this?
Answer: _____ (Use sorted orders + binary search, O(n log n) instead)
```

**[CALCULATE THIS]**

---

### ✅ Exercise 2.1 Solution

```
Naive matching:

for (buy in all_buys) {
    for (sell in all_sells) {
        check if they match
    }
}

Complexity: O(n × m) where n = # buys, m = # sells
For 100K × 100K: O(10^10) = 10 billion operations

At 1 GHz (1 billion ops/sec):
10 billion operations / 1 billion ops/sec = 10 seconds

This is unacceptable for trading! Orders match in microseconds.
```

**Optimized Approach:**

```
Sort buy orders by price: O(n log n)
Sort sell orders by price: O(m log m)

Use two pointers approach: O(n + m)

for (buy_ptr = 0; sell_ptr = 0; ...) {
    if (buy[buy_ptr].price >= sell[sell_ptr].price) {
        match them
        advance pointers
    }
}

Total: O(n log n + m log m + n + m) = O(n log n)

For 100K × 100K:
n log n = 100,000 × 17 = 1,700,000 operations

At 1 GHz: 1,700,000 / 1,000,000,000 = 0.0017 seconds = 1.7 milliseconds

Speedup: 10 seconds / 1.7 ms ≈ 5,800x FASTER!
```

**Lesson:** Choosing O(n log n) instead of O(n²) is the difference between "slow" and "impossible" at trading scale.

---

### **Exercise 2.2: Best, Average, Worst Cases in Live Trading**

**The Problem:**

QuantTrade uses Quick Sort to sort orders before matching:

```c
void quicksort(Order orders[], int left, int right) {
    if (left >= right) return;
    
    int pivot_idx = partition(orders, left, right);
    quicksort(orders, left, pivot_idx - 1);
    quicksort(orders, pivot_idx + 1, right);
}
```

**Your Task:**

```
Question 1: What's the best-case complexity?
Answer: O(___) - when pivots split array evenly

Question 2: What's the average-case complexity?
Answer: O(___) - typical random data

Question 3: What's the worst-case complexity?
Answer: O(___) - when pivots are always at extremes

Question 4: When does worst case happen?
Answer: _____ (already sorted data, or bad pivot selection)

Question 5: If orders are received in sorted order (best case):
- 100K orders, O(n log n)
- 100K × 17 = _____ operations
- Time: _____ milliseconds

Question 6: If orders are in reverse sorted order (worst case):
- 100K orders, O(n²)
- 100K × 100K = _____ operations
- Time: _____ seconds

Question 7: How to prevent worst case?
Answer: _____
```

**[THINK THROUGH THE SCENARIOS]**

---

### ✅ Exercise 2.2 Solution

```
Best case: O(n log n)
- Pivot always splits array in half
- Balanced recursion tree
- Depth = log n, each level does n work
- Total: n log n operations

Average case: O(n log n)
- Random pivot selection
- Most of the time, relatively balanced
- Expected: n log n operations

Worst case: O(n²)
- Pivot always at extreme (smallest or largest element)
- Unbalanced tree (linear like linked list)
- Depth = n, total: n + (n-1) + ... + 1 = n(n-1)/2 = O(n²)

When worst case happens:
1. Already sorted array + naive pivot selection (first element)
2. Reverse sorted array + naive pivot selection
3. All equal elements (degenerate)

Scenario analysis:

Best case (100K random orders):
- Quick sort O(n log n) = 100,000 × 17 = 1,700,000 ops
- Time: ~1.7 ms ✓

Worst case (100K sorted orders):
- Quick sort O(n²) = 100,000² = 10,000,000,000 ops
- Time: ~10 seconds ✗

Prevention strategies:
1. Randomize pivot selection (shuffle before sort)
2. Use median-of-three pivot selection
3. Use Merge Sort instead (guaranteed O(n log n))
4. Use Introsort (Quick Sort + fallback to Heap Sort if going deep)
```

**Real-world note:** Python's Timsort and C++ STL's sort (Introsort) prevent the worst case by detecting bad performance and switching algorithms.

---

## Exercise Set 3: Space Complexity & Stack Depth (Day 5)

### **Exercise 3.1: Recursive Position Calculator Stack Depth**

**The Problem:**

QuantTrade calculates portfolio positions recursively by summing across different account levels:

```c
int calculate_position(Account* account) {
    if (!account) return 0;
    
    int position = account->shares;
    position += calculate_position(account->parent_account);
    
    return position;
}

// Account hierarchy: Root → Desk → Trader → SubAccount
// Depth: ~100 levels for large organizations
```

**Your Task:**

```
Question 1: What's the maximum recursion depth?
Answer: _____ (at most account hierarchy depth)

Question 2: Each frame needs ~24 bytes. Space per call?
Answer: 100 × 24 = _____ bytes = _____ KB

Question 3: Is 2.4 KB safe?
Answer: YES / NO (compared to 8MB stack limit)

Question 4: What if organization has 1000-level hierarchy?
Answer: 1000 × 24 = _____ bytes = _____ KB. Safe? YES / NO

Question 5: Worst-case real organization:
Answer: _____ (probably <100 levels, safe)

Question 6: How to handle arbitrary depth?
Answer: _____ (use iteration instead of recursion)
```

**[TRACE THE RECURSION]**

---

### ✅ Exercise 3.1 Solution

```
Account hierarchy (typical):
Root (CEO level)
└── Desk (Equities Trading Desk)
    └── Trader (John Smith)
        └── SubAccount (Strategy A)
            └── SubAccount (Pair Trade)

Typical depth: 3-5 levels
Worst case: 10-20 levels
Super worst case (if hierarchically organized): ~100 levels

For depth = 100:
- Stack frames: 100
- Bytes per frame: 24
- Total: 2,400 bytes = 2.4 KB
- Stack limit: 8 MB = 8,192 KB
- 2.4 KB << 8 MB → SAFE ✓

For depth = 1000:
- Stack frames: 1000
- Bytes per frame: 24
- Total: 24,000 bytes = 24 KB
- 24 KB << 8 MB → Still SAFE ✓

For depth = 1,000,000 (absurd):
- Total: 24 MB > 8 MB → OVERFLOW ✗

Iterative version (if needed):
```

```c
int calculate_position(Account* account) {
    int total = 0;
    while (account) {
        total += account->shares;
        account = account->parent_account;
    }
    return total;
}

Space: O(1), always safe ✓
```

---

### **Exercise 3.2: Merge Sort on Mobile Device**

**The Problem:**

QuantTrade mobile app lets users sort their trading history. On a budget Android phone:
- RAM available: 512 MB
- Trading history: 100,000 trades
- Each trade: 200 bytes

**Choose between:**

**Approach A: Merge Sort**
- Guaranteed O(n log n) time
- Requires O(n) auxiliary space

**Approach B: Quick Sort**
- Average O(n log n) time
- Requires O(log n) extra space
- Worst case O(n²)

**Your Task:**

```
Question 1: Input size (100K trades × 200 bytes)?
Answer: _____ MB

Question 2: Merge Sort space needed?
- Input: _____ MB
- Auxiliary: _____ MB
- Total: _____ MB

Question 3: Fit in 512 MB?
Answer: YES / NO

Question 4: Quick Sort space needed?
- Input: _____ MB
- Auxiliary: O(log n) = _____ KB
- Total: _____ MB

Question 5: Which to choose?
Answer: _____ (and why?)
```

**[CALCULATE MEMORY USAGE]**

---

### ✅ Exercise 3.2 Solution

```
Input size:
100,000 trades × 200 bytes = 20,000,000 bytes = 20 MB

Merge Sort:
- Input: 20 MB
- Auxiliary temp array: 20 MB
- Recursion stack: log₂(100K) × 24 bytes ≈ 400 bytes
- Total: 40.0004 MB

Quick Sort:
- Input: 20 MB
- Auxiliary: O(log n) = log₂(100K) × 24 ≈ 400 bytes
- Recursion stack (average): log₂(100K) × 24 ≈ 400 bytes
- Total: 20.0008 MB

Available: 512 MB

Merge Sort: 40 MB < 512 MB → FITS ✓
Quick Sort: 20 MB << 512 MB → FITS ✓ (with margin)

Decision: Either works, but consider:
- Merge Sort: Guaranteed fast, but uses 2x memory
- Quick Sort: Slightly risky worst case, but uses less memory

RECOMMENDATION: Use Quick Sort with randomized pivot
- Average case is still O(n log n)
- Probability of worst case is negligible
- Saves 20MB of memory
- On mobile, memory is more precious than CPU
```

---

## Exercise Set 4: Integration Challenges

### **Exercise 4.1: Complete HFT Platform Design Review**

**The Problem:**

You're reviewing the entire QuantTrade platform. Give complexity analysis for:

```c
struct Trade {
    double price;
    int volume;
    char symbol[8];
};

void process_market_data() {
    // Step 1: Receive 1M quotes per second
    Quote* quotes = receive_quotes();  // O(?)
    
    // Step 2: Sort quotes by symbol
    sort_by_symbol(quotes, 1000000);  // O(?)
    
    // Step 3: Group by symbol
    Quote** groups = group_by_symbol(quotes);  // O(?)
    
    // Step 4: For each group, find best bid/ask
    for (int i = 0; i < num_symbols; i++) {
        Trade* best = find_best_trade(groups[i]);  // O(?)
    }
}
```

**Your Task:**

```
Question 1: Time complexity of entire function?
- Receive: O(n)
- Sort: O(n log n)
- Group: O(n)
- Find best (for each symbol): O(num_symbols × avg_quotes_per_symbol)
  = O(num_symbols × n/num_symbols) = O(n)
- Total: O(?)

Question 2: Space complexity?
- Input quotes: O(n)
- Sorted quotes: (in-place sort) O(1) auxiliary
- Groups array: O(num_symbols)
- Total: O(?)

Question 3: Can this handle 1M quotes/sec?
Time: n log n = 1,000,000 × 20 = 20,000,000 ops
At 2GHz: 20,000,000 / (2×10^9) = _____ milliseconds
Answer: YES / NO

Question 4: What's the bottleneck?
Answer: _____ (sorting is the most expensive step)

Question 5: How to optimize?
Answer: _____
```

**[THINK THROUGH THE ENTIRE PIPELINE]**

---

### ✅ Exercise 4.1 Solution

```
Complete analysis:

1. Receive quotes: O(n) where n = 1,000,000
   - Just reading from network, ~1 op per quote
   - Time: 1,000,000 ops

2. Sort by symbol: O(n log n)
   - n = 1,000,000
   - n log n = 1,000,000 × 20 ≈ 20,000,000 ops
   - Time: 20,000,000 ops

3. Group by symbol: O(n)
   - Single pass through sorted data
   - n = 1,000,000 ops

4. Find best trade per symbol: O(n)
   - For each quote, find best in its group
   - Total: n iterations across all quotes
   - n = 1,000,000 ops

Total time complexity: O(n) + O(n log n) + O(n) + O(n) = O(n log n)
Dominant term: Sorting

Space complexity:
- Input: O(n) = 1,000,000 quotes × 32 bytes ≈ 32 MB
- Sorted data: (in-place) O(1) auxiliary
- Groups: O(num_symbols) ≈ O(5000) = negligible
- Total: O(n) for input, O(1) auxiliary

Feasibility:
At 2 GHz (2 billion ops/sec):
20,000,000 ops / (2 × 10^9) = 0.01 seconds = 10 milliseconds

Can handle 1M quotes/sec? YES ✓
- 10 ms per batch
- Can process 100 batches in 1 second
- 100 batches × 1M quotes = 100M quotes/sec max

But wait, 1M quotes per second comes continuously:
- Need to process in < 1 ms (1,000,000 quotes in 1 second)
- 10 ms is too slow!

OPTIMIZATION NEEDED:
```

```
Optimizations:
1. Don't sort all quotes - maintain sorted order using balanced tree
2. Don't group - calculate best bid/ask incrementally
3. Use parallel processing - process multiple symbols simultaneously
4. Use approximate algorithms - don't need perfect sort, just approximate

Real solution:
Skip the global sort. Instead:
- Use hash table to bucket quotes by symbol: O(n)
- For each bucket, maintain heap of top quotes: O(n log k) where k=depth
- Total: O(n) or O(n log k) with k small

Time: 1,000,000 + 1,000,000 × 5 = 6,000,000 ops
At 2 GHz: 3 milliseconds ✓ (acceptable)
```

---

## Summary: Your Week 1 Mastery

If you can solve all 12 exercises, you've mastered:

**Day 1 Concepts:**
- ✅ Cache locality and memory layout
- ✅ Stack vs. heap allocation strategies
- ✅ Pointer reasoning

**Day 2 Concepts:**
- ✅ Time complexity analysis
- ✅ Recognizing O(n²) vs. O(n log n) problems
- ✅ Best, average, worst case analysis

**Day 5 Concepts:**
- ✅ Space complexity calculation
- ✅ Recursion depth and stack safety
- ✅ Space-time trade-offs

**Integration:**
- ✅ Analyzing complete systems
- ✅ Making real-world optimization decisions
- ✅ Predicting performance at scale

---

**End of Week 1 Comprehensive Exercises**
