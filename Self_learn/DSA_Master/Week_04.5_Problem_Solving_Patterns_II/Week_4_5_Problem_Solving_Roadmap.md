# Week 4.5: Problem-Solving Roadmap

## 📊 Problem-Solving Framework

**5-Step Process for ALL Tier 1 patterns:**

1. **Identify** the problem class (lookup, ordering, merging, segregation, optimization)
2. **Match** to Tier 1 pattern (Hash, Monotonic, Merge, Partition, Kadane)
3. **Analyze** complexity and constraints (time, space, in-place?)
4. **Implement** the pattern carefully
5. **Verify** on examples and edge cases

---

## 🎯 Pattern Decision Tree

```
START: Problem classification

Need fast membership or frequency?
├─ YES → Hash Map/Set
└─ NO → Continue

Need next/previous element efficiently?
├─ YES → Monotonic Stack
└─ NO → Continue

Combine two sorted structures?
├─ YES → Merge Operations
└─ NO → Continue

In-place rearrangement needed?
├─ YES → Partition
└─ NO → Continue

Subarray optimization problem?
├─ YES → Kadane DP
└─ NO → Other pattern (Week 5+)
```

---

## 🌳 Pattern-Specific Roadmaps

### Hash Map/Set Roadmap

**Condition:** Need O(1) lookup or frequency counting

**Template:**
```
1. Create hash map/set
2. Iterate through input
3. Check membership OR update frequency
4. Return result
```

**Examples:** Two Sum, Anagrams, Duplicates, Majority Element

---

### Monotonic Stack Roadmap

**Condition:** Need next/previous greater/smaller element

**Template:**
```
1. Create stack (stores indices)
2. For each element from left/right:
     while stack not empty AND condition:
       pop → answer for popped element
     push current index
3. Handle remaining stack (no next element)
```

**Examples:** Next Greater Element, Temperatures, Trapping Rain

---

### Merge Operations Roadmap

**Condition:** Combining two sorted structures

**Template:**
```
1. Two pointers: p1=0, p2=0
2. Compare elements at p1, p2
3. Take smaller, advance that pointer
4. When one exhausted, append rest
```

**Examples:** Merge Arrays, Merge Lists, Merge Intervals

---

### Partition Roadmap

**Condition:** In-place rearrangement by criteria

**Template:**
```
1. left=0, right=n-1
2. While left < right:
     Move left until condition violated
     Move right until condition violated
     Swap if left < right
3. Return partition position or verify
```

**Examples:** Move Zeros, Dutch Flag, Quicksort

---

### Kadane's Algorithm Roadmap

**Condition:** Subarray optimization (max sum, product, length)

**Template:**
```
1. current = arr[0], global = arr[0]
2. For i from 1 to n-1:
     current = max(arr[i], current + arr[i])
     global = max(global, current)
3. Return global
```

**Examples:** Max Subarray, Max Product, Longest Subarray

---

## 🔍 Common Pitfalls & Recovery

### Pitfall 1: "Hash gives O(1) always"
**Recovery:** Remember worst case O(n). Focus on average case. Handle collisions.

### Pitfall 2: "Monotonic stack doesn't apply"
**Recovery:** Check: does problem ask for next/previous element? If yes, try stack.

### Pitfall 3: "Forgot to handle remaining elements after merge"
**Recovery:** After one pointer exhausted, append rest of other array.

### Pitfall 4: "Partition didn't segregate correctly"
**Recovery:** Verify loop condition. Two pointers must actually swap.

### Pitfall 5: "Kadane resets at wrong point"
**Recovery:** Reset only when current + next < next alone. Not at every negative.

---

## 📋 Quick Reference Matrix

| Problem Type | Pattern | Time | Space | Precondition |
|--------------|---------|------|-------|--------------|
| Lookup/Count | Hash | O(1) avg | O(n) | None |
| Next Element | Monotonic Stack | O(n) | O(n) | None |
| Merge Sorted | Merge | O(n+m) | O(n+m) | Both sorted |
| Segregate | Partition | O(n) | O(1) | In-place |
| Subarray Opt | Kadane | O(n) | O(1) | None |

---

**Master this roadmap. Most Tier 1 problems fit exactly one pattern.**

