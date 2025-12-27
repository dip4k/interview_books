# Week 3: Interview Q&A Reference

## 🎯 Elementary Sorts — 10 Q&A Pairs

**Q1: When do you use bubble sort?**
A: Rarely. Insertion sort is always better. Only for teaching/learning.

**Q2: Is insertion sort ever used in production?**
A: Yes, in TimSort (hybrid) for small subarrays, and for nearly-sorted data (O(n) on nearly-sorted).

**Q3: Why is selection sort good for flash memory?**
A: Minimizes writes: O(n) swaps vs O(n²) in bubble/insertion. Write cost dominates on flash.

**Q4: What's the difference between stable and unstable sort?**
A: Stable preserves relative order of equal elements. Matters for multi-key sorting.

**Q5: Trace insertion sort on [5,2,8,1].**
A: [5|2,8,1] → [2,5|8,1] → [2,5,8|1] → [1,2,5,8]

**Q6: Why is insertion O(n) on nearly-sorted?**
A: Fewer inner loop iterations when element near correct position.

**Q7: Compare bubble vs insertion on [1,2,3,4,5].**
A: Bubble: O(n²) comparisons anyway. Insertion: O(n) comparisons, done early.

**Q8: Can you optimize bubble sort?**
A: Yes, track if any swaps happened. Stop early if no swaps (nearly-sorted).

**Q9: Is selection sort stable?**
A: No. Swapping elements can change relative order of equal elements.

**Q10: For what size arrays are elementary sorts acceptable?**
A: Generally n < 50. Beyond that, overhead of advanced algorithms not worth it.

---

## 🎯 Merge Sort — 10 Q&A Pairs

**Q1: Why is merge sort stable?**
A: Merge operation preserves relative order when values equal.

**Q2: Why does merge sort need O(n) space?**
A: Temporary arrays for merging. Can't merge in-place efficiently.

**Q3: What's the recurrence for merge sort?**
A: T(n) = 2×T(n/2) + O(n). Solution: O(n log n).

**Q4: Is merge sort better than quick sort?**
A: Merge sort: guaranteed O(n log n), stable. Quick sort: faster practice. Different trade-offs.

**Q5: Can you implement merge sort bottom-up (iterative)?**
A: Yes. Start with subarrays of size 1, merge to size 2, then 4, etc.

**Q6: Why is merge sort good for external sorting?**
A: Can read from disk in chunks, merge in memory. Avoids random disk access.

**Q7: What's the advantage of merge sort on linked lists?**
A: O(1) space (no copying needed). Quick sort requires random access (not possible in lists).

**Q8: Trace merge sort on [5,2,8,1,4].**
A: Divide: [5,2] [8,1,4]. Merge: [2,5] [1,4,8]. Final: [1,2,4,5,8].

**Q9: Can you optimize merge sort?**
A: Yes, switch to insertion sort for small subarrays (n < 10), avoid copying.

**Q10: Why is merge sort less cache-friendly than quick sort?**
A: Merge requires sequential access to multiple arrays. Quick sort accesses in-place array.

---

## 🎯 Quick Sort — 10 Q&A Pairs

**Q1: What's the average case complexity of quick sort?**
A: O(n log n) if pivot selection is good (splits array in half).

**Q2: What's the worst-case?**
A: O(n²) if pivot always smallest/largest (array always splits 0, n-1).

**Q3: How do you avoid worst-case?**
A: Use median-of-three, or randomize pivot selection.

**Q4: Why is quick sort faster than merge sort in practice?**
A: Better cache locality (in-place), fewer data movements, smaller constants.

**Q5: What's the space complexity of quick sort?**
A: O(log n) for recursion stack. O(1) if you exclude stack.

**Q6: Can you implement quick sort iteratively?**
A: Yes, use explicit stack to simulate recursion.

**Q7: Trace quick sort on [5,2,8,1,9] with pivot=5.**
A: Partition: [2,1] [5] [8,9]. Recurse on left/right.

**Q8: Why doesn't quick sort work well on linked lists?**
A: Requires random access for partitioning. Linked lists don't support O(1) access.

**Q9: What happens with duplicates in quick sort?**
A: Can degrade to O(n²) if many duplicates. Fix: 3-way partitioning (< pivot, = pivot, > pivot).

**Q10: Is quick sort stable?**
A: No. Partitioning can change relative order of equal elements.

---

## 🎯 Heap Sort — 8 Q&A Pairs

**Q1: Why is building a heap O(n) and not O(n log n)?**
A: Sum of heapify costs at each level = O(n/2×1 + n/4×2 + ...) = O(n).

**Q2: What's the space complexity of heap sort?**
A: O(1). In-place, no extra arrays needed.

**Q3: Is heap sort stable?**
A: No. Heap structure breaks relative order of equal elements.

**Q4: When is heap sort preferred?**
A: When worst-case O(n log n) required and space is limited.

**Q5: How do you find kth largest using a heap?**
A: Build min-heap of k elements, iterate through array.

**Q6: Why is heap sort slower than quick sort in practice?**
A: Poor cache behavior. Heap access pattern is scattered.

**Q7: Trace heapify on [3,7,8] with index 0.**
A: 3 has children 7,8. 3 < 8, swap with 8. Recurse on position 2.

**Q8: Can you use a heap for sorting in-place?**
A: Yes. Build max-heap, extract max one by one (heap sort).

---

## 🎯 Hash Tables I — 10 Q&A Pairs

**Q1: What's a good hash function?**
A: Distributes keys uniformly, computes quickly, deterministic.

**Q2: Why is O(1) average but O(n) worst-case?**
A: Worst-case: all keys hash to same bucket (collision chain length n).

**Q3: What's load factor and why does it matter?**
A: α = n/m (keys/buckets). Higher load factor = longer chains = slower. Keep α < 0.75.

**Q4: How do you handle collisions?**
A: Chaining (linked list in bucket) or open addressing (probe for empty slot).

**Q5: What's the hash function for integers?**
A: Simple: x % m (modulo). Better: multiply-shift hash.

**Q6: What's the hash function for strings?**
A: Polynomial rolling hash: hash(s) = (s[0]×p^0 + s[1]×p^1 + ... + s[n-1]×p^(n-1)) % m.

**Q7: Why can't you use negative hash values?**
A: Arrays indexed from 0. Take modulo to get positive index.

**Q8: What's the expected chain length with chaining?**
A: α (load factor). If α = 0.5, average chain length = 0.5.

**Q9: Can you use perfect hashing?**
A: Yes, but requires knowing all keys in advance. Not practical for dynamic tables.

**Q10: Is hashing better than balanced trees?**
A: Hash: O(1) average. Tree: O(log n) guaranteed. Hash better if distribution good.

---

## 🎯 Hash Tables II — 10 Q&A Pairs

**Q1: What's the difference between chaining and open addressing?**
A: Chaining: each bucket is linked list. Open: find empty slot nearby.

**Q2: What's linear probing?**
A: If slot i occupied, try i+1, i+2, i+3, etc.

**Q3: What's quadratic probing?**
A: If slot i occupied, try i+1², i+4², i+9², etc. (less clustering).

**Q4: What's primary clustering?**
A: In linear probing, clusters of occupied slots form, reducing effective capacity.

**Q5: How do you delete from open addressing?**
A: Mark as tombstone (not empty, but deleted). Keep searching through tombstones.

**Q6: When should you rehash?**
A: When load factor exceeds threshold (typically 0.75).

**Q7: What's the cost of rehashing?**
A: O(n) to rebuild table. But rare, so amortized O(1) per insertion.

**Q8: Is chaining or open addressing better?**
A: Chaining simpler, worse cache. Open addressing cache-friendly, harder to implement.

**Q9: How do you grow hash table capacity?**
A: Typically double (2×m). Rehash all entries with new capacity.

**Q10: Can load factor be > 1 with chaining?**
A: Yes. With open addressing, load factor must be < 1 (need empty slots).

---

## ✅ Interview Readiness Checklist

After Week 3, you should confidently answer:
- [ ] 10 elementary sort questions
- [ ] 10 merge sort questions
- [ ] 10 quick sort questions
- [ ] 8 heap sort questions
- [ ] 10 hash table I questions
- [ ] 10 hash table II questions

**Total: 58 Q&A pairs mastered**

**If 90%+ confident → Ready for Week 4**

