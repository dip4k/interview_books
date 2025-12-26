# ❓ WEEK 4 DAY 2: QUESTIONS & ANSWERS

**Sliding Window (Fixed) Pattern**

Generated: 2025-12-26

---

## 📌 HOW TO USE

- **Before reading:** Try to answer
- **Hints:** Don't peek!
- **Answers:** Read fully for understanding
- **Repeat:** Try again after 2 days

---

## ❓ QUESTIONS & DETAILED ANSWERS

### **Q1.** Why is fixed sliding window O(n) and not O(n·k)?

**Your answer:** _______________

**Hint:** How many times do you do O(k) work vs O(1) work?

**Answer:**

O(k) work: Once (initial window calculation)
O(1) work per iteration: n-k times (slide n-k positions)

Total: O(k) + (n-k) × O(1) = O(k) + O(n-k) = O(n)

NOT: O(n) iterations × O(k) work = O(n·k)

The key: after initial setup, each slide only removes one element and adds one element (constant time).

**Key Insight:** Initial work is amortized. Per-slide cost dominates in asymptotic analysis.

---

### **Q2.** Trace max sum on [2, 1, 5, 1, 3, 2] with k=3

**Your answer:** _______________

**Hint:** Calculate first window, then slide showing subtract/add.

**Answer:**

```
Initial window [2, 1, 5]: sum = 8
Slide 1: [1, 5, 1], sum = 8 - 2 + 1 = 7
Slide 2: [5, 1, 3], sum = 7 - 1 + 3 = 9
Slide 3: [1, 3, 2], sum = 9 - 5 + 2 = 6

Max sum: 9 (window [5, 1, 3])
```

**Key Insight:** Each slide is one subtraction + one addition = O(1).

---

### **Q3.** Can you track both MAX and MIN in each window?

**Your answer:** _______________

**Hint:** One variable for max, one for min. Both update each slide.

**Answer:**

```python
window_sum = sum(arr[:k])
max_val = window_sum
min_val = window_sum

for i in range(k, len(arr)):
    window_sum = window_sum - arr[i-k] + arr[i]
    max_val = max(max_val, window_sum)
    min_val = min(min_val, window_sum)
```

Still O(n) time, just two tracking variables instead of one.

**Key Insight:** Can track multiple aggregates in same pass without increasing complexity.

---

### **Q4.** How to return the INDEX of max window, not just value?

**Your answer:** _______________

**Hint:** Track index when you update max_sum.

**Answer:**

```python
window_sum = sum(arr[:k])
max_sum = window_sum
max_index = 0

for i in range(k, len(arr)):
    window_sum = window_sum - arr[i-k] + arr[i]
    if window_sum > max_sum:
        max_sum = window_sum
        max_index = i - k + 1  # Start of this window
```

**Key Insight:** Keep one more variable for index, update when max improves.

---

### **Q5.** Compare fixed window (Day 2) to two pointers (Day 1)

**Your answer:** _______________

**Hint:** How do pointers move? Different or same direction?

**Answer:**

| Feature | Two Pointers | Fixed Window |
|---------|--------------|--------------|
| Start | Opposite ends | Leftmost position |
| Direction | Toward middle | Same direction (right) |
| Distance | Shrinks | Fixed (k) |
| Goal | Find one pair | Process all windows |
| Time | O(n) | O(n) |
| Space | O(1) | O(1) |

Two pointers: "Meeting from both ends"
Fixed window: "Moving box of size k"

**Key Insight:** Same time complexity, different applications and patterns.

---

### **Q6.** What if k > array length?

**Your answer:** _______________

**Hint:** No valid windows exist if window size larger than array.

**Answer:**

Handle as edge case:
```python
if k > len(arr):
    return None  # No valid windows
```

Or return default:
```python
if k > len(arr):
    return arr  # Or return the entire array
```

Must check before sliding to avoid index errors.

**Key Insight:** Edge cases matter in interviews and production code.

---

### **Q7.** Why can't you use fixed sliding window for "longest substring without duplicate"?

**Your answer:** _______________

**Hint:** Is the window size fixed in that problem?

**Answer:**

"Longest substring without duplicate" requires VARIABLE window size:
- Sometimes expand (no duplicate found)
- Sometimes contract (duplicate found)

Fixed window always maintains size k, so it can't solve problems requiring variable sizing.

Need variable window algorithm (Day 3) for this.

**Key Insight:** Recognize when fixed vs variable window applies.

---

## REFERENCE ANSWERS FOR QUICK CHECK

| Q | Answer | Key Point |
|---|--------|-----------|
| 1 | O(k) + (n-k)·O(1) = O(n) | Initial amortized over slides |
| 2 | Max sum = 9 (window [5,1,3]) | Trace shows subtract/add |
| 3 | Track both max_val, min_val | Two variables, same pass |
| 4 | Store max_index = i-k+1 | Update when max improves |
| 5 | Two pointers from ends; Window slides right | Different patterns, same O(n) |
| 6 | Return None or handle edge case | Check k ≤ len(arr) first |
| 7 | Window size must be fixed | Variable needs Day 3 approach |

---

## SCORING GUIDE

- 7 correct: Mastered ✅ (move to Day 3)
- 6 correct: Strong 👍 (minor review)
- 5 correct: Solid 🟡 (review sections 1-5)
- <5 correct: Review 🔴 (re-read Day 2)

---

**Status:** Ready for self-assessment

