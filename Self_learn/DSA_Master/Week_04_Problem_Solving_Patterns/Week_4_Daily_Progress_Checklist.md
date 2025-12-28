# Week 4: Daily Progress Checklist & 50+ Interview Q&A

## ✅ DAY 1: Two Pointers

### Morning Learning Objectives
- [ ] Understand converging vs chasing pointer patterns
- [ ] Know why O(n) is possible on sorted arrays
- [ ] Trace Two Sum II example step-by-step
- [ ] Understand palindrome check logic
- [ ] Understand in-place removal mechanics

### Afternoon Practice (3-4 problems)
- [ ] Two Sum II Input Array Is Sorted (LeetCode 167)
- [ ] Valid Palindrome (LeetCode 125)
- [ ] Remove Duplicates from Sorted Array (LeetCode 26)
- [ ] (Optional) Container with Most Water (LeetCode 11)

### Evening Review
- [ ] Trace one complete two-pointer example by hand
- [ ] Compare two-pointers vs hash table approach
- [ ] Answer 5+ Q&A from interview section

**Confidence Rating Day 1:** ___ / 5

---

## ✅ DAY 2: Sliding Window (Fixed)

### Morning Learning Objectives
- [ ] Understand window building and sliding mechanics
- [ ] Know why build O(k) then slide O(n) = O(n) total
- [ ] Trace rolling window aggregate
- [ ] Understand deque for max/min maintenance
- [ ] Know amortized O(1) analysis

### Afternoon Practice (3-4 problems)
- [ ] Maximum Average Subarray I (LeetCode 643)
- [ ] Sliding Window Maximum (LeetCode 239)
- [ ] Contains Duplicate II (LeetCode 219)
- [ ] (Optional) Grumpy Bookstore Owner (LeetCode 1052)

### Evening Review
- [ ] Trace sliding window maximum with deque
- [ ] Explain why deque beats simple max tracking
- [ ] Answer 5+ Q&A from interview section

**Confidence Rating Day 2:** ___ / 5

---

## ✅ DAY 3: Sliding Window (Variable)

### Morning Learning Objectives
- [ ] Understand expand-contract paradigm
- [ ] Know constraint satisfaction logic
- [ ] Trace minimum window substring
- [ ] Understand hash map for character counting
- [ ] Know when to shrink vs expand

### Afternoon Practice (3-4 problems)
- [ ] Minimum Window Substring (LeetCode 76)
- [ ] Longest Substring Without Repeating Characters (LeetCode 3)
- [ ] Longest Substring with At Most Two Distinct Characters (LeetCode 159)
- [ ] (Optional) Permutation in String (LeetCode 567)

### Evening Review
- [ ] Trace minimum window end-to-end
- [ ] Understand why left pointer never resets
- [ ] Answer 5+ Q&A from interview section

**Confidence Rating Day 3:** ___ / 5

---

## ✅ DAY 4: Prefix Sums

### Morning Learning Objectives
- [ ] Understand prefix array construction
- [ ] Know range query formula: sum[i,j] = prefix[j+1] - prefix[i]
- [ ] Trace prefix building and querying
- [ ] Understand hash map for subarray matching
- [ ] Know preprocessing tradeoff

### Afternoon Practice (3-4 problems)
- [ ] Range Sum Query - Immutable (LeetCode 303)
- [ ] Subarray Sum Equals K (LeetCode 560)
- [ ] Contiguous Array (LeetCode 485)
- [ ] (Optional) Maximum Subarray (LeetCode 53)

### Evening Review
- [ ] Trace subarray sum = K with hash map
- [ ] Explain time/space tradeoff (O(n) space, O(1) query)
- [ ] Answer 5+ Q&A from interview section

**Confidence Rating Day 4:** ___ / 5

---

## ✅ DAY 5: Cycle Detection

### Morning Learning Objectives
- [ ] Understand relative speed convergence
- [ ] Know why meeting point exists in cycles
- [ ] Trace Floyd's algorithm step-by-step
- [ ] Understand cycle start finding mechanics
- [ ] Know mathematical relationship: a = c - m

### Afternoon Practice (3-4 problems)
- [ ] Linked List Cycle (LeetCode 141)
- [ ] Linked List Cycle II (LeetCode 142)
- [ ] Find the Duplicate Number (LeetCode 287)
- [ ] (Optional) Happy Number (LeetCode 202)

### Evening Review
- [ ] Trace cycle detection on full example
- [ ] Explain why cycle start finding works mathematically
- [ ] Answer 5+ Q&A from interview section

**Confidence Rating Day 5:** ___ / 5

---

## 🎯 INTERVIEW Q&A REFERENCE (50+ Pairs)

### TWO POINTERS (6 Pairs)

**Q1: Why is two-pointer O(n) and not O(n²)?**
A: Each element visited at most once. Left pointer moves right only (0→n), right moves left only (n-1→0). Total movements ≤ n. No backtracking.

**Q2: Can two-pointer work on unsorted array?**
A: Not reliably. Sorted is necessary because it guarantees moving left increases sum and moving right decreases sum. Unsorted requires hash table or sorting first.

**Q3: What's the difference between converging and chasing?**
A: Converging: pointers from opposite ends moving toward middle (two sum, palindrome). Chasing: both same direction, one catches other (duplicates, in-place removal).

**Q4: How handle case when no valid pair exists?**
A: Return special value (-1, null, empty) based on problem. In two sum: return [-1,-1] or equivalent.

**Q5: Can we use two-pointer on linked lists?**
A: Yes. Example: find middle (slow +1, fast +2), cycle detection (Floyd's), removing nth from end.

**Q6: Is two-pointer always better than hash table?**
A: For sorted arrays: yes (O(1) space). Unsorted arrays: hash table often better (avoid sort cost).

### FIXED SLIDING WINDOW (6 Pairs)

**Q1: How is fixed sliding window different from two-pointer?**
A: Two-pointer finds pairs. Sliding window processes all k-length subarrays. Different problems, different paradigms.

**Q2: Why build initial window O(k) instead of sliding from 0?**
A: Building first handles k elements correctly. Then sliding (remove left, add right) maintains window invariant. Prevents off-by-one errors.

**Q3: When is deque necessary for sliding window?**
A: Only when you need max/min in window. For simple sum/average, regular variable sufficient. Deque handles competitive candidates.

**Q4: Can window size be 1?**
A: Yes, works naturally. Max of size-1 window is the element itself. Code handles it without special cases.

**Q5: What if k > array size?**
A: No valid windows. Return empty result or error. Check n < k upfront if needed.

**Q6: How complex is deque operations?**
A: Push/pop O(1) amortized. Each element added once, removed once → O(n) total. Per operation: O(1) amortized.

### VARIABLE SLIDING WINDOW (6 Pairs)

**Q1: How know when to expand vs contract?**
A: Expand (move right): add new element, check constraint. Contract (move left): shrink while valid, stop when invalid.

**Q2: Why can left never reset in variable window?**
A: Monotonicity: if current [left, right] doesn't satisfy constraint, no smaller window from left satisfies either. So left only moves forward.

**Q3: Handle multiple valid windows?**
A: Track best window (minimum, maximum, etc.) during contraction. Update whenever window is valid.

**Q4: What hash map tracks?**
A: Counts of characters (or elements). Compare counts with required counts. When all match: constraint satisfied.

**Q5: Can variable window solve fixed-size problems?**
A: Yes, but unnecessarily complex. Fixed window simpler for k-length problems.

**Q6: Time complexity guarantee?**
A: O(n) because left and right each move 0 to n total. No nested loops (no inner while inside outer while that repeats).

### PREFIX SUMS (6 Pairs)

**Q1: Why prefix array size n+1 instead of n?**
A: To handle queries starting at index 0. prefix[0]=0 means "sum before any elements". Enables formula: sum[i,j] = prefix[j+1] - prefix[i].

**Q2: Can prefix sums handle updates?**
A: No, not efficiently. Simple update changes all future prefix values. Use segment trees for range updates + queries.

**Q3: How does hash map find subarrays with target sum?**
A: Store prefix sums seen so far. For each position, check if (current - target) exists in map. Count += frequency of that prefix sum.

**Q4: Does prefix sum work with negative numbers?**
A: Yes. Prefix values might decrease, but formula still works. sum[i,j] = prefix[j+1] - prefix[i] regardless of signs.

**Q5: Can we compute 2D prefix sums?**
A: Yes. 2D prefix: prefix[i][j] = element[i][j] + prefix[i-1][j] + prefix[i][j-1] - prefix[i-1][j-1]. Rectangle query in O(1).

**Q6: When is prefix sum worth the O(n) space?**
A: When q > log n (more than log n queries). If only 1 query, just compute directly. Preprocessing pays off for many queries.

### CYCLE DETECTION (6 Pairs)

**Q1: Why must pointers meet if cycle exists?**
A: In a list of n nodes, at most n unique states. After n iterations, pigeonhole principle: must repeat state. If state = (slow pos, fast pos), they must be at same position.

**Q2: Can slow and fast speeds be different (not 1 and 2)?**
A: Yes. Any relative speed > 1 works. Speed (1,2) simplest. Speed (1,3) also works, different convergence rate.

**Q3: How find cycle start after detecting?**
A: Mathematical property: restart slow at head, move both at speed 1. They meet at cycle start. Distance from head to start = distance from meeting point back to start.

**Q4: What's the math proving cycle start formula?**
A: a = head to cycle start, c = cycle length, m = meeting point to cycle start. When meet: 2(a+m) ≡ a+m+kc (mod c). Solves to: a = c-m. Restarting at head ensures they meet at cycle start.

**Q5: Can detect cycle with hash set instead?**
A: Yes, but O(n) space vs Floyd's O(1). Floyd's better for memory-constrained systems.

**Q6: How handle multiple cycles?**
A: Linked list can only have one cycle (enters once, loops). Function iteration can revisit same state (but then it's one cycle).

---

## 📊 Daily Self-Assessment

| Day | Understanding | Implementation | Confidence |
|-----|---|---|---|
| **1 (Two Pointers)** | ___ / 5 | ___ / 5 | ___ / 5 |
| **2 (Sliding Window Fixed)** | ___ / 5 | ___ / 5 | ___ / 5 |
| **3 (Sliding Window Variable)** | ___ / 5 | ___ / 5 | ___ / 5 |
| **4 (Prefix Sums)** | ___ / 5 | ___ / 5 | ___ / 5 |
| **5 (Cycle Detection)** | ___ / 5 | ___ / 5 | ___ / 5 |

**Target:** 4/5+ on all before Week 5

---

## ✅ WEEK 4 COMPLETION CHECKLIST

- [ ] Completed all 5 days instructional content
- [ ] Implemented all 5 patterns from scratch (no notes)
- [ ] Solved 30+ practice problems total (6+ per pattern)
- [ ] Answered all 50+ interview Q&A pairs
- [ ] Rate 4/5+ confidence on all 5 patterns
- [ ] Can identify problem type instantly using decision tree
- [ ] Know real-world applications (5+ systems per pattern)
- [ ] Traced each algorithm by hand (10+ complete examples)
- [ ] Ready for Week 5 (Trees & Heaps)

---

**Status:** ✅ Week 4 Complete  
**Next:** Week 5 - Trees and Heaps (build on pattern foundation)

