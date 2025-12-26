# Week_2_QA.md

## ❓ Week 2 Comprehensive Q&A (10 per Topic)

---

### Day 1 — Arrays (Contiguous Memory, Cache Locality)

1. **Q:** Why does array traversal benefit from spatial locality?  
   **A:** Because elements reside contiguously, fetching one element pulls its neighbors into cache lines, enabling low-latency sequential access.

2. **Q:** How is array index `i` translated to a memory address?  
   **A:** `address = base_pointer + i * element_size`, leveraging fixed-size elements and contiguous layout.

3. **Q:** What happens if you treat array indexing as O(1) without considering cache behavior?  
   **A:** You ignore significant constant factors—cache misses can turn theoretical O(1) into high-latency accesses, especially with poor access patterns.

4. **Q:** Why is `sizeof(arr)` different from `sizeof(ptr)` in C?  
   **A:** An array has embedded length at compile time; a pointer decays to address only, losing size information.

5. **Q:** When does row-major vs column-major order matter?  
   **A:** During multi-dimensional access; mismatched traversal order causes cache misses due to poor spatial locality.

6. **Q:** How can arrays incur alignment-related penalties?  
   **A:** If elements aren’t aligned to the CPU’s expected boundaries, loads can cause extra cycles or even faults on strict architectures.

7. **Q:** Why are arrays preferred over linked lists for iteration-heavy workloads?  
   **A:** Arrays leverage contiguous memory, minimizing pointer indirection and maximizing cache utilization.

8. **Q:** Can arrays be resized in low-level languages?  
   **A:** No. Once allocated, length is fixed; dynamic resizing requires allocating new array and copying.

9. **Q:** How do arrays map onto hardware instructions?  
   **A:** CPUs perform pointer arithmetic in registers, then issue load/store instructions; hardware prefetchers detect stride-1 access.

10. **Q:** What real systems rely on arrays for performance?  
    **A:** Kernel structures (process tables), database pages, networking descriptor rings, GPU vertex buffers—all exploit contiguous memory.

---

### Day 2 — Dynamic Arrays (Automatic Growth, Amortized Analysis)

1. **Q:** Why does doubling capacity yield amortized O(1) appends?  
   **A:** Total copies over n appends sum to <2n; average cost per append remains constant despite occasional O(n) reallocations.

2. **Q:** What happens to pointers into a dynamic array after resize?  
   **A:** They become invalid; data moves to new memory, so external references must not be reused.

3. **Q:** How does growth factor selection affect performance?  
   **A:** Small factors (e.g., 1.2) reduce memory waste but increase resize frequency; larger factors reduce reallocations but can waste space.

4. **Q:** What’s the difference between size and capacity?  
   **A:** Size counts elements actually stored; capacity is allocated slots available before resizing.

5. **Q:** Why might dynamic arrays be unsuitable for real-time systems?  
   **A:** Worst-case append can be O(n) due to resizing; unpredictable latency conflicts with real-time constraints.

6. **Q:** How do dynamic arrays interact with cache?  
   **A:** Between resizes, they retain contiguous layout, providing strong cache performance like static arrays.

7. **Q:** Why avoid automatic shrinking?  
   **A:** Frequent growth/shrink cycles cause thrashing; many libraries opt for lazy shrinking to maintain performance stability.

8. **Q:** In C++, how does `reserve()` help?  
   **A:** It preallocates capacity, preventing repeated reallocations and keeping iterators stable until capacity exhausted.

9. **Q:** What’s the amortized cost derivation for growth factor 2?  
   **A:** Copies accumulate as 1 + 2 + 4 + ... ≤ 2n, so total work O(n); average per push O(1).

10. **Q:** When should dynamic arrays be avoided in favor of linked structures?  
    **A:** When frequent insertions/deletions in the middle dominate, or when stable references beyond indexes are required.

---

### Day 3 — Linked Lists (Pointers, Trade-offs, Rare Use)

1. **Q:** Why are linked lists less cache-friendly than arrays?  
   **A:** Nodes may reside in scattered memory locations; pointer chasing defeats spatial locality.

2. **Q:** What is an intrusive linked list?  
   **A:** A list where linkage pointers (`next`, `prev`) are embedded directly in data objects, eliminating separate node allocations.

3. **Q:** When do linked lists outperform arrays?  
   **A:** When you need O(1) splicing or deletion given a node pointer, or stable references without reallocation.

4. **Q:** How do sentinel nodes simplify operations?  
   **A:** They eliminate special-case handling for head/tail, allowing uniform insert/remove logic.

5. **Q:** Why can’t you delete a singly linked node with only a pointer to it?  
   **A:** You lack access to the previous node; must either traverse from head or use data-copy trick (fails on tail).

6. **Q:** How do linked lists relate to LRU caches?  
   **A:** Doubly linked lists combined with hash maps provide O(1) move-to-front and eviction operations.

7. **Q:** Why did linked lists fall out of favor in high-performance systems?  
   **A:** Hardware caches and branch predictors favor contiguous, predictable access patterns; arrays outperform in most cases.

8. **Q:** What memory issues can linked lists cause?  
   **A:** Fragmentation due to many small allocations and increased overhead per node.

9. **Q:** How do you prevent null pointer errors in linked list operations?  
   **A:** Use sentinels or rigorous checks before dereferencing `next`/`prev`.

10. **Q:** Where are linked lists still common in production?  
    **A:** Linux kernel’s `list_head`, intrusive lists in LLVM IR, memory allocator free lists.

---

### Day 4 — Stacks & Queues (LIFO/FIFO ADTs)

1. **Q:** How does the call stack relate to a stack ADT?  
   **A:** Function calls push stack frames; returns pop them—exact LIFO behavior.

2. **Q:** Why use a circular buffer for queues?  
   **A:** Prevents O(n) shifting by wrapping indices via modulo, keeping enqueue/dequeue O(1).

3. **Q:** What is backpressure in queue systems?  
   **A:** Mechanism preventing unbounded growth; producers slow or block when queue full.

4. **Q:** How do stacks enable expression evaluation?  
   **A:** Postfix evaluation uses stack to store operands, applying operators as they appear.

5. **Q:** When is a queue superior to a stack?  
   **A:** When order matters (FIFO), such as BFS, task scheduling, or streaming.

6. **Q:** What is a deque and when is it useful?  
   **A:** Double-ended queue allowing efficient operations at both ends; used for sliding window maximum.

7. **Q:** How do bounded vs unbounded queues differ?  
   **A:** Bounded have fixed capacity and enforce backpressure; unbounded risk memory exhaustion.

8. **Q:** Why might recursion fail in deep problems?  
   **A:** Call stack overflow; iterative solution with explicit stack avoids exceeding stack memory.

9. **Q:** How do lock-free queues avoid contention?  
   **A:** Use atomic operations (CAS) to adjust head/tail, often with ABA problem mitigations.

10. **Q:** What role do queues play in operating systems?  
    **A:** Process scheduling, IO buffers, and kernel workqueues rely on FIFO semantics.

---

### Day 5 — Binary Search (Logarithmic Reduction)

1. **Q:** Why does binary search require sorted data?  
   **A:** Comparisons rely on order to eliminate half the search range each step.

2. **Q:** How do you avoid overflow in midpoint calculation?  
   **A:** Use `mid = lo + (hi - lo) // 2`, preventing `lo + hi` from exceeding integer limits.

3. **Q:** What is lower_bound used for?  
   **A:** Finding first index where element ≥ target; useful for insertion points and range queries.

4. **Q:** How does binary search handle duplicates?  
   **A:** Use lower/upper bound variants to find first/last occurrence.

5. **Q:** Why might linear search beat binary search on tiny arrays?  
   **A:** Branch misprediction and overhead; sequential scans exploit contiguous data and minimal branching.

6. **Q:** What is predicate-based binary search?  
   **A:** Searching over indices where a monotonic predicate switches from false to true, useful in optimization problems.

7. **Q:** How do you binary search on floating point ranges?  
   **A:** Use binary search on continuous domain, loop until interval width < ε.

8. **Q:** What happens if interval updates skip +1/-1 adjustments?  
   **A:** Without carefully updating `lo`/`hi`, the loop may not converge, causing infinite loops.

9. **Q:** How is binary search used in database indices?  
   **A:** B-tree nodes perform binary search among keys to locate child pointers efficiently.

10. **Q:** Can binary search be applied to answer spaces without arrays?  
    **A:** Yes; any monotonic function or decision process can be binary searched by evaluating predicate outcomes.

---