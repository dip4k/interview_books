# Week 5: Q&A Practice Questions (10 Per Day)

**Total Questions:** 50 (10 × 5 days)  
**Difficulty Range:** ⭐ Easy to ⭐⭐⭐ Hard  
**Purpose:** Self-assess and reinforce learning  

---

## 📍 DAY 1: BINARY TREE ANATOMY (10 Questions)

### Question 1 ⭐ Easy
**Q: What defines a binary tree?**  
A: A hierarchical data structure where each node has at most 2 children (left and right). Has a single root and leaves with no children.

**Why This Matters:** Foundation for everything in Week 5

---

### Question 2 ⭐ Easy
**Q: What's the difference between a tree and a graph?**  
A: Tree is acyclic (no cycles), connected, and has single root. Graph can have cycles, multiple components, and multiple roots.

**How to Remember:** "Tree = special graph" (with restrictions)

---

### Question 3 ⭐ Easy
**Q: A tree with 10 nodes has how many edges?**  
A: 9 edges. Rule: edges = nodes - 1 (every node except root has exactly 1 parent)

**Quick Test:** 15 nodes = 14 edges ✓

---

### Question 4 ⭐⭐ Medium
**Q: What's the relationship between tree height and number of levels?**  
A: Tree of height h has h+1 levels (or h levels if 0-indexed). Height is longest path from root to leaf.

**Example:** Height 3 = Levels 0,1,2,3 (4 levels) or Levels 1,2,3 (3 levels)

---

### Question 5 ⭐⭐ Medium
**Q: For a complete binary tree with 7 nodes, what's the height?**  
A: Height 2 (levels 0,1,2). Complete binary tree fills level-by-level, left-to-right.

**Formula:** Height = ⌊log₂(n)⌋ for complete tree

---

### Question 6 ⭐⭐ Medium
**Q: What's minimum height for binary tree with 1000 nodes?**  
A: Height ≈ log₂(1000) ≈ 10 (perfectly balanced). This is the BEST case.

**Comparison:** Maximum height = 999 (linear/skewed)

---

### Question 7 ⭐⭐ Medium
**Q: Can a tree have a cycle?**  
A: No, by definition. If there's a cycle, it becomes a graph. Trees are acyclic.

**Why:** Cycle = node reachable by 2 different paths

---

### Question 8 ⭐⭐⭐ Hard
**Q: What's the maximum number of nodes in a complete binary tree of height h?**  
A: 2^(h+1) - 1. Each level i has 2^i nodes.

**Proof:** Level 0 has 1 node, Level 1 has 2, Level 2 has 4, etc. Sum = 1+2+4+...+2^h = 2^(h+1) - 1

---

### Question 9 ⭐⭐⭐ Hard
**Q: Prove that every non-empty binary tree has at least 1 leaf.**  
A: Proof by contradiction. If no leaf exists, every node has at least 1 child. Following any path from root, you never terminate. But tree is finite → contradiction. Therefore, at least 1 leaf exists.

---

### Question 10 ⭐⭐⭐ Hard
**Q: Why is recursion natural for tree problems?**  
A: Trees are recursively defined: Tree = (Value, LeftSubtree, RightSubtree). To solve tree problem, we solve it on subtrees. Base case: empty tree.

---

## 📍 DAY 2: TREE TRAVERSALS (10 Questions)

### Question 1 ⭐ Easy
**Q: What's the difference between preorder, inorder, and postorder?**  
A: When you process the parent node relative to children. Preorder = before children, Inorder = between children, Postorder = after children.

---

### Question 2 ⭐ Easy
**Q: For tree [1, [2, [3], [4]], [5]], what's preorder?**  
A: 1, 2, 3, 4, 5 (parent always first)

---

### Question 3 ⭐ Easy
**Q: What's level-order traversal?**  
A: Visit nodes top-to-bottom, left-to-right, level by level. Uses queue (BFS).

---

### Question 4 ⭐⭐ Medium
**Q: For tree with inorder [4,2,5,1,3], what can you conclude?**  
A: If it's a BST, values appear sorted in inorder. This sequence IS sorted → could be valid BST inorder.

---

### Question 5 ⭐⭐ Medium
**Q: Given preorder [1,2,4,5,3] and inorder [4,2,5,1,3], reconstruct the tree.**  
A: Preorder's first element is root (1). Inorder shows: [4,2,5] are left subtree, [3] is right. Recursively reconstruct.

Result:
```
      1
     / \
    2   3
   / \
  4   5
```

---

### Question 6 ⭐⭐ Medium
**Q: Why does inorder of BST give sorted values?**  
A: BST property: left < parent < right. Inorder visits left, then parent, then right. By recursion, all values < parent visited before parent, all > parent after. Result: strictly increasing.

---

### Question 7 ⭐⭐ Medium
**Q: Implement preorder iteratively (using stack) in 5 lines.**  
A:
```python
stack = [root]
result = []
while stack:
    node = stack.pop()
    result.append(node.val)
    if node.right: stack.append(node.right)  # Push right first!
    if node.left: stack.append(node.left)    # Popped first
```

---

### Question 8 ⭐⭐⭐ Hard
**Q: What's space complexity of recursive inorder traversal?**  
A: O(h) where h = height. Recursion uses call stack. Best case O(log n) for balanced, worst case O(n) for skewed.

---

### Question 9 ⭐⭐⭐ Hard
**Q: Can you reconstruct a tree from ONLY preorder?**  
A: No (uniqueness lost). But if values are distinct AND all values in left subtree < parent < right subtree, you can assume BST property.

---

### Question 10 ⭐⭐⭐ Hard
**Q: Level-order uses O(w) space, where w = max width. Why?**  
A: Queue stores entire level. Widest level has most nodes. Complete binary tree's widest level ≈ n/2 nodes.

---

## 📍 DAY 3: BINARY SEARCH TREES (10 Questions)

### Question 1 ⭐ Easy
**Q: State BST property in one sentence.**  
A: For every node: all values in left subtree < node value < all values in right subtree.

---

### Question 2 ⭐ Easy
**Q: Is [2,1,3] a valid BST?**  
A: Yes. Root 2: left child 1 < 2, right child 3 > 2. Both subtrees are valid BSTs.

---

### Question 3 ⭐⭐ Medium
**Q: Implement BST search in 5 lines.**  
A:
```python
def search(node, target):
    if not node: return False
    if target == node.val: return True
    return search(node.left, target) if target < node.val else search(node.right, target)
```

---

### Question 4 ⭐⭐ Medium
**Q: What are the 3 cases of BST deletion?**  
A: 1) Node has no children (delete directly). 2) Node has 1 child (replace with child). 3) Node has 2 children (replace with inorder successor).

---

### Question 5 ⭐⭐ Medium
**Q: Deleting node with 2 children: why use inorder successor?**  
A: Inorder successor is smallest value > node. Replacing maintains BST property: it's > all left subtree values and < all right subtree values.

---

### Question 6 ⭐⭐ Medium
**Q: Insert sequence 1,2,3,4,5 into BST. What's resulting structure?**  
A: Degenerate tree (linked list):
```
1
 \
  2
   \
    3
     \
      4
       \
        5
Height: 5 (bad!)
```

---

### Question 7 ⭐⭐ Medium
**Q: Prove time complexity of BST search is O(h).**  
A: Each comparison eliminates one subtree. Maximum path from root to leaf = height h. Therefore worst case = h comparisons.

---

### Question 8 ⭐⭐⭐ Hard
**Q: Implement BST validation (check if valid).**  
A:
```python
def is_bst(node, min_val=float('-inf'), max_val=float('inf')):
    if not node: return True
    if not (min_val < node.val < max_val): return False
    return is_bst(node.left, min_val, node.val) and is_bst(node.right, node.val, max_val)
```

---

### Question 9 ⭐⭐⭐ Hard
**Q: Delete root from BST [4, 2, 6, 1, 3, 5, 7]. What's new root?**  
A: Find inorder successor (min of right subtree = 5). Replace 4 with 5, delete 5 from right subtree.

Result:
```
      5
     / \
    2   6
   / \   \
  1   3   7
```

---

### Question 10 ⭐⭐⭐ Hard
**Q: Why is AVL/Red-Black needed if BST is O(log n)?**  
A: O(log n) only if BALANCED. Skewed BST becomes O(n). Balancing trees guarantee balance regardless of insertion order.

---

## 📍 DAY 4: HEAPS & PRIORITY QUEUES (10 Questions)

### Question 1 ⭐ Easy
**Q: What's heap property?**  
A: Parent ≥ all children (max-heap) OR parent ≤ all children (min-heap).

---

### Question 2 ⭐ Easy
**Q: Is [9,7,8,3,2,1,5] a valid max-heap?**  
A: Yes. 9 ≥ 7,8; 7 ≥ 3,2; 8 ≥ 1,5. All parent-child relationships satisfy max-heap property.

---

### Question 3 ⭐ Easy
**Q: How do you access min element in min-heap?**  
A: It's always at the root (index 0). O(1) time!

---

### Question 4 ⭐⭐ Medium
**Q: Insert 10 into heap [9,7,8,3,2,1,5]. What's result?**  
A: Append at end: [9,7,8,3,2,1,5,10]. Bubble up: 10 > 8? Swap. Now [9,7,10,3,2,1,5,8]. 10 > 9? Swap. Result: [10,7,8,3,2,1,5,9].

---

### Question 5 ⭐⭐ Medium
**Q: What's space complexity of heap operations?**  
A: Insert: O(log n). Delete: O(log n). Both due to height. Array implementation: O(1) extra space (no pointers).

---

### Question 6 ⭐⭐ Medium
**Q: Can you search for element X in O(log n) time in heap?**  
A: No. Heap is prioritized, not sorted. Must scan all nodes: O(n).

---

### Question 7 ⭐⭐ Medium
**Q: What's the difference between heap and BST?**  
A: Heap: prioritized (min/max at root), no search, O(n) search. BST: sorted, efficient search O(log n), less efficient min/max.

---

### Question 8 ⭐⭐⭐ Hard
**Q: Build heap from array [5,3,8,1,2] in O(n) time.**  
A: Use heapify: iterate from last non-leaf (index 1), bubble down each.

Result (max-heap): [8,3,5,1,2]

---

### Question 9 ⭐⭐⭐ Hard
**Q: Find median in data stream using 2 heaps. Design.**  
A: Max-heap for lower half, min-heap for upper half. Maintain balance: max-heap size ≤ min-heap size + 1.

Median = max-heap root (if odd) OR (max-root + min-root)/2 (if even)

---

### Question 10 ⭐⭐⭐ Hard
**Q: Prove heapsort time complexity is O(n log n).**  
A: Build heap: O(n). Extract n times: n × O(log n) = O(n log n). Total: O(n log n).

---

## 📍 DAY 5: BALANCED TREES (10 Questions)

### Question 1 ⭐ Easy
**Q: What's AVL property?**  
A: For every node, height(left subtree) - height(right subtree) ∈ {-1, 0, 1}.

---

### Question 2 ⭐ Easy
**Q: Is a linked list a valid AVL tree?**  
A: No. Linked list has height n. AVL property violated (difference > 1).

---

### Question 3 ⭐⭐ Medium
**Q: What's a tree rotation?**  
A: Local restructuring that swaps parent-child roles. Preserves BST property while rebalancing.

---

### Question 4 ⭐⭐ Medium
**Q: Insert 1,2,3 into AVL tree. Show rebalancing.**  
A: After 3, tree becomes right-heavy. Left rotation gives:
```
    2
   / \
  1   3
```

---

### Question 5 ⭐⭐ Medium
**Q: What are 4 rotation cases in AVL?**  
A: LL (left-left): right rotate. RR (right-right): left rotate. LR: left-rotate parent, then right-rotate. RL: right-rotate parent, then left-rotate.

---

### Question 6 ⭐⭐ Medium
**Q: Why AVL stricter than Red-Black?**  
A: AVL: |height difference| ≤ 1. RB: looser balance. AVL more rotations during insert, RB faster insertions.

---

### Question 7 ⭐⭐ Medium
**Q: What's height bound for AVL tree with 1000 nodes?**  
A: Height ≤ 1.44 × log₂(1000) ≈ 14. Guaranteed O(log n) height!

---

### Question 8 ⭐⭐⭐ Hard
**Q: Implement left rotation in 5 lines.**  
A:
```python
def rotate_left(node):
    new_root = node.right
    node.right = new_root.left
    new_root.left = node
    # Update heights
    return new_root
```

---

### Question 9 ⭐⭐⭐ Hard
**Q: Why does rotation preserve BST property?**  
A: Rotation is LOCAL. All elements left of root stay left. Elements between old-root and new-root stay between them. All right elements stay right. BST property: maintained!

---

### Question 10 ⭐⭐⭐ Hard
**Q: Design LR rotation visually and explain why 2 rotations needed.**  
A: LR case: heavy on left-right. One left-rotation brings deep right child up to left. Then right-rotation brings it to top. Fixes imbalance.

---

## 🎯 SELF-ASSESSMENT GUIDE

**For Each Question:**
1. Attempt without looking at answer
2. Check answer
3. Rate yourself: Correct/Incorrect
4. If incorrect, understand why
5. Mark topic for review

**Scoring:**
- 45-50 correct: Master level
- 40-44 correct: Advanced level
- 35-39 correct: Solid level
- <35 correct: Review needed

**Topics to Focus Review On:**
- Questions you got wrong
- Concepts you guessed on
- Hard (⭐⭐⭐) questions you struggled with

---

**Q&A Version:** 1.0 Week 5 Complete  
**Total Questions:** 50  
**Target Accuracy:** 85%+

