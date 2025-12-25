# ❓ WEEK 4.5: QUESTIONS & ANSWERS

**Socratic Questions - 28 Total (7 per day × 4 days)**

Generated: 2025-12-26

---

## 📌 HOW TO USE

- **Attempt first:** Try to answer without looking
- **Hints provided:** For extra help if needed
- **Read fully:** Understanding > memorizing
- **Trace examples:** Critical for learning
- **Repeat:** Try again after 2 days

---

## DAY 1: HASH MAP / HASH SET QUESTIONS

### **Q1.** Why is hash set O(1) average but O(n) worst case?

**Your answer:** _______________

**Hint:** What happens when many elements hash to same bucket?

**Answer:**

Average case: Hash function distributes keys uniformly across buckets. Most lookups hit bucket directly without collision. O(1) average.

Worst case: Poor hash function causes collisions. Many elements hash to same bucket. Must search linked list of collisions. O(n) worst case.

In practice, Python's hash functions are excellent, so worst case is extremely rare.

---

### **Q2.** Trace duplicate detection on [1, 2, 3, 2, 5]

**Your answer:** _______________

**Hint:** Track seen set at each step

**Answer:**

```
seen = {}, num = 1 → seen = {1}
seen = {1}, num = 2 → seen = {1, 2}
seen = {1, 2}, num = 3 → seen = {1, 2, 3}
seen = {1, 2, 3}, num = 2 → 2 IN SET! Duplicate found!
```

---

### **Q3.** How do you count character frequencies?

**Your answer:** _______________

**Hint:** Use dict.get() with default value

**Answer:**

```python
freq = {}
for char in string:
    freq[char] = freq.get(char, 0) + 1
# Example: "hello" → {'h': 1, 'e': 1, 'l': 2, 'o': 1}
```

---

### **Q4.** When would you use hash set instead of sorted list?

**Your answer:** _______________

**Hint:** Think about what operations you need

**Answer:**

Use hash set when:
- Need O(1) membership testing (vs O(log n) for sorted)
- Don't care about order
- Space available

Use sorted list when:
- Need sorted order
- Range queries needed (find all elements between x and y)
- Space critical

---

### **Q5.** What's the space-time tradeoff for hash maps?

**Your answer:** _______________

**Hint:** Compare to array search

**Answer:**

Hash map: O(n) space for O(1) lookup
Array: O(n) space for O(n) lookup

Trade extra space management complexity for instant lookup. Worth it when lookups frequent.

---

### **Q6.** How does hash collision resolution work in Python?

**Your answer:** _______________

**Hint:** What happens when two keys hash to same index?

**Answer:**

Python uses chaining: Multiple values that hash to same bucket stored in linked list. On lookup, hash to bucket, then search linked list. With good hash function, linked lists remain short, keeping O(1) average.

---

### **Q7.** When would you NOT use a hash set?

**Your answer:** _______________

**Hint:** Think about constraints and requirements

**Answer:**

Don't use when:
- Need sorted order (use TreeSet/sorted list)
- Very limited space (hash set uses O(n))
- Need range queries (use BST or sorted array)
- Need ordered iteration (use TreeMap)

---

## DAY 2: MONOTONIC STACK QUESTIONS

### **Q8.** Why is monotonic stack O(n) instead of O(n²)?

**Your answer:** _______________

**Hint:** How many times can each element be pushed/popped?

**Answer:**

Each element pushed exactly once: n operations
Each element popped at most once: n operations
Total: 2n operations = O(n)

Not O(n²) because we don't compare to every other element. Stack maintains monotonicity as invariant.

---

### **Q9.** Trace next greater element on [1, 3, 2, 4]

**Your answer:** _______________

**Hint:** Track stack contents at each step

**Answer:**

```
i=0 (1): stack=[], push 0, stack=[0]
i=1 (3): arr[0]=1<3, pop 0→result[0]=3, push 1, stack=[1]
i=2 (2): arr[1]=3>2, push 2, stack=[1,2]
i=3 (4): arr[2]=2<4, pop 2→result[2]=4
         arr[1]=3<4, pop 1→result[1]=4, push 3, stack=[3]

Result: [3, 4, 4, -1]
```

---

### **Q10.** What's the difference between increasing and decreasing stack?

**Your answer:** _______________

**Hint:** Which pops when new element arrives?

**Answer:**

Increasing stack: Pop when arr[i] > arr[top] (finds next greater)
Decreasing stack: Pop when arr[i] < arr[top] (finds next smaller)

Same logic, opposite direction. Choose based on problem requirement.

---

### **Q11.** Why does popped element always find correct answer?

**Your answer:** _______________

**Hint:** What property is maintained by stack monotonicity?

**Answer:**

When element popped by current element:
- All elements between them were checked
- First one larger/smaller is guaranteed (due to monotonicity)
- So answer is definitely current element
- No need to look further right

---

### **Q12.** How to find PREVIOUS greater instead of NEXT?

**Your answer:** _______________

**Hint:** Change direction of iteration

**Answer:**

Process array right-to-left instead of left-to-right. Same monotonic stack logic, opposite direction. Finds previous greater/smaller instead.

---

### **Q13.** What problems use monotonic stack?

**Your answer:** _______________

**Hint:** Think about "next/previous" patterns

**Answer:**

- Next/previous greater or smaller element
- Trapping rain water
- Largest rectangle in histogram
- Daily temperatures
- Stock span
- Remove K digits
- Build array from permutation

---

### **Q14.** What happens to elements remaining in stack after iteration?

**Your answer:** _______________

**Hint:** If iteration complete and element still in stack...

**Answer:**

Remaining elements have no answer (no greater/smaller element to their right). Set their result to -1 (or specified default).

---

## DAY 3: MERGE OPERATIONS QUESTIONS

### **Q15.** Why is merge O(n+m) instead of O((n+m) log(n+m))?

**Your answer:** _______________

**Hint:** What property allows faster than sort?

**Answer:**

Because arrays already sorted! No sorting needed. Just one pass comparing front elements. Sorting adds log(n+m) factor. Merge uses pre-sorted property for O(n+m).

---

### **Q16.** Trace merge of [1, 5, 9] and [2, 3, 8, 13]

**Your answer:** _______________

**Hint:** Compare front elements, move smaller

**Answer:**

```
1 vs 2 → 1, result=[1]
5 vs 2 → 2, result=[1,2]
5 vs 3 → 3, result=[1,2,3]
5 vs 8 → 5, result=[1,2,3,5]
9 vs 8 → 8, result=[1,2,3,5,8]
9 vs 13 → 9, result=[1,2,3,5,8,9]
[13] → result=[1,2,3,5,8,9,13]
```

---

### **Q17.** What happens when one array is exhausted?

**Your answer:** _______________

**Hint:** Are remaining elements already sorted?

**Answer:**

Yes! Remaining elements in non-empty array are all ≥ all previously merged elements. Simply append them directly to result.

---

### **Q18.** How to do in-place merge?

**Your answer:** _______________

**Hint:** Work from right-to-left instead

**Answer:**

Start from end of both arrays. Compare and place larger element at end of combined array. Move pointers left. Handles overflow naturally.

---

### **Q19.** When is merge necessary vs concatenate+sort?

**Your answer:** _______________

**Hint:** Compare O(n+m) vs O((n+m) log(n+m))

**Answer:**

Merge for large arrays where pre-sorted is given. Concatenate+sort for small arrays or when not pre-sorted. For 1000 items each, merge is ~100x faster.

---

### **Q20.** What about merging 3+ arrays?

**Your answer:** _______________

**Hint:** Can extend pairwise or use different structure?

**Answer:**

Recursively merge pairs: merge(A,B) then result with C.
Or use heap for k arrays: O((sum) log k) complexity.
Or use merge sort for k lists simultaneously.

---

### **Q21.** What's relationship between merge and merge sort?

**Your answer:** _______________

**Hint:** How does merge sort work?

**Answer:**

Merge sort uses merge as combining step. Divides array in half, recursively sorts each half, then merges. Merge is O(n) part, division/sorting is O(log n) parts.

---

## DAY 4: PARTITION & KADANE'S QUESTIONS

### **Q22.** How does partition segregate elements in-place?

**Your answer:** _______________

**Hint:** Use write pointer tracking

**Answer:**

Write pointer tracks position for valid elements. Read pointer scans array. When valid element found, swap to write position and advance write. Non-valid elements skip.

---

### **Q23.** Trace move zeroes on [0, 1, 0, 3, 12]

**Your answer:** _______________

**Hint:** Track write pointer position

**Answer:**

```
read=0 (0): skip
read=1 (1): swap to write[0]→[1,0,0,3,12], write=1
read=2 (0): skip
read=3 (3): swap to write[1]→[1,3,0,0,12], write=2
read=4 (12): swap to write[2]→[1,3,12,0,0], write=3
Result: [1,3,12,0,0]
```

---

### **Q24.** What's Dutch National Flag?

**Your answer:** _______________

**Hint:** Partition into 3 groups (0s, 1s, 2s)

**Answer:**

3-way partition using low, mid, high pointers. Maintains three regions: 0s (0..low), 1s (low..mid), 2s (mid..high). Swap mid element to appropriate region.

---

### **Q25.** How does Kadane's algorithm work?

**Your answer:** _______________

**Hint:** Decision at each position: extend or restart?

**Answer:**

At each position, decide: extend previous sum or start fresh?
- current_max = max(arr[i], current_max + arr[i])
- Track global maximum
- O(n) single pass instead of O(n²) brute force

---

### **Q26.** When do you extend vs restart in Kadane's?

**Your answer:** _______________

**Hint:** When is current value > previous sum + value?

**Answer:**

Extend if: previous_sum + current ≥ current
Restart if: previous_sum + current < current

Essentially: Is the previous sum helpful? If yes, extend. If no, start fresh.

---

### **Q27.** Why Kadane's O(n) vs O(n²) naive?

**Your answer:** _______________

**Hint:** Compare checking all subarrays vs DP decision

**Answer:**

Naive: Check all O(n²) subarrays, calculate sum for each
Kadane: Dynamic decision at each position, single pass, O(n)

1000x speedup for 1000 elements!

---

### **Q28.** Can you find subarray indices with Kadane's?

**Your answer:** _______________

**Hint:** Track temp_start and when max updates

**Answer:**

Yes! Track:
- temp_start: potential start of current subarray
- start, end: actual maximum subarray indices
- When global_max updates, record current indices

Return max_sum and indices.

---

## REFERENCE ANSWERS QUICK CHECK

| Q | Answer | Key Point |
|---|--------|-----------|
| 1 | Collisions | Hash function uniformity |
| 2 | Find on step 4 | Duplicate detected |
| 3 | freq.get(char,0)+1 | Dictionary update |
| 4 | Order doesn't matter | Use case determines |
| 5 | O(n) space for O(1) | Space-time tradeoff |
| 6 | Chaining | Linked list in bucket |
| 7 | Need ordered | Alternative structures |
| 8 | 2n operations | Amortized O(n) |
| 9 | Result = [3,4,4,-1] | Stack trace |
| 10 | Opposite logic | Next vs previous |
| 11 | Monotonicity guarantee | Stack invariant |
| 12 | Right-to-left | Direction change |
| 13 | Next greater, etc | Pattern matching |
| 14 | No answer, -1 | Remaining elements |
| 15 | Pre-sorted | O(n+m) vs sort |
| 16 | Result shown | Two pointer merge |
| 17 | Append directly | Already sorted |
| 18 | Right-to-left | In-place strategy |
| 19 | 100x faster | Size dependent |
| 20 | Recursive or heap | K-way merge |
| 21 | Combining step | Merge sort basis |
| 22 | Write pointer | Segregation |
| 23 | Result shown | Partition trace |
| 24 | 3-region partition | Dutch flag |
| 25 | DP decision | Current max concept |
| 26 | Extend if helpful | Greedy decision |
| 27 | O(n) vs brute force | 1000x speedup |
| 28 | Track indices | Extended Kadane |

---

## SCORING GUIDE

### **Per Day:**
- 7 correct: Mastered ✅
- 6 correct: Strong 👍
- 5 correct: Solid 🟡
- <5 correct: Review 🔴

### **Week 4.5 Total (28 Questions):**
- 26-28: Expert 🏆
- 24-25: Very Good ⭐
- 22-23: Good ✅
- 20-21: Adequate 🟡
- <20: Review Needed 🔴

---

**Status:** Ready for daily self-assessment | **Next:** Check after each day!

