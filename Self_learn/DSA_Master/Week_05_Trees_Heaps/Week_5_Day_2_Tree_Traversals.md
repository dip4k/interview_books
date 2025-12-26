# Week 5, Day 2: Tree Traversals

**Week:** 5 | **Day:** 2 | **Topic:** Tree Traversals  
**Time:** 75 minutes reading | **Difficulty:** 🔴 Hard  
**Prerequisites:** Day 1 (Binary Tree Anatomy)  

---

## 1️⃣ THE WHY — Engineering Motivation

### Why Traversals Matter

**Single question:** How do you visit every node in a tree?

**Answer:** 4 different ways, each revealing different information:
- **Preorder:** Parent first (useful: cloning trees, evaluating expressions)
- **Inorder:** Middle (useful: sorted output from BST)
- **Postorder:** Parent last (useful: deleting trees, post-process evaluation)
- **Level-Order:** Row by row (useful: queue-based algorithms, shortest paths)

### Real-World Applications

```
Compiler AST (Abstract Syntax Tree):
  Preorder: Parse expression
  Postorder: Evaluate bottom-up
  
File System Backup:
  Postorder: Backup children before parent
  
Network Routing:
  Level-order: BFS shortest path
```

---

## 2️⃣ THE WHAT — Mental Model & Intuition

### Core Concept: Three Moments Per Node

For every node, you have **three moments** to take action:
1. **Before visiting children** (preorder)
2. **Between left and right child** (inorder)
3. **After visiting children** (postorder)

```
       1
      / \
     2   3

Timeline for node 2:
[preorder: 2] → visit left → visit right → [postorder: 2]
                                           ↑ inorder: 2
```

### Visualization: Circular Walk

Imagine **walking around the tree in a circle**:
```
        1
       / \
      2   3
     /
    4

Circular walk (return to each node 3 times):
1 ← preorder
├─ 2 ← preorder  
│  ├─ 4 ← preorder
│  │  4 ← postorder
│  2 ← inorder
│  2 ← postorder
1 ← inorder
└─ 3 ← preorder
   3 ← inorder
   3 ← postorder
1 ← postorder

Extract at different points:
Preorder:  1, 2, 4, 3
Inorder:   4, 2, 1, 3
Postorder: 4, 2, 3, 1
```

---

## 3️⃣ THE HOW — Mechanical Walkthrough

### Recursive Implementations

**Preorder (Root → Left → Right):**
```python
def preorder(node):
    if not node:
        return []
    return [node.val] + preorder(node.left) + preorder(node.right)
    # Process root first, then children
```

**Inorder (Left → Root → Right):**
```python
def inorder(node):
    if not node:
        return []
    return inorder(node.left) + [node.val] + inorder(node.right)
    # Process left, then root, then right
    # For BST: produces sorted order!
```

**Postorder (Left → Right → Root):**
```python
def postorder(node):
    if not node:
        return []
    return postorder(node.left) + postorder(node.right) + [node.val]
    # Process children first, then root
```

**Level-Order (BFS with Queue):**
```python
from collections import deque

def level_order(root):
    if not root:
        return []
    
    result = []
    queue = deque([root])
    
    while queue:
        node = queue.popleft()
        result.append(node.val)
        
        if node.left:
            queue.append(node.left)
        if node.right:
            queue.append(node.right)
    
    return result
    # Queue ensures level-by-level processing
```

### Iterative Implementations (Using Stack)

**Preorder Iterative:**
```python
def preorder_iterative(root):
    if not root:
        return []
    
    result = []
    stack = [root]
    
    while stack:
        node = stack.pop()
        result.append(node.val)
        
        if node.right:
            stack.append(node.right)  # Push right first
        if node.left:
            stack.append(node.left)   # Push left second (popped first!)
    
    return result
```

---

## 4️⃣ VISUALIZATION — Traced Examples

### Example 1: All Four Traversals on Same Tree

```
Tree:
        1
       / \
      2   3
     / \
    4   5

Preorder (parent first):    1, 2, 4, 5, 3
  Visit 1 first
  Then traverse left: 2, 4, 5
  Then traverse right: 3

Inorder (left, parent, right): 4, 2, 5, 1, 3
  Left subtree of 1: 4, 2, 5
  Visit 1
  Right subtree of 1: 3

Postorder (children, then parent): 4, 5, 2, 3, 1
  Left subtree: 4, 5, 2
  Right subtree: 3
  Visit 1

Level-Order (top to bottom): 1, 2, 3, 4, 5
  Level 0: 1
  Level 1: 2, 3
  Level 2: 4, 5
```

### Example 2: Tracing Recursive Inorder

```
Tree:
       1
      / \
     2   3

Trace inorder(1):
  inorder(1.left=2):
    inorder(2.left=None): return []
    append 2: [2]
    inorder(2.right=None): return []
    return [2]
  append 1: [2, 1]
  inorder(1.right=3):
    inorder(3.left=None): return []
    append 3: [3]
    inorder(3.right=None): return []
    return [3]
  return [2, 1, 3]

Result: [2, 1, 3] ✓ Inorder
```

---

## 5️⃣ CRITICAL ANALYSIS — Performance & Robustness

### Complexity Analysis

| Traversal | Time | Space | Notes |
|-----------|------|-------|-------|
| **Preorder** | O(n) | O(h) | Must visit every node once |
| **Inorder** | O(n) | O(h) | Same as preorder |
| **Postorder** | O(n) | O(h) | Same as preorder |
| **Level-Order** | O(n) | O(w) | w = max width (at widest level) |

Where **h = height**, **n = total nodes**

### Why O(h) Space?

```
Recursive traversal uses call stack:
- Best case (balanced): h = log n → O(log n) space
- Worst case (skewed): h = n → O(n) space

Level-order uses explicit queue:
- Best case (skewed line): w = 1 → O(1) space
- Worst case (complete): w = n/2 → O(n) space
```

### Edge Cases to Handle

**Empty tree:**
```python
if not node:
    return []  # Must return early!
```

**Single node:**
```python
      1
# All traversals: [1]
```

**Skewed tree (linked list):**
```python
  1
   \
    2
     \
      3

Recursive depth = 3
Could cause stack overflow for very deep trees
→ Use iterative approach for safety
```

---

## 6️⃣ REAL SYSTEM INTEGRATION — Production Applications

### Compiler Design (Expression Trees)

```
Expression: (2 + 3) * 5

Parse to AST:
        *
       / \
      +   5
     / \
    2   3

Postorder evaluation: 2, 3, +, 5, *
→ (2+3) = 5, then 5*5 = 25

Compiler evaluates bottom-up (postorder)
```

### File System Deletion

```
/home/
  ├─ user1/
  │  ├─ file1.txt
  │  └─ file2.txt
  └─ user2/
     └─ file3.txt

Delete /home: Must delete children first (postorder)
1. Delete file1.txt
2. Delete file2.txt
3. Delete user1/ (now empty)
4. Delete file3.txt
5. Delete user2/ (now empty)
6. Delete /home/ (now empty)

Postorder = delete safely!
```

### Graph Traversal (BFS)

```
Level-order traversal = Breadth-First Search

       1
      / \
     2   3
    / \
   4   5

BFS from 1: 1, 2, 3, 4, 5
(Discovers neighbors before going deep)

Used for:
- Shortest path in unweighted graphs
- Network broadcasts
- Peer discovery in distributed systems
```

---

## 7️⃣ CONCEPT CROSSOVERS — Connections

### Week 2: Stacks & Queues Return

```
Preorder (iterative): Uses STACK
Inorder (iterative): Uses STACK
Postorder (iterative): Uses STACK
Level-order: Uses QUEUE

Trees + traversals = trees don't exist without stacks/queues!
```

### Week 4: Pattern Recognition

```
Binary Search (Week 4.5): One "search path"
Tree Traversals (Week 5): Visit ALL nodes systematically

Same divide-and-conquer idea:
- Eliminate half (binary search)
- Visit subtrees (tree traversals)
```

### Connection to Graphs (Week 5.5+)

```
Trees are special graphs with:
- No cycles
- Single root
- Every node reachable from root

Tree traversals = Graph traversal on acyclic graphs
DFS (depth-first) = Preorder/Postorder
BFS (breadth-first) = Level-order
```

---

## 8️⃣ MATHEMATICAL & THEORETICAL — Formal Foundations

### Traversal Order Theorem

For any binary tree, traversals have relationship:

```
Preorder = [Root | Preorder(Left) | Preorder(Right)]
Inorder = [Inorder(Left) | Root | Inorder(Right)]
Postorder = [Postorder(Left) | Postorder(Right) | Root]

Given any two traversal orders, can reconstruct tree uniquely!
(Exception: Preorder + Postorder alone insufficient)
```

### Proving Inorder Gives Sorted BST Values

**Theorem:** Inorder traversal of BST yields sorted sequence.

**Proof:**
- By definition of BST: left subtree < parent < right subtree
- Inorder visits left, then parent, then right
- Therefore values increase: Left's values < Parent < Right's values
- Recursively applies to subtrees
- Result: strictly increasing sequence ∎

---

## 9️⃣ ALGORITHMIC DESIGN INTUITION — Why Design Works

### Why Preorder for Cloning?

```
To clone a tree, need parent before children:

def clone(node):
    if not node:
        return None
    
    new_node = TreeNode(node.val)  # Create parent first!
    new_node.left = clone(node.left)   # Then children
    new_node.right = clone(node.right)

Why preorder? Parent pointer must exist before creating children!
```

### Why Postorder for Deletion?

```
To delete a tree, need children before parent:

def delete(node):
    if not node:
        return
    
    delete(node.left)      # Delete children first
    delete(node.right)
    free(node)             # Then delete parent

Why postorder? Can't free parent until children freed!
```

### Why Level-Order Reveals Structure?

```
Queue ensures we process all nodes at level i
before any node at level i+1

       1          Queue: [1]
      / \         Dequeue 1, add 2,3: [2, 3]
     2   3        Dequeue 2, add 4,5: [3, 4, 5]
    / \           Dequeue 3: [4, 5]
   4   5          Process all level 1 before level 2
```

---

## 🔟 KNOWLEDGE CHECK — Socratic Reasoning

1. **Why does inorder traversal of a BST give sorted output?** Can you prove this by thinking about BST properties (left < parent < right)?

2. **What's the relationship between tree height and stack space in recursive traversals?** Could a very deep tree cause a stack overflow?

3. **Why do iterative preorder and preorder recursive produce same output?** Why does iterative push right then left (not left then right)?

4. **Given preorder [1,2,4,5,3] and inorder [4,2,5,1,3], can you reconstruct the tree?** How would you approach this?

5. **Why use level-order (BFS) instead of preorder (DFS) in some cases?** What does level-order reveal that preorder doesn't?

---

## 1️⃣1️⃣ RETENTION HOOK — Memory Anchors

### Three Moments = Three Traversals

```
PREORDER:  (Parent) Left Right     → Parent first
INORDER:   Left (Parent) Right     → Middle  
POSTORDER: Left Right (Parent)     → Parent last
```

### Application Anchors

```
PREORDER → ClOning (copy Parent before children)
INORDER → **I**ncreasing (sorted output)
POSTORDER → **P**arent last (delete/free parent last)
LEVEL-ORDER → **L**evel-by-level (BFS shortest path)
```

### Stack vs Queue

```
Recursive (implicit stack) = DFS = Preorder/Postorder
Explicit stack (iterative) = DFS = Preorder/Postorder  
Explicit queue = BFS = Level-order
```

---

## 📊 SUPPLEMENTARY: Traversal Comparison Table

| Traversal | Order | Use Case | Implementation |
|-----------|-------|----------|-----------------|
| **Preorder** | Parent, Left, Right | Cloning, prefix evaluation | Recursive or stack |
| **Inorder** | Left, Parent, Right | BST sorted output | Recursive or stack |
| **Postorder** | Left, Right, Parent | Deletion, postfix evaluation | Recursive or stack |
| **Level-Order** | Top to bottom, left to right | BFS, shortest path | Queue (iterative only) |

---

## 🔗 EXTERNAL RESOURCES

**Visualization:**
- Traversal Visualizer: https://www.cs.usfca.edu/~galles/visualization/BinarySearchTree.html
- GeeksforGeeks Traversal: https://www.geeksforgeeks.org/tree-traversals-inorder-preorder-postorder/

**Practice:**
- LeetCode Binary Tree Traversal: https://leetcode.com/problems/binary-tree-inorder-traversal/
- Binary Tree Preorder: https://leetcode.com/problems/binary-tree-preorder-traversal/
- Binary Tree Postorder: https://leetcode.com/problems/binary-tree-postorder-traversal/

---

## 📝 KEY TAKEAWAYS

✅ **Four traversals: Preorder, Inorder, Postorder, Level-Order**  
✅ **Each reveals different structure (parent first, sorted, children first, level)**  
✅ **Can be implemented recursively (stack) or iteratively**  
✅ **Inorder of BST = sorted values**  
✅ **Traversals are foundations for DFS/BFS algorithms**

**Next:** Day 3 — Binary Search Trees (using traversals to maintain sorted order)

