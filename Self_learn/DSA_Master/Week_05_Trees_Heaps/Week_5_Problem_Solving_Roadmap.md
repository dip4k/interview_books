# Week 5: Problem-Solving Roadmap

## 📊 Problem-Solving Framework

**5-Step Process for ALL Week 5 problems:**

1. **Identify** tree type (general, BST, heap, balanced)
2. **Recognize** operation needed (search, insert, delete, traverse, rebalance)
3. **Choose** algorithm (DFS, BFS, rotations, heapify)
4. **Implement** carefully (pointer handling, edge cases)
5. **Verify** on small examples and edge cases

---

## 🎯 Pattern Decision Tree

```
Problem type classification:

Need to traverse tree?
├─ YES → Use traversal (in/pre/post/level-order)
└─ NO → Continue

Need sorted structure with fast operations?
├─ YES → Use BST or balanced variant
└─ NO → Continue

Need fast min/max extraction?
├─ YES → Use Heap / Priority Queue
└─ NO → Continue

Need to represent hierarchy?
├─ YES → Use general tree structure
└─ NO → Other data structure
```

---

## 🌳 Operation-Specific Roadmaps

### Tree Traversal Roadmap

**When:** Process all nodes in specific order

**Decision:**
- In-order? → For BST sorted output or root-between-children order
- Pre-order? → For cloning, serialization, or root-first processing
- Post-order? → For deletion, cleanup, or children-first processing
- Level-order? → For breadth-first, nearest neighbors, or level-by-level

**Implementation:**
- Recursive: Natural, uses call stack O(h)
- Iterative: Manual stack management, more control

---

### BST Search Roadmap

**When:** Need to find value in ordered tree

**Template:**
```
1. Start at root
2. Compare target with current
3. If equal, found
4. If less, go left
5. If greater, go right
6. If null, not found
Cost: O(log n) balanced, O(n) skewed
```

---

### BST Insert Roadmap

**When:** Need to maintain sorted tree while adding element

**Template:**
```
1. Find correct position (like search)
2. When null reached, insert new node
3. Check BST property (left < node < right)
4. Rebalance if unbalanced (for AVL/Red-Black)
Cost: O(log n) balanced, O(n) skewed
```

---

### BST Delete Roadmap

**When:** Need to remove element while maintaining BST property

**Cases:**
1. **Leaf:** Simply delete
2. **One child:** Replace with child
3. **Two children:** Replace with inorder successor, delete successor

---

### Heap Insert Roadmap

**When:** Adding element to priority queue

**Template:**
```
1. Add at end (maintain complete tree property)
2. Bubble up: compare with parent
3. If violates heap property, swap with parent
4. Continue until correct position
Cost: O(log n)
```

---

### Heap Delete Roadmap

**When:** Removing min/max from priority queue

**Template:**
```
1. Remove root (min or max)
2. Move last element to root
3. Bubble down: compare with children
4. Swap with smaller (min-heap) or larger (max-heap)
5. Continue until correct position
Cost: O(log n)
```

---

## 🔍 Common Pitfalls & Recovery

### Pitfall 1: "Forgot to maintain BST property"
**Recovery:** After insert/delete, verify: left < parent < right everywhere.

### Pitfall 2: "Traversal produces wrong order"
**Recovery:** Check recursion order: in = Left-Root-Right, pre = Root-Left-Right, post = Left-Right-Root.

### Pitfall 3: "Heap bubble-up/down infinite loop"
**Recovery:** Ensure termination: stop when position valid or reached leaf/root.

### Pitfall 4: "Delete two-child case wrong"
**Recovery:** Use inorder successor (smallest in right subtree), not inorder predecessor.

### Pitfall 5: "Forgot to handle edge case: empty tree, single node"
**Recovery:** Always check null pointers before dereferencing.

---

## 📋 Quick Reference Matrix

| Problem Type | Structure | Algorithm | Time | Edge Cases |
|--------------|-----------|-----------|------|------------|
| Find in sorted | BST | Binary search | O(log n) | Unbalanced → O(n) |
| Find min/max | Heap | Peek root | O(1) min, O(log n) others | |
| Traverse | Any tree | DFS/BFS | O(n) | Empty tree |
| Rebalance | AVL/RB | Rotations | O(1) per rotation | Multiple rotations needed |
| Merge priority | Heap | Heappush each | O(n log n) | Large k makes slow |

---

## 🎓 Practice Strategy

1. **Small Example:** Trace by hand on 3-5 node tree
2. **Identify Pattern:** Which traversal/operation?
3. **Code Carefully:** Pointer handling is error-prone
4. **Test Edge Cases:** Empty, single node, duplicates
5. **Verify Complexity:** Balanced vs skewed behavior

**Master this roadmap. Most Week 5 problems fit exactly one pattern.**

