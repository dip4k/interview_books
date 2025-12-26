# Week 5, Day 4: Heaps & Priority Queues

**Week:** 5 | **Day:** 4 | **Topic:** Heaps & Priority Queues  
**Time:** 75 minutes reading | **Difficulty:** 🔴 Hard  
**Prerequisites:** Days 1-2 (Tree Anatomy, Traversals)  

---

## 1️⃣ THE WHY — Engineering Motivation

### Different Problem, Different Tree

**BST Question:** "Is value X in this set?" (search)  
**Heap Question:** "What's the maximum/minimum value?" (priority)

### Real-World Heaps

- **Dijkstra's Algorithm:** Find nearest unvisited node (min-heap)
- **Task Scheduling:** Always run highest priority task (max-heap)
- **Huffman Coding:** Repeatedly merge lowest frequency nodes (min-heap)
- **Median Finding:** Track median in data stream (min + max heap)

---

## 2️⃣ THE WHAT — Mental Model & Intuition

### Core Concept: Heap Property

**Max-Heap:** Parent ≥ all children (parent is maximum locally)  
**Min-Heap:** Parent ≤ all children (parent is minimum locally)

```
Max-Heap:          Min-Heap:
       9                  1
      / \                / \
     7   8              2   3
    / \                / \
   3   2              4   5

In max-heap: 9 ≥ 7, 9 ≥ 8, 7 ≥ 3, 7 ≥ 2
In min-heap: 1 ≤ 2, 1 ≤ 3, 2 ≤ 4, 2 ≤ 5
```

### Key Insight: NOT Sorted

```
Heap ≠ Sorted tree

BST (sorted):      Max-Heap (not sorted):
       4                    9
      / \                  / \
     2   6                5   8
    / \ / \              / \ /
   1  3 5  7            3  4 6

BST: inorder gives 1,2,3,4,5,6,7
Heap: inorder gives random order
But: max-element is always at root!
```

---

## 3️⃣ THE HOW — Mechanical Walkthrough

### Heap as Array

```python
# Heaps stored in array for cache efficiency
# Parent of i at index i//2
# Left child at 2*i, right at 2*i+1

Array: [9, 7, 8, 3, 2, 1, 5]

Tree view:
       9(0)
      /    \
   7(1)    8(2)
   / \     / \
 3(3) 2(4) 1(5) 5(6)

Index calculation:
- Parent of 3: (3)//2 = 1 → 7 ✓
- Left of 7: 2*1 = 2 → 8... wait wrong!
  
Actually indices 0-based:
- Parent of i: (i-1)//2
- Left of i: 2*i+1
- Right of i: 2*i+2
```

### Insert (Bottom-Up "Bubble Up")

```python
def insert(heap, val):
    heap.append(val)                # Add to end
    
    # Bubble up to maintain heap property
    idx = len(heap) - 1
    while idx > 0:
        parent_idx = (idx - 1) // 2
        if heap[idx] > heap[parent_idx]:  # Max-heap
            heap[idx], heap[parent_idx] = heap[parent_idx], heap[idx]
            idx = parent_idx
        else:
            break

Example: Insert 10 into [9,7,8,3,2,1,5]
[9,7,8,3,2,1,5,10]
     10 > 8? Yes, swap with parent at index 2
[9,7,10,3,2,1,5,8]
     10 > 9? Yes, swap with parent at index 0
[10,7,8,3,2,1,5,9]
     Done, 10 is new root
```

### Delete Root (Top-Down "Bubble Down")

```python
def delete_root(heap):
    if len(heap) == 0:
        return None
    
    root = heap[0]
    heap[0] = heap.pop()  # Move last element to root
    
    # Bubble down
    idx = 0
    while 2*idx + 1 < len(heap):  # Has at least left child
        left = 2*idx + 1
        right = 2*idx + 2
        
        # Find larger child (for max-heap)
        larger = left
        if right < len(heap) and heap[right] > heap[left]:
            larger = right
        
        if heap[idx] < heap[larger]:
            heap[idx], heap[larger] = heap[larger], heap[idx]
            idx = larger
        else:
            break
    
    return root

Example: Delete from [10,7,8,3,2,1,5,9]
Move 9 to root: [9,7,8,3,2,1,5,_]
9 < max(7,8)=8? Yes, swap: [8,7,9,3,2,1,5]
8 > max(3,2)=3? Yes, stay: Done
Result: [8,7,9,3,2,1,5]
```

### Build Heap (Efficient Construction)

```python
def build_heap(arr):
    # Start from last non-leaf, bubble down each
    for i in range(len(arr)//2 - 1, -1, -1):
        bubble_down(arr, i)
    return arr

Time: O(n) not O(n log n)!
Why? Most nodes don't move far, math works out.
```

---

## 4️⃣ VISUALIZATION — Traced Examples

### Example 1: Insert Sequence

```
Insert 5, 10, 3, 20, 15 into empty max-heap

Insert 5:
[5]

Insert 10:
[5,10] → 10 > 5, swap → [10,5]

Insert 3:
[10,5,3]

Insert 20:
[10,5,3,20] → 20 > 5, swap
[10,20,3,5] → 20 > 10, swap
[20,10,3,5]

Insert 15:
[20,10,3,5,15] → 15 > 10? No, stay
[20,10,3,5,15]

Tree view:
       20
      /  \
    10    3
    / \
   5   15
```

### Example 2: Extract Maximum Sequence

```
Extract from [20,10,3,5,15]

Extract 20:
Move 15 to root: [15,10,3,5,_]
15 < max(10,3)=10? No
15 < max(5,15)? Wait, indices wrong...

Index 0: children at 1,2 (10,3)
15 > max(10,3), stay
Result: [15,10,3,5], extracted 20

Extract 15:
Move 5 to root: [5,10,3,_,_]
5 < max(10,3)=10, swap
[10,5,3], 5 < max(children)?
No more children
Result: [10,5,3], extracted 15
```

---

## 5️⃣ CRITICAL ANALYSIS — Performance & Robustness

### Complexity Analysis

| Operation | Time | Why |
|-----------|------|-----|
| **Insert** | O(log n) | Bubble up height |
| **Delete min/max** | O(log n) | Bubble down height |
| **Get min/max** | O(1) | At root |
| **Build heap** | O(n) | Efficient bubble down |
| **Heapify** | O(n log n) | Using insert |

### Space Efficiency

```
Heap stored as array = cache-friendly
No pointers needed (use array indices)
Especially efficient for heapsort
```

### Robustness: No Search

```
Heap doesn't support efficient search!
To find specific element: must scan all O(n)

This is tradeoff for fast min/max
```

---

## 6️⃣ REAL SYSTEM INTEGRATION — Production Applications

### Priority Queue (Abstract Data Type)

```python
import heapq

pq = []
heapq.heappush(pq, (priority, value))  # Insert
priority, value = heapq.heappop(pq)    # Extract min

Used in:
- Dijkstra's algorithm
- Prim's MST
- Huffman encoding
- Load balancing
```

### Heap Sort

```python
def heapsort(arr):
    heapq.heapify(arr)           # Build heap O(n)
    return [heapq.heappop(arr) for _ in range(len(arr))]  # O(n log n)

Total: O(n log n) in-place sorting
```

### Median Finding in Stream

```
Maintain two heaps:
- Max-heap for lower half (max at root)
- Min-heap for upper half (min at root)

Median = middle element(s)
All operations: O(log n)
```

---

## 7️⃣ CONCEPT CROSSOVERS — Connections

### Week 2: Back to Queues

```
Priority Queue = Queue where elements have priority
Regular queue: FIFO (first in, first out)
Priority queue: element with highest priority out first

Heap = efficient implementation of priority queue
```

### Days 1-2: Different Tree Property

```
BST: left < parent < right (sorted)
Heap: parent ≥ children (prioritized)

Same tree, different property!
Enables different operations
```

### Algorithms (Week 6+)

```
Dijkstra: Uses min-heap for "nearest unvisited"
Prim's MST: Uses min-heap for "cheapest edge"
Huffman: Uses min-heap for "lowest frequency"
```

---

## 8️⃣ MATHEMATICAL & THEORETICAL — Formal Foundations

### Heap Property Proof

**Theorem:** For any heap, maximum is at root.

**Proof:** By heap property, parent ≥ children.
Root has no parent. Root ≥ its children.
Recursively, root ≥ all descendants.
Maximum must be a descendant or root.
Therefore root is maximum. ∎

### Complexity of Bubble-Up

Height of heap = ⌈log₂(n)⌉

Bubble-up moves from leaf to root = at most height moves.

Therefore: O(log n) ∎

---

## 9️⃣ ALGORITHMIC DESIGN INTUITION — Why Design Works

### Why Array Representation?

```
Heap property allows direct index calculation
No pointers needed = dense packing
Better cache locality than pointer-based tree

This is why heaps are practical for algorithms
```

### Why Bubble-Up Works?

```
Adding to end preserves heap-property except:
Parent might be smaller than new child
Swap with parent, recurse
Parent of parent might now be smaller
Eventually reach root or parent ≥ child
Heap property restored
```

---

## 🔟 KNOWLEDGE CHECK — Socratic Reasoning

1. **Why is a heap not sorted?** Can you give an example where inorder traversal isn't in order?

2. **Why is search O(n) in a heap?** Could you search efficiently in a BST? What's the difference?

3. **How does building a heap from scratch differ from repeatedly inserting?** Why is O(n) vs O(n log n)?

4. **Can you use a heap as a sorted container?** What would happen if you kept extracting the root?

5. **Why use two heaps (max + min) to find median?** How would you keep them balanced?

---

## 1️⃣1️⃣ RETENTION HOOK — Memory Anchors

### **"Priority Wins"**
Heap finds priority element (max or min) instantly
Trade-off: No efficient search elsewhere

### **"Array is Heap"**
Heap stored as array with index arithmetic
No pointers needed!

### **"Bubble Up, Bubble Down"**
Insert: bubble up (smaller → larger)
Delete: bubble down (smaller → larger)

---

## 📊 SUPPLEMENTARY: Heap vs BST

| Property | Heap | BST |
|----------|------|-----|
| **Sorted** | No | Yes |
| **Get min/max** | O(1) | O(log n) |
| **Search** | O(n) | O(log n) |
| **Insert** | O(log n) | O(log n) |
| **Space** | Array | Pointers |

---

## 🔗 EXTERNAL RESOURCES

- Python heapq: https://docs.python.org/3/library/heapq.html
- LeetCode Heap Problems: https://leetcode.com/tag/heap/
- Heap Visualization: https://www.cs.usfca.edu/~galles/visualization/Heap.html

---

## 📝 KEY TAKEAWAYS

✅ **Heap = efficiently get min/max (O(1) access, O(log n) insert/delete)**  
✅ **Different from BST: not sorted, but prioritized**  
✅ **Implemented as array, not pointers**  
✅ **Bubble-up for insert, bubble-down for delete**  
✅ **Foundation for priority queues and many algorithms**

**Next:** Day 5 — Balanced Trees (solving BST skewing with rotations)

