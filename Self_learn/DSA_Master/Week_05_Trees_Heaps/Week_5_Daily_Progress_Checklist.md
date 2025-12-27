# Week 5: Daily Progress Checklist & Interview Q&A

## ✅ DAY 1: Binary Tree Anatomy

### Morning Objectives
- [ ] Understand node structure (value + left/right pointers)
- [ ] Know tree properties (root, leaves, height, depth, balance)
- [ ] Difference between balanced and skewed trees
- [ ] Why balance matters for complexity

### Core Learning
- [ ] Read: Week_5_Day_1_Binary_Tree_Anatomy_Instructional.md
- [ ] Trace: Insert [5,3,7,2,4] into BST
- [ ] Trace: Height and depth calculations
- [ ] Understand: Why recursive natural for trees

### Practice Problems
- [ ] Maximum Depth of Binary Tree
- [ ] Same Tree
- [ ] Symmetric Tree
- [ ] Invert Binary Tree

**Confidence Rating**: ___ / 5

---

## ✅ DAY 2: Tree Traversals

### Morning Objectives
- [ ] Master in-order (Left, Node, Right)
- [ ] Understand pre-order (Node, Left, Right)
- [ ] Know post-order (Left, Right, Node)
- [ ] Recognize level-order (BFS, breadth-first)

### Core Learning
- [ ] Read: Week_5_Day_2_Tree_Traversals_Instructional.md
- [ ] Trace: 4 traversals on same tree
- [ ] Understand: When each traversal useful
- [ ] Implement: Both recursive and iterative

### Practice Problems
- [ ] Level Order Traversal
- [ ] In-order (recursive)
- [ ] In-order (iterative with stack)
- [ ] Serialize and Deserialize

**Confidence Rating**: ___ / 5

---

## ✅ DAY 3: Binary Search Trees

### Morning Objectives
- [ ] Understand BST property
- [ ] Search in O(log n) on balanced
- [ ] Insert while maintaining property
- [ ] Delete with 3 cases (leaf, 1 child, 2 children)

### Core Learning
- [ ] Read: Week_5_Day_3_4_5_Consolidated_Instructional.md (Day 3)
- [ ] Trace: Search, insert, delete on BST
- [ ] Understand: Inorder successor concept
- [ ] Know: Why balance critical

### Practice Problems
- [ ] Validate Binary Search Tree
- [ ] Search in BST
- [ ] Insert into BST
- [ ] Delete Node in BST

**Confidence Rating**: ___ / 5

---

## ✅ DAY 4: Heaps & Priority Queues

### Morning Objectives
- [ ] Understand min-heap property
- [ ] Know max-heap (reverse property)
- [ ] Bubble up operation (insert)
- [ ] Bubble down operation (delete min)

### Core Learning
- [ ] Read: Week_5_Day_3_4_5_Consolidated_Instructional.md (Day 4)
- [ ] Trace: Bubble up on insertion
- [ ] Trace: Bubble down on deletion
- [ ] Understand: Array representation (i's children at 2i+1, 2i+2)

### Practice Problems
- [ ] Kth Largest Element in Array
- [ ] Merge K Sorted Lists
- [ ] Top K Frequent Elements
- [ ] Sliding Window Maximum

**Confidence Rating**: ___ / 5

---

## ✅ DAY 5: Balanced Trees

### Morning Objectives
- [ ] Understand AVL balance condition (height diff ≤ 1)
- [ ] Know Red-Black color properties
- [ ] Understand rotation mechanics
- [ ] Compare AVL vs Red-Black trade-offs

### Core Learning
- [ ] Read: Week_5_Day_3_4_5_Consolidated_Instructional.md (Day 5)
- [ ] Trace: Single and double rotations
- [ ] Understand: When rebalancing needed
- [ ] Know: AVL stricter, Red-Black faster

### Practice Problems
- [ ] Understand rotation types
- [ ] Trace rebalancing
- [ ] Know when AVL vs Red-Black
- [ ] Study std library implementations

**Confidence Rating**: ___ / 5

---

## 🎯 INTERVIEW Q&A REFERENCE (30+ Pairs)

### Tree Anatomy (5 pairs)

**Q1: What's difference between height and depth?**
A: Height = distance from node to farthest leaf. Depth = distance from root to node.

**Q2: How many edges in tree with n nodes?**
A: n-1 edges (by definition of tree).

**Q3: Can complete binary tree be unbalanced height-wise?**
A: No, complete tree guarantees balanced heights by definition.

**Q4: BST with duplicates: allowed?**
A: Standard BST no duplicates. Some allow duplicates in right subtree.

**Q5: Why in-order traversal of BST gives sorted?**
A: In-order processes left (all smaller), then root, then right (all larger).

---

### Traversals (6 pairs)

**Q1: When use pre-order vs post-order?**
A: Pre-order = root-first (cloning, serialization). Post-order = children-first (deletion, bottom-up).

**Q2: Level-order space complexity?**
A: O(width) = O(2^h) worst for full tree, but typically O(n/2) for last level.

**Q3: Serialize BST pre-order, deserialize back?**
A: Pre-order gives root, then recursively construct left/right.

**Q4: Morris traversal: what advantage?**
A: O(1) space in-order traversal (no recursion stack). Modifies tree temporarily.

**Q5: LCA (Lowest Common Ancestor) in BST?**
A: If both targets < node, go left. If both > node, go right. Otherwise, node is LCA.

**Q6: BFS vs DFS memory?**
A: BFS uses queue O(width). DFS uses stack O(height). BFS wider, DFS deeper.

---

### BST Operations (8 pairs)

**Q1: Validate BST: what's the check?**
A: For each node, verify all left descendants < node < all right descendants.

**Q2: Delete two-child case strategy?**
A: Find inorder successor (smallest in right subtree), replace node with it, delete successor.

**Q3: Inorder successor in BST?**
A: Go right once, then left as far as possible.

**Q4: Kth smallest in BST?**
A: In-order traversal is sorted. Return kth element.

**Q5: BST from sorted array?**
A: Divide & conquer: choose middle as root, left half as left subtree, right half as right.

**Q6: Lowest Common Ancestor in binary tree (not BST)?**
A: Recursively find both targets in left/right subtrees. First node finding both is LCA.

**Q7: Balanced BST performance vs unbalanced?**
A: Balanced O(log n) all operations. Unbalanced O(n) degenerates to linked list.

**Q8: Flatten BST to sorted linked list?**
A: In-order traversal storing in list, then convert.

---

### Heaps (6 pairs)

**Q1: Min-heap vs max-heap usage?**
A: Min-heap for priority queue (smallest priority). Max-heap for largest.

**Q2: Heapify operation time complexity?**
A: Building heap from array O(n), not O(n log n).

**Q3: Top K elements using heap?**
A: Maintain min-heap of size K. Add all, pop smallest when size > K. O(n log k).

**Q4: Merge K sorted lists with heap?**
A: Use min-heap of k elements (one per list). Extract min, add next from that list.

**Q5: Dijkstra uses min-heap why?**
A: Always process smallest unvisited distance next. Min-heap gives O(log n) extract.

**Q6: Heap sort stability?**
A: Heap sort unstable. Heapify can swap equal elements.

---

### Balanced Trees (5 pairs)

**Q1: AVL rotation types?**
A: Single left, single right, left-right, right-left. Fix height imbalance.

**Q2: Red-Black vs AVL trade-off?**
A: AVL stricter (height diff ≤1) → more rotations. RB relaxed → fewer rotations.

**Q3: When height rebalancing needed?**
A: After insert/delete if balance factor changes or becomes imbalanced.

**Q4: Real-world usage: databases, filesystems?**
A: B-trees (generalization), not exact AVL/RB. Optimize for disk I/O blocks.

**Q5: Self-balancing overhead worth it?**
A: Yes. Guarantee O(log n) vs risky O(n) in unbalanced tree.

---

## 📊 DAILY SELF-ASSESSMENT

| Day | Topic | Understanding | Implementation | Confidence |
|-----|-------|---|---|---|
| **1** | Anatomy | ___ | ___ | ___ / 5 |
| **2** | Traversals | ___ | ___ | ___ / 5 |
| **3** | BST | ___ | ___ | ___ / 5 |
| **4** | Heaps | ___ | ___ | ___ / 5 |
| **5** | Balanced | ___ | ___ | ___ / 5 |

**Target:** 4/5 or higher on all before Week 6

