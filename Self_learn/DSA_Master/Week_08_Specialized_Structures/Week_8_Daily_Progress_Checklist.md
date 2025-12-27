# Week 8: Daily Progress Checklist & Interview Q&A (40+ Pairs)

## ✅ DAY 1: Tries (Prefix Trees)

### Morning Objectives
- [ ] Understand prefix tree structure and traversal
- [ ] Know O(m) search independent of dictionary size
- [ ] Understand when to use vs hash maps
- [ ] Know real-world applications

### Core Learning
- [ ] Read: Week_8_Day_1_Tries_Instructional.md
- [ ] Trace: Insert, search, startsWith operations
- [ ] Trace: Prefix filtering and autocomplete
- [ ] Implement: Trie from scratch

### Practice Problems
- [ ] Implement Trie
- [ ] Autocomplete System
- [ ] Word Search II
- [ ] Longest Word in Dictionary by Deleting Letters

**Confidence Rating**: ___ / 5

---

## ✅ DAY 2: Segment Trees I (Basics & Lazy)

### Morning Objectives
- [ ] Understand range query data structure
- [ ] Know O(log n) per operation
- [ ] Understand lazy propagation concept
- [ ] Know when use vs Fenwick

### Core Learning
- [ ] Read: Week_8_Day_2_Segment_Trees_I_Instructional.md
- [ ] Trace: Build process bottom-up
- [ ] Trace: Range query combining
- [ ] Implement: Basic segment tree with lazy prop

### Practice Problems
- [ ] Range Sum Query - Mutable
- [ ] The Skyline Problem
- [ ] Describe the Painting
- [ ] Range Query with Addition

**Confidence Rating**: ___ / 5

---

## ✅ DAY 3: Segment Trees II (Advanced)

### Morning Objectives
- [ ] Understand 2D segment trees
- [ ] Know coordinate compression
- [ ] Understand persistent trees
- [ ] Know merge sort tree for inversions

### Core Learning
- [ ] Read: Week_8_Day_3_Segment_Trees_II_Advanced_Instructional.md
- [ ] Trace: 2D tree structure
- [ ] Trace: Coordinate compression mapping
- [ ] Implement: 2D queries (simplified)

### Practice Problems
- [ ] Falling Squares
- [ ] 2D Range Sum Query
- [ ] Reverse Pairs
- [ ] Largest Rectangle in Histogram

**Confidence Rating**: ___ / 5

---

## ✅ DAY 4: Fenwick Trees (Binary Indexed)

### Morning Objectives
- [ ] Understand lowbit trick: i & (-i)
- [ ] Know O(n) space vs O(4n)
- [ ] Know O(log n) same as segment
- [ ] Understand when simpler than segment

### Core Learning
- [ ] Read: Week_8_Day_4_Fenwick_Trees_Instructional.md
- [ ] Trace: Update via lowbit propagation
- [ ] Trace: Query via prefix sums
- [ ] Implement: Fenwick tree

### Practice Problems
- [ ] Range Sum Query - Mutable
- [ ] Count Smaller Numbers After Self
- [ ] Reverse Pairs
- [ ] 2D Binary Indexed Tree

**Confidence Rating**: ___ / 5

---

## ✅ DAY 5: Suffix Structures

### Morning Objectives
- [ ] Understand suffix arrays and sorting
- [ ] Know pattern matching via binary search
- [ ] Understand LCP arrays for LCS/LRS
- [ ] Understand suffix trees (optional)

### Core Learning
- [ ] Read: Week_8_Day_5_Suffix_Structures_Instructional.md
- [ ] Trace: Build suffix array from suffixes
- [ ] Trace: Binary search for pattern
- [ ] Implement: Suffix array (simple version)

### Practice Problems
- [ ] Implement Suffix Array
- [ ] Pattern Matching with SA
- [ ] Longest Common Substring
- [ ] Longest Repeated Substring

**Confidence Rating**: ___ / 5

---

## 🎯 INTERVIEW Q&A REFERENCE (40+ Pairs)

### Tries (5 pairs)

**Q1: Why is Trie O(m) instead of O(log n) like balanced trees?**
A: Trie traversal fixed m steps (string length). Not binary search, direct path traversal.

**Q2: When use Trie vs Hash Map?**
A: Trie for prefixes and multiple searches. Hash Map for single search on static data.

**Q3: How implement autocomplete efficiently?**
A: Trie stores words. DFS from prefix node to get all words with that prefix.

**Q4: Space complexity of Trie?**
A: O(alphabet_size × total_chars) = O(26n) for English, O(n) for sparse.

**Q5: Is Trie only for English?**
A: No, works for any alphabet. Just adjust children map size.

---

### Segment Trees I (5 pairs)

**Q1: Why 4n size for segment tree with n elements?**
A: Worst case: perfectly balanced binary tree with n leaves has ~2n nodes. 4n is safe upper bound.

**Q2: What's lazy propagation?**
A: Delay range updates, mark them as pending. Only push down to children when recursing there.

**Q3: Can you combine any function?**
A: Any associative function (sum, min, max, AND, OR). Not working: division, non-associative ops.

**Q4: Query complexity with/without lazy?**
A: O(log n) both. With lazy: range updates also O(log n) instead of O(n).

**Q5: When do you push lazy update?**
A: When recursing into children. Or during point query if that subtree needed.

---

### Segment Trees II (5 pairs)

**Q1: Why use 2D segment tree?**
A: 2D range queries (rectangle) in O(log² n) instead of O(nm).

**Q2: How does coordinate compression work?**
A: Map large values to small indices via sorting. Preserve relative order, so segment tree logic unchanged.

**Q3: What's persistent segment tree?**
A: Keep all tree versions. Query any version in O(log n). Space: O(n log n) for all versions.

**Q4: Merge sort tree purpose?**
A: Count inversions and similar problems. Each node stores sorted list, merge on query.

**Q5: Which advanced technique for which problem?**
A: 2D for grids. Compression for sparse large coords. Persistence for time-travel. Merge for inversions.

---

### Fenwick Trees (5 pairs)

**Q1: Why lowbit(i) = i & (-i)?**
A: Two's complement: -i = NOT(i) + 1. ANDing gives lowest bit.

**Q2: Why O(log n) and not O(1)?**
A: Path from i to root has O(log n) nodes. Each lowbit operation visits one node.

**Q3: Update vs query which is harder?**
A: Neither, both O(log n) simple operations.

**Q4: Fenwick vs Segment Tree trade-off?**
A: Fenwick: O(n) space, only sums, simpler. Segment: O(4n) space, flexible ops, complex.

**Q5: Can Fenwick do min/max?**
A: Not directly. Segment trees better for operations other than sum.

---

### Suffix Structures (5+ pairs)

**Q1: Why are matches contiguous in sorted suffix array?**
A: Because lexicographic order preserves prefix relationships. All "ana" suffixes alphabetically together.

**Q2: Build suffix array complexity?**
A: O(n log n) with comparison sort, O(n) with specialized algorithms.

**Q3: Pattern matching in suffix array?**
A: Binary search for pattern. All matches form contiguous range in SA.

**Q4: What's LCP array?**
A: Longest Common Prefix between consecutive SA entries. Used for LCS/LRS.

**Q5: Suffix array vs tree?**
A: Array O(n log n) build, O(m log n) search. Tree O(n) build, O(m) search. Array simpler.

**Q6: How find LCS of two strings?**
A: Concatenate strings, build suffix array + LCP. Find max LCP where suffixes from different strings.

**Q7: How find longest repeated substring?**
A: Build suffix array + LCP. Find max LCP (repetition means same substring at different positions).

---

## 📊 DAILY SELF-ASSESSMENT

| Day | Topic | Understanding | Implementation | Confidence |
|-----|-------|---|---|---|
| **1** | Tries | ___ | ___ | ___ / 5 |
| **2** | Segment I | ___ | ___ | ___ / 5 |
| **3** | Segment II | ___ | ___ | ___ / 5 |
| **4** | Fenwick | ___ | ___ | ___ / 5 |
| **5** | Suffix | ___ | ___ | ___ / 5 |

**Target:** 4/5+ on all before Week 9

---

## ✅ WEEK 8 COMPLETION CHECKLIST

### Knowledge Check
- [ ] Can explain all 5 structures and when to use
- [ ] Understand complexity trade-offs
- [ ] Know constraints and preconditions
- [ ] Can recognize problem types

### Skills Check
- [ ] Can implement Trie from scratch
- [ ] Can implement Segment Tree (basic)
- [ ] Can implement Fenwick Tree
- [ ] Can build Suffix Array
- [ ] Can solve variants of each
- [ ] Can choose structure for problem
- [ ] Can optimize for constraints

---

## 📈 Week 8 Summary

**Time:** ~14-16 hours  
**Topics:** 5 specialized structures  
**Problems:** 40+  
**Coverage:** +5-8% (cumulative 95-100%)

**Ready for Week 9+ (If Continuing)?** YES / NO

