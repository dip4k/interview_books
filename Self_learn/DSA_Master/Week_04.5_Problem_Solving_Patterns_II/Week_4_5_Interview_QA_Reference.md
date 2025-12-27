# Week 4.5: Interview Q&A Reference

## 🎯 Hash Map / Hash Set — 10 Q&A Pairs

**Q1: Why is hash O(1) and not O(log n)?**
A: Hash function maps key directly to index (O(1) computation). No search needed. Compare: binary search requires O(log n) comparisons even after locating position.

**Q2: What happens if hash function is bad (all keys hash to same bucket)?**
A: Degenerate to O(n) linked list lookup. This is worst case. Good hash functions have uniform distribution to avoid this.

**Q3: Load factor 0.5 vs 0.9: which is better?**
A: 0.5 uses more memory, fewer collisions, faster O(1). 0.9 uses less memory, more collisions, slower O(1+λ). Trade-off.

**Q4: Why rehash when load factor > 0.75?**
A: At λ=0.75, collisions become likely (birthday paradox). Expected cost O(1+λ) becomes O(1.75). Rehashing to larger table restores O(1).

**Q5: Can floating point numbers be hash keys?**
A: Risky. Precision issues cause same key to hash differently (0.1+0.1+0.1 ≠ 0.3). Use integers or strings instead.

**Q6: How does mutable object as key fail?**
A: Object hash code based on state. Modifying object changes hash, key becomes unfindable in table.

**Q7: Two Sum: why use hash instead of sorted + two pointers?**
A: Hash: O(n) time, O(n) space, preserves order. Sorted: O(n log n) time for sorting, then O(n) two pointers. Hash faster if space available.

**Q8: What if hash table runs out of memory?**
A: Implementation-dependent. Some resize, some fail. Python dict resizes automatically. Others throw OutOfMemory.

**Q9: Why is chaining better than open addressing for delete?**
A: Chaining: delete node from linked list, O(1). Open addressing: must mark as deleted (lazy deletion) or rehash, complex.

**Q10: Can null be a hash key?**
A: Yes in many languages (Python, Java). Some implement special case: hash(None) = 0. Others disallow.

---

## 🎯 Monotonic Stack — 8 Q&A Pairs

**Q1: Why does monotonic stack give O(n) despite nested while loop?**
A: Each element pushed exactly once, popped exactly once. Total operations: n pushes + n pops = O(n), not O(n²).

**Q2: Trace Next Greater [2,1,2,4,3]. What's the answer?**
A: [4, 2, 4, -1, -1]. Process each: find first greater to right using stack.

**Q3: Monotonic increasing vs decreasing: when use which?**
A: Increasing: next **smaller** element. Decreasing: next **greater** element. Determine by problem requirement.

**Q4: Why must we store indices, not values?**
A: Need to know position of element for result array. Values alone don't tell us where to store answer.

**Q5: Can monotonic stack solve "previous greater element"?**
A: Yes, process from right to left instead of left to right. Mirror the logic.

**Q6: Trapping Rain Water: why does monotonic stack work?**
A: Maintains increasing heights. Water trapped between left boundary, right boundary, current position. Monotonic stack efficiently finds these.

**Q7: What if array has duplicates?**
A: Works fine. Handle >= vs > carefully in comparison. Adjacent equal heights don't trap water.

**Q8: Can you find second next greater element?**
A: Harder. Requires more complex tracking. Single monotonic stack doesn't directly give you this.

---

## 🎯 Merge Operations — 6 Q&A Pairs

**Q1: Why merge O(n) while sort is O(n log n)?**
A: Merge leverages sorted property. No need to compare globally. Just compare fronts of two lists. Sort must globally order.

**Q2: Merge [1,3] and [2]: trace the process.**
A: p1=0, p2=0: 1<2, take 1. p1=1, p2=0: 3>2, take 2. p1=1, p2=1: 3 left, take 3. Result: [1,2,3].

**Q3: What if one list much longer than other?**
A: Merge is O(m+n). Longer list doesn't hurt, just processes more elements. Time still linear in total size.

**Q4: Can you merge in-place without extra space?**
A: Only if allowed to modify first array. Otherwise, need O(n) space for result. In-place merges are complex, rare in practice.

**Q5: Merge K sorted lists: how to extend from 2?**
A: Option 1: Heap, extract min K times. Option 2: Divide & conquer, merge pairs recursively. Option 2 is O(n log k).

**Q6: Why is merge fundamental for merge sort?**
A: Merge sort divides problem (divide & conquer). Merge combines sorted halves in O(n). Without merge, can't achieve O(n log n).

---

## 🎯 Partition — 4 Q&A Pairs

**Q1: Partition [1,0,2,0,3] to move zeros to end: trace.**
A: Two pointers at 0,0. Find first zero at 1. Move to end. Continue. Result: [1,2,3,0,0].

**Q2: Why is partition O(1) space?**
A: Only swapping in place. No extra data structures. Compare: merge which needs O(n) extra array.

**Q3: Dutch National Flag: sort 0,1,2. How does partition extend?**
A: Three pointers: left (for 0), right (for 2), mid (for 1). Segregate into three regions. O(n) single pass.

**Q4: Quicksort uses partition. What if pivot is bad?**
A: Worst case pivot is always smallest/largest → O(n²) time. Good pivot selection (random, median-of-3) avoids this.

---

## 🎯 Kadane's Algorithm — 8 Q&A Pairs

**Q1: Max Subarray [-2,1,-3,4,-1,2,1,-5,4]. What's answer?**
A: 6 (subarray [4,-1,2,1]). Kadane gives global max 6.

**Q2: When do you reset current sum?**
A: When current + next < next alone. Meaning starting fresh at next is better than extending current.

**Q3: What if all numbers negative?**
A: Maximum is least negative. Kadane handles this: max_global initializes to arr[0], doesn't default to 0.

**Q4: Max Product Subarray: does Kadane work directly?**
A: No. Need track both max and min (negative × negative = positive). Template adapts but not identical.

**Q5: Can you find actual subarray, not just max?**
A: Yes, track start/end indices. When updating max_global, save current start position.

**Q6: Why is Kadane DP?**
A: Overlapping subproblems (max ending at i depends on max ending at i-1). Optimal substructure (max sum uses optimal of subproblems). DP solution with O(1) space.

**Q7: House Robber: is it Kadane?**
A: Similar DP. Current decision (rob or skip) depends on previous states. Not exact Kadane but same template.

**Q8: Longest Subarray with K distinct: Kadane approach?**
A: No, use sliding window. Kadane assumes all subarrays valid. Here, window must satisfy constraint.

---

## ✅ Interview Readiness Checklist

After Week 4.5, confidently answer:
- [ ] 10 hash questions
- [ ] 8 monotonic stack questions
- [ ] 6 merge questions
- [ ] 4 partition questions
- [ ] 8 Kadane questions

**Total: 36 Q&A pairs mastered**

**If 90%+ confident → Ready for Week 5**

