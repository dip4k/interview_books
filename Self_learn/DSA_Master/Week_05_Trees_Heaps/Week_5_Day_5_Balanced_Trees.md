# Week 5, Day 5: Balanced Trees

**Week:** 5 | **Day:** 5 | **Topic:** Balanced Trees (AVL & Red-Black)  
**Time:** 90 minutes reading | **Difficulty:** 🔴 Hard  
**Prerequisites:** Days 1-3 (Tree Anatomy, Traversals, BSTs)  

---

## 1️⃣ THE WHY — Engineering Motivation

### The BST Problem Recap

**Sorted insert:** 1, 2, 3, 4, 5 creates linked list (height = n)  
**Search becomes:** O(n), defeating the purpose of BST!

### The Solution: Auto-Balancing

**Balanced Trees maintain:** height ≈ log(n) regardless of insertion order

```
Linked list tree:        Balanced tree:
1                             3
 \                           / \
  2                         1   4
   \                           \
    3                           5
     \
      4
       \
        5

Height: 5 (bad)              Height: 3 (good)
Search: O(5)                 Search: O(log 5)
```

### Why This Matters

Every Google search, database query, file system operation uses balanced trees.

---

## 2️⃣ THE WHAT — Mental Model & Intuition

### AVL Trees: Height-Balanced

**AVL Property:** For every node, heights of left and right subtrees differ by at most 1.

```
Valid AVL:           Invalid AVL:
      1                   1
     / \                 / \
    2   3               2   3
   /                   /
  4                   4
                     /
                    5

Heights: |1-1|=0 ✓    Heights: |2-0|=2 ✗
```

### Red-Black Trees: Color-Balanced

**RB Properties:**
1. Every node is red or black
2. Root is black
3. Leaves (nil) are black
4. Red node's children are black
5. All paths from node to leaf have same black count

```
Valid RB Tree:
        B(5)
       /    \
     R(3)  B(7)
     / \      \
   B(1)B(4)  B(8)

Every property checked ✓
```

### Key Difference

```
AVL: Stricter balance → More rotations → Less insert overhead
RB: Looser balance → Fewer rotations → More insertion speed

AVL: Used in read-heavy systems (e.g., databases)
RB: Used in write-heavy systems (e.g., Java TreeMap)
```

---

## 3️⃣ THE HOW — Mechanical Walkthrough

### AVL Rotations (Key Technique)

**Left Rotation (when right subtree is too heavy):**

```python
def rotate_left(node):
    # Move right child up
    new_root = node.right
    node.right = new_root.left
    new_root.left = node
    
    # Update heights
    node.height = 1 + max(height(node.left), height(node.right))
    new_root.height = 1 + max(height(new_root.left), height(new_root.right))
    
    return new_root

Visual:
Before:          After:
    a                b
     \              / \
      b      →     a   c
       \
        c
```

**Right Rotation (opposite):**

```python
def rotate_right(node):
    # Move left child up
    new_root = node.left
    node.left = new_root.right
    new_root.right = node
    
    # Update heights
    # ... same as left
    
    return new_root
```

### AVL Insert with Rebalancing

```python
def insert_avl(node, val):
    # Standard BST insert
    if not node:
        return TreeNode(val)
    
    if val < node.val:
        node.left = insert_avl(node.left, val)
    else:
        node.right = insert_avl(node.right, val)
    
    # Update height
    node.height = 1 + max(height(node.left), height(node.right))
    
    # Check balance and rebalance if needed
    balance = height(node.left) - height(node.right)
    
    # Left heavy
    if balance > 1:
        if val < node.left.val:  # Left-Left case
            return rotate_right(node)
        else:  # Left-Right case
            node.left = rotate_left(node.left)
            return rotate_right(node)
    
    # Right heavy
    if balance < -1:
        if val > node.right.val:  # Right-Right case
            return rotate_left(node)
        else:  # Right-Left case
            node.right = rotate_right(node.right)
            return rotate_left(node)
    
    return node
```

---

## 4️⃣ VISUALIZATION — Traced Examples

### Example 1: AVL Balancing

```
Insert 1, 2, 3 (would create skewed BST):

Step 1: Insert 1
    1

Step 2: Insert 2
    1
     \
      2

Step 3: Insert 3 (triggers rebalance)
    1
     \
      2
       \
        3

Balance of 1: height(left) - height(right) = 0 - 2 = -2 (too right-heavy)
Right-Right case: rotate left

After rotation:
      2
     / \
    1   3

Heights: |0-0| = 0 ✓ Balanced!
```

### Example 2: Four Rotation Cases

```
LL (Left-Left):        LR (Left-Right):
  a                      a
 /                      /
b          →rotate→    c
/                     / \
c                    b   ...

RR (Right-Right):      RL (Right-Left):
    a                      a
     \                       \
      b        →rotate→       c
       \                     / \
        c                  ... b

Each requires different combination of rotations
```

---

## 5️⃣ CRITICAL ANALYSIS — Performance & Robustness

### Complexity Analysis

| Operation | AVL | RB | BST (unbalanced) |
|-----------|-----|----|----|
| **Search** | O(log n) | O(log n) | O(n) worst |
| **Insert** | O(log n) | O(log n) | O(n) worst |
| **Delete** | O(log n) | O(log n) | O(n) worst |
| **Space** | O(n) | O(n) | O(n) |
| **Rebalances per insert** | ~1.2 | ~0.5 | 0 |

### Why AVL Stricter?

```
AVL: Balance factor ∈ [-1, 1]
     More rebalancing, taller tree for same n

RB: Balance factor unbounded
    Fewer rebalancing, shorter for same n
    
    Trade-off: more rotations (AVL) vs worse constants (RB)
```

### Implementation Complexity

```
RB Trees: Much harder to implement correctly
Colors + black-height = complex invariants
Usually not in interviews (Java has TreeMap built-in)

AVL: Slightly simpler (just heights)
More commonly implemented/tested
```

---

## 6️⃣ REAL SYSTEM INTEGRATION — Production Applications

### Database Indexing (B-Trees)

```
MySQL primary key: B-Tree (generalization of balanced BST)
- Each node: multiple children (m-way tree)
- Keys in node: sorted
- Logarithmic height maintained

Stores millions of records with O(log n) search
```

### Operating Systems

```
Virtual memory page tables: Often Red-Black Trees
Linux kernel (mm/rbtree.c): RB-Tree implementation
Used for scheduler, memory management, etc.
```

### Languages & Collections

```
Java: TreeMap, TreeSet → Red-Black Trees
C++ STL: std::map, std::set → RB-Trees
Python: No built-in balanced BST
  (heapq for heaps, but no balanced tree)

Why? RB-Trees balance write performance
```

---

## 7️⃣ CONCEPT CROSSOVERS — Connections

### Days 1-3: BST Evolution

```
Day 1: Tree structure
Day 2: How to visit trees
Day 3: Sorted structure (BST)
Day 5: Making BSTs practical (balancing)
```

### Problem-Solving Pattern

```
Problem: "BST degenerates to linked list"
Solution: Add balancing constraint
Technique: Rotations maintain BST property while rebalancing

This pattern recurs: when simple doesn't work, add constraint
```

### Week 6+: Graph Algorithms

```
Many algorithms assume balanced trees for O(log n) operations
Dijkstra with AVL: O((E+V) log V)
Without balancing: could be O(EV)

Balancing makes algorithms practical!
```

---

## 8️⃣ MATHEMATICAL & THEORETICAL — Formal Foundations

### AVL Height Bound

**Theorem:** AVL tree with n nodes has height ≤ 1.44 log₂(n+1)

**Proof:** Fibonacci-based lower bound on node count for height h.
Minimum nodes for height h ≈ φ^h / √5 (golden ratio)
Therefore h ≤ log_φ(√5 · n) ≈ 1.44 log₂(n) ∎

### RB Height Bound

**Theorem:** RB-Tree with n nodes has height ≤ 2 log₂(n+1)

**Proof:** Each RB-tree node height ≥ black-height/2
Black-height ≥ log₂(n), so height ≤ 2 log₂(n) ∎

---

## 9️⃣ ALGORITHMIC DESIGN INTUITION — Why Design Works

### Why Rotations Preserve BST Property

```
Rotation is local restructuring.
Left rotation:       Before:  a < b < c
   a                 After:   a < b < c
    \                Still true! (only local reordering)
     b      →
    / \
   c   d

All elements left of a remain < a
All elements between a and b remain in that relationship
All elements right of b remain > b

BST property preserved!
```

### Why Balance Guarantees O(log n)

```
Balanced tree height = O(log n)
Any path from root to leaf = O(log n) steps
Operations follow paths (search, insert, delete)
Therefore all operations = O(log n)
```

---

## 🔟 KNOWLEDGE CHECK — Socratic Reasoning

1. **Why is AVL stricter than RB-Tree?** How does more rebalancing help? What's the trade-off?

2. **Can you perform a left rotation by hand?** What about left-right rotation?

3. **Why does rotating left fix right-heavy imbalance?** Which nodes move where?

4. **What happens if you don't balance after insertion?** Use the 1,2,3 example.

5. **Why are RB-Trees used in production more than AVL?** What makes them more practical?

---

## 1️⃣1️⃣ RETENTION HOOK — Memory Anchors

### **"One Difference Max"**
AVL: Left height - right height ∈ {-1, 0, 1}
That's the entire rule!

### **"Rotate to Rebalance"**
Left-heavy → rotate right
Right-heavy → rotate left
(Remember: opposite direction)

### **"Four Cases"**
LL: rotate right
RR: rotate left
LR: left-rotate, then right-rotate
RL: right-rotate, then left-rotate

---

## 📊 SUPPLEMENTARY: Tree Comparison

| Tree Type | Balance | Height | Operations | Implementation |
|-----------|---------|--------|------------|-----------------|
| **BST** | None | O(n) worst | O(n) worst | Simple |
| **AVL** | Strict | O(log n) | O(log n) | Medium |
| **RB** | Loose | O(log n) | O(log n) | Hard |
| **B-Tree** | Multi-way | O(log n) | O(log n) | Very hard |

---

## 🔗 EXTERNAL RESOURCES

- AVL Visualization: https://www.cs.usfca.edu/~galles/visualization/AVLtree.html
- RB-Tree Visualization: https://www.cs.usfca.edu/~galles/visualization/RedBlack.html
- LeetCode Problems: https://leetcode.com/tag/binary-search-tree/

---

## 📝 KEY TAKEAWAYS

✅ **Unbalanced BSTs degenerate to linked lists**  
✅ **AVL and RB-Trees maintain O(log n) height**  
✅ **Rotations restructure while maintaining BST property**  
✅ **AVL: stricter but more rebalancing**  
✅ **RB: looser but faster insertions**  
✅ **Production systems use balanced trees everywhere**

---

## 🎯 WEEK 5 INTEGRATION

**Day 1:** Tree anatomy (structure)  
**Day 2:** Traversals (visiting)  
**Day 3:** BSTs (maintaining order)  
**Day 4:** Heaps (maintaining priority)  
**Day 5:** Balanced trees (maintaining balance)

**All together:** Complete mastery of hierarchical data structures!

**Next Week:** Week 5.5 — TIER 2: STRATEGIC PATTERNS (Greedy, DP, Graphs)

