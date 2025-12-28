# Week 4: Problem-Solving Roadmap & Decision Trees

## 📊 Problem-Solving Framework (5-Step Process)

**For EVERY Week 4 problem, follow this process:**

1. **IDENTIFY** problem type: What are we solving for? (pair, aggregate, range, cycle)
2. **RECOGNIZE** specific pattern: Which of 5 patterns matches?
3. **SELECT** algorithm: What complexity/space tradeoff is needed?
4. **IMPLEMENT** with proper data structures (hash map, deque, array)
5. **OPTIMIZE** for constraints (space, time, edge cases)

---

## 🎯 Algorithm Decision Tree

```
Is it a PAIR/RELATIONSHIP problem?
├─ YES: Are we on a SORTED array?
│   ├─ YES: Use TWO POINTERS (converging) → O(n) time
│   └─ NO: Use HASH TABLE or sort first → O(n log n) total
└─ NO: Continue below

Is it a CONTIGUOUS SUBARRAY problem?
├─ YES: Is the window size FIXED/KNOWN?
│   ├─ YES: Use FIXED SLIDING WINDOW → O(n) time
│   │   └─ Need max/min? → Use DEQUE
│   └─ NO: Is it CONSTRAINT-based?
│       ├─ YES: Use VARIABLE SLIDING WINDOW → O(n) time
│       └─ NO: Maybe prefix sums or DP
└─ NO: Continue below

Is it a RANGE QUERY problem?
├─ YES: Many independent queries?
│   ├─ YES: Use PREFIX SUMS → O(n+q) time
│   └─ NO: Compute on-the-fly → O(n) per query
└─ NO: Continue below

Is it a CYCLE/SEQUENCE problem?
├─ YES: Detect or find cycle?
│   ├─ YES: Use FLOYD'S ALGORITHM → O(n) time, O(1) space
│   └─ NO: Use other techniques
└─ NO: Different problem type
```

---

## 🌳 Pattern-Specific Roadmaps

### TWO POINTERS Roadmap

**When:** Pair finding, sorted array, linear scan both ends

**Template:**
```
1. Validate: Array sorted? Pair exists?
2. Initialize: left=0, right=n-1
3. Loop: While left < right
   - Compute: sum/comparison
   - Update: left or right based on result
   - Track: best answer so far
4. Return: Answer or null/empty
```

**Complexity:** O(n) time, O(1) space

**Problems:**
- Two Sum II (sorted)
- Valid Palindrome
- Container with Most Water
- Remove Duplicates (in-place)
- 3Sum, 4Sum

---

### FIXED SLIDING WINDOW Roadmap

**When:** Fixed-size window, rolling aggregate, k consecutive elements

**Template:**
```
1. Build: Initial window (first k elements) → O(k)
2. Iterate: From position k to n-1
   - Remove: array[left]
   - Add: array[right]
   - Track: best aggregate
3. Return: Best value or window
```

**Complexity:** O(n) time, O(1) or O(k) space

**Problems:**
- Maximum Average Subarray
- Max Sum of k Elements
- Sliding Window Maximum (with deque)
- Rolling Statistics

---

### VARIABLE SLIDING WINDOW Roadmap

**When:** Window size unknown, constraint-based, optimal subarray

**Template:**
```
1. Initialize: left=0, char_count={}
2. Expand: right pointer moves forward
   - Add: array[right]
   - Check: constraint satisfied?
3. Contract: While valid, shrink left
   - Track: best window
   - Remove: array[left]
4. Return: Best window or answer
```

**Complexity:** O(n) time, O(charset) or O(n) space

**Problems:**
- Minimum Window Substring
- Longest Substring Without Repeating
- Longest Substring with K Distinct Chars
- Smallest Subarray with Sum ≥ Target

---

### PREFIX SUMS Roadmap

**When:** Range queries, preprocessing for O(1) lookups

**Template:**
```
1. Build: prefix[i] = prefix[i-1] + array[i-1] → O(n)
2. Query: sum(left, right) = prefix[right+1] - prefix[left] → O(1)
3. Optional: Hash map for subarray patterns
```

**Complexity:** O(n) preprocessing + O(1) per query

**Problems:**
- Range Sum Query
- Subarray Sum Equals K
- Contiguous Array (0s and 1s)
- 2D Matrix Sum

---

### CYCLE DETECTION Roadmap

**When:** Cycle in sequences, O(1) space constraint

**Template:**
```
1. Initialize: slow=head, fast=head
2. Detect: Move slow by 1, fast by 2
   - While both != null: continue
   - If slow == fast: cycle exists
3. Find Start: Restart slow at head
   - Move both at speed 1
   - When they meet: cycle start
4. Calculate Length: Traverse cycle once
```

**Complexity:** O(n) time, O(1) space

**Problems:**
- Linked List Cycle
- Linked List Cycle II (find start)
- Find Duplicate Number
- Happy Number (functional)

---

## 🔍 Common Pitfalls & Recovery

### Pitfall 1: Using Wrong Pattern
**Symptom:** Solution works but inefficient or wrong approach
**Recovery:** Use decision tree to reclassify. Two-pointers or hash table? Fixed or variable window? Prefix or DP?

### Pitfall 2: Off-by-One Errors
**Symptom:** Array index out of bounds or wrong window size
**Recovery:** Draw array with indices. Code loop bounds explicitly (left=0, right=n-1, etc.)

### Pitfall 3: Ignoring Constraints
**Symptom:** Solution correct but uses O(n) space when O(1) required
**Recovery:** Reread problem. "O(1) space" → Floyd's or two-pointers. "Sorted array" → two-pointers possible.

### Pitfall 4: Edge Case Failures
**Symptom:** Crashes on edge cases (empty, single element, no solution)
**Recovery:** Test explicitly: size=0, size=1, size=n, no valid answer

### Pitfall 5: Misunderstanding Window Semantics
**Symptom:** Fixed/variable window confusion
**Recovery:** Is size fixed? → fixed window. Size varies? → variable window.

### Pitfall 6: Not Updating Aggregates
**Symptom:** Sliding window gives wrong sums (forgets to remove old element)
**Recovery:** When moving pointers: REMOVE old first, then ADD new. Order matters.

### Pitfall 7: Hash Map for Two-Pointers
**Symptom:** Using hash set when sorted array allows two-pointers
**Recovery:** Check if input sorted. If yes, two-pointers beats hash table (O(1) space).

---

## 📋 Quick Reference Matrix

| Problem | Best Pattern | Time | Space | Notes |
|---------|--|------|-------|---|
| Two Sum (sorted) | Two Pointers | O(n) | O(1) | Array must be sorted |
| Container with Water | Two Pointers | O(n) | O(1) | Greedy height selection |
| Sliding Max K | Fixed Window + Deque | O(n) | O(k) | Deque maintains candidates |
| Min Window Substring | Variable Window | O(n) | O(charset) | Hash map tracks chars |
| Subarray Sum = K | Prefix Sums + Hash Map | O(n) | O(n) | Store prefix sums seen |
| Linked List Cycle | Floyd's | O(n) | O(1) | No hash set needed |
| 3Sum | Two Pointers + Sort | O(n²) | O(1) or O(n) | Sort first O(n log n), then two-pointers |
| Palindrome | Two Pointers | O(n) | O(1) | Compare from ends |

---

## 🎯 Pattern Selection Checklist

**Before coding, answer these:**

- [ ] **Type:** Pair, range, aggregate, cycle, or other?
- [ ] **Size:** Fixed or variable (if window)?
- [ ] **Constraint:** Space (O(1)?) or time critical?
- [ ] **Input:** Sorted? Positive/negative mix?
- [ ] **Output:** Index, value, count, or modified array?
- [ ] **Edge cases:** Empty, single, no solution?

---

**Use this roadmap while solving. Pattern clarity → correct solution.**

