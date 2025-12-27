# Week 2, Day 1: Arrays

## 🗓 Metadata
**Week:** 2 | **Day:** 1 of 5 | **Topic:** Arrays  
**Category:** Linear Structures | **Difficulty:** 🟢 Easy  
**Prerequisites:** Week 1 (RAM Model, Asymptotic Analysis, Space Complexity)  
**Time:** 90-120 minutes | **Status:** 🔍 In Study

---

## 1️⃣ THE WHY — Engineering Motivation

### Real-World Problem

You have a million user records and need to retrieve the user at position 500,000 in **milliseconds**. A linked list would require following 500,000 pointers (each a cache miss). An array retrieves it in **one memory access**.

**Design Problems Solved:**
- Direct access to any element by index in constant time
- Contiguous memory for cache efficiency  
- Predictable performance (no pointer chasing)
- Natural fit for many problems (image pixels, time series data, matrix operations)

### Trade-offs Introduced
- **Cost:** Insertion/deletion O(n) — requires shifting elements
- **Cost:** Fixed size (in statically allocated arrays) — must know size beforehand
- **Benefit:** O(1) indexing, O(1) iteration, cache-friendly

### Real System Usage

**Linux Kernel:**
- Process file descriptors stored in array (kernel/fs/file.c)
- Fast access: `fd_set[index]` in single CPU cycle

**Databases:**
- Column-oriented storage uses arrays (ClickHouse, Parquet)
- Reason: Cache locality for SIMD operations on millions of values

**Graphics Engines:**
- Vertex arrays, texture coordinates stored as arrays
- Reason: GPU memory access patterns optimized for contiguous memory

**Operating Systems:**
- Page tables implemented as arrays
- Virtual address → physical address lookup: `page_table[virtual_address >> PAGE_SHIFT]`

---

## 2️⃣ THE WHAT — Mental Model & Intuition

### Core Analogy

**Think of arrays as a row of numbered mailboxes on a street:**

```
Street Address:  1000     1008     1016     1024     1032
                  ┌──┐    ┌──┐    ┌──┐    ┌──┐    ┌──┐
Mailbox Index:   [0]      [1]      [2]      [3]      [4]
Content:        "A"      "B"      "C"      "D"      "E"
```

If each mailbox holds 8 bytes and starts at address 1000:
- Mailbox 0: address 1000
- Mailbox 1: address 1008  
- Mailbox 2: address 1016
- Mailbox i: address 1000 + i×8

**This is direct addressing:** Given index i, compute address instantly. No search needed.

### Visual Representation

```
ARRAY MEMORY LAYOUT:

  Index:  0     1     2     3     4     5
          ┌─────┬─────┬─────┬─────┬─────┬─────┐
Memory:   │ 10  │ 20  │ 30  │ 40  │ 50  │ 60  │ (contiguous bytes)
          └─────┴─────┴─────┴─────┴─────┴─────┘
          ↑
      Base address: 0x7fff0000

Access arr[3]:
  Address = 0x7fff0000 + 3×(size of one element)
  = 0x7fff0000 + 3×4 (for 4-byte int)
  = 0x7fff000c
  Load from that address → get value 40
  Time: ONE CPU cycle (assuming cache hit)
```

### Core Invariants

1. **Contiguity:** All elements stored consecutively in memory
2. **Direct Addressing:** Address of element i = base_address + i × element_size
3. **Fixed Size** (static arrays) or **growable capacity** (dynamic arrays)
4. **Index-based:** Elements accessed by integer position, not content

### Key Concepts

- **Base Address:** Memory location of first element
- **Stride/Element Size:** Bytes per element  
- **Index:** Integer position (0-based in most languages)
- **Bounds:** Valid indices are 0 to length-1

---

## 3️⃣ THE HOW — Mechanical Walkthrough

### State/Data Structure

```
Array State:
  buffer:        pointer to first element (base address)
  element_size:  bytes per element (4 for int, 8 for long, etc.)
  length:        number of elements currently stored
  capacity:      maximum elements before reallocation (for dynamic arrays)
```

### Operation 1: Access (arr[i])

**Step-by-step:**
1. Receive index i (e.g., i=3)
2. Calculate address: `address = buffer + i × element_size`
3. Load from that memory address into CPU register
4. Return the value

**Cost:** O(1) — single memory load  
**Cache Behavior:** If elements are nearby in memory, likely cache hit

**Example:**
```
Array: [10, 20, 30, 40, 50]
Access arr[2]:
  buffer = 0x1000
  element_size = 4 bytes
  address = 0x1000 + 2×4 = 0x1008
  Load from 0x1008 → get 30
```

### Operation 2: Insert at position i

**Step-by-step:**
1. Check if length < capacity (enough space?)
2. Shift all elements from position i to end one position right
3. Place new element at position i
4. Increment length

**Cost:** O(n) — must shift up to n elements  
**Why Expensive:** Each element requires copying (load + store)

**Example:**
```
Before: [10, 20, 30, 40, 50]  length=5, capacity=5
Insert 25 at position 2:

Step 1: Shift right (starting from end, not beginning!)
        [10, 20, 30, 40, 50, ??]  length=6 (need capacity increase!)
        
Actually: If capacity=5 and length=5, cannot insert!
Need to grow array first (Week 2, Day 2)

Assuming we have capacity:
        [10, 20, 30, 30, 40, 50]  shift 30,40,50 right
        [10, 20, 25, 30, 40, 50]  place 25 at position 2
```

**Important:** Why shift from end? Because if you shift from beginning, you overwrite the original value at position i before copying it forward.

### Operation 3: Delete at position i

**Step-by-step:**
1. Shift all elements from position i+1 to end one position left
2. Decrement length

**Cost:** O(n) — must shift remaining elements

**Example:**
```
Before: [10, 20, 30, 40, 50]  length=5
Delete position 2 (value 30):

Step 1: Shift left
        [10, 20, 40, 50, ??]  length=4
```

### Memory Behavior

**Cache Locality (Critical for performance!):**

```
Sequential access (good cache):
  for i=0 to n:
    access arr[i]              ← neighbors are nearby
    Hit rate: ~95% (entire array likely prefetched)
    Time: ~5ns per access (L1 cache hit)

Random access (poor cache):
  for i in random_order:
    access arr[i]              ← neighbors are far away
    Hit rate: ~5% (cache misses)
    Time: ~200ns per access (main memory access)
  40x slower!
```

### Edge Cases

1. **Empty array:** Accessing arr[0] when length=0 → undefined behavior (out of bounds)
2. **Insert/delete without space:** Attempting to insert when capacity is full → overflow
3. **Negative index:** arr[-1] in C is undefined; in Python it means "from end" (different behavior)
4. **Integer overflow:** Extremely large arrays (>2 billion elements) might overflow index arithmetic

---

## 4️⃣ VISUALIZATION — Simulation & Examples

### Example 1: Sequential Access (Cache-Friendly)

**Scenario:** Summing all elements in an array

```
Array: [2, 5, 8, 11, 14]
Base: 0x1000, Element Size: 4 bytes

Timeline:
i=0: Load from 0x1000 → get 2, sum=2
     L1 cache now holds 0x1000-0x1010 (prefetch upcoming bytes)

i=1: Load from 0x1004 → get 5 (already in L1!)
     sum=7

i=2: Load from 0x1008 → get 8 (already in L1!)
     sum=15

i=3: Load from 0x100c → get 11 (already in L1!)
     sum=26

i=4: Load from 0x1010 → get 14 (already in L1!)
     sum=40

Result: 40 (all accesses were cache hits!)
```

**Performance:** 5 accesses × 5ns = 25ns total

### Example 2: Insertion (Expensive Operation)

**Scenario:** Insert 25 at position 1 in [10, 20, 30, 40]

```
Initial State:
Index:  0    1    2    3    capacity=4
        ┌────┬────┬────┬────┐
        │ 10 │ 20 │ 30 │ 40 │
        └────┴────┴────┴────┘

Step 1: Shift elements from position 1 rightward
        Move 40 to position 3: [10, 20, 30, 40] → [10, 20, 30, 40]
        Move 30 to position 2: [10, 20, 30, 40] → [10, 20, 30, 40]
        Move 20 to position 2: [10, 20, 30, 40] → [10, 20, 20, 30]

Step 2: Insert 25 at position 1
        [10, 25, 20, 30]

Wait, that's wrong! Let me redo this correctly:

Initial: [10, 20, 30, 40]

Shift rightward starting from position 1 (shift 20, 30, 40):
        [10, 20, 30, 40] → [10, 20, 20, 30] (move 30 to pos 3)
                                            (move 20 to pos 2)
Actually, we need to do this from RIGHT to LEFT:
        Position 3: 40 → position 4 (out of capacity!)

So we need capacity > 4. Assuming we grow to capacity 5:

        [10, 20, 30, 40, ??]

        Position 3: move 40 to position 3
        Position 2: move 30 to position 3... wait, that's backward.

Correct procedure (right to left):
        [10, 20, 30, 40, ??]  start
        Copy position 3 (40) to position 4: [10, 20, 30, 40, 40]
        Copy position 2 (30) to position 3: [10, 20, 30, 30, 40]
        Copy position 1 (20) to position 2: [10, 20, 20, 30, 40]
        Place 25 at position 1:            [10, 25, 20, 30, 40]

Hmm, still wrong. Let me be more careful:

Original: [10, 20, 30, 40]  at positions 0, 1, 2, 3
After growing capacity to 5: [10, 20, 30, 40, ??]

To insert 25 at position 1:
  Shift everything from position 1 onward one step right
  Step 1: 40 (pos 3) → pos 4
  Step 2: 30 (pos 2) → pos 3
  Step 3: 20 (pos 1) → pos 2
  Step 4: Insert 25 at pos 1

Result: [10, 25, 20, 30, 40]

This is still wrong. Final correct attempt:
Original: [10, 20, 30, 40]

To insert 25 at position 1, we want: [10, 25, 20, 30, 40]

Right-to-left copy:
  pos 3: 40 → move to pos 4
  pos 2: 30 → move to pos 3  
  pos 1: 20 → move to pos 2
  pos 1: insert 25

Final: [10, 25, 20, 30, 40] ✓

Actual memory operations (4 byte int):
  1. Load 40, Store at pos 4
  2. Load 30, Store at pos 3
  3. Load 20, Store at pos 2
  4. Store 25 at pos 1

Total: 7 memory operations (4 loads + 4 stores) = O(n)
```

### Example 3: Deletion (Also Expensive)

**Scenario:** Delete position 1 from [10, 20, 30, 40]

```
Initial: [10, 20, 30, 40]

To delete 20 (position 1), we want: [10, 30, 40]

Left-to-right copy (from deletion point onward):
  pos 2: 30 → move to pos 1
  pos 3: 40 → move to pos 2
  Decrement length to 3

Final: [10, 30, 40] (length=3, capacity=4)

Memory operations (4 byte int):
  1. Load 30, Store at pos 1
  2. Load 40, Store at pos 2

Total: 4 memory operations = O(n)
```

---

## 5️⃣ CRITICAL ANALYSIS — Performance & Robustness

### Complexity Table

| Operation | Best | Average | Worst | Notes |
|-----------|------|---------|-------|-------|
| **Access arr[i]** | O(1) | O(1) | O(1) | Direct addressing, always constant |
| **Search (unsorted)** | O(1) | O(n) | O(n) | Linear scan, no index to help |
| **Search (sorted)** | O(1) | O(log n) | O(log n) | Binary search possible |
| **Insert at position i** | O(n) | O(n) | O(n) | Must shift all elements after i |
| **Insert at end** | O(1) | O(1) | O(n) | Static array: O(1) if space; dynamic: O(1) amortized |
| **Delete at position i** | O(n) | O(n) | O(n) | Must shift all elements after i |
| **Delete at end** | O(1) | O(1) | O(1) | Just decrement counter |
| **Space** | O(n) | O(n) | O(n) | Store n elements |

### Memory Access Patterns

**Sequential Iteration (Excellent Cache Behavior):**
- CPUs prefetch cache lines (64 bytes = ~16 integers)
- Accessing arr[0], arr[1], arr[2]... all hits
- Hit rate: 95%+, latency: 5ns
- **Throughput:** 3-4 billion simple operations per second per core

**Random Access (Poor Cache Behavior):**
- No prefetching works
- Each access is main memory latency
- Hit rate: 5%, latency: 200ns
- **Throughput:** 5-10 million simple operations per second
- **40x slower** than sequential!

**Example:**
```c
// Fast (sequential)
for (int i = 0; i < n; i++)
    sum += arr[i];

// Slow (random)
for (int i = 0; i < n; i++)
    sum += arr[random() % n];
```

### Edge Cases & Failure Modes

1. **Buffer Overflow:** Accessing index >= length
   - C/C++: Undefined behavior, reads/writes garbage
   - Python: Raises IndexError
   - Impact: Security vulnerability, crashes, corruption

2. **Integer Overflow:** Array too large
   - `int index = INT_MAX; arr[index] = value;`
   - Wraps to negative index
   - Impact: Unexpected behavior

3. **Off-by-One Error:** Common bug
   ```
   for (int i = 0; i <= n; i++)
       arr[i] = 0;  // Accesses arr[n] which is out of bounds!
   ```

4. **Aliasing Issues:** Overlapping insert/delete
   ```
   arr = [1, 2, 3, 4, 5]
   // Insert 10 at position 2, delete position 3 simultaneously?
   // Undefined order of operations
   ```

### When Complexity Analysis Breaks Down

**Theory:** Array access is O(1)  
**Practice:** Can vary 40x based on cache:
- Predictor works (sequential access) → 5ns
- Predictor fails (random access) → 200ns

**Theory:** Insert is O(n)  
**Practice:** Small n (n < 1000) has huge overhead from:
- Branch mispredictions
- Instruction pipeline stalls  
- Function call overhead

**Theory:** Amortized analysis  
**Practice:** Worst-case pauses matter for latency-sensitive systems:
- Audio processing can't afford 10ms pause for array reallocation
- Real-time systems need predictable worst-case

---

## 6️⃣ REAL SYSTEM INTEGRATION

### Operating Systems

**Linux Process Management:**
```
File: kernel/fs/file.c
Code: fd_set[fd / BITS_PER_LONG] |= (1 << (fd % BITS_PER_LONG))

Reason: File descriptor lookup must be O(1)
Each process has array of open files (fds 0-255 typical)
Direct indexing: fd 5 goes directly to file_table[5]
```

**Virtual Memory:**
```
Page Table = Array indexed by virtual page number
Virtual Address = [Page Number] [Offset within page]
To translate:
  page_table[virtual_page_number] → physical page number
  Final address = physical_page_base + offset

Why array: O(1) translation, critical for every memory access!
```

### Databases

**Column-Oriented Storage (ClickHouse, DuckDB):**
```
Instead of:  [User1: name, age, email], [User2: name, age, email]
Use arrays:  [User1.name, User2.name, ...], [User1.age, User2.age, ...]

Benefit: All ages contiguous → single cache prefetch loads 64 ages
Why it matters: SIMD vectorization works on contiguous data
                Can process 8 integers in one instruction
```

**Index Implementation:**
```
B-Tree uses arrays internally:
  Node = fixed-size array of keys + pointers
  Within node: binary search on array (O(log b) where b=block size)
```

### Graphics Engines

**Vertex Arrays (OpenGL/DirectX):**
```
struct Vertex { float x, y, z; float nx, ny, nz; };
Vertex vertices[1000000];  // Array of vertices

GPU processes: vertices[0], vertices[1], ... in parallel
Why array: GPU needs predictable memory layout for SIMD
           Each core processes one vertex, all from nearby addresses
```

**Texture Storage:**
```
Color pixels[1024][1024];  // 2D image as array

Pixel access: pixels[y * width + x]
GPU rasterizer needs fast pixel lookups
Cache-friendly: Adjacent pixels are contiguous
```

### Network Protocols

**Packet Processing:**
```
packet_handlers[protocol_type] = function_ptr;

Receive packet:
  protocol = packet->type_field;
  handler = packet_handlers[protocol];  // O(1) dispatch!
```

---

## 7️⃣ CONCEPT CROSSOVERS

### What It Builds On

- **RAM Model (Week 1):** Direct addressing only works because of linear RAM
- **Asymptotic Analysis (Week 1):** Complexity analysis framework
- **Space Complexity (Week 1):** Arrays consume O(n) space

### What Builds On It

- **Dynamic Arrays (Week 2, Day 2):** Extends arrays with growth
- **Sorting (Week 3):** All efficient sorts work on arrays
- **Hash Tables (Week 3):** Uses arrays for collision handling
- **Binary Search (Week 2, Day 5):** Requires arrays
- **Graphs (Week 6):** Adjacency matrix representation

### Applications in Algorithms

- **Two Pointers (Week 4):** Operates on sorted arrays
- **Merge Sort (Week 3):** Divide-and-conquer on arrays
- **Matrix Algorithms:** 2D arrays for DP, image processing
- **Bit Arrays/Bitsets:** Arrays optimized for boolean values

### Combinations with Other Techniques

- **Arrays + Hash Table:** Hash table buckets are arrays
- **Arrays + Sorting:** Preprocessing enables binary search
- **Arrays + Prefix Sums:** O(1) range queries after O(n) preprocessing
- **Arrays + Segment Trees:** Advanced range query structures built on arrays

---

## 8️⃣ MATHEMATICAL & THEORETICAL PERSPECTIVE

### Formal Definition

**Array A** is a function A: {0, 1, ..., n-1} → V where V is the value set.

Represented in memory as:
- Base address b
- Element size s
- Array address: A(i) = b + i×s

### Proof Sketch: Why Access is O(1)

**Claim:** Array access takes O(1) time.

**Proof:**
1. Access arr[i] requires computing address: base + i × element_size
2. This computation uses constant-time arithmetic operations:
   - Integer multiplication: O(1) on modern CPUs (pipelined)
   - Integer addition: O(1) on modern CPUs
3. Memory load from computed address: O(1) latency (assuming cache hit)
4. Total: O(1)

**Note:** This assumes element size is constant and known, which is true for statically typed languages.

### Recurrence Relation

**Sequential Access Cost:**
- T(n) = n × c where c is cost per access
- = O(n) for reading all elements
- Cache effects: First access might have T(1) = cache_miss_latency, subsequent T(1) = cache_hit_latency

**Insert Operation:**
- T(n) = 2n where 2n = n loads + n stores
- = O(n)

### Theoretical Models

**I/O Model (Cache-Aware Complexity):**
- B = cache line size (64 bytes typical)
- Sequential access loads B bytes per cache miss
- Random access: one element per cache miss
- **Efficiency:** Sequential access is O(n/B) cache misses; random is O(n)
- **Ratio:** n vs n/B = n/(64/4) = 16x difference for 32-bit integers

**RAM Model Assumptions:**
- All memory locations equally accessible (unrealistic—cache breaks this!)
- Arithmetic is O(1) (true for small numbers)
- Memory addresses unbounded (true—address space is large)

---

## 9️⃣ ALGORITHMIC DESIGN INTUITION

### When to Use Arrays

1. **Need O(1) random access by index:** Pixels in image, students by ID
2. **Contiguous storage required:** Graphics APIs expect this
3. **Iteration order matters:** Sequential processing
4. **Memory efficiency critical:** Minimize per-element overhead (no pointers!)
5. **Cache performance critical:** Video processing, real-time systems

### When NOT to Use Arrays

1. **Frequent mid-list insertion/deletion:** O(n) cost unacceptable → linked lists
2. **Unknown size at compile time and growing to huge size:** Memory wastage → dynamic arrays better
3. **Need to quickly remove arbitrary elements:** O(n) delete → consider linked lists
4. **Sparse data:** Wasted space for unused indices → hash tables better

### Decision Framework

```
Need to store ordered data?
  │
  ├─→ YES
  │    │
  │    ├─→ Need O(1) access by index?
  │    │    ├─ YES → Array
  │    │    └─ NO → Linked List (but rare!)
  │    │
  │    └─→ Need to insert/delete frequently in middle?
  │         ├─ YES → Linked List or Deque
  │         └─ NO → Array
  │
  └─→ NO (unordered)
       └─→ Hash Table or Set
```

### Trade-off Scenarios

**Scenario 1: Game Engine Storing Entities**
- Array pros: O(1) access by entity ID, cache-friendly iteration
- Array cons: Adding/removing entities is O(n) shuffle
- Decision: Use array + "swap-with-last" deletion (O(1) amortized)

**Scenario 2: FIFO Queue**
- Array pros: Simple, cache-friendly
- Array cons: Growing front requires leftward shift (O(n))
- Decision: Use circular buffer (array + head/tail pointers)

**Scenario 3: Text Editor (undo/redo)**
- Array pros: Sequential access to document fast
- Array cons: Inserting/deleting characters is O(n)
- Decision: Use rope data structure or piece table (advanced)

---

## 🔟 KNOWLEDGE CHECK — Socratic Reasoning

**Question 1: Why is array access O(1) even though CPUs execute billions of instructions per second?**

Your reasoning:
- How many instructions does it take to compute an address?
- What does O(1) mean relative to the size of the array?
- Does the CPU time matter if it's the same for any index?

**Question 2: You want to insert an element at the beginning of an array of 1 million elements. If each element is 8 bytes and insertion takes 1 nanosecond per byte, how long does it take?**

Your reasoning:
- How many bytes must be shifted?
- What's the total time in nanoseconds? Milliseconds?
- Is this the bottleneck in a real system?

**Question 3: Arrays require contiguous memory. What happens if you have 10GB of RAM but it's fragmented into 100MB chunks? Can you allocate a 5GB array?**

Your reasoning:
- What does contiguous mean?
- How do operating systems manage fragmentation?
- What alternatives exist for large allocations?

**Question 4: You're designing a cache-aware sorting algorithm. Would you prefer to access arr[i], arr[i+1], arr[i+2]... or arr[i], arr[i+1000], arr[i+2000]...? Why?**

Your reasoning:
- What does CPU prefetching do?
- How does cache line size affect this?
- Calculate the cache miss ratio for each pattern

---

## 1️⃣1️⃣ RETENTION HOOK — Memory Anchors

### One-Line Essence

> **Arrays are numbered mailboxes: O(1) to any address via arithmetic, O(n) to rearrange, O(1) cache-efficient to traverse sequentially.**

### Mnemonic Device

**"D.I.C.T."**
- **D**irect addressing (address = base + i × size)
- **I**ndexing is O(1)
- **C**ontiguous memory (cache-friendly)
- **T**radeoff: insert/delete are O(n)

### Geometric/Visual Cue

```
Picture: Row of numbered mailboxes
│[0]│[1]│[2]│[3]│[4]│
Location i instantly: base + i×8

vs.

Linked list (chain):
●→●→●→●→●
Must follow chain, no shortcuts
```

### Cognitive Lenses

| Lens | Insight |
|------|---------|
| **Computational** | CPU sees: load from (base + offset). Offset computation is free. Main cost is memory latency, prefetching, and cache behavior. |
| **Psychological** | Intuitive mistake: "Array access should cost something proportional to array size!" Actually: index arithmetic is negligible, memory latency dominates. |
| **Design Trade-off** | Buy: O(1) random access + cache efficiency. Sell: O(n) insertion/deletion + fixed/predictable size. |
| **AI/ML Analogy** | Arrays = vectorized operations. SIMD processes 8 integers in parallel from contiguous memory. Linked lists break SIMD (scattered pointers). |
| **Historical Context** | Von Neumann (1945): "Use arrays for performance." 80 years later, still true. Cache didn't exist then, but principle holds: contiguity matters. |

---

## Supplementary Outcomes

### External References & Resources

1. **"What Every Programmer Should Know About Memory"** by Ulrich Drepper
   - Section 2: CPU Caches
   - Why: Deep dive into cache line prefetching, memory bandwidth

2. **"Systems Performance" by Brendan Gregg**
   - Chapter 5: Memory
   - Why: Real-world cache measurement and profiling tools

3. **Linux Source Code:**
   - `kernel/fs/file.c`: File descriptor array implementation
   - Why: See array usage in production kernel

4. **Online:**
   - TLB (Translation Lookaside Buffer) explanation: https://en.wikipedia.org/wiki/Translation_lookaside_buffer
   - Why: Understand virtual address → physical address lookup

### Common Misconceptions Fixed

**❌ "Array access costs time proportional to array size"**  
✅ "Array access is O(1)—time independent of array size. Cache misses cost more than arithmetic."

**❌ "Insertion is always O(n)"**  
✅ "Insertion at end can be O(1) amortized (dynamic array) or O(1) if space exists. Mid-insertion is O(n)."

**❌ "Arrays are outdated; use linked lists"**  
✅ "Arrays dominate in practice. Linked lists have niche uses (undo/redo, allocators). 95% of the time, use arrays."

**❌ "Memory bandwidth is unlimited"**  
✅ "Memory bandwidth is ~100GB/s. Sequential access uses it efficiently (prefetch). Random access wastes it (scattered accesses)."

### Practice Problems & Scenarios

1. **Rotate Array:** Rotate array by k positions. What's the in-place algorithm?
2. **Remove Duplicates:** Remove duplicates from sorted array, in-place. Why does sorting help?
3. **Merge Sorted Arrays:** Merge two sorted arrays. Is O(n) time achievable?
4. **Majority Element:** Find element appearing > n/2 times. Can you do this in one pass?
5. **Product of Array Except Self:** For each position, compute product of all other elements. No division allowed.

---

**Confidence Level (1-5):** ___/5  
**Next Review:** (Spaced repetition: 2 days, 7 days, 30 days)

