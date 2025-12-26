# Week 5, Day 3: Binary Search Trees

**Week:** 5 | **Day:** 3 | **Topic:** Binary Search Trees  
**Time:** 80 minutes reading | **Difficulty:** 🔴 Hard  
**Prerequisites:** Days 1-2 (Tree Anatomy, Traversals)  

---

## 1️⃣ THE WHY — Engineering Motivation

### The Problem We Solve

**Scenario:** You need a data structure that supports:
- Search (O(log n))
- Insert (O(log n))
- Delete (O(log n))
- Ordered iteration (in-order gives sorted)

**Array:** Sorted, but insertion/deletion O(n)  
**Linked List:** Fast insertion/deletion, but search O(n)  
**BST:** Best of both worlds!

### Why BSTs Power Databases

```
MySQL, PostgreSQL use variants (B-Trees)
Why? BSTs solve the "searching + modifying" problem
That's exactly what databases do all day
```

---

## 2️⃣ THE WHAT — Mental Model & Intuition

### Core Property: Sorted Structure

**BST Property:**
- **Left subtree:** all values < parent
- **Right subtree:** all values > parent
- **Applies recursively** to every subtree

```
        4
       / \
      2   6
     / \ / \
    1  3 5  7

Why this works:
- Everything left of 4: 1,2,3 < 4 ✓
- Everything right of 4: 5,6,7 > 4 ✓
- Left subtree (rooted 2): 1,2,3 is itself a BST ✓
- Right subtree (rooted 6): 5,6,7 is itself a BST ✓
```

### Insight: Why Search Works

```
Search for 5 in BST(4):
  5 > 4? Go right to node 6
  5 < 6? Go left to node 5
  Found! 3 comparisons, not 7

Compare: Linear search needs 5 comparisons to confirm found
```

---

## 3️⃣ THE HOW — Mechanical Walkthrough

### Search Implementation

```python
def search(node, target):
    if not node:
        return False
    
    if target == node.val:
        return True
    elif target < node.val:
        return search(node.left, target)   # Go left
    else:
        return search(node.right, target)  # Go right
```

### Insert Implementation

```python
def insert(node, val):
    if not node:
        return TreeNode(val)  # Create new node
    
    if val < node.val:
        node.left = insert(node.left, val)   # Insert left
    elif val > node.val:
        node.right = insert(node.right, val) # Insert right
    # else: val == node.val, skip duplicates
    
    return node
```

### Delete Implementation (Complex)

```python
def delete(node, val):
    if not node:
        return None
    
    if val < node.val:
        node.left = delete(node.left, val)
    elif val > node.val:
        node.right = delete(node.right, val)
    else:
        # Found node to delete
        # Case 1: No children (leaf)
        if not node.left and not node.right:
            return None
        
        # Case 2: One child
        if not node.left:
            return node.right
        if not node.right:
            return node.left
        
        # Case 3: Two children (hardest!)
        # Find minimum in right subtree (inorder successor)
        min_right = find_min(node.right)
        node.val = min_right.val              # Copy value up
        node.right = delete(node.right, min_right.val)  # Delete successor
    
    return node

def find_min(node):
    while node.left:
        node = node.left
    return node
```

---

## 4️⃣ VISUALIZATION — Traced Examples

### Example 1: Building a BST

```
Insert: 4, 2, 6, 1, 3, 5, 7

Step 1: Insert 4
    4

Step 2: Insert 2 (2 < 4, go left)
    4
   /
  2

Step 3: Insert 6 (6 > 4, go right)
    4
   / \
  2   6

Step 4: Insert 1 (1 < 4 < 6, go left, 1 < 2, go left)
    4
   / \
  2   6
 /
1

... continuing ...

Final:
      4
     / \
    2   6
   / \ / \
  1  3 5  7
```

### Example 2: Searching in BST

```
Search for 5:
      4
     / \
    2   6
   / \ / \
  1  3 5  7

Path: 4 → (5 > 4, go right) → 6 → (5 < 6, go left) → 5 → Found!
Comparisons: 3 (log n)

Compare to array: [1,2,3,4,5,6,7] needs 5 comparisons (linear search)
```

### Example 3: Deleting with Two Children

```
Delete 2 from:
      4
     / \
    2   6
   / \ / \
  1  3 5  7

Step 1: Find inorder successor (min of right subtree)
  Right subtree of 2: node 3
  Min of 3: is 3 itself
  Successor: 3

Step 2: Copy successor value to node
      4
     / \
    3   6     (node value changed 2→3)
   / \ / \
  1  3 5  7

Step 3: Delete successor from right subtree
      4
     / \
    3   6
   /   / \
  1   5   7   (removed duplicate 3)
```

---

## 5️⃣ CRITICAL ANALYSIS — Performance & Robustness

### Complexity Analysis

| Operation | Balanced | Skewed | Notes |
|-----------|----------|--------|-------|
| **Search** | O(log n) | O(n) | Height-dependent |
| **Insert** | O(log n) | O(n) | Search + attach |
| **Delete** | O(log n) | O(n) | Hardest operation |
| **Traverse** | O(n) | O(n) | Visit all nodes |

### Why Skew Happens

```
Insert sorted sequence: 1, 2, 3, 4, 5

Result becomes linked list:
1
 \
  2
   \
    3
     \
      4
       \
        5

Height = 5 (should be ~2 for balanced)
Search becomes O(n)!
Solution: Next week—balanced trees (AVL, Red-Black)
```

### Robustness Issues

**Issue 1: Duplicate Handling**
```python
# Need to decide: allow duplicates or skip?
if val < node.val:
    node.left = insert(node.left, val)
elif val > node.val:
    node.right = insert(node.right, val)
else:
    # val == node.val
    # Option A: Skip (no duplicates)
    # Option B: Add to count field
    # Option C: Store list at each node
```

**Issue 2: Delete Complexity**
Three cases (0, 1, 2 children) make delete complex. Easy to get wrong.

---

## 6️⃣ REAL SYSTEM INTEGRATION — Production Applications

### Database Indexing

```
B-Tree (variant of BST):
- Used by MySQL for primary keys
- Maintains sorted order while supporting insertions
- Every operation: log(n) disk accesses
```

### Autocomplete Systems

```
Trie (similar to BST):
- Each node = letter
- Sorted path = autocomplete suggestions
```

### Operating System Task Scheduling

```
Scheduler uses BST to find next highest-priority task
O(log n) per insert/delete, crucial for performance
```

---

## 7️⃣ CONCEPT CROSSOVERS — Connections

### Week 4.5: Binary Search Returns

```
Binary Search: Look in sorted array
BST: Same idea, but tree-based
- Both exploit sorted data
- Both O(log n) search
- BST is dynamic (supports insert/delete), array doesn't
```

### Days 1-2: Traversals

```
Inorder of BST = sorted values!
That's THE key property we exploit

Delete uses postorder (children before parent)
Insert uses preorder-like (parent pointer before children)
```

### Week 6: Comparison

```
Sorted Array vs BST vs Hash Table:
- Array: O(log n) search, O(n) insert
- BST: O(log n) all, ordered traversal
- Hash: O(1) search (average), unordered
```

---

## 8️⃣ MATHEMATICAL & THEORETICAL — Formal Foundations

### BST Property Proof

**Theorem:** Any BST can be uniquely reconstructed from inorder + preorder

**Proof sketch:**
- Preorder gives root (first element)
- Inorder splits values < root | root | > root
- Recursively reconstruct left/right subtrees
- Uniqueness follows from definition

### Height-Balance Relationship

For BST with n nodes:
- Minimum height: ⌈log₂(n+1)⌉ (perfectly balanced)
- Maximum height: n (linear—skewed)

**Problem:** Insertion order affects height  
**Solution:** Week 5.5—self-balancing trees

---

## 9️⃣ ALGORITHMIC DESIGN INTUITION — Why Design Works

### Why Inorder = Sorted?

```
Inorder visits: Left < Parent < Right (by BST property)
Recursively applies to all subtrees
Result: strictly increasing sequence
```

### Why Delete Uses Successor?

```
When deleting node with 2 children:
- Replace with inorder successor (min of right subtree)
- Why? Successor is smallest value > node
- Maintains BST property after deletion
```

### Why Search Works So Well

```
Binary Search Tree = binary search on dynamic data
- Binary search assumed sorted array
- BST structure maintains order automatically
- No need to pre-sort, insert/delete in real-time
```

---

## 🔟 KNOWLEDGE CHECK — Socratic Reasoning

1. **Why does inorder traversal of ANY BST produce sorted output?** Can you trace through why left < parent < right?

2. **What's the difference between a BST and a random binary tree?** Why can't you search a random tree efficiently?

3. **When deleting a node with two children, why use the inorder successor?** Could you use something else? What would break?

4. **Why does inserting sorted data create a skewed tree?** Can you draw what happens when you insert 1,2,3,4,5 in order?

5. **How would you validate if a tree is a valid BST?** What property must hold at every node?

---

## 1️⃣1️⃣ RETENTION HOOK — Memory Anchors

### **Left < Parent < Right**
```
That's the entire BST property in one line.
Every operation (search, insert, delete) uses this.
```

### **LISR** (Left Is Smaller Right)
```
L < P < R
Helps remember: left smaller, right greater
```

### **Delete Cases: LRB**
```
L: only Left child → replace with left
R: only Right child → replace with right
B: Both children → use inorder successor
```

---

## 📊 SUPPLEMENTARY: BST Operations Complexity

| Operation | Time | Why |
|-----------|------|-----|
| Search | O(h) | Follow path from root |
| Insert | O(h) | Search + attach new node |
| Delete | O(h) | Search + restructure |
| Min | O(h) | Go left until leaf |
| Max | O(h) | Go right until leaf |

h = height (O(log n) balanced, O(n) skewed)

---

## 🔗 EXTERNAL RESOURCES

- LeetCode BST Problems: https://leetcode.com/tag/binary-search-tree/
- GeeksforGeeks BST: https://www.geeksforgeeks.org/binary-search-tree-data-structure/
- Visualizer: https://www.cs.usfca.edu/~galles/visualization/BST.html

---

## 📝 KEY TAKEAWAYS

✅ **BST maintains sorted order with dynamic insert/delete**  
✅ **Search/Insert/Delete all O(log n) in balanced case**  
✅ **Inorder traversal yields sorted values**  
✅ **Delete is complex (3 cases), easy to get wrong**  
✅ **Balanced trees (next week) solve the skewing problem**

**Next:** Day 4 — Heaps & Priority Queues (different tree property, different purpose)

