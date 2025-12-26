# Week 4: Q&A - 50 Socratic Questions with Detailed Answers

**10 Questions per Day × 5 Days = 50 Total Questions**

---

## 📅 DAY 1: TWO POINTERS (10 Questions)

### Q1.1: Why does two pointers only work on SORTED arrays?

**Difficulty:** ⭐ Easy

**Answer:**
Two pointers rely on monotonicity: moving left increases value, moving right decreases it. On unsorted arrays, moving a pointer doesn't guarantee moving toward the target. Example: [5,2,8,1,3], left might point to 5, but moving right goes to 2 (smaller!). The algorithm needs to know moving right direction → target.

---

### Q1.2: Why is two pointers O(n) and not O(n²)?

**Difficulty:** ⭐ Easy

**Answer:**
Each pointer moves at most n times total. Left moves from 0→n-1 (n moves). Right moves from n-1→0 (n moves). Total: 2n = O(n). Contrast: nested loops touch each pair separately.

---

### Q1.3: Trace two sum on [1,2,3,4,5], target=7

**Difficulty:** ⭐ Medium

**Answer:**
```
left=0(1), right=4(5): 1+5=6 < 7 → left=1
left=1(2), right=4(5): 2+5=7 == 7 → FOUND (1,4) ✓
```

---

### Q1.4: Why move the pointer with smaller value in container problem?

**Difficulty:** ⭐⭐ Medium

**Answer:**
The limiting factor is the smaller height. Moving the taller pointer loses width without gaining height (already limited by shorter). Moving shorter pointer might find taller element. Greedy choice: maximize potential.

---

### Q1.5: Can you apply two pointers to linked lists?

**Difficulty:** ⭐⭐ Medium

**Answer:**
Yes! Two pointers become node references. Example: detect cycle, find middle, remove kth from end. Can't index, but can traverse. Used extensively in linked list problems.

---

### Q1.6: Why does valid palindrome need character filtering?

**Difficulty:** ⭐⭐ Medium

**Answer:**
Palindrome definition: ignoring non-alphanumeric. "A man, a plan, a canal: Panama" → "amanaplanacanalpanama" (palindrome). Need to skip spaces/punctuation while comparing.

---

### Q1.7: What happens if you forget to sort before two pointers?

**Difficulty:** ⭐⭐ Medium

**Answer:**
Algorithm breaks. Moving right doesn't guarantee smaller values. Might miss solutions or give wrong answer. Example: [5,2,8,1,3] target=6, two pointers might fail.

---

### Q1.8: How do you handle duplicates in two sum?

**Difficulty:** ⭐⭐ Medium

**Answer:**
Just find one pair; duplicates are different pairs by index. If need unique pairs: skip after finding (less common).

---

### Q1.9: Compare two pointers vs binary search for two sum

**Difficulty:** ⭐⭐ Medium

**Answer:**
Two pointers: O(n) time, O(1) space. Binary search: O(n log n) time (for each element, binary search rest), O(1) space. Two pointers faster!

---

### Q1.10: Can you solve two sum without sorting?

**Difficulty:** ⭐⭐ Medium

**Answer:**
Yes! Use hash table: O(n) time, O(n) space. Trade space for avoiding sort. When array is already sorted: two pointers better.

---

## 📅 DAY 2: SLIDING WINDOW (10 Questions)

### Q2.1: Why is sliding window O(n) even with while loop inside?

**Difficulty:** ⭐ Easy

**Answer:**
Left pointer moves at most n times TOTAL (not per right pointer movement). So while loop across all iterations processes n total shrinks. Total work: n expands + n shrinks = O(n).

---

### Q2.2: Why must metric be "incrementally updatable"?

**Difficulty:** ⭐ Easy

**Answer:**
Need to compute new metric from old metric in O(1). Sum works (subtract old, add new). Max/min don't (need to reconsider all elements). Frequency count works (decrement count).

---

### Q2.3: Can you use sliding window on unsorted arrays?

**Difficulty:** ⭐ Easy

**Answer:**
Yes! Unlike two pointers. Sliding window doesn't rely on sorting. Only relies on ability to incrementally update metric. Works on unsorted, partially sorted, or sorted data.

---

### Q2.4: Trace longest substring unique on "abcabcbb"

**Difficulty:** ⭐⭐ Medium

**Answer:**
```
right=0 (a): char_count={a:1}, len=1
right=1 (b): char_count={a:1,b:1}, len=2
right=2 (c): char_count={a:1,b:1,c:1}, len=3
right=3 (a): char_count={a:2,b:1,c:1}, shrink:
  left=0 (a): char_count={a:1,b:1,c:1}, left=1, len=3
right=4 (b): char_count={a:1,b:2,c:1}, shrink:
  left=1 (b): char_count={a:1,b:1,c:1}, left=2, len=3
... max_len = 3
```

---

### Q2.5: How do you handle two distinct conditions in sliding window?

**Difficulty:** ⭐⭐ Medium

**Answer:**
Track both metrics. Expand when both satisfied. Shrink when either violated. Example: "at most 2 distinct characters AND all characters appear ≥ 1 time" - track both conditions.

---

### Q2.6: Can sliding window solve max/min in window?

**Difficulty:** ⭐⭐ Medium

**Answer:**
Not efficiently with basic sliding window. Max/min requires segment tree or deque. Sliding window requires O(1) incremental update.

---

### Q2.7: What if window becomes empty during shrinking?

**Difficulty:** ⭐⭐ Medium

**Answer:**
It's fine! Just means current position doesn't satisfy condition. Keep moving right. Example: unique characters, if character repeats, shrink until unique again (may result in single char window).

---

### Q2.8: How to implement "at most k distinct characters"?

**Difficulty:** ⭐⭐ Medium

**Answer:**
```
char_count = {}
for right:
    char_count[s[right]] += 1
    
    while len(char_count) > k:
        char_count[s[left]] -= 1
        if char_count[s[left]] == 0:
            del char_count[s[left]]
        left += 1
    
    max_len = max(max_len, right - left + 1)
```

---

### Q2.9: Minimum window substring: what's special?

**Difficulty:** ⭐⭐ Medium

**Answer:**
Must track frequency of required characters. Shrink while still valid (all required chars present with required count). Update best window during shrinking phase.

---

### Q2.10: When would fixed-size window be better?

**Difficulty:** ⭐⭐ Medium

**Answer:**
When window size is fixed! Example: "average of all subarrays of size 5". Much simpler: just subtract leftmost, add new rightmost each step.

---

## 📅 DAY 3: PREFIX SUMS (10 Questions)

### Q3.1: Why is building prefix O(n) not O(n²)?

**Difficulty:** ⭐ Easy

**Answer:**
Each element processed once: prefix[i] = prefix[i-1] + arr[i]. No nested loops. Single pass through array.

---

### Q3.2: Why is query O(1) and not O(n)?

**Difficulty:** ⭐ Easy

**Answer:**
Query is just arithmetic: prefix[right+1] - prefix[left]. Constant time regardless of range size.

---

### Q3.3: What's the formula for range sum [left, right]?

**Difficulty:** ⭐ Easy

**Answer:**
sum = prefix[right+1] - prefix[left]

Why +1 on right? Because prefix[i] = sum of elements [0, i-1]. So prefix[right+1] includes element at right.

---

### Q3.4: Trace prefix sum on [3, 2, 5, 1, 4]

**Difficulty:** ⭐ Easy

**Answer:**
```
arr:    [3, 2, 5, 1, 4]
prefix: [0, 3, 5, 10, 11, 15]

Query sum(1,3) = prefix[4] - prefix[1] = 11 - 3 = 8 ✓ (2+5+1)
```

---

### Q3.5: How does product of array except self work?

**Difficulty:** ⭐⭐ Medium

**Answer:**
Result[i] = product of all left × product of all right.

Pass 1: result[i] = product of [0, i-1]
Pass 2: result[i] *= product of [i+1, n-1]

Two passes, no division!

---

### Q3.6: Why use prefix sums if single query doesn't need it?

**Difficulty:** ⭐ Easy

**Answer:**
Unnecessary overhead. Single query: O(n) direct better than O(n) preprocessing + O(1) query. Multiple queries: amortized O(1) per query wins.

---

### Q3.7: What's the 2D prefix sum formula?

**Difficulty:** ⭐⭐ Medium

**Answer:**
```
prefix[i][j] = prefix[i-1][j] + prefix[i][j-1] 
             - prefix[i-1][j-1] + matrix[i-1][j-1]

Query sum(r1,c1 to r2,c2) = prefix[r2+1][c2+1] - prefix[r1][c2+1]
                           - prefix[r2+1][c1] + prefix[r1][c1]
```

Why subtract overlap? Inclusion-exclusion principle.

---

### Q3.8: Can you update array with prefix sums?

**Difficulty:** ⭐ Medium

**Answer:**
No efficiently. Updating one element requires rebuilding entire prefix (O(n)). Use segment tree for updates.

---

### Q3.9: Prefix sums vs segment tree: when use each?

**Difficulty:** ⭐⭐ Medium

**Answer:**
Prefix: static array, multiple queries. Segment: dynamic array, frequent updates. Prefix simpler, segment more powerful.

---

### Q3.10: How to generalize to 3D range sums?

**Difficulty:** ⭐⭐ Hard

**Answer:**
Extend inclusion-exclusion to 3D. prefix[i][j][k] includes + excludes 7 overlaps (2³-1). Formula gets complex but follows same pattern. O(n³) space, O(1) query.

---

## 📅 DAY 4: ADVANCED TWO POINTERS (10 Questions)

### Q4.1: How does 3Sum reduce to multiple 2Sum problems?

**Difficulty:** ⭐ Medium

**Answer:**
Fix one element arr[i]. Then find two numbers in rest that sum to (target - arr[i]). Use two pointers on rest. Do this for each i.

---

### Q4.2: Why sort array first for 3Sum?

**Difficulty:** ⭐ Easy

**Answer:**
Two pointers on rest require sorted data. Plus, sorting helps skip duplicates more easily.

---

### Q4.3: Trace 3Sum on [-1, 0, 1, 2, -1, -4], target=0

**Difficulty:** ⭐⭐ Medium

**Answer:**
```
Sorted: [-4, -1, -1, 0, 1, 2]

i=0 (-4): need sum 4, two pointers find none
i=1 (-1): need sum 1, find (-1, 2) ✓, skip duplicates
i=2 (-1): skip (duplicate)
i=3 (0): need sum 0, find (0, 1)? No, skip
Result: [[-1, -1, 2], [-1, 0, 1]]
```

---

### Q4.4: Why must you skip duplicates in 3Sum?

**Difficulty:** ⭐ Medium

**Answer:**
Without skipping, same triplet returned multiple times. Example: [-1, -1, 2] appears at different indices but is same triplet. Skip arr[i] == arr[i-1] and after finding triplet, skip duplicate pointers.

---

### Q4.5: What's 4Sum time complexity?

**Difficulty:** ⭐ Easy

**Answer:**
O(n³). Two nested fixed loops (O(n²)), two pointers on rest (O(n)). Total O(n³).

---

### Q4.6: Can you extend to 5Sum?

**Difficulty:** ⭐⭐ Medium

**Answer:**
Technically yes, O(n⁴). But becomes impractical. Most interviews: 3Sum, maybe 4Sum. For larger k: different approach needed.

---

### Q4.7: How to handle negative target in 3Sum?

**Difficulty:** ⭐ Easy

**Answer:**
Sorting handles negatives. Rest of algorithm identical. Negatives are just smaller values.

---

### Q4.8: What if array is very large with 3Sum?

**Difficulty:** ⭐⭐ Medium

**Answer:**
O(n²) might be slow (1T operations for n=1M). Hash table alternative: O(n) space, O(n²) time without sort. Trade space for no sorting overhead.

---

### Q4.9: Is 3Sum on unsorted array possible?

**Difficulty:** ⭐⭐ Medium

**Answer:**
Yes! Use hash table approach. For each pair, check if complement exists. O(n²) time, O(n) space. Skip sorting overhead, pay space cost.

---

### Q4.10: Closest 3Sum: how to adapt?

**Difficulty:** ⭐⭐ Hard

**Answer:**
Instead of checking == target, track closest sum. When sum < target, move left (try larger). When sum > target, move right (try smaller). Update closest at each step.

---

## 📅 DAY 5: INTEGRATION (10 Questions)

### Q5.1: When would you choose O(n) space over O(1)?

**Difficulty:** ⭐ Medium

**Answer:**
When readability/simplicity matters more than space. Prefix array approach (O(n) space) simpler to understand than two-pointer tracking. Interview: often both are acceptable.

---

### Q5.2: How do you combine prefix sums with two pointers?

**Difficulty:** ⭐⭐ Medium

**Answer:**
Precompute prefix, then use two pointers on prefix array (searching for property). Example: find subarray with sum > k.

---

### Q5.3: Can sliding window replace two pointers?

**Difficulty:** ⭐⭐ Medium

**Answer:**
Sometimes! Both are O(n). Two pointers needs sorted. Sliding window doesn't. So unsorted array? Sliding window. Sorted? Either, but two pointers simpler conceptually for pairs.

---

### Q5.4: Trapping rain water: what makes it complex?

**Difficulty:** ⭐⭐ Medium

**Answer:**
Need to consider both left and right context. Naive: for each position, find max left and max right separately (O(n²)). Optimization: precompute (O(n) space) or track dynamically (O(1) space with two pointers).

---

### Q5.5: Two-pointer vs prefix for trapping rain?

**Difficulty:** ⭐⭐ Medium

**Answer:**
Two pointers: O(n) time, O(1) space, harder to understand.
Prefix: O(n) time, O(n) space, easier to understand.
Choose based on constraint: space critical → two pointers. Clarity important → prefix.

---

### Q5.6: How to solve "contains duplicate in range k"?

**Difficulty:** ⭐⭐ Medium

**Answer:**
Sliding window! Keep window of size k, check for duplicates using hash set. If duplicate found in window, return True. If window size exceeds k without duplicates, shrink.

---

### Q5.7: Max subarray sum vs 3Sum: why different techniques?

**Difficulty:** ⭐⭐ Medium

**Answer:**
Max subarray sum: contiguous, maximize value → Kadane/sliding window.
3Sum: non-contiguous triplets → advanced two pointers (sort + nested).
Different goals → different techniques.

---

### Q5.8: Can you solve all week 4 problems with one technique?

**Difficulty:** ⭐⭐ Hard

**Answer:**
No. Each problem has constraints. Two pointers for sorted pairs. Sliding window for subarray properties. Prefix for range queries. Advanced TP for multiple targets. Integration is knowing which to use.

---

### Q5.9: Longest subarray with sum ≤ k: what approach?

**Difficulty:** ⭐⭐ Medium

**Answer:**
Sliding window! Expand right to add elements. When sum > k, shrink from left. Track max window size. Works on unsorted array.

---

### Q5.10: How to prepare for week 4 interview questions?

**Difficulty:** ⭐ Easy

**Answer:**
1. Master each technique individually
2. Solve 20+ problems per technique
3. Practice recognizing technique from problem statement
4. Code without hints, test edge cases
5. Explain approach before coding
6. Know trade-offs and alternatives

---

## 📋 Self-Assessment

**After answering all 50 questions:**

- [ ] Confidence 1-2/5: Review relevant sections deeply
- [ ] Confidence 3/5: Understand concepts, gaps remain
- [ ] Confidence 4/5: Good understanding, minor gaps
- [ ] Confidence 5/5: Mastered all topics ✓ Ready for Week 5!

---

**Total Questions:** 50  
**Estimated Time:** 5-6 hours to work through thoroughly  
**Success Criteria:** Confident answers to 80%+ of questions

