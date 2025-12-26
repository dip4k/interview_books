# Week 5.5: Summary & Quick Reference

**Week:** 5.5 | **Topic:** Optimization Techniques | **Difficulty:** Hard | **Time:** 15-20 hours

---

## 📊 QUICK OVERVIEW

| Technique | Time | Space | Use Case | Interview % |
|-----------|------|-------|----------|------------|
| **Difference Array** | O(m+n) | O(n) | Range updates | 10-15% |
| **In-Place Replacement** | O(n) | O(1) | Space optimization | 8-12% |
| **Deque Sliding Window** | O(n) | O(k) | Max/min in window | 5-10% |
| **Combinations** | Varies | Varies | Multi-step problems | 15-20% |

---

## 🎯 TECHNIQUE DECISION TREE

```
Problem has:
├─ Range updates followed by queries?
│  └─ Use Difference Array (Day 1)
├─ Need O(1) space for modifications?
│  └─ Use In-Place Replacement (Day 2)
├─ Sliding window max/min queries?
│  └─ Use Deque Monotonic (Day 3)
├─ Multiple of above?
│  └─ Use Combination Approach (Day 4)
└─ Can't solve? → Refer to pattern recognition
```

---

## 📝 CORE CONCEPTS SUMMARY

### Day 1: Difference Array
**What:** Mark start (+val) and end (-val) of range updates
**Why:** O(1) per update instead of O(k)
**How:** diff[left]+=val, diff[right+1]-=val, then prefix sum
**Key:** Array size = n+1 to handle boundaries

### Day 2: In-Place Replacement
**What:** Modify array using two pointers (i=read, j=write)
**Why:** O(1) extra space (i always ahead of j)
**How:** Scan for valid elements, write to position j, increment j
**Key:** i > j always ensures no read-write collision

### Day 3: Deque Sliding Window
**What:** Maintain monotonic queue of indices for window max/min
**Why:** O(n) instead of O(n log n) or O(n×k)
**How:** Remove old indices, remove dominated candidates, add current
**Key:** Front of deque = max/min of current window

### Day 4: Combinations
**What:** Chain multiple techniques for complex problems
**Why:** Real problems need 2-3 techniques working together
**How:** Identify each part, apply correct technique, combine results
**Key:** Order matters (usually updates before queries)

---

## 💾 CODE TEMPLATES

### Template 1: Difference Array

```python
# Range updates, O(1) per update
diff = [0] * (n + 1)
for left, right, val in updates:
    diff[left] += val
    diff[right + 1] -= val

# Reconstruct, O(n)
current = 0
result = []
for i in range(n):
    current += diff[i]
    result.append(current)
```

### Template 2: In-Place Removal

```python
# Remove elements, O(1) space
j = 0
for i in range(len(arr)):
    if should_keep(arr[i]):
        arr[j] = arr[i]
        j += 1
return j  # New length
```

### Template 3: Deque Sliding Window Max

```python
# Sliding window maximum, O(n)
from collections import deque
dq = deque()
for i in range(len(arr)):
    if dq and dq[0] < i - k + 1:
        dq.popleft()
    while dq and arr[dq[-1]] < arr[i]:
        dq.pop()
    dq.append(i)
    if i >= k - 1:
        result.append(arr[dq[0]])
```

---

## ⚡ COMMON MISTAKES & FIXES

| Mistake | Why Wrong | Fix |
|---------|-----------|-----|
| Difference array size = n | Array index out of bounds | Size = n+1 |
| i ≤ j in in-place | Overwrites unread data | Ensure i > j always |
| Remove from front in deque | Changes index references | Track indices, not values |
| Update while querying | Results incorrect | Update first, reconstruct, then query |
| Use heap for window max | O(n log n) instead of O(n) | Use deque for monotonic |
| Recreate array when possible in-place | Wastes O(n) space | Use in-place two-pointer |

---

## 🧠 PATTERN RECOGNITION KEYWORDS

**Difference Array triggers:**
- "Range update"
- "Add to all in [L,R]"
- "Multiple updates then query"
- "Shift range"

**In-Place triggers:**
- "In-place"
- "O(1) space"
- "Cannot use extra array"
- "Remove duplicates/elements"

**Deque triggers:**
- "Sliding window"
- "Maximum/minimum in window"
- "Every window of size k"
- "Streaming data"

**Combination triggers:**
- "Update then query"
- "Filter then analyze"
- "Multiple operations"
- "After all updates"

---

## 📊 COMPLEXITY COMPARISON

| Task | Naive | Optimized | Savings |
|------|-------|-----------|---------|
| m range updates | O(m×k) | O(m+n) | 1000x for k=1000, m=1M |
| n element removal | O(n) space | O(1) space | n space units saved |
| k window max queries | O(n×k) | O(n) | k-fold improvement |
| Combination | varies | O(m+n) | Problem dependent |

---

## ✅ INTERVIEW CHECKLIST

**Before Interview:**
- [ ] Can you recognize each technique? (30 sec)
- [ ] Can you code each from scratch? (5 min)
- [ ] Can you explain why it works? (2 min)
- [ ] Can you identify which to use? (1 min)

**During Interview:**
- [ ] Clarify problem requirements
- [ ] Identify technique needed
- [ ] Explain approach before coding
- [ ] Code cleanly with comments
- [ ] Verify with test cases
- [ ] Discuss complexity

**After Interview:**
- [ ] Can you improve further?
- [ ] Are there edge cases?
- [ ] Could you combine techniques?

---

## 🔗 PROBLEM LINKS

**Day 1 (Difference Array):**
- LeetCode 370: Range Addition
- LeetCode 1109: Corporate Flight Bookings
- LeetCode 1421: NPV of Account After Cashback

**Day 2 (In-Place):**
- LeetCode 26: Remove Duplicates from Sorted Array
- LeetCode 27: Remove Element
- LeetCode 1119: Remove Vowels from String

**Day 3 (Deque):**
- LeetCode 239: Sliding Window Maximum
- LeetCode 480: Sliding Window Median
- LeetCode 1696: Jump Game VI

**Day 4 (Combinations):**
- LeetCode 1354: Construct Target Array With Multiple Sums
- Various "hard" level problems

---

## 💡 TIPS & TRICKS

**Difference Array:**
- Always use size n+1
- Mark right+1, not right
- Reconstruct = prefix sum

**In-Place:**
- i always ahead of j
- j = number of valid elements
- Return j (new length)

**Deque:**
- Store indices, not values
- Maintain decreasing order
- dq[0] = answer

**Combinations:**
- Do updates first
- Reconstruct once
- Then answer queries

---

## 🎓 WEEK 5.5 AT A GLANCE

```
Day 1: Range updates → Difference Array → O(m+n)
Day 2: Space optimization → In-Place Two-Pointer → O(1) space
Day 3: Window queries → Deque Monotonic → O(n)
Day 4: Complex problems → Combine Techniques → Optimal
Day 5: Recognition → Interview Ready → Pattern Master
```

**Total Coverage:** 38-57% of advanced array interview problems

