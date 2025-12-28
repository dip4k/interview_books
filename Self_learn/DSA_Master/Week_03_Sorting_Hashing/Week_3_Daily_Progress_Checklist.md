# Week 3: Daily Progress Checklist & Interview Q&A

## ✅ DAY 1: Elementary Sorts

### Morning Learning Objectives
- [ ] Understand bubble sort mechanics (bubble to end)
- [ ] Understand insertion sort mechanics (card hand model)
- [ ] Understand selection sort mechanics (find minimum repeatedly)
- [ ] Know O(n²) timing and when acceptable
- [ ] Trace all 3 sorts on same array by hand

### Afternoon Practice (3-4 problems)
- [ ] Implement bubble sort (LeetCode variant)
- [ ] Implement insertion sort (LeetCode variant)
- [ ] Implement selection sort (LeetCode variant)
- [ ] Compare performance on nearly-sorted data

### Evening Review
- [ ] Trace one complete sort by hand
- [ ] Compare all 3 sorts (swaps, shifts, stability)
- [ ] Answer 5+ Q&A from interview section

**Confidence Rating Day 1:** ___ / 5

---

## ✅ DAY 2: Merge Sort & Quick Sort

### Morning Learning Objectives
- [ ] Understand divide-and-conquer principle
- [ ] Understand merge sort (divide, merge upward)
- [ ] Understand quick sort (partition by pivot)
- [ ] Know O(n log n) guarantee vs average
- [ ] Understand why merge is stable

### Afternoon Practice (3-4 problems)
- [ ] Implement merge sort
- [ ] Implement quick sort with Hoare partition
- [ ] Practice on random arrays
- [ ] Test on sorted/reverse-sorted data

### Evening Review
- [ ] Trace merge sort dividing and merging phases
- [ ] Trace quick sort partition step
- [ ] Compare merge vs quick trade-offs

**Confidence Rating Day 2:** ___ / 5

---

## ✅ DAY 3: Heap Sort

### Morning Learning Objectives
- [ ] Understand heap invariant
- [ ] Understand heapify-down operation
- [ ] Understand build-heap phase (O(n))
- [ ] Know extract phase (n log n)
- [ ] Why heap sort is only guaranteed in-place

### Afternoon Practice (3-4 problems)
- [ ] Implement heap sort
- [ ] Implement max-heap building
- [ ] Trace extraction phase
- [ ] Verify in-place behavior

### Evening Review
- [ ] Trace heapify-down on example
- [ ] Understand why O(n log n) despite O(n) build

**Confidence Rating Day 3:** ___ / 5

---

## ✅ DAY 4: Hash Tables I

### Morning Learning Objectives
- [ ] Understand hash function (deterministic mapping)
- [ ] Understand collision (multiple keys → same bucket)
- [ ] Understand load factor (n/m)
- [ ] Know chaining approach
- [ ] Understand rehashing trigger

### Afternoon Practice (3-4 problems)
- [ ] Design hash function
- [ ] Implement hash table with chaining
- [ ] Handle collisions
- [ ] Test load factor scenarios

### Evening Review
- [ ] Understand hash → index conversion
- [ ] Know when collisions happen
- [ ] Answer hash-specific Q&A

**Confidence Rating Day 4:** ___ / 5

---

## ✅ DAY 5: Hash Tables II

### Morning Learning Objectives
- [ ] Understand open addressing (probing)
- [ ] Understand linear probing (i+1, i+2, ...)
- [ ] Understand quadratic probing (i², reduction of clustering)
- [ ] Understand double hashing (different hash2)
- [ ] Compare chaining vs open addressing

### Afternoon Practice (3-4 problems)
- [ ] Implement open addressing with linear probing
- [ ] Implement double hashing
- [ ] Handle deletion (tombstones)
- [ ] Compare performance with chaining

### Evening Review
- [ ] Trace open addressing probing sequence
- [ ] Understand primary clustering problem
- [ ] Compare implementation trade-offs

**Confidence Rating Day 5:** ___ / 5

---

## 🎯 INTERVIEW Q&A REFERENCE (50+ Pairs)

### ELEMENTARY SORTS (6 Pairs)

**Q1: Why is bubble sort O(n) best case but selection sort always O(n²)?**
A: Bubble sort detects when sorted (no swaps) and exits early. Selection must find minimum each time, no early exit possible.

**Q2: What's the practical difference between bubble and insertion sort?**
A: Insertion shifts elements (one operation per gap). Bubble swaps (two operations per pair). Insertion faster in practice despite same O(n²).

**Q3: Can we optimize selection sort for minimizing writes?**
A: Yes, selection sort has only n swaps (each element written once). Good for write-constrained storage.

**Q4: When would you use elementary sorts in production?**
A: Small arrays (< 50), embedded systems (limited memory), educational purposes. Python/C++ use insertion sort for tiny partitions.

**Q5: How do you detect if array is already sorted?**
A: Add flag. If no swaps/shifts in full pass, array sorted. Exit early.

**Q6: What's the memory overhead of each elementary sort?**
A: All O(1) in-place (no extra array). Recursion: none. Pointers: only loop indices.

---

### MERGE SORT (6 Pairs)

**Q1: Why is merge sort O(n log n) guaranteed?**
A: Recursion depth O(log n), each level processes all n elements during merge → O(n log n) total.

**Q2: Can merge sort be done in-place?**
A: Theoretically yes, but complex. Usually O(n) extra space for merge buffer.

**Q3: How does merge preserve stability?**
A: When values equal, we take from left array first. This preserves original order.

**Q4: Is merge sort used in production?**
A: Yes. Linux sort command, Python Timsort uses merge principles, databases use external merge sort.

**Q5: What's the space trade-off for merge sort?**
A: O(n) extra space for temporary arrays during merge. Can't avoid without complex in-place merge.

**Q6: How does merge sort handle large datasets?**
A: Merge sort is standard for external sorting (data on disk). Divides into chunks, sorts, merges.

---

### QUICK SORT (6 Pairs)

**Q1: Why is quick sort O(n log n) average but O(n²) worst case?**
A: Depends on pivot choice. Good pivot (median) → balanced tree → O(n log n). Bad pivot (smallest) → skewed tree → O(n²).

**Q2: How does pivot selection affect performance?**
A: Random pivot usually prevents worst case. Median-of-three heuristic improves. Bad pivot selection causes O(n²).

**Q3: Can quick sort be made stable?**
A: Yes, but requires extra space for subarrays. Usually unstable version used (simpler, faster).

**Q4: How does quick sort's O(log n) space work?**
A: Recursion stack depth O(log n) average, O(n) worst. In-place partitioning uses no extra array.

**Q5: When is quick sort preferred over merge sort?**
A: Average-case speed usually wins. Less memory overhead. Practical for general sorting.

**Q6: How does Introsort avoid quick sort's worst case?**
A: Starts with quick sort. If recursion depth exceeds threshold → switches to heap sort. Hybrid safety.

---

### HEAP SORT (6 Pairs)

**Q1: Why is heap sort's build phase O(n) not O(n log n)?**
A: Heapify from bottom half upward. Early elements have little height to bubble. Total: O(n) amortized.

**Q2: Why is heap sort rarely used despite guarantees?**
A: Slower average than quick sort. Constant factors poor. But guaranteed O(n log n) and O(1) space valuable in some systems.

**Q3: Can you use heap sort for k largest elements?**
A: Yes. Build max-heap, extract k times → O(n + k log n). Or use min-heap, maintain size k → O(n log k).

**Q4: How does heap invariant ensure correctness?**
A: Parent ≤ children (min-heap) always maintained. Root always minimum. Extraction gives sorted sequence.

**Q5: Why is heap sort not used for external sorting?**
A: Requires random access (array indexing). External sort uses sequential access (merge sort better).

**Q6: What's the practical use case for heap sort?**
A: Guaranteed O(n log n) + O(1) space. Real-time systems, memory-constrained embedded systems, safety-critical code.

---

### HASH TABLES I (6 Pairs)

**Q1: What makes a good hash function?**
A: Deterministic (same input → same output). Uniform distribution (minimize collisions). Fast to compute. Avalanche effect (small change → big hash change).

**Q2: Why do collisions happen despite good hash function?**
A: By pigeonhole principle, with m buckets and > m items, collisions inevitable. Even perfect hash with probability 1/m per pair.

**Q3: What does load factor α = n/m mean?**
A: Average chain length (chaining) or fullness (open addressing). α > 0.75 triggers rehashing. Higher α → more collisions.

**Q4: How does rehashing work?**
A: Create new table (usually double size). Re-hash all items. O(n) operation. Done when α exceeds threshold.

**Q5: Why is hash function design critical?**
A: Bad hash → all items same bucket → O(n) per lookup. Good hash → uniform distribution → O(1) average.

**Q6: What's universal hashing?**
A: Mathematically proven: P(collision) ≤ 1/m for any two keys. Stronger than just "good distribution".

---

### HASH TABLES II (6 Pairs)

**Q1: What's primary clustering in open addressing?**
A: Items cluster around original hash position. Poor pivot → long probes. Double hashing prevents this.

**Q2: Why can't open addressing's load factor exceed 1?**
A: All n items need slots in m buckets. Can't overfill. So max α = 1 (full table).

**Q3: How does quadratic probing reduce clustering?**
A: Instead of i, i+1, i+2... probe h + 1², h + 2², h + 3². Creates different probe sequences.

**Q4: What's the difference between linear and quadratic probing?**
A: Linear: sequential (+1, +2, +3). Quadratic: squares (+1, +4, +9). Quadratic better distribution, prevents clustering.

**Q5: Why is deletion difficult in open addressing?**
A: Can't delete items (breaks probe chain). Mark as TOMBSTONE instead. Tombstones accumulate → rehash needed.

**Q6: When do you choose chaining vs open addressing?**
A: Chaining: simpler, allows α > 1, easier deletion. Open addressing: better cache (linear memory), less space overhead.

---

### CROSS-ALGORITHM (5 Pairs)

**Q1: Compare merge vs quick sort for large data?**
A: Merge: guaranteed O(n log n), stable, good for external sort, needs O(n) space. Quick: faster average, in-place, unstable, risk O(n²).

**Q2: When would you choose heap sort over quick sort?**
A: When worst-case guarantee matters, or O(1) space required. Quick sort faster average, but no guarantee.

**Q3: Compare sorting vs hashing for duplicate detection?**
A: Sorting: O(n log n), then linear scan. Hashing: O(n) average, simpler. Hash better unless sorting useful for other reasons.

**Q4: Can hashing solve all problems that sorting solves?**
A: No. Hashing for lookup/counting. Sorting for ordering, ranges, k-largest. Different problems, complementary solutions.

**Q5: How do Timsort and Introsort combine multiple algorithms?**
A: Timsort: insertion + merge. Introsort: quick + heap + insertion. Hybrids optimize for different data patterns and safety.

---

## 📊 Daily Self-Assessment

| Day | Understanding | Implementation | Confidence |
|-----|---|---|---|
| **1 (Elementary)** | ___ / 5 | ___ / 5 | ___ / 5 |
| **2 (Merge/Quick)** | ___ / 5 | ___ / 5 | ___ / 5 |
| **3 (Heap)** | ___ / 5 | ___ / 5 | ___ / 5 |
| **4 (Hash I)** | ___ / 5 | ___ / 5 | ___ / 5 |
| **5 (Hash II)** | ___ / 5 | ___ / 5 | ___ / 5 |

**Target:** 4/5+ on all before Week 4

---

## ✅ WEEK 3 COMPLETION CHECKLIST

- [ ] Completed all 5 days instructional content
- [ ] Implemented all 6 sorting algorithms from scratch
- [ ] Implemented hash tables (chaining + open addressing)
- [ ] Solved 40+ practice problems (8+ per topic)
- [ ] Answered all 50+ interview Q&A pairs
- [ ] Rate 4/5+ confidence on all algorithms
- [ ] Can identify problem type using decision tree
- [ ] Know 3+ real-world systems per algorithm
- [ ] Traced each algorithm by hand (10+ examples)
- [ ] Ready for Week 4 (Problem-Solving Patterns)

---

**Status:** ✅ Week 3 Complete  
**Next:** Week 4 - Two-Pointers, Sliding Window, Prefix Sum, Cycle Detection

