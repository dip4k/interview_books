# ❓ WEEK 4 DAY 3: QUESTIONS & ANSWERS

**Sliding Window (Variable) Pattern**

Generated: 2025-12-26

---

## 📌 HOW TO USE

- **Before reading:** Try to answer
- **Hints:** Don't peek!
- **Answers:** Read fully for understanding
- **Repeat:** Try again after 2 days

---

## ❓ QUESTIONS & DETAILED ANSWERS

### **Q1.** Why can't left pointer move backward in variable sliding window?

**Your answer:** _______________

**Hint:** Once we leave a position, do we ever need to revisit it?

**Answer:**

Once left moves past position i, we've determined all windows [i, j] don't satisfy our condition. Moving right forward won't create a new [i-1, j] that suddenly satisfies (we'd reject for same reason).

Intuition: If condition fails with left=i, and we move right=i+1, no benefit to checking left=i-1 (would need to add back arr[i] which caused original failure).

**Key Insight:** One-pass guarantee: each element examined once entering, once exiting.

---

### **Q2.** Trace longest unique substring on "dvdf"

**Your answer:** _______________

**Hint:** Expand until duplicate, then contract until valid, track max length.

**Answer:**

```
Step 1: right=0, 'd'
  set={d}, left=0, length=1

Step 2: right=1, 'v'
  set={d,v}, left=0, length=2

Step 3: right=2, 'd' (duplicate!)
  Contract: remove set[left=0]='d'
  set={v,d}, left=1, length=2

Step 4: right=3, 'f'
  set={v,d,f}, left=1, length=3

Max length: 3 (substring "vdf")
```

**Key Insight:** Duplicates force contraction.

---

### **Q3.** How to modify for "at most k distinct characters"?

**Your answer:** _______________

**Hint:** Instead of checking duplicates, check number of distinct chars.

**Answer:**

```python
def max_k_distinct(s, k):
    left = 0
    char_count = {}
    max_len = 0
    
    for right in range(len(s)):
        # Expand: add char at right
        char_count[s[right]] = char_count.get(s[right], 0) + 1
        
        # Contract: while more than k distinct
        while len(char_count) > k:
            char_count[s[left]] -= 1
            if char_count[s[left]] == 0:
                del char_count[s[left]]
            left += 1
        
        # Update max
        max_len = max(max_len, right - left + 1)
    
    return max_len
```

**Key Insight:** Change condition, same algorithm structure.

---

### **Q4.** Compare variable window to two pointers (Day 1). When use which?

**Your answer:** _______________

**Hint:** What does each pattern optimize for?

**Answer:**

| Feature | Two Pointers | Variable Window |
|---------|--------------|-----------------|
| Input | Sorted array | Any array/string |
| Goal | Find one pair | Find optimal substring |
| Condition | Equality/inequality | Property of substring |
| Direction | Opposite ends | Same direction |
| Time | O(n) | O(n) |

Use two pointers when: Find pair in sorted array
Use variable window when: Find substring with property

Different problems, same O(n) complexity.

**Key Insight:** Recognize problem type to choose pattern.

---

### **Q5.** Why is variable sliding window O(n) not O(n²)?

**Your answer:** _______________

**Hint:** How many times does each pointer move in total?

**Answer:**

Right pointer: moves n times (0 to n-1)
Left pointer: moves at most n times total (starts at 0, only goes right)

Total movements: n + n = 2n = O(n)

NOT: n iterations × n work = O(n²)

Key: Each element is added once (right pointer) and removed once (left pointer).

**Key Insight:** Amortized analysis: two O(n) pointers = O(n) total.

---

### **Q6.** How to find MINIMUM length instead of maximum?

**Your answer:** _______________

**Hint:** Track minimum instead of maximum.

**Answer:**

```python
def min_window(s, t):
    left = 0
    min_len = float('inf')
    needed = len(t)
    # ... build window until have all chars ...
    # ... contract until missing chars ...
    min_len = min(min_len, right - left + 1)
    return min_len
```

Pattern: Same expand-contract, just track minimum length instead of maximum.

**Key Insight:** Algorithm adapts to different goals (min vs max).

---

### **Q7.** What if you need BOTH length AND the substring itself?

**Your answer:** _______________

**Hint:** Track the best position and length, then extract substring.

**Answer:**

```python
def longest_unique_substring(s):
    left = 0
    char_set = set()
    max_len = 0
    max_start = 0
    
    for right in range(len(s)):
        while s[right] in char_set:
            char_set.remove(s[left])
            left += 1
        char_set.add(s[right])
        
        if right - left + 1 > max_len:
            max_len = right - left + 1
            max_start = left
    
    return s[max_start:max_start + max_len]
```

Track start position of best window, then extract substring.

**Key Insight:** Remember position, not just length.

---

## REFERENCE ANSWERS FOR QUICK CHECK

| Q | Answer | Key Point |
|---|--------|-----------|
| 1 | No revisit: each element once | One-pass algorithm |
| 2 | Length 3, substring "vdf" | Duplicates cause contraction |
| 3 | len(char_count) > k condition | Change condition, same algo |
| 4 | Two pointers: pair; Variable: substring | Different problem types |
| 5 | 2n movements = O(n) | Each element added/removed once |
| 6 | Track min_len not max_len | Adapt for different goals |
| 7 | Track max_start and max_len | Extract substring after |

---

## SCORING GUIDE

- 7 correct: Mastered ✅ (move to Day 4)
- 6 correct: Strong 👍 (minor review)
- 5 correct: Solid 🟡 (review sections 1-5)
- <5 correct: Review 🔴 (re-read Day 3)

---

**Status:** Ready for self-assessment

