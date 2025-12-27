# Week 2: Linear Structures — Summary & Key Concepts

## 📖 Week Overview

**Week 2 teaches the fundamental data structures** that appear in nearly every problem. After Week 1's theoretical tools (Big-O, RAM, recursion), you now learn the practical building blocks.

**Central theme:** **Trade-offs.** No universal best structure. Choose based on your access pattern.

---

## 📊 Algorithm Comparison Table

| Structure | Access | Insert Mid | Delete Mid | Space | Cache | Use Case |
|-----------|--------|------------|------------|-------|-------|----------|
| **Array** | O(1) | O(n) | O(n) | O(n) | ✅ Excellent | Indexed data, sequential access |
| **Vector** | O(1) | O(n) | O(n) | O(n) | ✅ Excellent | Dynamic growth, unknown size |
| **LinkedList** | O(n) | O(1)* | O(1)* | O(n) | ❌ Terrible | Undo/redo, allocators (rare!) |
| **Stack** | - | O(1)† | O(1)† | O(n) | ✅ Good | LIFO (undo, recursion) |
| **Queue** | - | O(1)† | O(1)† | O(n) | ✅ Good | FIFO (scheduling, BFS) |
| **BinarySearch** | O(log n) | - | - | O(1) | ✅ Excellent | Sorted lookup |

*At known position †Push/pop or enqueue/dequeue

---

## 🧠 Mental Models Per Day

### Day 1: Arrays
**Picture:** Numbered mailboxes on a street. Walk to mailbox i instantly.  
**Key:** Direct addressing via arithmetic. O(1) to any element.

### Day 2: Dynamic Arrays  
**Picture:** Theater expanding when full. Seats double each time.  
**Key:** Exponential growth = O(log n) resizes = O(n) total copies = O(1) amortized per append.

### Day 3: Linked Lists
**Picture:** Treasure hunt with clue cards, each pointing to next.  
**Key:** Follow chain to reach position (O(n)). Relink pointers fast (O(1)).

### Day 4: Stacks & Queues
**Picture:** Plate stack (LIFO) vs checkout line (FIFO).  
**Key:** Different access orderings, both O(1) for their operations.

### Day 5: Binary Search
**Picture:** Guessing game that eliminates half with each guess.  
**Key:** Halve search space each step = O(log n).

---

## 🔑 Key Insights

### Insight 1: Cache Dominates Real Performance
- **Theory:** Array O(n) scan = List O(n) scan
- **Practice:** Array ~5ms, List ~250ms (50x!)
- **Why:** Cache prefetching works for contiguous, fails for scattered pointers

### Insight 2: Exponential Growth is Optimal
- Linear growth (+k): O(n) resizes, O(n²) total cost
- Exponential growth (×2): O(log n) resizes, O(n) total cost
- **Benefit:** Log factor difference in total cost

### Insight 3: The Pointer-Chasing Caveat
- "Insert O(1) in lists" ✗ (misleading without context)
- "Insert O(1) IF you have pointer to position" ✓
- Total insertion cost often O(n) (need to find position)

### Insight 4: Arrays Default, Others Rare
- 95% of problems: arrays or dynamic arrays
- 5%: lists for undo/redo, allocators, caches
- Consensus in industry: use vectors by default

### Insight 5: Binary Search is Powerful
- O(log n) for n=1M: 20 comparisons
- Precondition (sorted) is **critical and often overlooked**

---

## 🎯 Common Problem Patterns

### Pattern 1: Choose Data Structure
**Example:** "Need to insert/remove at arbitrary positions"
1. If frequent mid-operations → Linked list
2. If mostly append → Dynamic array
3. If need random access → Array + re-allocate on insert

### Pattern 2: Analyze Structure Complexity
**Example:** "What's total cost of n appends to empty vector?"
1. Resizes at: n=2, 4, 8, 16, ...
2. Total copies: 1+2+4+8+... ≈ 2n
3. Amortized: 2n / n = O(1) per append

### Pattern 3: Recognize Real-World Structure Choices
**Example:** "Database uses B-tree for indexing"
1. B-tree nodes: arrays (fast search within node)
2. Chaining: linked lists (handle collisions)
3. Reasoning: cache-friendly arrays + dynamic lists

---

## ❌ Common Misconceptions Fixed

### ❌ "Insert O(1) in list, O(n) in array, so list wins"
✅ **Reality:** Finding insertion point O(n) in list too. Total O(n) both ways.

### ❌ "Amortized O(1) means no pauses"
✅ **Reality:** Occasional O(n) pauses happen. Averaged over n operations = O(1).

### ❌ "Dynamic arrays waste memory (capacity > size)"
✅ **Reality:** 25% waste on average. Trade space for time savings is good deal.

### ❌ "Linked list better for unknown size"
✅ **Reality:** Dynamic arrays better (cache, simple, standard).

### ❌ "Binary search O(log n) so always use"
✅ **Reality:** Requires sorted data. Linear search is O(n) but works unsorted.

---

## 📈 Mastery Progression Levels

### Level 1: Recognition (Days 1-2)
- [ ] Name the structure
- [ ] State its main operations' complexity
- [ ] Give one real example

### Level 2: Understanding (Days 3-4)
- [ ] Explain WHY complexity is what it is
- [ ] Compare two structures
- [ ] Analyze given code

### Level 3: Application (Days 5+)
- [ ] Choose structure for problem
- [ ] Implement correctly
- [ ] Trace operations by hand

### Level 4: Mastery (Week 3+)
- [ ] Combine structures (hashtable + list)
- [ ] Recognize subtle patterns
- [ ] Optimize real systems

---

## 🔗 Week 2 → Week 3+ Connections

**Week 3: Sorting & Hashing**
- Sorting works on arrays (Week 2)
- Hash table buckets are arrays
- Chaining uses linked lists

**Week 4: Problem-Solving Patterns**
- Two pointers on sorted arrays (binary search)
- Sliding window on arrays
- Prefix sums on arrays

**Week 4.5: Tier 1 Patterns**
- Monotonic stack combines stack + deque
- Merge operations on arrays/lists
- Hash maps use array buckets

**Weeks 6+: Advanced**
- Graphs use adjacency lists
- Queues for BFS
- Trees built on arrays or pointers

---

## ❓ Quick-Reference FAQ

**Q: Should I use array or list?**
A: Array ~95% of the time. List only for undo/redo, allocators, LRU caches.

**Q: How much memory does vector waste?**
A: Average 25% (capacity ranges from n to 2n).

**Q: Can I binary search a linked list?**
A: No. Requires random access. Binary search only on arrays or skip lists.

**Q: Is insertion always O(n)?**
A: No. Insert at end of vector: O(1) amortized. Insert at known position in list: O(1). Insert at known position in array: O(n) (must shift).

**Q: Why is cache speed critical?**
A: Memory latency: 200ns. Cache hit: 5ns. 40x difference. Contiguity matters.

---

## ✨ Week 2 Key Takeaway

> **Master these trade-offs. Arrays for access, lists for rearrangement (rare), stacks for LIFO, queues for FIFO, binary search for sorted lookup. This week is your foundation.**

---

## 🎓 Before Week 3

**Confidence Check:**
- [ ] Rate yourself 4/5 or higher on each day
- [ ] Can you explain cache impact?
- [ ] Can you choose the right structure for a problem?
- [ ] Can you derive amortized complexity?

**If not ready:** Spend 1-2 more days on weak areas.

