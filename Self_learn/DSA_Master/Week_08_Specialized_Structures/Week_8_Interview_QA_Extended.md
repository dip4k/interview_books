# Week 8: Extended Interview Q&A Reference (40+ Pairs)

## 🎯 COMPLETE INTERVIEW PREPARATION

---

## TRIES (5 Pairs)

**Q1: Why is Trie O(m) instead of O(log n) like balanced trees?**
A: Trie traversal is direct path following, not binary search. Each character is one step, so m characters = m steps. No halving, pure traversal.

**Q2: When use Trie vs Hash Map for word search?**
A: Trie for prefixes (autocomplete), multiple lookups on static dictionary, spelling suggestions. Hash map for single lookups, static data, memory critical.

**Q3: How implement autocomplete with Trie efficiently?**
A: Store Trie, insert all words. For prefix input, traverse to prefix node, DFS to collect all words below. Can cache top-k words per node.

**Q4: Space complexity of Trie?**
A: O(alphabet_size × total_characters). For English: O(26n) = O(n). For arbitrary Unicode: O(n). Sparse trie with hash map: O(actual_edges).

**Q5: Can Trie handle non-English alphabets?**
A: Yes, works for any alphabet. Just adjust children map. Complexity same but alphabet_size changes (26 vs 256 vs larger).

---

## SEGMENT TREES I (5 Pairs)

**Q1: Why allocate 4n size for segment tree?**
A: Perfectly balanced binary tree with n leaves has ~2n nodes. 4n is conservative upper bound covering worst cases and simplifying indexing. Practical bound.

**Q2: What exactly is lazy propagation?**
A: Defer range updates instead of immediate propagation. Mark nodes with pending updates. Only push down to children when recursing there. Enables O(log n) range updates.

**Q3: Can segment tree combine any operation?**
A: Any associative binary operation (sum, min, max, AND, OR, XOR). Not: division, non-associative ops, string operations. Operation must combine results from children.

**Q4: Complexity difference: with vs without lazy propagation?**
A: Without: O(log n) point updates, O(n) range updates. With: O(log n) point and range updates. Lazy propagation crucial for range-heavy workloads.

**Q5: When do you actually push lazy updates down?**
A: On next traversal of children nodes. Or can eagerly push when accessing. Key: only compute and push what's needed.

---

## SEGMENT TREES II (5 Pairs)

**Q1: Why use 2D segment tree instead of 1D?**
A: 2D rectangle range queries directly. 1D approach: iterate rows, each with segment tree = O(n log n) space, O(log² n) queries. 2D nested: O(n log n) space still, O(log² n) queries.

**Q2: How does coordinate compression work step-by-step?**
A: (1) Collect all coordinate values. (2) Sort and deduplicate. (3) Create mapping old→new (1 to k). (4) Replace all coordinates with mapped values. (5) Build tree on compressed space. Preserves relative order, so logic unchanged.

**Q3: What is persistent segment tree?**
A: Maintain all tree versions. On update, copy only path from root to leaf. Query any version in O(log n). Total space: O(versions × log n) = O(n log n) for n updates.

**Q4: How use merge sort tree to count inversions?**
A: Each internal node stores sorted list of elements in range. Query: binary search merged list. Count elements satisfying condition. Time: O(log² n) per query after O(n log n) build.

**Q5: Which advanced technique solves which problem?**
A: 2D for grids/2D range. Compression for sparse large coords. Persistence for time-travel/history. Merge sort for inversion/comparison-based counting.

---

## FENWICK TREES (5 Pairs)

**Q1: Why does lowbit(i) = i & (-i) give lowest set bit?**
A: Two's complement: -i = ~i + 1 (bitwise NOT, then add 1). When ANDed: all higher bits cancel, only lowest bit remains. Example: i=6 (110₂), -i=~110+1=010 (in simple logic), 110 & 010 = 010 (lowbit 2).

**Q2: Why is Fenwick O(log n) and not O(log² n)?**
A: Single path from index to root via lowbit operations. Each operation: remove one bit. Number of set bits ≤ log₂(n), so O(log n) operations total.

**Q3: How does range query work with two prefix sums?**
A: RangeSum(l, r) = PrefixSum(r) - PrefixSum(l-1). Both prefix sums computed independently via Fenwick in O(log n).

**Q4: Fenwick vs Segment Tree trade-offs?**
A: Fenwick: O(n) space, O(log n) queries/updates, sum only, simpler code. Segment: O(4n) space, O(log n) queries/updates, any operation, more complex, more flexible.

**Q5: Can Fenwick Tree do operations other than sum?**
A: Directly: no (inherent to structure). Indirectly: can modify for min (different update logic). But segment trees natural for non-sum ops. Use segment tree if min/max needed.

---

## SUFFIX STRUCTURES (7 Pairs)

**Q1: Why are all matches of a pattern contiguous in suffix array?**
A: Lexicographic sort preserves prefix relationships. All suffixes starting with "ana" are alphabetically consecutive. No suffix starting with "ana" can be separated from others starting with "ana".

**Q2: Build suffix array complexity and optimizations?**
A: Naïve sort: O(n²) comparisons × O(n) per comparison = O(n³). Better sort: O(n²) comparisons × O(log n) with hashing = O(n² log n). Specialized (DC3, SA-IS): O(n) optimal but complex.

**Q3: How implement pattern matching in suffix array?**
A: Binary search for pattern in suffix array. Find leftmost and rightmost positions where pattern matches. All indices between are occurrences. Time: O(m log n) for binary search.

**Q4: What is LCP (Longest Common Prefix) array and use?**
A: LCP[i] = length of common prefix between SA[i] and SA[i+1]. Use: find LCS (max LCP where suffixes from different strings), LRS (max LCP = longest repeated substring).

**Q5: When use Suffix Array vs Suffix Tree?**
A: Array: simpler to implement, O(n log n) build, O(m log n) search, cleaner code. Tree: optimal O(n) build, O(m) search, more complex, overkill unless time critical.

**Q6: How find longest common substring (LCS) via suffix array?**
A: Concatenate strings with separator: str1 + '#' + str2. Build suffix array + LCP. Find max LCP where SA[i] from str1 and SA[i+1] from str2 (or vice versa).

**Q7: How find longest repeated substring (LRS) via suffix array?**
A: Build suffix array on single string + LCP. Find max LCP value (any value > 0 means repetition). Corresponding SA values give start positions of repeated substrings.

---

## SUMMARY & STRATEGY

### Problem Recognition

**String/Prefix Problem?**
→ Trie for autocomplete/spell-check
→ Suffix for pattern/LCS/LRS

**Range Query Problem?**
→ Fenwick for sums (simpler, O(n))
→ Segment I for other ops (min/max)
→ Segment II for 2D or persistence

**Pattern Matching?**
→ Suffix array O(m log n) simple
→ Suffix tree O(m) fast but complex
→ KMP/Z-algorithm for single pattern

### Interview Tips

1. **Start simple:** Use basics before advanced structures
2. **Explain complexity:** Show time/space understanding
3. **Discuss trade-offs:** Why this structure vs alternatives
4. **Code cleanly:** Focus on correctness over optimization
5. **Test edge cases:** Empty input, single element, duplicates

### Time Management

- **Easy problem:** 15-20 min explain, code, test
- **Medium problem:** 20-30 min (more complex structure)
- **Hard problem:** 30-45 min (may combine multiple structures)

---

## READINESS CHECKLIST

**Before Interview:**
- [ ] Can implement all 5 structures from scratch
- [ ] Can answer all 40+ Q&A pairs
- [ ] Can recognize problem → structure in < 1 min
- [ ] Rate 4/5+ on all topics
- [ ] Solved 15-20 practice problems total
- [ ] Timed yourself (< 1 hour per medium problem)
- [ ] Reviewed common pitfalls
- [ ] Can explain trade-offs clearly

**Interview Day:**
- [ ] Clarify problem before starting
- [ ] Explain approach before coding
- [ ] Code, test, optimize in that order
- [ ] Discuss complexity and trade-offs
- [ ] Handle edge cases
- [ ] Stay calm (you know this material!)

---

**Good luck! You've mastered 95-100% of interview problems.**

