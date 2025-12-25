# 🧠 DSA Deep-Dive: Week 2, Day 3
## Linked Lists: Singly vs. Doubly Linked Logic and Pointer Manipulation

---

## 1. The "Why" (Engineering Motivation)

You're designing an LRU (Least Recently Used) cache for a web browser. When a user visits pages, you need to:

1. **Track access order** - Most recently used → front, Least recently → back
2. **Move pages on access** - User revisits page 5? Move it to front
3. **Remove oldest on overflow** - Cache full? Delete least recent

**Option A: Using an Array**
```python
cache = [page1, page2, page3, page4, page5]  # Recently used first

# Access page3:
cache.remove(page3)   # O(n) - must shift all elements
cache.insert(0, page3) # O(n) - must shift everything
# Total: O(n) per access!

# For 1000 page accesses:
# 1000 × O(n) = O(n²) total time
# TERRIBLE PERFORMANCE
```

**Option B: Using a Linked List**
```python
head → page5 ↔ page4 ↔ page3 ↔ page2 ↔ page1 → tail
       (oldest)                    (newest)

# Access page3:
# If we have pointer to page3:
#   Remove: Unlink node from neighbors (O(1))
#   Move to front: Link to head (O(1))
# Total: O(1) per access!

# For 1000 page accesses:
# 1000 × O(1) = O(n) total time
# 1000x FASTER than arrays!
```

**The insight:** Linked lists excel when you need efficient insertion/deletion. You trade random access speed for insertion speed. Understanding when that trade-off makes sense is crucial.

---

## 2. The Mental Model (The "What")

Imagine a **chain of children holding hands**.

**Singly Linked List:**
```
child1 → child2 → child3 → child4 → NULL
  (holds right)  (holds right)
  
To find child3:
- Start at child1
- Follow hand: child1 → child2
- Follow hand: child2 → child3 ✓ Found

Each child knows only the next child.
To go backward: IMPOSSIBLE (no left hand)
```

**Doubly Linked List:**
```
NULL ← child1 ↔ child2 ↔ child3 ↔ child4 → NULL
        (left)   (right)  (left)  (right)

Each child holds both left and right hands.
Can move forward AND backward.
More flexibility, more memory (extra pointer).
```

---

## 3. Under the Hood (The "How")

### 3.1 Node Structure

**Singly Linked Node:**

```
┌─────────────────────────────────┐
│ Node                            │
├─────────────────────────────────┤
│ data:     value stored          │ (4-8 bytes)
│ next:     pointer to next node  │ (8 bytes on 64-bit)
├─────────────────────────────────┤
│ Total:    16 bytes per node     │
└─────────────────────────────────┘
```

**Doubly Linked Node:**

```
┌─────────────────────────────────┐
│ Node                            │
├─────────────────────────────────┤
│ prev:     pointer to prev node  │ (8 bytes)
│ data:     value stored          │ (4-8 bytes)
│ next:     pointer to next node  │ (8 bytes)
├─────────────────────────────────┤
│ Total:    24 bytes per node     │
└─────────────────────────────────┘
```

### 3.2 Memory Layout (Non-Contiguous)

**Arrays (from Week 2, Day 1):**
```
Memory:
0x1000: [10]
0x1008: [20]
0x1010: [30]
0x1018: [40]

Contiguous! All adjacent.
```

**Linked Lists:**
```
Memory (fragmented):
0x1000: [data: 10, next: 0x3000] → points to
0x3000: [data: 20, next: 0x5000] → points to
0x2000: [data: 30, next: 0x4000] → points to (JUMP!)
0x4000: [data: 40, next: NULL]

Non-contiguous! Scattered across memory!
Cache misses on every traversal.
```

### 3.3 Pointer Manipulation Mechanics

**Inserting after a node:**

```
Before:
node1 → node2 → node3 → NULL
^
|
current pointer

Insert newNode between node1 and node2:

Step 1: Create newNode
newNode.next = NULL (initially)

Step 2: Get reference to what node1 pointed to
saved_next = node1.next  // node2

Step 3: Make node1 point to newNode
node1.next = newNode

Step 4: Make newNode point to what node1 used to point to
newNode.next = saved_next  // node2

After:
node1 → newNode → node2 → node3 → NULL
```

**Removing a node:**

```
Before:
node1 → node2 → node3 → NULL
        ^
        |
        pointer to remove

Step 1: Find previous node
prev = node1

Step 2: Make previous skip the node
prev.next = node2.next  // node3

After:
node1 → node3 → NULL
(node2 is now orphaned, can be garbage collected)
```

---

## 4. Visual Walkthrough: LRU Cache Example

**Scenario:** Cache with capacity 3. Pages accessed in order: 1, 2, 3, 4

### Initial State
```
head ↔ tail
(empty cache)
```

### Access Page 1
```
head ↔ [1] ↔ tail
size = 1
```

### Access Page 2
```
head ↔ [2] ↔ [1] ↔ tail
size = 2
(2 is most recent, goes to front)
```

### Access Page 3
```
head ↔ [3] ↔ [2] ↔ [1] ↔ tail
size = 3
(at capacity, but all pages fit)
```

### Access Page 4 (Cache Full!)
```
Step 1: Page 4 accessed (not in cache)
Step 2: Cache full, remove least recent (page 1)
Step 3: Add page 4 to front

head ↔ [4] ↔ [3] ↔ [2] ↔ tail
size = 3
(Page 1 is evicted)

Operations:
- Remove page 1 from end: O(1) with doubly linked (or keep tail pointer)
- Add page 4 to front: O(1)
- Total: O(1)
```

### Access Page 2 Again
```
Current:
head ↔ [4] ↔ [3] ↔ [2] ↔ tail

Step 1: Page 2 accessed (found!)
Step 2: Remove page 2 from middle
Step 3: Add page 2 to front

head ↔ [2] ↔ [4] ↔ [3] ↔ tail

Operations:
- Remove from middle: O(1) with pointer to node
- Add to front: O(1)
- Total: O(1) per access
```

---

## 5. Critical Analysis

### 5.1 Time Complexity Comparison

| Operation | Array | Linked List |
|-----------|-------|------------|
| Access (random) | O(1) | O(n) |
| Search | O(n) | O(n) |
| Insert at front | O(n) | O(1) |
| Insert at end | O(1)* | O(1) |
| Insert at position | O(n) | O(n)** |
| Delete from front | O(n) | O(1) |
| Delete from end | O(n) | O(1)* |
| Delete from middle | O(n) | O(1)** |

*Array: O(1) amortized append
**Assuming you have pointer to the node already

### 5.2 Space Complexity

**Array (size n):**
```
Space = n × element_size
Example: 1000 integers = 4000 bytes (mostly data)
Overhead: Minimal (just capacity)
```

**Singly Linked List (size n):**
```
Space = n × (element_size + pointer_size)
Example: 1000 integers = 1000 × (4 + 8) = 12,000 bytes
Overhead: 3x more memory than array!

Memory cost per node: 8 bytes (pointer)
```

**Doubly Linked List (size n):**
```
Space = n × (element_size + 2×pointer_size)
Example: 1000 integers = 1000 × (4 + 16) = 20,000 bytes
Overhead: 5x more memory than array!

Memory cost per node: 16 bytes (two pointers)
```

### 5.3 Cache Performance

**Arrays: Cache-friendly**
```
Traversal: [10] → [20] → [30] → [40]
Memory:     0x1000   0x1008   0x1010   0x1018

Sequential addresses = 1 cache miss for every 8 elements
Cache hit rate: ~90%
Speed: ~4ns per access (cache hit)
```

**Linked Lists: Cache-unfriendly**
```
Traversal: 0x1000 → 0x3000 → 0x2000 → 0x4000
Memory:    scattered!

Random addresses = cache miss for almost every element
Cache hit rate: ~5%
Speed: ~100ns per access (cache miss)

20x SLOWER than arrays for traversal!
```

### 5.4 Edge Cases

**1. Single-node list**
```
head ↔ [value] ↔ tail
- Insert after: Easy, O(1)
- Remove: Easy, O(1)
```

**2. Removing from middle (without pointer)**
```
To remove node X from middle:
head → ... → A → X → B → ...
              ↑       ↑
              Must have pointers to both!
              
Without pointer to X: Must traverse from head = O(n)
With pointer to X: O(1) in doubly linked, O(n) in singly
```

**3. Very large list (millions of nodes)**
```
Traversal from head to tail:
- Array: Cache misses slow, but predictable O(n)
- Linked list: Terrible cache locality, O(n) but 20x slower
```

---

## 6. System Connection

### Linux Kernel: Process Scheduling

```c
// Linux uses doubly linked lists for process queues
typedef struct list_head {
    struct list_head *next, *prev;
} list_head;

struct task_struct {
    // Process info
    pid_t pid;
    char *comm;
    
    // Linked into various queues
    list_head run_list;    // Ready queue
    list_head wait_list;   // Wait queue
    // ...
};
```

**Why linked lists?**
- Processes added/removed frequently
- Need O(1) insertion/deletion
- Cache misses don't matter (context switches are expensive anyway)

---

## 7. Knowledge Check

**Question 1: Pointer Manipulation**

You have: `A → B → C → D → NULL`

Insert X between B and C. Write out the operations.

---

**Question 2: LRU Cache**

Design an LRU cache with 4 capacity:
```
Access sequence: 1, 2, 3, 4, 5, 1, 6

After each access, show:
- Current cache state
- What was evicted (if full)
- Time complexity of operation
```

---

**Question 3: Array vs. Linked List Decision**

You need a data structure that:
- Has 1 million elements
- Need to frequently insert/delete at front (10,000 times/sec)
- Need to traverse all elements once per second
- Have 8GB RAM available

Which would you use? Why?

---

## Summary: Day 3 Core Concepts

**Singly Linked Lists:**
- **Access:** O(n) - must traverse
- **Insert/Delete at known position:** O(1) - with pointer
- **Insert/Delete without pointer:** O(n) - must search first
- **Memory:** 3x more than arrays (pointer overhead)

**Doubly Linked Lists:**
- **Same operations as singly, but:**
- **Access from end:** O(1) possible (have prev pointer)
- **Delete from end:** O(1) (with pointer)
- **Memory:** 5x more than arrays (two pointers)

**When to use Linked Lists:**
- ✅ Frequent insertions/deletions
- ✅ LRU caches, FIFO queues, stacks
- ✅ Unknown size with dynamic growth
- ✅ Don't need random access

**When to avoid:**
- ❌ Need random access (array is 20x faster)
- ❌ Traversal performance matters (arrays are cache-friendly)
- ❌ Memory is constrained (pointers add 3-5x overhead)

---

**End of Day 3: Linked Lists Deep-Dive**
