# Week 5: Summary & Key Concepts

## 📖 Week 5 Overview

Trees & Heaps are foundational hierarchical data structures. Together they unlock efficient searching, sorting, prioritization, and balanced operations.

---

## 📊 Structure Comparison Table

| Structure | Find Min | Insert | Delete | Balance | Use |
|-----------|----------|--------|--------|---------|-----|
| **BST** | O(log n) | O(log n) | O(log n) | Manual | Sorted search |
| **AVL** | O(log n) | O(log n) | O(log n) | Auto | Strict balance |
| **Red-Black** | O(log n) | O(log n) | O(log n) | Auto | Fewer rotations |
| **Heap** | O(1) | O(log n) | O(log n) | Implicit | Priority queue |
| **General Tree** | O(n) | O(1) | O(1) | N/A | Hierarchy |

---

## 🧠 Key Insights

### Insight 1: Balance Determines Performance
Skewed BST = linked list (O(n)). Balanced BST = true binary search (O(log n)).

### Insight 2: Different Traversals, Different Purposes
In-order for sorted output, pre-order for cloning, post-order for deletion, level-order for nearest neighbors.

### Insight 3: Heaps are Partially Ordered
Not fully sorted but satisfy heap property. Enables O(log n) insert/delete with O(1) finding min.

### Insight 4: Self-Balancing Adds Complexity
Rotations are mechanical but required to maintain height balance across all insertions/deletions.

### Insight 5: Real-World Everywhere
File systems (tree), DOM (tree), databases (B-tree variants), priority queues (heaps), OS schedulers (heaps).

---

## 🎯 Pattern Recognition

**When Use BST:**
- Need sorted structure
- Want O(log n) search
- Plan to insert/delete frequently
- Example: In-memory sorted index

**When Use Heap:**
- Need O(1) find-min + O(log n) insert/delete
- Implementing priority queue
- Example: Dijkstra's algorithm, merge K lists

**When Use Balanced Tree:**
- Need guaranteed O(log n) even worst case
- Example: Database indexes (B-trees, actually)

**When Use General Tree:**
- Representing pure hierarchy
- DOM tree, organizational chart
- Example: File system directories

---

## ❌ Common Misconceptions Fixed

### ❌ "In-order only for BST"
✅ In-order works on any binary tree. Produces sorted only if BST.

### ❌ "Tree always height ≤ log(n)"
✅ Only if balanced. Unbalanced can be O(n) height.

### ❌ "Heaps are fully sorted"
✅ Only parent-child property guaranteed. Level-order not sorted.

### ❌ "Balanced trees always better"
✅ Trade-off: rotation cost vs guaranteed O(log n). For most uses, worth it.

### ❌ "AVL and Red-Black equivalent"
✅ Both O(log n) but different trade-offs. AVL stricter (more rotations), Red-Black faster (fewer rotations).

---

## 📈 Mastery Progression

### Level 1: Recognition (Days 1-2)
- Identify tree type
- Know basic properties
- Trace traversals

### Level 2: Understanding (Days 3-4)
- Explain WHY tree structure matters
- Understand preconditions (e.g., BST property)
- Trace insert/delete carefully

### Level 3: Application (Day 5+)
- Implement insert/delete correctly
- Handle edge cases
- Choose between structures

### Level 4: Mastery (Week 6+)
- Teach others
- Design tree-based solutions
- Optimize tree operations

---

## 🔗 Week 5 → Week 6+ Connections

**Week 6 (Graphs):** Trees are special graphs (acyclic, connected). DFS/BFS are tree traversal generalizations.

**Week 8 (Tries, Segment Trees):** Specialized tree variants for strings and range queries.

**Week 11 (DP):** DP problems often have tree structure (decision tree at each step).

**Week 12 (Integration):** Complex problems combine trees with other patterns.

---

## ✨ Week 5 Key Takeaway

> **Master 5 tree structures: Binary Trees (structure), Traversals (pattern), BST (order), Heaps (priority), Balanced (guarantee). Together they unlock hierarchical data processing and 60-70% of tree problems.**

---

**Cumulative (Weeks 1-5):** 60-70% interview coverage (up from 70-80% with patterns)

