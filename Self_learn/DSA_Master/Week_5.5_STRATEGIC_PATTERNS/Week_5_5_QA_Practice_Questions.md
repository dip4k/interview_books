# Week 5.5: Q&A Practice Questions (12 Per Day)

**Total Questions:** 60 (12 × 5 days)  
**Difficulty Range:** ⭐ Easy to ⭐⭐⭐ Hard  

---

## 📍 DAY 1: DIFFERENCE ARRAY (12 Questions)

**Q1 ⭐:** What's the inverse of prefix sum?  
A: Difference array. Where prefix sum is cumulative, diff array stores consecutive differences.

**Q2 ⭐:** Why use size n+1 for diff array?  
A: To safely mark right+1 boundary without index out of bounds.

**Q3 ⭐:** What does diff[left]+=val, diff[right+1]-=val do?  
A: Marks start of range (+val effect) and end of range (-val cancellation).

**Q4 ⭐⭐:** Given updates: [1,3,5] and [2,4,3], what's diff array?  
A: diff[1]+=5, diff[4]-=5, diff[2]+=3, diff[5]-=3 → [0, 5, 3, 0, -5, -3]

**Q5 ⭐⭐:** How do you reconstruct final array from diff?  
A: Compute prefix sum: arr[i] = sum(diff[0..i])

**Q6 ⭐⭐:** Time complexity: m updates, n array size?  
A: O(m + n). Updates O(1) each, reconstruction O(n).

**Q7 ⭐⭐:** Can overlapping ranges interfere?  
A: No. Each range mark independently accumulated in reconstruction.

**Q8 ⭐⭐:** What if you forget diff[right+1]-=val?  
A: Range effect extends beyond right, wrong results.

**Q9 ⭐⭐⭐:** Can you use diff for multiplicative updates (*2)?  
A: No directly. Difference tracks additive changes only.

**Q10 ⭐⭐⭐:** Design: range updates + range query max. How?  
A: Diff array for updates, reconstruct once, then scan for range max.

**Q11 ⭐⭐⭐:** Prove: marking boundaries correctly handles overlaps.  
A: Overlapping ranges each contribute their value; accumulated correctly.

**Q12 ⭐⭐⭐:** Compare with: naive O(m×k) vs diff O(m+n).  
A: For k large, diff array saves orders of magnitude.

---

## 📍 DAY 2: IN-PLACE REPLACEMENT (12 Questions)

**Q1 ⭐:** What does "in-place" mean?  
A: Modify array without creating new array, O(1) extra space.

**Q2 ⭐:** Why use two pointers (i, j)?  
A: i reads, j writes. i > j ensures safe overwriting.

**Q3 ⭐:** When does i > j matter?  
A: When we write arr[j], we haven't read arr[j] yet (since i > j).

**Q4 ⭐:** Remove all 2s from [1,2,3,2,4]. Trace.  
A: i scans, j marks valid position. Final: [1,3,4], return j=3.

**Q5 ⭐⭐:** Why initialize j=0, not j=1?  
A: For sorted duplicates, check if first element is valid. For remove element, always start from 0.

**Q6 ⭐⭐:** What's returned: the array or a number?  
A: Return j (new length). Array modified in-place.

**Q7 ⭐⭐:** Can i ever catch up to j (i == j)?  
A: Yes, when all elements are valid (none removed).

**Q8 ⭐⭐:** Remove duplicates from [1,1,2,2,3]. Trace.  
A: Compare arr[i] to arr[i-1]. Move forward j when different.

**Q9 ⭐⭐⭐:** What happens if i <= j?  
A: Read-write collision. Would overwrite unread data.

**Q10 ⭐⭐⭐:** Design: remove elements AND update remaining. How?  
A: In-place first, reduce array logically, then apply other technique.

**Q11 ⭐⭐⭐:** For string removal (vowels), what changes?  
A: Convert to list, same two-pointer logic, convert back.

**Q12 ⭐⭐⭐:** Space comparison: O(n) array vs O(1) in-place.  
A: For 1B elements: 4GB saved. Huge for memory-constrained systems.

---

## 📍 DAY 3: DEQUE SLIDING WINDOW (12 Questions)

**Q1 ⭐:** What's monotonic deque?  
A: Deque storing indices in decreasing order of their values.

**Q2 ⭐:** Why store indices, not values?  
A: Need to check if index is outside window.

**Q3 ⭐:** What's at dq[0]?  
A: Index of maximum value in current window.

**Q4 ⭐:** Why remove arr[dq[-1]] < arr[i]?  
A: Those elements can never be max while current element exists.

**Q5 ⭐⭐:** Sliding max for [1,3,1,2,0,5], k=3. Trace.  
A: dq tracks indices: [1], [1,2], [1], [3], [5] → results [3,3,2,5].

**Q6 ⭐⭐:** What's the window boundary check?  
A: if dq[0] < i - k + 1: remove oldest.

**Q7 ⭐⭐:** Can deque ever be empty during window?  
A: No, always has current element. Empty only before window ready.

**Q8 ⭐⭐:** For minimum instead of maximum, what changes?  
A: Change < to > in the comparison. Same structure.

**Q9 ⭐⭐⭐:** Why dq[0] always points to max?  
A: Monotonic property + removal of smaller elements guarantee it.

**Q10 ⭐⭐⭐:** Compare heap (O(n log n)) vs deque (O(n)).  
A: Deque uses monotonic property; heap requires binary search.

**Q11 ⭐⭐⭐:** Design: sliding window max on filtered array.  
A: Filter first (in-place), then apply deque on filtered elements.

**Q12 ⭐⭐⭐:** Prove each element enters/leaves deque once.  
A: Each enters when i reaches it, leaves when outside window. O(n) total.

---

## 📍 DAY 4: ADVANCED COMBINATIONS (12 Questions)

**Q1 ⭐:** When combine multiple techniques?  
A: When problem has 2+ distinct operations (updates + queries).

**Q2 ⭐:** Order of techniques matters?  
A: Usually yes: updates → reconstruction → queries.

**Q3 ⭐:** Combine diff array + deque: how?  
A: Diff array for updates, reconstruct, apply deque for window queries.

**Q4 ⭐⭐:** Problem: range updates + range max query. Solution?  
A: Diff array (O(1) per update), reconstruct (O(n)), scan range for max.

**Q5 ⭐⭐:** Problem: filter array + sliding window. How?  
A: In-place filter first, then deque on filtered elements.

**Q6 ⭐⭐:** Can you apply deque before diff array?  
A: No. Deque needs final array values, diff array produces them.

**Q7 ⭐⭐:** Combining in-place + diff array: when needed?  
A: When removing elements changes indices for later operations.

**Q8 ⭐⭐⭐:** Hotel problem: bookings, cancellations, peak period.  
A: Track bookings (diff), track cancellations (diff), combine, reconstruct.

**Q9 ⭐⭐⭐:** When combining 3 techniques, what's pitfall?  
A: Order wrong, or forgetting to reconstruct between stages.

**Q10 ⭐⭐⭐:** Complexity of combined solution?  
A: Sum of each part: O(m) + O(n) + O(k) for updates + reconstruction + queries.

**Q11 ⭐⭐⭐:** Design: range updates + in-place removal + window max.  
A: Reconstruct from diff, filter in-place, apply deque.

**Q12 ⭐⭐⭐:** Most common combination in interviews?  
A: Diff array + reconstruction + linear query. Simple but effective.

---

## 📍 DAY 5: INTEGRATION & MASTERY (12 Questions)

**Q1 ⭐:** Which technique for "range update"?  
A: Difference array.

**Q2 ⭐:** Which technique for "O(1) space"?  
A: In-place replacement.

**Q3 ⭐:** Which technique for "sliding window max"?  
A: Deque monotonic.

**Q4 ⭐⭐:** Problem: "Update ranges, find max after". Approach?  
A: Identify: diff (updates), query (find max). Combine.

**Q5 ⭐⭐:** How do you recognize when techniques combine?  
A: Look for keywords from multiple techniques.

**Q6 ⭐⭐:** Complexity of: 10M updates, 1B elements, 1M queries?  
A: Diff: O(10M) + reconstruct: O(1B) + query: O(1B) = O(1.01B).

**Q7 ⭐⭐⭐:** What's the master skill of Week 5.5?  
A: Pattern recognition. Identifying which technique(s) apply.

**Q8 ⭐⭐⭐:** Your strongest technique?  
A: (Personal reflection)

**Q9 ⭐⭐⭐:** Your weakest technique?  
A: (Personal reflection) Focus on this next.

**Q10 ⭐⭐⭐:** Can you solve hard problems mixing all 3?  
A: (Test yourself on hardest problem)

**Q11 ⭐⭐⭐:** Interview mock: solve in 30 minutes?  
A: (Time yourself)

**Q12 ⭐⭐⭐:** Ready for Week 6?  
A: Check readiness against criteria.

---

## 📊 SELF-ASSESSMENT SCORING

- **50-60 correct:** Master level (proceed to Week 6)
- **45-49 correct:** Advanced level (ready but review weak areas)
- **40-44 correct:** Solid level (practice more before Week 6)
- **<40 correct:** Review needed (extend current week)

---

**Q&A Version:** 1.0 Week 5.5 Complete  
**Total Questions:** 60  
**Target Accuracy:** 80%+

