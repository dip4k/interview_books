# Week 4: Extended Interview Q&A Reference (50+ Complete Pairs)

## 🎯 COMPREHENSIVE INTERVIEW PREPARATION

Complete Q&A coverage for all 5 algorithm patterns. Study these thoroughly before interviews.

---

## TWO POINTERS (6 Pairs)

**Q1: Explain LPS array concept and how two-pointers differs from it**
A: LPS (Longest Proper Prefix) is for KMP string matching. Two-pointers is for finding pairs in sorted arrays. Different problems, different techniques. Two-pointers: exploit sorted order invariant.

**Q2: Why is two-pointer O(n) and not O(n²)?**
A: Text pointer i increases monotonically from 0 to n, never resets. Left pointer moves right only, right pointer moves left only. Total movements ≤ n, not nested O(n²) loops.

**Q3: Can you find pairs in unsorted array with two-pointers?**
A: Not reliably. Sorted order is essential because it guarantees: moving left increases aggregate, moving right decreases it. Unsorted requires sorting first O(n log n) or using hash table O(n) space.

**Q4: How detect when no valid pair exists?**
A: When pointers cross (left >= right) without finding pair, no solution exists. Return special value: -1, null, empty array, or raise exception based on problem.

**Q5: Difference between converging (opposite ends) vs chasing (same direction)?**
A: Converging: from opposite ends moving toward middle (two sum, palindrome). Chasing: both same direction, one catches other (duplicates, in-place removal).

**Q6: Can two-pointers work on linked lists?**
A: Yes! Floyd's cycle detection uses two-pointers at different speeds on linked lists. Also: find middle node, detect cycles, remove nth from end.

---

## FIXED SLIDING WINDOW (6 Pairs)

**Q1: Why build initial window O(k) instead of starting from position 0?**
A: Building first ensures window correctly contains exactly k elements. Starting from 0 would require special handling for positions 0 to k-1. Building first simplifies code and logic.

**Q2: What's the amortized complexity of sliding window with deque?**
A: O(1) amortized. Each element added once and removed once from deque = O(n) total. Per operation: O(1) amortized. Not O(1) worst-case (removal can take O(k)), but O(1) amortized.

**Q3: Why is deque necessary for sliding window maximum?**
A: Simple max tracking only remembers current max. Deque remembers all candidates in decreasing order, enabling O(1) removal when element exits window and O(1) max lookup (front element).

**Q4: Can you use sliding window with variable-size k?**
A: Not with fixed sliding window algorithm. Use variable sliding window instead (next day). Different paradigms: fixed size known upfront, variable size determined by constraint.

**Q5: How handle edge case where k > array length?**
A: No valid windows exist. Check n < k upfront, return empty result or error. Some problems allow k ≥ n (treat as single window = whole array).

**Q6: Why does fixed window give O(n) when k could be large?**
A: Build O(k) once, slide n-k times with O(1) update each = O(k + n - k) = O(n) total. Build cost amortized over n positions.

---

## VARIABLE SLIDING WINDOW (6 Pairs)

**Q1: How know when to expand vs contract in variable window?**
A: Expand right: add new element, check if constraint still satisfied. Contract left: remove elements while constraint satisfied, stop when about to violate.

**Q2: Why can left pointer never reset/move backward?**
A: Monotonicity principle. If current [left, right] doesn't satisfy constraint, no window [left, j] for any j < right will satisfy it either. So left only moves forward.

**Q3: What happens if constraint never satisfied for any window?**
A: Left and right both reach end without finding valid window. Return empty result, -1, or null based on problem definition.

**Q4: How handle multiple valid windows of different sizes?**
A: Track best window (minimum length, maximum value, etc.) during contraction phase. Update whenever valid window found. Return best at end.

**Q5: Can you use variable sliding window with fixed-size problem?**
A: Yes, but unnecessary. Fixed window simpler for known k-length windows. Variable window solves harder constraint-based problems.

**Q6: Time complexity guarantee for variable window?**
A: O(n) because left and right each move at most n times total. No nested loops repeating. Some confusion from "while left <= right" looking nested, but left only moves forward (total n across entire array).

---

## PREFIX SUMS (6 Pairs)

**Q1: Why prefix array size n+1 and not n?**
A: To enable sum(0, j) = prefix[j+1] - prefix[0]. prefix[0] = 0 represents "no elements". Without it, querying sum starting at index 0 requires special handling.

**Q2: Can prefix sum handle array updates efficiently?**
A: No. Single update requires recomputing all subsequent prefix values O(n). For updates + queries, use segment trees or Fenwick trees (Week 8).

**Q3: How does hash map find subarrays with target sum?**
A: Store prefix sums encountered so far. For each position, check if (current_sum - target) exists in map. Count += frequency of that prefix sum.

**Q4: Does prefix sum work with negative numbers?**
A: Yes. Prefix values might decrease, but formula remains correct: sum(i, j) = prefix[j+1] - prefix[i] works regardless of positive/negative mix.

**Q5: How compute 2D prefix for matrix rectangle queries?**
A: 2D: prefix[i][j] = element[i][j] + prefix[i-1][j] + prefix[i][j-1] - prefix[i-1][j-1]. Rectangle sum in O(1) after O(mn) preprocessing.

**Q6: When is prefix sum worth the O(n) space investment?**
A: When queries (q) > log n. If q = 1, compute directly. If q >> n, preprocessing saves time. Fundamental space-time tradeoff.

---

## CYCLE DETECTION (6 Pairs)

**Q1: Why must Floyd's pointers meet if cycle exists?**
A: Linked list of n nodes has at most n unique states (node positions). In cycle, pigeonhole principle: within n iterations, must revisit state. If state = (slow pos, fast pos), they must be at same position.

**Q2: Can slow/fast speeds be different from 1x and 2x?**
A: Yes. Any speed ratio > 1 works (1x and 3x, 1x and 4x, etc.). Speed 2x simplest and most common. Different speeds change convergence rate.

**Q3: How find cycle start after detecting with Floyd's?**
A: Restart slow at head, keep fast at meeting point. Move both at speed 1. When they meet again: that's cycle start. Mathematical property: distance from head to cycle start = distance from meeting point back to start.

**Q4: What's the mathematical proof for cycle start finding?**
A: Let a = head to cycle start, c = cycle length, m = meeting point to cycle start. When meet: slow traveled a + km + m, fast traveled 2(a + km + m). But fast in cycle, so: 2(a + m) ≡ a + m (mod c). Solves to: a = c - m. Restarting at head ensures they meet at cycle start.

**Q5: Is hash set approach worse than Floyd's?**
A: Hash set O(n) space, Floyd's O(1) space. Both O(n) time. Floyd's wins on memory. Hash set simpler to code. Choose based on constraints.

**Q6: Can detect cycle in undirected graphs with Floyd's?**
A: No, Floyd's specific to sequences/linked lists. For undirected graphs, use DFS/BFS cycle detection (different algorithm).

---

## CROSS-PATTERN COMPARISON (6 Pairs)

**Q1: When to use two-pointers vs sliding window?**
A: Two-pointers: finding pairs. Sliding window: processing contiguous subarrays. Different goals, different techniques. Two-pointers doesn't process all windows, sliding window does.

**Q2: When to use prefix sums vs sliding window?**
A: Prefix: many range sum queries, range is arbitrary. Sliding: contiguous windows, size varies. Prefix preprocesses for O(1) query. Sliding processes sequentially.

**Q3: Which pattern solves "minimum sum of k consecutive elements"?**
A: Fixed sliding window (day 2). Window size k is fixed. Build initial, slide, find minimum aggregate.

**Q4: Which pattern solves "minimum window containing all characters"?**
A: Variable sliding window (day 3). Window size varies based on constraint (have all chars). Expand until valid, contract until invalid.

**Q5: Which pattern solves "sum of all elements from index i to j"?**
A: Prefix sums (day 4). Multiple range queries benefit from preprocessing. O(1) query after O(n) preprocessing.

**Q6: Which pattern solves "detect cycle in linked list"?**
A: Cycle detection (day 5). Floyd's algorithm O(1) space. Hash set alternative O(n) space.

---

## EDGE CASES & CORNER SCENARIOS (6 Pairs)

**Q1: How handle empty array?**
A: Two-pointers: check length > 0. Sliding: no valid windows. Prefix: prefix[0] = 0 still valid. Cycle: empty list = no cycle.

**Q2: How handle single element array?**
A: Two-pointers: single element, can't form pair. Sliding: window = element, if k=1. Prefix: prefix = [0, element]. Cycle: single node checks self-loop.

**Q3: How handle array with all identical elements?**
A: Two-pointers: all pairs equivalent. Sliding: all windows same aggregate. Prefix: all prefix sums valid. Cycle: depends on structure.

**Q4: How handle negative numbers?**
A: Two-pointers: works (aggregate monotonic still). Sliding: works (aggregates can decrease). Prefix: works (prefix values can decrease). Cycle: N/A (structural problem).

**Q5: How handle integer overflow?**
A: Prefix sums: use 64-bit integers or check overflow. Two-pointers: usually no overflow (comparing not summing). Sliding: use 64-bit for aggregates. Cycle: N/A.

**Q6: How handle no valid answer?**
A: Return special value (-1, null, empty, exception). Define upfront in problem. Test explicitly in code.

---

## INTERVIEW READINESS ASSESSMENT

### Before Your Interview:

- [ ] Can implement two-pointers from scratch (< 5 min)
- [ ] Can implement fixed sliding window (< 5 min)
- [ ] Can implement variable sliding window (< 8 min)
- [ ] Can build prefix array and query (< 3 min)
- [ ] Can implement Floyd's cycle detection (< 5 min)
- [ ] Answer all 36+ Q&A pairs fluently
- [ ] Solved 30+ practice problems
- [ ] Timed yourself: medium problems < 20 min
- [ ] Explained each pattern to someone else
- [ ] Know 5+ real-world systems per pattern

### Interview Day Execution:

- [ ] Clarify problem requirements (1-2 min)
- [ ] Identify pattern using decision tree (2-3 min)
- [ ] Explain approach before coding (1-2 min)
- [ ] Code solution with tracing (10-15 min)
- [ ] Test edge cases (3-5 min)
- [ ] Optimize if time (2-5 min)
- [ ] Discuss complexity and tradeoffs (1-2 min)

---

## PATTERN SELECTION DECISION TREE

```
Problem asks for pairs or relationships?
├─ YES: Sorted array?
│   ├─ YES: Use TWO POINTERS → O(n) time, O(1) space
│   └─ NO: Use HASH TABLE or sort first
└─ NO: Continues below...

Contiguous elements in array?
├─ YES: Window size fixed/known?
│   ├─ YES: Use FIXED SLIDING WINDOW → O(n) time
│   │   └─ Need max/min? → Use DEQUE
│   └─ NO: Constraint-based?
│       ├─ YES: Use VARIABLE SLIDING WINDOW → O(n) time
│       └─ NO: Other approach
└─ NO: Continues below...

Range query problem?
├─ YES: Many independent queries?
│   ├─ YES: Use PREFIX SUMS → O(n+q) time
│   └─ NO: Compute on-the-fly
└─ NO: Continues below...

Cycle detection?
├─ YES: Use FLOYD'S ALGORITHM → O(n) time, O(1) space
└─ NO: Different problem type
```

---

## FINAL TIPS FOR SUCCESS

✅ **Understand before coding:** Know WHY algorithm works  
✅ **Trace by hand:** Don't just read examples  
✅ **Practice patterns:** 6+ problems per pattern minimum  
✅ **Test edge cases:** Empty, single, no solution, etc.  
✅ **Explain clearly:** Talk through your approach  
✅ **Know tradeoffs:** Time vs space, simple vs optimal  
✅ **Real systems matter:** Understand where patterns used  
✅ **Interview confidence:** You have 35-45% coverage now

---

**Good luck! You now have comprehensive interview preparation for Week 4.**

