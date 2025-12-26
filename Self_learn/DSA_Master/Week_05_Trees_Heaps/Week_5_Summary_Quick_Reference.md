# Week 5: Summary & Quick Reference

**Week:** 5 | **Topic:** Trees & Heaps | **Difficulty:** Hard | **Time:** 15-20 hours

---

## 📊 EXECUTIVE SUMMARY (One Line Per Topic)

**Binary Tree Anatomy:** Hierarchical structure (root + left/right subtrees) enabling O(log n) algorithms on hierarchical data  
**Tree Traversals:** Four visit orders (preorder/inorder/postorder/level-order) revealing different structural properties  
**Binary Search Trees:** Sorted tree maintaining left < parent < right for O(log n) search/insert/delete  
**Heaps & Priority Queues:** Tree prioritizing min/max element at root for O(1) access, O(log n) insert/delete  
**Balanced Trees:** AVL/RB-Trees auto-rebalancing to maintain height ≈ log(n) despite arbitrary insertions  

---

## 🎯 COMPLEXITY COMPARISON TABLE

| Operation | Array | Linked List | BST (Unbalanced) | BST (Balanced) | Heap |
|-----------|-------|-------------|------------------|----------------|------|
| **Search** | O(log n*) | O(n) | O(n) worst | O(log n) | O(n) |
| **Insert** | O(n) | O(1) at head | O(n) worst | O(log n) | O(log n) |
| **Delete** | O(n) | O(n) | O(n) worst | O(log n) | O(log n) |
| **Min/Max** | O(n) | O(n) | O(n) | O(n) | O(1) |
| **Sorted Iterate** | O(n) | O(n) | O(n) | O(n) | O(n log n) |
| **Space** | O(1) extra | O(1) extra | O(n) pointers | O(n) pointers | O(1) extra |

*Sorted array only

---

## 🌳 DECISION MATRIX: WHICH STRUCTURE TO USE?

| Need | Use | Why |
|------|-----|-----|
| **Search fast** | Balanced BST | O(log n) search |
| **Get min/max fast** | Heap | O(1) access |
| **Maintain sorted + modify** | Balanced BST | O(log n) all ops |
| **Priority ordering** | Heap | O(1) priority, O(log n) insert |
| **Iterate in order** | Balanced BST | Inorder = sorted |
| **Fast insert/delete** | Heap | O(log n), no search |
| **Hierarchical data** | Tree structure | Natural representation |
| **Range queries** | B-Tree | Optimize disk access |

---

## 📋 KEY INSIGHTS BY TOPIC

### Binary Tree Anatomy
✓ Tree = Root + Left Subtree + Right Subtree (recursive definition)  
✓ Height h: best case log(n), worst case n (depends on balance)  
✓ Recursion is natural (tree is recursive structure)  

### Tree Traversals
✓ Preorder = Parent first (use for cloning)  
✓ Inorder = Middle (use for sorted BST output)  
✓ Postorder = Parent last (use for deletion)  
✓ Level-order = Top-down (use for BFS)  

### Binary Search Trees
✓ Left < Parent < Right (everywhere, recursively)  
✓ Inorder traversal = sorted values  
✓ All ops O(log n) IF balanced, O(n) IF skewed  
✓ Delete hardest (3 cases, last case needs rebalancing)  

### Heaps & Priority Queues
✓ Heap = tree that's PRIORITIZED not SORTED  
✓ Min/Max at root always (O(1) access)  
✓ Array representation = cache efficient  
✓ No search allowed (O(n) linear)  

### Balanced Trees
✓ AVL = strict height balance (|left height - right height| ≤ 1)  
✓ Rotations = local restructuring preserving BST property  
✓ O(log n) height guaranteed for n nodes  
✓ Production systems use variants (B-Trees, RB-Trees)  

---

## 🔀 TREE TRAVERSALS QUICK REFERENCE

| Traversal | Order | Use Case | Implementation |
|-----------|-------|----------|-----------------|
| **Preorder** | Parent, Left, Right | Cloning trees, prefix | Stack/recursion |
| **Inorder** | Left, Parent, Right | BST sorted output | Stack/recursion |
| **Postorder** | Left, Right, Parent | Deletion, postfix | Stack/recursion |
| **Level-Order** | Top-to-bottom | BFS, breadth-first | Queue only |

**Memory Anchor:** "Pre = parent first, In = middle, Post = parent last"

---

## 📈 COMMON MISTAKES & FIXES

| Mistake | Why Wrong | How to Fix |
|---------|-----------|-----------|
| Using skewed BST for search | Degenerates to O(n) | Balance tree (AVL/RB) |
| Searching in heap | O(n) required | Use BST if need search |
| Unbalanced after insertion | Height becomes O(n) | Apply rotations |
| Wrong traversal order | Get wrong info | Preorder=cloning, Inorder=sorted |
| Deleting from heap wrong | Breaks heap property | Bubble-down after move-to-root |
| Not updating heights in AVL | Can't detect imbalance | Track height at every node |
| Circular parent-child refs | Creates cycle (not tree) | Ensure parent-child one direction |

---

## 🧠 PROBLEM-SOLVING FRAMEWORKS

### "Is This a BST?" Framework
```
Check at EVERY node:
- All left subtree values < node value ✓
- All right subtree values > node value ✓
- Both left AND right subtrees are BSTs ✓

Common mistake: only checking immediate children
(Must check all descendants!)
```

### "Which Traversal?" Framework
```
Need to print in order? → INORDER
Need to copy tree? → PREORDER  
Need to delete tree? → POSTORDER
Need level-by-level? → LEVEL-ORDER
Not sure? → INORDER (most common)
```

### "Find Min/Max" Framework
```
BST:
  - Min: go left until can't → node.val
  - Max: go right until can't → node.val
  - O(h) time

Heap:
  - Min: root (if min-heap)
  - Max: need to scan all children → O(n)
  - O(1) for the property-aligned min/max
```

---

## 💾 COMPLEXITY CHEAT SHEET

**Tree Operations:**
```
Search:     O(h) [h=height]
Insert:     O(h)
Delete:     O(h)
Traverse:   O(n)
Build:      O(n log n) via insert, O(n) via build_heap
```

**Height Relationships:**
```
Balanced BST:    h = O(log n)
Unbalanced BST:  h = O(n)
Complete Binary: h = O(log n)
Heap:            h = O(log n)
AVL:             h ≤ 1.44 log n
Red-Black:       h ≤ 2 log n
```

---

## 📝 QUICK LOOKUP: INTERVIEW ANSWERS

**Q: What's a binary tree?**  
A: Hierarchical data structure where each node has at most 2 children (left, right). Root at top, leaves at bottom.

**Q: Difference between tree and graph?**  
A: Tree = acyclic connected graph. Single root, every node reachable, no cycles.

**Q: When use BST vs heap?**  
A: BST when need search + sorted iteration. Heap when need fast min/max without search.

**Q: What's tree rotation?**  
A: Local restructuring that swaps parent-child roles while maintaining BST property. Used to rebalance.

**Q: Why balanced trees?**  
A: Unbalanced BST can degenerate to linked list (O(n)). Balancing guarantees O(log n) height.

**Q: What's heap property?**  
A: Parent ≥ all children (max-heap) or parent ≤ all children (min-heap). Enables O(1) min/max access.

---

## 🎓 WEEK 5 MASTERY CHECKLIST

**Conceptual Understanding:**
- [ ] Why trees organize hierarchical data
- [ ] What makes tree vs graph vs linked list
- [ ] Why balance matters (O(n) vs O(log n))
- [ ] Difference between BST and heap purpose
- [ ] How traversals reveal structure

**Implementation:**
- [ ] Build tree from values
- [ ] Implement all 4 traversals
- [ ] BST search/insert/delete
- [ ] Heap insert/delete_root
- [ ] Tree rotations (AVL)

**Application:**
- [ ] Recognize when to use tree
- [ ] Solve 15+ tree problems
- [ ] Explain complexity trade-offs
- [ ] Design real-world tree solutions
- [ ] Debug tree code

**Production Awareness:**
- [ ] Know databases use B-Trees
- [ ] Know OS uses RB-Trees
- [ ] Understand heap in priority queues
- [ ] Recognize trees in your code

---

## 🔗 QUICK LINKS

**Visualization:**
- VisuAlgo Trees: https://www.cs.usfca.edu/~galles/visualization/BST.html
- AVL Visualizer: https://www.cs.usfca.edu/~galles/visualization/AVLtree.html

**Practice:**
- LeetCode Trees: https://leetcode.com/tag/binary-tree/
- HackerRank: https://www.hackerrank.com/challenges/tree-height-of-a-binary-tree/

**Theory:**
- GeeksforGeeks Trees: https://www.geeksforgeeks.org/binary-tree-data-structure/
- Competitive Programming: https://codeforces.com/blog/entry/11080

---

## 📊 WEEK 5 AT A GLANCE

```
Day 1: Tree anatomy (structure)
Day 2: Traversals (visiting)
Day 3: BSTs (searching)
Day 4: Heaps (prioritizing)
Day 5: Balanced (performance)

Total: 15-20 hours
Reading: 6-8 hours
Practice: 9-12 hours
Difficulty: Hard
Interview Weight: 25-30%
```

---

**Week 5 Quick Ref Version:** 1.0  
**Status:** Ready for reference  
**Print This:** Yes, keep handy

