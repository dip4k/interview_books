# Week 8: Problem-Solving Roadmap

## 📊 Problem-Solving Framework

**5-Step Process for ALL Week 8 problems:**

1. **Analyze** problem (string? range? pattern?)
2. **Identify** needs (updates? all occurrences? prefix?)
3. **Match** structure (Trie? Segment? Fenwick? Suffix?)
4. **Implement** with proper data structure
5. **Optimize** for constraints and trade-offs

---

## 🎯 Structure Decision Tree

```
Is it a STRING/PREFIX problem?
├─ Prefix-based (autocomplete)? → Trie
├─ Pattern matching? → Suffix Array/Tree
├─ Word manipulation? → Trie or suffix
└─ Other string ops? → Basic string algorithms

Is it a RANGE QUERY problem?
├─ Only sum queries? → Fenwick Tree
├─ Other operations (min/max)? → Segment Tree I
├─ 2D ranges needed? → Segment Tree II
├─ Lazy updates? → Segment Tree with lazy prop
└─ Simple enough for O(n)? → Preprocessing + O(1)

Is it a PATTERN MATCHING problem?
├─ Single pattern? → KMP or binary search
├─ Multiple patterns? → Aho-Corasick or suffix
├─ Find all occurrences? → Suffix array binary search
├─ Longest common substring? → Suffix + LCP
└─ Longest repeated substring? → Suffix + LCP
```

---

## 🌳 Structure-Specific Roadmaps

### Trie Roadmap (Prefix Matching)

**When:** Autocomplete, spell-check, IP routing

**Template:**
```
1. TrieNode with children map
2. Insert: traverse path, create nodes, mark end
3. Search: traverse path, check end marker
4. StartsWith: traverse path, return if exists
5. DFS for all words with prefix

Time: O(m) for m-length string
Space: O(alphabet_size × total_length)
```

**Examples:** Autocomplete, word search in board

---

### Segment Tree I Roadmap (Range Queries)

**When:** Range sum/min/max, point updates, lazy propagation

**Template:**
```
1. Build tree bottom-up O(n)
2. Query: traverse, combine overlaps O(log n)
3. Update: point update, propagate up O(log n)
4. LazyPropagate: defer updates, push on need

Time: O(log n) per operation
Space: O(4n)
```

**Examples:** Range sum, skyline, painting

---

### Segment Tree II Roadmap (Advanced)

**When:** 2D queries, coordinate compression, persistence

**Techniques:**
1. **2D:** Outer tree (rows), inner trees (cols)
2. **Compression:** Map large values to small
3. **Persistence:** Version tracking for time-travel
4. **Merge Sort:** Count inversions

**Examples:** Falling squares, 2D range sum

---

### Fenwick Tree Roadmap (Range Sum)

**When:** Range sum only, prefer simplicity, O(n) space critical

**Template:**
```
1. BIT[i] stores sum([i - lowbit(i) + 1, i])
2. lowbit(i) = i & (-i)
3. Update: add delta, propagate up via lowbit
4. Query: sum via prefix sums, subtract for ranges

Time: O(log n) per operation
Space: O(n)
```

**Examples:** Range sum, inversion counting, 2D prefix

---

### Suffix Array Roadmap (Pattern Matching)

**When:** Pattern matching, LCS, LRS, text indexing

**Template:**
```
1. Create (suffix, index) pairs
2. Sort lexicographically
3. Extract indices to array
4. Binary search for pattern (ranges are contiguous)
5. Build LCP for LCS/LRS

Time: O(n log n) build, O(m log n) search
Space: O(n)
```

**Examples:** Pattern matching, LCS, LRS

---

### Suffix Tree Roadmap (Fast Matching)

**When:** Pattern matching, speed critical, LCS/LRS

**Template:**
```
1. Build via Ukkonen's algorithm O(n)
2. Traverse tree for pattern O(m)
3. All matches accessible from pattern node

Time: O(n) build, O(m) search
Space: O(n)
```

**Examples:** Same as suffix array but faster

---

## 🔍 Common Pitfalls & Recovery

### Pitfall 1: "Wrong structure choice"
**Recovery:** Use decision tree above. Match problem type exactly.

### Pitfall 2: "Segment tree complexity overwhelming"
**Recovery:** Start simple, add lazy prop only if needed.

### Pitfall 3: "Fenwick off-by-one errors"
**Recovery:** 1-indexed array, careful with lowbit operations.

### Pitfall 4: "Suffix array TLE"
**Recovery:** Optimize sort (use hashing), or implement O(n) build.

### Pitfall 5: "Wrong combining function"
**Recovery:** Test with small examples, verify operation associativity.

---

## 📋 Quick Reference Matrix

| Problem | Structure | Time | When |
|---------|-----------|------|------|
| Autocomplete | Trie | O(m) | Prefix-based |
| Range Sum | Fenwick | O(log n) | Simple, O(n) space |
| Range Min/Max | Segment I | O(log n) | Other operations |
| 2D Range | Segment II | O(log² n) | 2D grids |
| Pattern Match | Suffix Array | O(m log n) | Simple, indexed |
| Pattern Match | Suffix Tree | O(m) | Speed critical |
| LCS/LRS | Suffix + LCP | O(n log n) | Via preprocessing |

---

**Master this roadmap. Each Week 8 problem fits exactly one pattern.**

