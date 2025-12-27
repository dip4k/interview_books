# Week 4.5: Summary & Key Concepts

## 📖 Week Overview

**Tier 1 teaches CRITICAL patterns** solving 70-80% of interview problems. These 5 patterns are the foundation of algorithm mastery.

---

## 📊 Pattern Comparison Table

| Pattern | Use Case | Time | Space | When |
|---------|----------|------|-------|------|
| **Hash Map** | Fast lookup, frequency count | O(1) avg | O(n) | Always first choice |
| **Monotonic Stack** | Next greater/smaller element | O(n) | O(n) | When order matters |
| **Merge** | Combine sorted structures | O(n+m) | O(n+m) | When both sorted |
| **Partition** | In-place segregation | O(n) | O(1) | When space critical |
| **Kadane** | Max subarray, DP pattern | O(n) | O(1) | Subarray problems |

---

## 🧠 Key Insights

### Insight 1: Hash is Foundation (70% coverage!)
Most problems first check membership or count frequency. Hash makes this O(1).

### Insight 2: Stack Order Matters
Monotonic stack transforms O(n²) to O(n) by maintaining order during processing.

### Insight 3: Sorted Arrays Enable Efficiency
Merge, partition, sliding window all leverage sorted/ordered properties.

### Insight 4: Space-Time Trade-offs
Kadane shows O(1) space DP possible. Partition shows O(1) space segregation possible.

### Insight 5: Patterns Combine
Hash + heap = top K. Hash + DP = memoization. Monotonic stack + hash = efficient counting.

---

## 🎯 Common Problem Patterns

**Pattern 1: Fast Lookup Needed**
→ Use Hash Map/Set. Example: Two Sum, Anagrams, Duplicates.

**Pattern 2: Next/Previous Element Query**
→ Use Monotonic Stack. Example: Next Greater Element, Temperatures.

**Pattern 3: Combine Two Sorted Structures**
→ Use Merge. Example: Merge Arrays, Merge K Lists.

**Pattern 4: In-Place Rearrangement**
→ Use Partition. Example: Move Zeros, Dutch Flag.

**Pattern 5: Subarray Optimization**
→ Use Kadane DP. Example: Max Subarray, Max Product.

---

## ❌ Common Misconceptions Fixed

### ❌ "Hash always O(1)"
✅ **Reality:** Average O(1), worst O(n). Load factor and hash distribution matter.

### ❌ "Monotonic stack only for next greater"
✅ **Reality:** Any problem requiring efficient tracking of extremes in order.

### ❌ "Merge only for merge sort"
✅ **Reality:** Merging is general technique for combining sorted data.

### ❌ "Partition only for quicksort"
✅ **Reality:** Partition segregates based on criteria (zeros, colors, values).

### ❌ "Kadane only for max subarray"
✅ **Reality:** Template works for max product, longest subarray, many DP variants.

---

## 📈 Mastery Progression

### Level 1: Recognition (Days 1-2)
- Identify which pattern applies
- Trace example by hand

### Level 2: Understanding (Days 3-4)
- Explain WHY pattern works
- Identify preconditions (e.g., sorted for merge)

### Level 3: Application (Day 5+)
- Implement correctly
- Combine patterns if needed
- Solve variants

### Level 4: Mastery (Week 5+)
- Teach others
- Recognize in unfamiliar contexts
- Choose among patterns

---

## 🔗 Tier 1 → Week 5+ Connections

**Week 5 (Trees):** Tree problems use hash sets (visited), hash maps (indices)  
**Week 6 (Graphs):** Graph BFS/DFS use hash (visited set). Topological sort uses stack.  
**Week 11 (DP):** Memoization is hash map. Kadane is simplest DP.  
**Week 12 (Integration):** All complex problems combine Tier 1 patterns.  

---

## ✨ Week 4.5 Key Takeaway

> **Master Tier 1 patterns: Hash (70%), Monotonic (20%), Merge (30%), Partition (15%), Kadane (10%). Combined, they unlock 70-80% of interview problems.**

---

**Cumulative (Weeks 1-4.5):** 70-80% interview coverage

