# Week 5: Guidelines, Summary, Roadmap, Checklist, Q&A, Manifest (Combined)

## 📅 GUIDELINES: Daily Breakdown

| Day | Topic | Time | Coverage |
|-----|-------|------|----------|
| **1** | Binary Tree Anatomy | 2.5h | Structure, properties, representation |
| **2** | Tree Traversals | 2.5h | In/Pre/Post/Level-order (4 patterns) |
| **3** | Binary Search Trees | 2.5h | Sorted trees, balanced vs skewed |
| **4** | Heaps & Priority Queues | 2.5h | Min/max heaps, priority extraction |
| **5** | Balanced Trees | 2.5h | AVL, Red-Black, rotation mechanics |

**Total:** 12-14 hours, 5 hierarchical data structures

---

## 🎯 LEARNING OBJECTIVES

- [ ] Understand tree anatomy (nodes, edges, parent-child)
- [ ] Master all 4 traversal types and when to use each
- [ ] Recognize BST property and maintain during insert/delete
- [ ] Implement heap operations (bubble up/down)
- [ ] Know AVL vs Red-Black trade-offs
- [ ] Solve 40-50% of tree problems

---

## 📊 SUMMARY: Pattern Comparison

| Structure | Use Case | Find | Insert | Delete | Balance |
|-----------|----------|------|--------|--------|---------|
| **BST** | Sorted search | O(log) | O(log) | O(log) | Need balance |
| **AVL** | Strict balance | O(log) | O(log) | O(log) | Self-balancing |
| **Red-Black** | Faster rebalance | O(log) | O(log) | O(log) | Self-balancing |
| **Heap** | Priority queue | O(1) min | O(log) | O(log) | Complete tree |

---

## 🌳 PROBLEM ROADMAP: Decision Tree

```
Need sorted structure + fast search?
├─ YES → Binary Search Tree (or balanced variant)
└─ NO → Continue

Need priority extraction (min/max)?
├─ YES → Heap / Priority Queue
└─ NO → Continue

Need hierarchical representation?
├─ YES → General tree structure
└─ NO → Other data structure
```

---

## 📋 DAILY CHECKLIST

### Day 1: Binary Tree Anatomy
- [ ] Understand node structure (value + pointers)
- [ ] Know tree properties (root, leaves, height, depth)
- [ ] Trace search/insert on BST
- [ ] Practice: Maximum Depth, Same Tree

### Day 2: Tree Traversals
- [ ] Trace in-order, pre-order, post-order
- [ ] Understand when each traversal useful
- [ ] Implement recursive and iterative versions
- [ ] Practice: Level Order, Serialize Tree

### Day 3: Binary Search Trees
- [ ] Understand BST property
- [ ] Insert and maintain BST
- [ ] Delete with 3 cases (leaf, one child, two children)
- [ ] Practice: Validate BST, Insert into BST, Delete Node

### Day 4: Heaps & Priority Queues
- [ ] Understand heap property (min/max)
- [ ] Trace bubble up (insert)
- [ ] Trace bubble down (delete min)
- [ ] Practice: Kth Largest, Merge K Lists

### Day 5: Balanced Trees
- [ ] Understand rotation mechanics
- [ ] Know AVL vs Red-Black differences
- [ ] Trace rebalancing after insert/delete
- [ ] Study implementation details

---

## 🎯 INTERVIEW Q&A (30+ Pairs)

**Tree Anatomy (5):**
1. What's difference between height and depth?
2. Can BST have duplicates?
3. Why in-order traversal of BST gives sorted?
4. How many edges in tree with n nodes?
5. Can complete binary tree be unbalanced?

**Traversals (6):**
1. When use pre-order vs post-order?
2. Iterative in-order without recursion?
3. Level-order space complexity?
4. Serialize tree pre-order, deserialize back?
5. Find LCA (lowest common ancestor)?
6. Morris traversal (no stack)?

**BST (6):**
1. Validate BST correctness check?
2. Delete node with two children strategy?
3. Find kth smallest in BST?
4. BST to sorted linked list?
5. Inorder successor in BST?
6. Balance vs unbalanced BST performance?

**Heaps (6):**
1. Min-heap vs max-heap usage?
2. Heapify operation correctness?
3. Top K elements using heap?
4. Merge K sorted lists with heap?
5. Dijkstra uses min-heap why?
6. Build heap from array O(n)?

**Balanced Trees (7):**
1. AVL rotation types?
2. Red-Black color properties?
3. When AVL vs Red-Black?
4. Rebalancing after insertion?
5. Height guarantee after rebalancing?
6. Delete rebalancing logic?
7. Real world usage (databases, filesystems)?

---

## 📈 CUMULATIVE PROGRESS (Weeks 1-5)

| Weeks | Topics | Hours | Coverage |
|-------|--------|-------|----------|
| 1-3 | Foundations, Linear, Sorting | 36 | 40-50% |
| 4 | Patterns | 12.5 | 50-60% |
| 4.5 | Tier 1 | 12-14 | 70-80% |
| 5 | Trees & Heaps | 12-14 | **60-70%** |

---

## ✨ KEY TAKEAWAYS

**Week 5 Focus:** Hierarchical data structures enable efficient sorted access, priority extraction, and balanced operations. Foundation for Week 6 (Graphs) and Week 11 (DP).

**Interview Value:** Tree questions appear in 30-40% of medium/hard problems. Mastery is essential.

**Next:** Week 6 (Graphs) builds on tree traversal concepts (DFS/BFS).

