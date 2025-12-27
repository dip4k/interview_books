# Week 5: Trees & Heaps — Guidelines

## 📅 Daily Breakdown & Time Allocation

**Total Week:** 12-14 hours (2.5-2.8 hours per day)

| Day | Topic | Time | Focus |
|-----|-------|------|-------|
| **1** | Binary Tree Anatomy | 2.5h | Structure, properties, representation |
| **2** | Tree Traversals | 2.5h | In/Pre/Post/Level-order 4 patterns |
| **3** | Binary Search Trees | 2.5h | Sorted trees, insert/delete, balance |
| **4** | Heaps & Priority Queues | 2.5h | Min/max heaps, bubbling operations |
| **5** | Balanced Trees | 2.5h | AVL, Red-Black, rotation mechanics |
| **Weekend** | Integration | 2h | Combining tree operations |

---

## 🎯 Learning Objectives

### By End of Week 5
- [ ] Master tree anatomy and properties
- [ ] Implement all 4 traversals (recursive + iterative)
- [ ] Maintain BST property in insert/delete
- [ ] Implement heap bubble up/down correctly
- [ ] Understand AVL vs Red-Black trade-offs
- [ ] Solve 40-50% of tree problems

---

## 📚 Core Concepts

**Concept 1: Hierarchical Structure**  
Trees represent parent-child relationships efficiently. Better than arrays for sparse hierarchies.

**Concept 2: Tree Traversal Patterns**  
Different orders for different purposes: in-order for sorting, pre-order for cloning, post-order for deletion.

**Concept 3: Binary Search Property**  
Maintaining sorted order enables O(log n) operations. Balance is critical.

**Concept 4: Heap Ordering**  
Partial ordering (not fully sorted) enables O(log n) insert/delete while O(1) finding min/max.

**Concept 5: Self-Balancing**  
Rotations maintain O(log n) height guarantee across all operations.

---

## 🔄 Recommended Learning Path

**Morning (90 min):** Read instructional, trace examples, understand mechanics  
**Afternoon (60 min):** Answer questions, solve 4-5 problems, implement from scratch  
**Evening (30 min):** Review checklist, rate confidence, prepare next day

---

## ⚠️ Common Mistakes

**Mistake 1: "All trees are binary"**  
Reality: N-ary trees possible. Binary trees have ≤ 2 children.

**Mistake 2: "In-order only works for BST"**  
Reality: In-order works on any binary tree (just no sort guarantee unless BST).

**Mistake 3: "BST always O(log n)"**  
Reality: O(log n) only if balanced. Skewed tree = linked list O(n).

**Mistake 4: "Heaps must be fully sorted"**  
Reality: Heaps partial order. Only guarantee parent-child relationship.

**Mistake 5: "Balanced tree operations complex"**  
Reality: Rotations mechanical. Practice tracing until intuitive.

---

## 🎓 Practice Problems (30-40 total)

### Tree Anatomy (5)
1. Maximum Depth of Binary Tree
2. Same Tree
3. Symmetric Tree
4. Invert Binary Tree
5. Binary Tree Diameter

### Traversals (8)
1. Level Order Traversal
2. In-order Traversal (recursive)
3. In-order Traversal (iterative)
4. Pre-order, Post-order (similar)
5. Serialize and Deserialize
6. Vertical Order Traversal
7. Right View of Binary Tree
8. Zig-Zag Level Order

### BST (8)
1. Validate Binary Search Tree
2. Search in BST
3. Insert into BST
4. Delete Node in BST
5. Kth Smallest in BST
6. Lowest Common Ancestor (BST)
7. Binary Tree to BST
8. Balanced BST from sorted array

### Heaps (6)
1. Kth Largest Element
2. Merge K Sorted Lists
3. Top K Frequent Elements
4. Sliding Window Maximum
5. Find Median from Data Stream
6. K Closest Points to Origin

### Balanced Trees (5)
1. AVL tree insert/delete (understanding)
2. Red-Black tree properties
3. Self-balancing intuition
4. Rotation mechanics
5. Real-world usage understanding

---

## 💼 Interview Preparation

**Week 5 Coverage:** 60-70% of tree problems (30-40% overall with other weeks)

**Interview strategy:**
1. Identify problem type (find, insert, traversal, etc.)
2. Choose data structure (BST, heap, general tree)
3. Trace through small example
4. Code carefully (pointer handling is error-prone)
5. Test edge cases (single node, empty tree, etc.)

---

## 📊 Connection to Future Weeks

**Week 6 (Graphs):** DFS/BFS are tree traversal generalizations  
**Week 11 (DP):** DP problems often have tree structure (decisions at each step)  
**Week 12 (Integration):** Tree problems combined with other patterns

---

## ✅ Before Moving to Week 6

- [ ] Rate 4/5 or higher on all 5 days
- [ ] Can implement tree traversals from scratch
- [ ] Understand when BST balanced vs skewed
- [ ] Can trace heap operations correctly
- [ ] Know AVL vs Red-Black trade-offs

