# Week 5.5: Problem-Solving Roadmap

## 📊 Problem-Solving Framework

**3-Step Process for ALL Week 5.5 problems:**

1. **Classify** problem (range updates? space optimization? sliding window?)
2. **Match** Tier 2 pattern (difference array? in-place? deque?)
3. **Implement** with edge cases and verify

---

## 🎯 Pattern Decision Tree

```
Problem involves range updates on array?
├─ YES → Difference Array
└─ NO → Continue

Problem needs array modification with space O(1)?
├─ YES → In-Place Replacement (two pointers)
└─ NO → Continue

Problem needs max/min in every sliding window?
├─ YES → Deque (monotonic)
└─ NO → Other pattern (previous weeks)
```

---

## 🌳 Pattern-Specific Roadmaps

### Difference Array Roadmap

**When:** Range updates (add/subtract values to ranges)

**Template:**
```
1. Create diff array of size n+1
2. For each update (L, R, value):
     diff[L] += value
     diff[R+1] -= value
3. Reconstruct via prefix sum
4. Result in O(n+k)
```

**Examples:** Range addition, hotel bookings, shift queries

---

### In-Place Replacement Roadmap

**When:** Modify array to remove/rearrange elements, O(1) space required

**Template:**
```
1. i = 0 (read), j = 0 (write)
2. While i < n:
     if arr[i] satisfies condition:
       arr[j] = arr[i]
       j++
     i++
3. Return j (new length)
```

**Examples:** Remove duplicates, remove vowels, move zeros

---

### Deque Operations Roadmap

**When:** Find max/min in every sliding window

**Template:**
```
1. Deque stores indices (decreasing value order)
2. For i from 0 to n-1:
     Remove expired indices from front
     Remove smaller values from back
     Add current index
     Output max at front (if window complete)
```

**Examples:** Sliding window max/min, first negative

---

## 🔍 Common Pitfalls & Recovery

### Pitfall 1: "Forgot diff[R+1] boundary"
**Recovery:** Always use size n+1. diff[R+1] -= value marks end.

### Pitfall 2: "Forgot to reconstruct difference array"
**Recovery:** Difference array is intermediate. Must prefix-sum before using values.

### Pitfall 3: "Using new array instead of in-place"
**Recovery:** Two pointers: read ahead, write selectively. Only O(1) extra.

### Pitfall 4: "Storing values instead of indices in deque"
**Recovery:** Store indices to check window membership. Values alone insufficient.

### Pitfall 5: "Using increasing order in deque"
**Recovery:** Must be DECREASING order. Front = max. Back = potential future max.

---

## 📋 Quick Reference Matrix

| Problem | Pattern | Key Insight | Time | Space |
|---------|---------|-------------|------|-------|
| Range updates, batch | Difference | Mark boundaries | O(n+k) | O(n) |
| Remove duplicates | In-Place | Two pointers | O(n) | O(1) |
| Sliding max | Deque | Monotonic order | O(n) | O(k) |

---

**Master this roadmap. Each Week 5.5 problem fits exactly one pattern.**

