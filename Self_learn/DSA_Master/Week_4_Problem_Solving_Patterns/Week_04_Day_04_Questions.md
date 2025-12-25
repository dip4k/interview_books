# ❓ WEEK 4 DAY 4: QUESTIONS & ANSWERS

**Prefix Sum Pattern**

Generated: 2025-12-26

---

## 📌 HOW TO USE

- **Before reading:** Try to answer
- **Hints:** Don't peek!
- **Answers:** Read fully for understanding
- **Repeat:** Try again after 2 days

---

## ❓ QUESTIONS & DETAILED ANSWERS

### **Q1.** Why is O(n) space worth it if you only have a few queries?

**Your answer:** _______________

**Hint:** Compare O(n·q) vs O(n + q) for different q values.

**Answer:**

It's NOT worth it for few queries!

Compare:
- Few queries (q=1): O(n·1)=O(n) vs O(n+1)=O(n) → same
- Medium queries (q=10): O(n·10) vs O(n+10) → slightly better
- Many queries (q=1M): O(n·1M) vs O(n+1M) → vastly better (100x+)

Use prefix sum when: q >> log(n) (many queries)
Use naive when: q small (few queries)

**Key Insight:** Space-time tradeoff only worth it at scale.

---

### **Q2.** What does prefix[i] represent exactly?

**Your answer:** _______________

**Hint:** Is it sum up to i, or up to i-1?

**Answer:**

prefix[i] = sum of arr[0] through arr[i-1]

Note the offset-by-one! It includes i-1, excludes i.

Example:
```
arr = [3, 2, 5, 1]
prefix[0] = 0           (sum of nothing)
prefix[1] = 3           (sum of arr[0])
prefix[2] = 3 + 2 = 5   (sum of arr[0..1])
prefix[3] = 5 + 5 = 10  (sum of arr[0..2])
prefix[4] = 10 + 1 = 11 (sum of arr[0..3])
```

This offset makes the formula work cleanly.

**Key Insight:** Offset-by-one is essential to math.

---

### **Q3.** Why does range_sum(left, right) = prefix[right+1] - prefix[left]?

**Your answer:** _______________

**Hint:** What does each prefix value contain?

**Answer:**

prefix[right+1] contains sum of arr[0..right]
prefix[left] contains sum of arr[0..left-1]

Subtracting removes everything before left:
```
prefix[right+1] - prefix[left]
= (arr[0] + ... + arr[right]) - (arr[0] + ... + arr[left-1])
= arr[left] + arr[left+1] + ... + arr[right]
= sum(arr[left..right]) ✓
```

The key: subtract to remove unwanted prefix.

**Key Insight:** Subtraction gets exact range.

---

### **Q4.** Trace prefix array on [2, 4, 1, 3]

**Your answer:** _______________

**Hint:** Start with prefix[0]=0, add each element.

**Answer:**

```
arr = [2, 4, 1, 3]

prefix[0] = 0
prefix[1] = 0 + 2 = 2
prefix[2] = 2 + 4 = 6
prefix[3] = 6 + 1 = 7
prefix[4] = 7 + 3 = 10

Result: prefix = [0, 2, 6, 7, 10]
```

Verify:
- prefix[1] = 2 = sum(arr[0]) ✓
- prefix[2] = 6 = sum(arr[0..1]) = 2+4 ✓
- prefix[3] = 7 = sum(arr[0..2]) = 2+4+1 ✓

---

### **Q5.** Using prefix from Q4, calculate sum(1, 2)

**Your answer:** _______________

**Hint:** Use formula prefix[right+1] - prefix[left]

**Answer:**

sum(1, 2) = prefix[3] - prefix[1]
          = 7 - 2
          = 5

Verify: arr[1] + arr[2] = 4 + 1 = 5 ✓

**Key Insight:** Query is just one subtraction!

---

### **Q6.** What happens with negative numbers in the array?

**Your answer:** _______________

**Hint:** Does the math still work with negatives?

**Answer:**

Works perfectly! Prefix sum works with ANY numbers.

Example with negatives:
```
arr = [-2, 5, -1, 3]

prefix[0] = 0
prefix[1] = 0 + (-2) = -2
prefix[2] = -2 + 5 = 3
prefix[3] = 3 + (-1) = 2
prefix[4] = 2 + 3 = 5

Query sum(1, 2) = prefix[3] - prefix[1] = 2 - (-2) = 4
Verify: 5 + (-1) = 4 ✓
```

Negative numbers just decrease the running total.

**Key Insight:** Math works regardless of sign.

---

### **Q7.** How to adapt prefix sum for PRODUCT instead of SUM?

**Your answer:** _______________

**Hint:** Multiplication instead of addition. What's the identity?

**Answer:**

Use multiplication, start with 1 not 0:

```python
def build_prefix_product(arr):
    prefix = [1]  # Identity for multiplication!
    for num in arr:
        prefix.append(prefix[-1] * num)

def range_product(prefix, left, right):
    return prefix[right + 1] / prefix[left]  # Division instead!
```

Example:
```
arr = [2, 3, 4]
prefix_product = [1, 2, 6, 24]

Query product(0, 1) = prefix[2] / prefix[0] = 6 / 1 = 6
Verify: 2 * 3 = 6 ✓

Query product(1, 2) = prefix[3] / prefix[1] = 24 / 2 = 12
Verify: 3 * 4 = 12 ✓
```

Caveat: Watch for zeros! Division by zero undefined.

**Key Insight:** Generalize to other operations with identity elements.

---

## REFERENCE ANSWERS FOR QUICK CHECK

| Q | Answer | Key Point |
|---|--------|-----------|
| 1 | Only worth when q >> log n | Space-time tradeoff |
| 2 | Sum of arr[0..i-1] | Offset-by-one crucial |
| 3 | Subtracts prefix before index | Removes unwanted part |
| 4 | [0, 2, 6, 7, 10] | Running total |
| 5 | 5 (just one subtraction) | O(1) query |
| 6 | Works fine! | Math universal |
| 7 | Use multiplication & division | Generalize pattern |

---

## SCORING GUIDE

- 7 correct: Mastered ✅ (move to Day 5)
- 6 correct: Strong 👍 (minor review)
- 5 correct: Solid 🟡 (review sections 1-5)
- <5 correct: Review 🔴 (re-read Day 4)

---

**Status:** Ready for self-assessment

