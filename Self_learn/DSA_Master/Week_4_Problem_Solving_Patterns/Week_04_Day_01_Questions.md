# ❓ WEEK 4 DAY 1: QUESTIONS & ANSWERS

**Two Pointers Pattern**

Generated: 2025-12-26

---

## 📌 HOW TO USE

- **Before reading:** Try to answer
- **Hints:** Don't peek!
- **Answers:** Read fully for understanding
- **Repeat:** Try again after 2 days

---

## ❓ QUESTIONS & DETAILED ANSWERS

### **Q1.** Why does two pointers only work on sorted arrays?

**Your answer:** _______________

**Hint:** What property does sorting guarantee about elements?

**Answer:**

Sorted arrays guarantee: arr[i] < arr[i+1]

This means:
- If arr[left] + arr[right] < target
- We know arr[left] is too small
- Incrementing left increases sum (guaranteed)
- No way smaller left values help

In unsorted array, incrementing left might decrease sum (no property to rely on).

**Key Insight:** Sorting creates monotonic property we exploit.

---

### **Q2.** Trace two-sum on [-1, 0, 1, 2, 3] target=2

**Your answer:** _______________

**Hint:** Start left=0, right=4. Track each iteration.

**Answer:**

```
Iteration 1: left=0, right=4
  arr[0]=-1, arr[4]=3, sum=2 (FOUND!)
  Return (-1, 3)
```

Took 1 iteration. Two pointers exploits sorted order to find quickly.

**Key Insight:** Lucky first try, but worst case would scan more.

---

### **Q3.** Can two pointers find ALL pairs with target sum? Why/why not?

**Your answer:** _______________

**Hint:** What happens after we find one pair?

**Answer:**

No, two pointers finds one pair and stops.

Why:
- Once sum == target, we return
- To find all pairs, need to continue
- But then it's O(n²) or use hash set

For all pairs:
```python
pairs = set()
left, right = 0, n-1
while left < right:
    s = arr[left] + arr[right]
    if s == target:
        pairs.add((arr[left], arr[right]))
        left += 1  # Continue searching
        right -= 1
    elif s < target:
        left += 1
    else:
        right -= 1
```

**Key Insight:** Problem determines if we need one or all.

---

### **Q4.** Two-pointers is O(n) vs O(n²) nested loop. Why?

**Your answer:** _______________

**Hint:** How many times does each pointer move?

**Answer:**

Nested loop:
- Outer loop: n iterations
- Inner loop: n iterations
- Total: n × n = n²

Two pointers:
- left pointer moves: at most n times (0 → n-1)
- right pointer moves: at most n times (n-1 → 0)
- Total movements: at most 2n = O(n)

The key difference:
- Nested loop: inner resets each outer iteration
- Two pointers: each pointer moves at most once per element

**Key Insight:** One pass with intelligent movement beats nested scan.

---

### **Q5.** How would you find triplets summing to target (3-sum)?

**Your answer:** _______________

**Hint:** Fix one element, then use two pointers on remainder.

**Answer:**

```python
def three_sum(arr, target):
    arr.sort()  # O(n log n)
    result = []
    
    for i in range(len(arr)-2):  # O(n)
        left, right = i+1, len(arr)-1
        while left < right:  # O(n)
            s = arr[i] + arr[left] + arr[right]
            if s == target:
                result.append((arr[i], arr[left], arr[right]))
                left += 1
            elif s < target:
                left += 1
            else:
                right -= 1
    
    return result
```

Complexity:
- Sort: O(n log n)
- Outer loop: O(n)
- Inner two-pointers: O(n)
- Total: O(n²)

**Key Insight:** Fixing one element, solve reduced problem with two pointers.

---

### **Q6.** Valid palindrome vs two-sum: why use two pointers for both?

**Your answer:** _______________

**Hint:** How are they similar? How do pointers move?

**Answer:**

**Two-sum:** Find two numbers from ends that sum to target
- Start: left=0, right=n-1
- Compare: sum vs target
- Move: left if too small, right if too big

**Valid palindrome:** Check if string reads same both directions
- Start: left=0, right=n-1
- Compare: char[left] == char[right]
- Move: left++ and right-- if match, return false if mismatch

**Similarity:** Both start at opposite ends, work toward middle.

**Why:** Sorted property (for sum) or symmetric property (for palindrome) makes this efficient.

**Key Insight:** Two pointers elegant for many start-and-end problems.

---

### **Q7.** Space complexity O(1) for two pointers. How?

**Your answer:** _______________

**Hint:** What data structures are needed?

**Answer:**

Only need:
- left: one integer (index)
- right: one integer (index)

Don't need:
- Hash map (would be O(n))
- Result array (can return pair directly)
- Temp array (no copying)

Total space: 2 integers = O(1) constant space.

Compare to:
- Hash set approach: O(n) for set storage
- Nested loop: O(1) space but O(n²) time

**Key Insight:** Sorted array enables space-efficient solution.

---

## REFERENCE ANSWERS FOR QUICK CHECK

| Q | Answer | Time | Space |
|---|--------|------|-------|
| 1 | Sorting guarantees monotonicity | - | - |
| 2 | (-1, 3) in 1 iteration | - | - |
| 3 | No; returns first pair | - | - |
| 4 | 2n movements vs n² iterations | - | - |
| 5 | O(n²) - one element fixed, two pointers | O(n²) | O(1) |
| 6 | Both use opposite end property | - | - |
| 7 | Only two integers needed | - | O(1) |

---

## SCORING GUIDE

- 7 correct: Mastered ✅ (move to Day 2)
- 6 correct: Strong 👍 (minor review)
- 5 correct: Solid 🟡 (review sections 1-5)
- <5 correct: Review 🔴 (re-read Day 1)

---

**Status:** Ready for self-assessment

