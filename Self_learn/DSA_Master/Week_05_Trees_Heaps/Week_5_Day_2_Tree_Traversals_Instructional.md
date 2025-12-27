# Week 5, Day 2: Tree Traversals

## 🗓 Metadata
**Week:** 5 | **Day:** 2 of 5 | **Topic:** Tree Traversals  
**Difficulty:** 🟡 Medium | **Time:** 90-120 minutes

---

## 1️⃣ THE WHY

Process all nodes in specific order without storing all in memory simultaneously. Essential for searching, serialization, expression evaluation.

---

## 2️⃣ THE WHAT

Four traversal patterns:
- **In-order:** Left, Node, Right (BST → sorted)
- **Pre-order:** Node, Left, Right (cloning, serialization)
- **Post-order:** Left, Right, Node (deletion, cleanup)
- **Level-order:** BFS (breadth-first, level by level)

---

## 3️⃣ THE HOW

**In-order (Left, Node, Right):**
```
def inorder(node):
  if node:
    inorder(node.left)
    print(node.val)
    inorder(node.right)
Cost: O(n) time, O(h) space (recursion stack)
```

**Pre-order (Node, Left, Right):**
```
Process node first, then children.
Used for cloning: create new node, then recurse.
```

**Post-order (Left, Right, Node):**
```
Process children first, then node.
Used for deletion: delete children before parent.
```

**Level-order (BFS):**
```
Use queue, process one level at a time.
Cost: O(n) time, O(width) space
```

---

## 4️⃣ VISUALIZATION

**Example tree:**
```
    1
   / \
  2   3
 / \
4   5
```

**In-order:** 4,2,5,1,3 (sorted for BST)  
**Pre-order:** 1,2,4,5,3 (useful for cloning)  
**Post-order:** 4,5,2,3,1 (useful for deletion)  
**Level-order:** 1,2,3,4,5 (breadth-first)

---

## 5️⃣ CRITICAL ANALYSIS

| Traversal | Time | Space | When |
|-----------|------|-------|------|
| **In-order** | O(n) | O(h) | BST → sorted |
| **Pre-order** | O(n) | O(h) | Cloning, serialization |
| **Post-order** | O(n) | O(h) | Deletion, bottom-up |
| **Level-order** | O(n) | O(w) | BFS, nearest neighbors |

---

## 6️⃣-1️⃣1️⃣ CORE CONCEPTS

**Real systems:** Expression evaluation (postfix), DOM rendering (depth-first), nearest neighbor search (BFS).

**One-Liner:**
> **Tree Traversal: O(n) processing of all nodes in specific order (in/pre/post/level). Choose order by use case.**

**Cognitive Lenses:**
| **Computational** | Each node visited once; stack/queue management |
| **Psychological** | In-order feels natural (left-root-right like reading) |
| **Design** | Recursive vs iterative; memory stack vs explicit queue |
| **AI/ML** | Similar to: DFS vs BFS in graph exploration |
| **Historical** | Traversal algorithms fundamental since 1950s |

