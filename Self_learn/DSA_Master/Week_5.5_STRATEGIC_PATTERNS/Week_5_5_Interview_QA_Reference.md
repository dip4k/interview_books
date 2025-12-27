# Week 5.5: Interview Q&A Reference

## 🎯 Difference Array — 5 Q&A Pairs

**Q1: Why only modify two positions (L and R+1) for range update [L,R]?**
A: Mark start (increase at L) and boundary (decrease at R+1). Prefix sum reconstruction automatically fills range.

**Q2: What happens if you query values in difference array before reconstructing?**
A: You get difference values, not final values. Example: diff=[5,0,0,-5] looks wrong, but cumsum=[5,5,5,0] correct.

**Q3: Can you apply negative value updates (subtract from range)?**
A: Yes. diff[L] -= value, diff[R+1] += value. Cumulative sum handles it correctly.

**Q4: How does it handle overlapping ranges?**
A: Perfectly. Overlapping updates accumulate via cumulative sum. Example: +5 and +3 to overlapping ranges sum to +8 in overlap.

**Q5: When should you use difference array vs segment tree?**
A: Difference array: batch range updates, one reconstruction. Segment tree: mixed updates + queries. Different trade-offs.

---

## 🎯 In-Place Replacement — 5 Q&A Pairs

**Q1: Why must read pointer (i) always be >= write pointer (j)?**
A: Ensures no valid data overwritten. Data written to position j is never read again after writing.

**Q2: What does the return value (j) represent?**
A: New length of valid elements. Array is modified in-place, only elements [0...j) are valid. Trailing garbage ignored.

**Q3: Can this technique work on unordered arrays?**
A: Yes, but need preprocessing. Sorted: direct two-pointer. Unordered: two-pass or sort first.

**Q4: Why do interviews strongly prefer in-place solutions?**
A: O(1) space is gold standard. Demonstrates pointer mastery and shows algorithmic thinking, not just brute force.

**Q5: How do you handle multiple removal conditions (remove type A AND type B)?**
A: Single two-pointer pass. Condition checks both: if !(isA || isB), then write. All removals in one pass.

---

## 🎯 Deque Operations — 5+ Q&A Pairs

**Q1: Why store indices in deque instead of values?**
A: Need to check window membership. Value alone doesn't tell if element is inside or outside current window. Index needed.

**Q2: Why remove smaller values from back when adding new element?**
A: Smaller values will never be max in current or future windows. Larger value will always block them. Optimize by removing.

**Q3: How can nested while loops be O(n) when there's a while loop inside the for loop?**
A: Each element pushed to deque exactly once, popped at most once. Total: n pushes + n pops = O(n) despite nested structure.

**Q4: Can you use a regular queue instead of deque?**
A: No. Need both remove-from-front (expired indices) and remove-from-back (smaller values) operations. Only deque provides both.

**Q5: What if array contains duplicates?**
A: Deque property still holds. Handle == in comparison: pop equal values or keep first. Depends on problem requirements.

**Q6: Why is front of deque always the maximum of current window?**
A: Deque maintains decreasing order. Front = largest. When new element arrives, smaller are removed. Front remains maximum.

---

## 🔗 Cross-Pattern Questions

**Q: When do you use Difference Array vs In-Place vs Deque?**
A: 
- Difference Array: Range updates on same array (add to ranges)
- In-Place: Modify array while removing elements
- Deque: Find max/min in sliding windows

**Q: Can you combine patterns?**
A: Yes. Example: Range update differences + deque for sliding max = complex optimization.

**Q: Are Tier 2 patterns sufficient for all hard problems?**
A: No. They cover 80-88%. Combined with Tier 1 (70-80%), weeks 1-4 (40-50%). Hard problems combine multiple patterns.

---

## ✅ Interview Readiness Check

After Week 5.5, confidently answer:
- [ ] 5 difference array questions
- [ ] 5 in-place questions
- [ ] 6 deque questions

**Total: 16 Q&A pairs mastered**

**If 90%+ confident → Ready for Week 6**

