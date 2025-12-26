# Week 4: Executive Summary & Key Takeaways

**Quick Reference Guide for Week 4: Two Pointers, Sliding Window, Prefix Sums**

---

## 🎯 One-Line Essence Per Day

| Day | Topic | Core Idea |
|-----|-------|-----------|
| **1** | Two Pointers | O(n) on sorted arrays; converging pointers eliminate nested loops; works in-place |
| **2** | Sliding Window | O(n) on any array; dynamic window expands/shrinks; each element touched ≤2 times |
| **3** | Prefix Sums | O(1) range queries after O(n) preprocessing; trade space for query speed |
| **4** | Advanced TP | Extend to k targets; fix k-2 elements, two-pointers on rest; O(n^(k-1)) |
| **5** | Integration | Combine techniques strategically; choose based on constraints; space vs time |

---

## 📊 Complexity Cheat Sheet

### Technique Comparison

```
Problem: Find pairs summing to target

Approach              Time        Space   Requires Sorting
Brute Force (nested)  O(n²)       O(1)    No
Hash Table           O(n)         O(n)    No
Two Pointers         O(n log n)   O(1)    YES (sort included)
Two Pointers (sorted) O(n)        O(1)    YES (input already sorted)
```

### When Each Technique Shines

| Technique | Best Case | Avg Case | Worst Case | Space | Requirement |
|-----------|-----------|----------|-----------|-------|-------------|
| **Two Pointers** | O(n) | O(n) | O(n) | O(1) | Sorted array |
| **Sliding Window** | O(n) | O(n) | O(n) | O(k) | Monotonic validity |
| **Prefix Sums** | O(n) | O(n) | O(n) | O(n) | Static array |

---

## 🎓 Technique Decision Tree

### Choosing the Right Technique

```
Is array sorted?
  ├─ YES
  │   ├─ Need pairs? → Two Pointers (converging)
  │   └─ Need triplets/quads? → Advanced Two Pointers
  │
  └─ NO
      ├─ Need subarray property? → Sliding Window
      ├─ Need range queries? → Prefix Sums (after sorting)
      └─ Need pairs? → Hash Table

Is space critical?
  ├─ YES → Two Pointers (O(1)) or Sliding Window (O(k))
  └─ NO → Hash Table or Prefix Sums

Need multiple queries?
  ├─ YES → Prefix Sums (O(n) + O(1) per query)
  └─ NO → Direct calculation
```

---

## 🎓 Key Concepts & Formulas

### Two Pointers (Day 1)

**When:** Array is sorted, find pair matching condition  
**How:** Converge from opposite ends  
**Movement:** Based on comparison with target  

```
left = 0, right = n-1
while left < right:
    if condition(arr[left], arr[right]):
        return (left, right)
    elif need_larger:
        left += 1  ← Move toward larger
    else:
        right -= 1  ← Move toward smaller
```

**Why O(n):** Each pointer moves once (n total movements)

### Sliding Window (Day 2)

**When:** Need optimal subarray/substring property  
**How:** Expand right, shrink left  
**Requirement:** Can incrementally update metric  

```
left = 0
for right in range(n):
    add arr[right] to window
    
    while window_invalid:
        remove arr[left] from window
        left += 1
    
    update_result(window)
```

**Why O(n):** Right pointer moves n times, left pointer moves n times total

### Prefix Sums (Day 3)

**When:** Multiple range sum queries  
**How:** Precompute cumulative sums  
**Formula:** sum(left, right) = prefix[right+1] - prefix[left]  

```
# Build: O(n)
prefix[0] = 0
for i in range(n):
    prefix[i+1] = prefix[i] + arr[i]

# Query: O(1)
range_sum = prefix[right+1] - prefix[left]
```

**Space-Time Trade-off:** O(n) space → O(1) queries

### Advanced Two Pointers (Day 4)

**When:** Multiple target elements (3Sum, 4Sum)  
**How:** Fix k-2 elements, two-pointers on rest  
**Complexity:** O(n^(k-1)) vs O(n^k) brute force  

```
for i in range(n):         # Fix 1st element
    left = i+1, right = n-1
    while left < right:
        if arr[i] + arr[left] + arr[right] == target:
            add triplet
        elif sum < target:
            left += 1
        else:
            right -= 1
```

---

## 📈 Real-World Applications

### Two Pointers
- **Target sum problems:** Trading pairs, debt matching
- **Validation:** Palindrome checks, balanced parentheses
- **Geometry:** Container with max water, closest points

### Sliding Window
- **Substring problems:** Longest unique, min window
- **Time series:** Moving averages, trending analysis
- **Network:** Packet processing in time windows
- **DNA:** Pattern matching in genome sequences

### Prefix Sums
- **Analytics:** Cumulative metrics over time
- **Image processing:** Integral images for features
- **Warehouse:** Quick aggregation queries
- **Finance:** Rolling sum calculations

### Advanced Two Pointers
- **Optimization:** Multi-target solutions efficiently
- **Database:** Multi-field matching queries
- **Geometry:** Finding special point combinations

---

## 💡 Critical Insights That Changed Everything

### Two Pointers

1. **Sorted property enables directional movement**
   - Increasing left increases sum
   - Decreasing right decreases sum
   - This monotonicity is KEY

2. **O(n) because no backtracking**
   - Once left moves right, never moves left again
   - Once right moves left, never moves right again
   - "Squeezing" pattern guarantees single pass

3. **Works in-place with O(1) space**
   - No extra arrays needed
   - Just indices and one/two variables
   - Elegant optimization

### Sliding Window

1. **Incremental updates are the magic**
   - Don't recalculate from scratch
   - Just add new, remove old
   - Enables O(n) where naive is O(n²)

2. **Works on unsorted data (unlike two pointers)**
   - No sorting required
   - Conditions based on content, not order
   - More general applicability

3. **Window size changes dynamically**
   - Contrasts with fixed-size windows
   - Flexibility enables optimization
   - Requires understanding when to shrink

### Prefix Sums

1. **Trading space for query speed**
   - O(n) preprocessing, O(1) queries
   - For q queries: O(n + q) vs O(nq) naive
   - Strategic trade-off decision

2. **Formula-based correctness**
   - No ambiguity in calculation
   - Easy to verify
   - Foundation for advanced structures

3. **Generalizes to dimensions**
   - 1D: linear arrays
   - 2D: rectangular regions
   - 3D: boxes (inclusion-exclusion)

### Advanced Two Pointers

1. **Nesting reduces exponential complexity**
   - 3Sum: O(n²) vs O(n³)
   - 4Sum: O(n³) vs O(n⁴)
   - Factor of n improvement

2. **Duplicate handling is critical**
   - Not a minor detail
   - Determines correctness
   - Common interview mistake

---

## ❌ Common Mistakes to Avoid

### Two Pointers
1. **Forgetting array must be sorted**
   - Won't work on unsorted arrays
   - Need to sort first (adds O(n log n))

2. **Moving wrong pointer**
   - Wrong direction leads to missing solutions
   - Example: Always moving left when should move right

3. **Off-by-one errors**
   - left < right vs left <= right matters
   - Index boundaries critical

### Sliding Window
1. **Metric not incrementally updatable**
   - Max/min in window doesn't work (need segment tree)
   - Not all problems fit pattern
   - Know when NOT to use

2. **Forgetting window can shrink below valid size**
   - May need to re-expand
   - Process might not be linear
   - Analyze carefully

3. **Not handling duplicates/frequency**
   - Unique character problems need frequency tracking
   - Hash map vs set crucial

### Prefix Sums
1. **Array must be static**
   - If array changes, must rebuild prefix
   - For updates: use segment tree
   - Know the limitation

2. **Index confusion**
   - Off-by-one in building or querying
   - prefix[i] vs arr[i] distinction critical
   - Test with small examples

### Advanced Two Pointers
1. **Not skipping duplicates**
   - Returns same triplet multiple times
   - Algorithm correctness requires careful skipping

2. **Thinking it solves 5Sum efficiently**
   - O(n⁴) still expensive
   - Practical limit: 3Sum, maybe 4Sum
   - Beyond: different approaches needed

---

## 📋 Quick Test: Do You Understand?

**Quick check—without looking, can you answer?**

1. Why is two pointers O(n) and not O(n²)?
2. When does sliding window work better than two pointers?
3. What's the formula for range sum using prefix?
4. How do you skip duplicates in 3Sum correctly?
5. When would you choose O(n) space over O(1)?

**If all five are clear:** You understand Week 4 ✓  
**If ≤ 3 clear:** Review those sections before moving to Week 5  
**If 0-2 clear:** Work through examples more carefully  

---

## 🏆 Mastery Checklist

**You've mastered Week 4 when:**

- [ ] Can implement two pointers without hints
- [ ] Understand why sliding window O(n)
- [ ] Know prefix sum formula intuitively
- [ ] Can trace 3Sum on paper
- [ ] Recognize technique in new problems
- [ ] Choose optimal approach automatically
- [ ] Handle all edge cases
- [ ] Explain to others clearly
- [ ] Solve LeetCode medium problems
- [ ] Combine techniques in complex problems

---

## 📚 Conceptual Connections

### Week 3 → Week 4
- **Sorting:** Required for two pointers
- **Hash Tables:** Alternative for some two-pointer problems
- **Arrays:** Foundation for all three techniques

### Week 4 → Week 5
- **Binary Search:** Works with sorted data (like two pointers)
- **Greedy:** Similar decision-making as sliding window
- **Dynamic Programming:** Sometimes alternative to prefix sums

### Week 4 → Week 6
- **Graphs:** DFS/BFS sometimes use similar pointer patterns
- **Strings:** Many string algorithms use sliding window

---

## 🚀 When to Use What

### Use Two Pointers When
```
✓ Array is sorted (or sortable)
✓ Need to find pair matching condition
✓ Space is critical (O(1))
✓ In-place solution required
✗ Array is random (unsorted, must sort first)
✗ Need all pairs (better: hash table)
```

### Use Sliding Window When
```
✓ Need optimal subarray/substring
✓ Can incrementally update metric
✓ Works on unsorted data
✓ Want O(n) on non-sorted array
✗ Need max/min (use other structure)
✗ Metric not incrementally updatable
```

### Use Prefix Sums When
```
✓ Multiple range queries
✓ Array is static
✓ Want O(1) after preprocessing
✓ Need 2D/3D ranges
✗ Array changes frequently (use segment tree)
✗ Single query (overhead not worth it)
```

---

## 📊 Space vs Time Trade-offs Summary

| Scenario | Space-Optimized | Time-Optimized | Balance |
|----------|-----------------|----------------|---------|
| **Single query** | O(1) direct | Hash O(n) | Direct |
| **Multiple queries** | O(1) + O(nq) | O(n) + O(q) | Prefix sums |
| **Dynamic data** | Recalculate | Segment tree | Balanced tree |
| **Extreme size** | O(1) crucial | O(n) space | streaming |

---

## 🎓 Study Tips for Week 4

1. **Master one technique per day**
   - Don't try to learn all at once
   - Each day builds on previous
   - Solidify before moving on

2. **Trace by hand, code second**
   - Understanding algorithm first
   - Implementation details later
   - Paper traces catch bugs

3. **Recognize technique in problems**
   - Don't just memorize solutions
   - Learn to identify "this is a two-pointer problem"
   - Pattern recognition is key skill

4. **Start with simple examples**
   - Two pointers: [1,2,3,4,5], target = 6
   - Sliding window: "abc"
   - Prefix sums: [1,2,3,4,5]
   - Build intuition on simple cases

5. **Combine with previous weeks**
   - Two pointers needs sorting (Week 3)
   - Sliding window uses hash tables (Week 3)
   - These aren't isolated techniques

---

## 🎯 Interview Preparation

**Common interview questions:**

1. "Optimize this O(n²) solution"
   - Answer: Use two pointers (if sorted)
   - Or: Use sliding window (if subarray)
   - Or: Use hash table (if pairs)

2. "Can you do this in-place?"
   - Answer: Two pointers works in O(1) space
   - Show why: no extra arrays

3. "Solve without extra space"
   - Answer: Two pointers (O(1) optimal)
   - Contrast with prefix sums (needs O(n))

4. "Handle multiple queries efficiently"
   - Answer: Prefix sums (O(n) + O(1) each)
   - Show trade-off thinking

---

## 📞 Quick Reference

**Two Pointers:** left ← → right, O(n)  
**Sliding Window:** [left → right], O(n), expand/shrink  
**Prefix Sums:** prefix[i+1] = prefix[i] + arr[i], O(1) query  
**Advanced TP:** Fix k-2, two-pointers on rest, O(n^(k-1))  

---

**Week 4 Complete!** Ready to move to Week 5 (Binary Search, Greedy, etc.)?

**Total Estimated Time:** 6-8 hours for deep understanding  
**Mastery Level After Week 4:** Intermediate → Advanced on arrays/strings ✓

