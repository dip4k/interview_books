# Week 5.5: Daily Progress Checklist & Interview Q&A

## ✅ DAY 1: Difference Array

### Morning Objectives
- [ ] Understand range update problem (O(n×k) naive)
- [ ] Know boundary marking concept (L, R+1)
- [ ] Understand reconstruction (prefix sum)
- [ ] Why O(n+k) is better than O(n×k)

### Core Learning
- [ ] Read: Week_5_5_Day_1_Difference_Array_Instructional.md
- [ ] Trace: Apply 3+ range updates to array
- [ ] Trace: Reconstruct array from difference array
- [ ] Understand: When to reconstruct (once vs repeatedly)

### Practice Problems
- [ ] Range Addition
- [ ] Hotel Bookings II
- [ ] Difference Array Queries
- [ ] Shift Queries

**Confidence Rating**: ___ / 5

---

## ✅ DAY 2: In-Place Replacement

### Morning Objectives
- [ ] Understand two-pointer technique
- [ ] Know why O(1) space possible
- [ ] Understand when to write vs skip
- [ ] Know interview preference (space optimization)

### Core Learning
- [ ] Read: Week_5_5_Day_2_In_Place_Replacement_Instructional.md
- [ ] Trace: Remove duplicates step-by-step
- [ ] Trace: Remove specific value
- [ ] Understand: Trailing elements irrelevant

### Practice Problems
- [ ] Remove Duplicates from Sorted Array
- [ ] Remove Element
- [ ] Move Zeroes to End
- [ ] Remove Vowels from String

**Confidence Rating**: ___ / 5

---

## ✅ DAY 3: Deque Operations

### Morning Objectives
- [ ] Understand sliding window problem
- [ ] Know monotonic deque concept
- [ ] Understand why O(n) (each element processed twice)
- [ ] Know deque stores indices, not values

### Core Learning
- [ ] Read: Week_5_5_Day_3_Deque_Operations_Instructional.md
- [ ] Trace: Sliding window max detailed example
- [ ] Understand: Remove expired, remove smaller, add current
- [ ] Know: Front always = max of current window

### Practice Problems
- [ ] Sliding Window Maximum
- [ ] Sliding Window Minimum
- [ ] First Negative Integer in Every Window
- [ ] Building a Bigger Window

**Confidence Rating**: ___ / 5

---

## 🎯 INTERVIEW Q&A REFERENCE (15+ Pairs)

### Difference Array (5 pairs)

**Q1: Why only modify two positions (L and R+1) per range update?**
A: Mark start and end. Reconstruction adds the value between them automatically via cumulative sum.

**Q2: What happens if you query array before reconstruction?**
A: You get values in difference array, not final values. Must reconstruct first.

**Q3: Can you handle negative updates?**
A: Yes. diff[L] -= value subtracts from range. Cumulative sum handles correctly.

**Q4: How does it handle overlapping ranges?**
A: Cumulative sum adds them correctly. Overlapping updates accumulate properly.

**Q5: When use difference array vs segment tree?**
A: Difference for batch updates + one reconstruction. Segment tree for mixed updates + queries.

---

### In-Place Replacement (5 pairs)

**Q1: Why must i >= j always (read >= write)?**
A: Ensures no valid data overwritten. Data written to j never read again after writing.

**Q2: What does return value represent?**
A: New length of valid elements. Original array modified, only [0...length) valid.

**Q3: Can this work on unordered arrays?**
A: Sorted arrays directly. Unordered needs preprocessing (sort or two-pass).

**Q4: Why do interviews prefer in-place?**
A: O(1) space is gold standard. Shows algorithmic mastery and pointer manipulation.

**Q5: How extend to multiple conditions (remove multiple types)?**
A: Add each to condition. Single two-pointer pass handles all in one go.

---

### Deque Operations (5+ pairs)

**Q1: Why store indices instead of values?**
A: Need to check window membership. Indices tell us if element still in window.

**Q2: Why remove smaller values from back?**
A: They'll never be max in current or future windows. Larger value will always shadow them.

**Q3: Is complexity really O(n) with nested while loops?**
A: Yes. Each element pushed once, popped once. Total O(n) despite nested loops.

**Q4: Can you use regular queue instead of deque?**
A: No. Need both front (remove expired) and back (remove smaller) operations.

**Q5: What if array has duplicates?**
A: Deque property still holds. Handle == carefully (usually pop duplicates or keep one).

---

## 📊 DAILY SELF-ASSESSMENT

| Day | Topic | Understanding | Implementation | Confidence |
|-----|-------|---|---|---|
| **1** | Difference Array | ___ | ___ | ___ / 5 |
| **2** | In-Place | ___ | ___ | ___ / 5 |
| **3** | Deque | ___ | ___ | ___ / 5 |

**Target:** 4/5 or higher on all before Week 6

---

## ✅ WEEK 5.5 COMPLETION CHECKLIST

### Knowledge Check
- [ ] Can explain all 3 Tier 2 patterns
- [ ] Understand when each pattern applies
- [ ] Know complexity for each
- [ ] Can recognize patterns in problems

### Skills Check
- [ ] Can implement all 3 patterns
- [ ] Can trace each pattern by hand
- [ ] Can choose pattern for problem
- [ ] Can solve variants and extensions

---

## 📈 Week 5.5 Summary

**Time:** ~9-10.5 hours  
**Topics:** 3 strategic optimization patterns  
**Problems:** 24+  
**Coverage:** +10-12% (cumulative 80-88%)

**Ready for Week 6 (Graphs)?** YES / NO

