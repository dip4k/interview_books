# Week 2: Linear Structures — Guidelines

## 📅 Daily Breakdown & Time Allocation

**Total Week:** 10-12 hours (2-2.5 hours per day)

| Day | Topic | Time | Core Concepts | Practice |
|-----|-------|------|---------------|----------|
| **1** | Arrays | 2.5h | Direct addressing, O(1) access, cache | 10 problems |
| **2** | Dynamic Arrays | 2.5h | Exponential growth, amortized analysis | 8 problems |
| **3** | Linked Lists | 2.5h | Pointer-based, O(n) access, O(1) relink | 8 problems |
| **4** | Stacks & Queues | 2h | LIFO/FIFO, O(1) ops, circular buffer | 8 problems |
| **5** | Binary Search | 2h | Divide-by-2, O(log n), preconditions | 8 problems |
| **Weekend** | Integration | 2h | Synthesis, comparison, patterns | Review all |

---

## 🎯 Learning Objectives

### By End of Day 1 (Arrays)
- [ ] Understand direct addressing: address = base + index × size
- [ ] Know array access is O(1)
- [ ] Know insertion/deletion is O(n)
- [ ] Understand cache locality impact
- [ ] Can explain when to use arrays

### By End of Day 2 (Dynamic Arrays)
- [ ] Understand exponential growth strategy
- [ ] Know amortized O(1) append
- [ ] Understand why 2x is better than +k growth
- [ ] Can calculate total cost for n appends

### By End of Day 3 (Linked Lists)
- [ ] Understand pointer-based access (O(n))
- [ ] Know O(1) insertion/deletion at known position
- [ ] Know cache behavior is poor
- [ ] Understand when lists are appropriate (rarely!)

### By End of Day 4 (Stacks & Queues)
- [ ] Understand LIFO (stack) and FIFO (queue) semantics
- [ ] Know push/pop/enqueue/dequeue are O(1)
- [ ] Can implement both using arrays
- [ ] Know real applications (undo, scheduling, BFS)

### By End of Day 5 (Binary Search)
- [ ] Understand divide-and-conquer: halve search space each step
- [ ] Know precondition: array must be sorted
- [ ] Can trace binary search by hand
- [ ] Know O(log n) complexity and why

---

## 📚 Core Concepts Overview

### Concept 1: Direct Addressing
**What:** Computing address via arithmetic: base + index × size  
**Why:** O(1) access without search  
**Where:** All array-based structures

### Concept 2: Amortized Analysis
**What:** Occasional expensive operation amortized over many cheap ones  
**Why:** O(1) append despite O(n) resizes  
**Where:** Dynamic arrays, dynamic structures

### Concept 3: Pointer Chasing
**What:** Following pointer → pointer → pointer to reach element  
**Why:** O(n) access in linked lists  
**Cache Impact:** 50x slower than arrays due to cache misses

### Concept 4: LIFO vs FIFO
**What:** Different access orderings  
**Stack:** Last-in-first-out (undo, recursion)  
**Queue:** First-in-first-out (scheduling, BFS)

### Concept 5: Divide-and-Conquer
**What:** Halve problem size each step  
**Binary Search:** Halve search space → O(log n)  
**Precondition:** Sorted array required

---

## 🔄 Recommended Learning Path

**Morning (90 min):**
1. Read instructional file (all 11 sections)
2. Trace examples by hand on paper
3. Visualize operations mentally

**Afternoon (60 min):**
1. Answer Socratic questions
2. Solve 5-8 practice problems
3. Identify misconceptions

**Evening (30 min):**
1. Check checklist progress
2. Rate confidence (1-5)
3. Plan next day

---

## ⚠️ Common Mistakes to Avoid

### Mistake 1: "Insert/delete is O(n), so never use arrays"
**Reality:** Insert at END is O(1) amortized. Only mid-insertion is O(n). For most problems, use arrays.

### Mistake 2: "Amortized O(1) means it's always O(1)"
**Reality:** Occasional O(n) pauses happen (resizes). Averaged over n operations, each is O(1).

### Mistake 3: "Linked lists are better than arrays for unknown size"
**Reality:** Use dynamic arrays! Better cache, O(1) amortized append, simpler.

### Mistake 4: "Arrays and lists have same O(n) insertion"
**Reality:** Array insertion requires shifting (O(n) copies). List insertion is O(1) IF you have pointer to position.

### Mistake 5: "Binary search works on unsorted arrays"
**Reality:** Completely breaks. You'll skip over the target element.

---

## 🎓 Practice Problems Guide

### Arrays (Day 1)
1. Two Sum (find pair with given sum)
2. Best Time to Buy Stock (max difference)
3. Contains Duplicate
4. Product of Array Except Self
5. Rotate Array

### Dynamic Arrays (Day 2)
1. Design Dynamic Array class
2. Analyze growth factor impact
3. Implement resizable stack

### Linked Lists (Day 3)
1. Reverse Linked List
2. Merge Two Sorted Lists
3. Detect Cycle
4. Remove Nth Node from End

### Stacks & Queues (Day 4)
1. Valid Parentheses (stack)
2. Implement Queue using Stacks
3. Next Greater Element (monotonic stack preview)
4. Moving Average (circular buffer)

### Binary Search (Day 5)
1. Binary Search on sorted array
2. Search Insert Position
3. First Bad Version
4. Find Peak Element (modified binary search)

---

## 💼 Interview Preparation

**Interview Coverage:** Week 2 covers ~30-40% of interview problems

### Key Topics for Interviews
- **Arrays:** 2-pointer problems, prefix sums (Week 4)
- **Stacks:** Matching parentheses, monotonic stack (Week 4.5)
- **Queues:** BFS-based problems (Week 6)
- **Binary Search:** Log n optimization technique (appear everywhere)

### Common Interview Questions
- "Design a data structure that supports..."
- "Optimize this O(n²) solution"
- "What's the space/time trade-off?"

---

## 🔗 Resources & References

### Books
- "Cracking the Coding Interview" (Chapter 1-2: Arrays, Stacks/Queues)
- "Algorithms" by Sedgewick & Wayne (Chapters 1-2)

### Online
- LeetCode: Array, Stack, Queue, Binary Search tags
- GeeksforGeeks: Data structure visualizations

### Code Examples
- C++ `<vector>`, `<stack>`, `<queue>`
- Python `list`, `collections.deque`
- Java `ArrayList`, `Stack`, `Queue`

---

## ✅ Assessment & Success Criteria

### Knowledge (Can you explain?)
- [ ] Why array access is O(1)
- [ ] Difference between amortized and worst-case
- [ ] When to use stack vs queue
- [ ] Why binary search requires sorted array

### Skills (Can you do?)
- [ ] Trace array insertion/deletion by hand
- [ ] Trace binary search on any array
- [ ] Implement stack and queue
- [ ] Analyze time/space complexity of operations

### Judgment (Can you choose?)
- [ ] Array vs list for problem
- [ ] Stack vs queue for problem
- [ ] Dynamic array vs fixed array
- [ ] Binary search vs linear search

**Red Flags (Need more practice):**
- Can't derive O(1) array access from RAM model
- Confused about amortized analysis
- Don't know when linked lists are useful
- Can't trace binary search by hand

---

## 📊 Connection to Future Weeks

**Week 3 (Sorting & Hashing):**
- Sorting algorithms use arrays
- Hash table implementation uses arrays (chaining or probing)
- Hashtable collision resolution uses linked lists

**Week 4 (Problem-Solving Patterns):**
- Two pointers on sorted arrays (binary search preprocessed)
- Sliding windows on arrays
- Prefix sums on arrays

**Week 4.5 (Tier 1 Patterns):**
- Monotonic stack uses stack + deque
- Merge operations on arrays/lists
- Hash maps use arrays for buckets

**Weeks 6+ (Advanced):**
- Graphs use adjacency lists (linked lists)
- Queues for BFS
- Binary search in B-trees

---

## ❓ Frequently Asked Questions

**Q: Do I need to implement arrays from scratch?**
A: Once, for understanding. Then use library containers (vector, ArrayList).

**Q: Is linked list ever better than array?**
A: Rarely. Only for: (1) undo/redo systems, (2) memory allocators, (3) LRU caches. 99% use arrays.

**Q: Why is amortized analysis important?**
A: Because worst-case (O(n) resize) isn't representative. Average case (O(1)) is what matters for repeated operations.

**Q: Can I use hashtable as fallback for array/list?**
A: Not really. Hashtables have different semantics (unordered, hashing overhead). Use right structure for problem.

**Q: Is binary search just "divide by 2"?**
A: Yes, conceptually. Implementation requires careful details: (left + right) / 2, proper boundary checks.

---

## 🎯 Before Moving to Week 3

**Verification Checklist:**
- [ ] Can explain direct addressing (address = base + i × size)
- [ ] Understand amortized O(1) append for dynamic arrays
- [ ] Know linked list O(n) access vs O(1) relink trade-off
- [ ] Can implement stack/queue correctly
- [ ] Can trace binary search by hand
- [ ] Rate 4/5 or higher on all 5 days

**If not:**
- Spend 1-2 more days on weak areas
- Re-read instructional files
- Solve more practice problems
- Don't move forward with gaps!

---

## 📝 Week 2 Quick Summary (Table)

| Structure | Access | Insert | Delete | Space | Use Case |
|-----------|--------|--------|--------|-------|----------|
| **Array** | O(1) | O(n) | O(n) | O(n) | Indexed access, sequential |
| **Vector** | O(1) | O(n)* | O(n)* | O(n) | Dynamic, append-heavy |
| **LinkedList** | O(n) | O(1)† | O(1)† | O(n) | Undo/redo, allocators |
| **Stack** | — | O(1)‡ | O(1)‡ | O(n) | LIFO semantics |
| **Queue** | — | O(1)‡ | O(1)‡ | O(n) | FIFO semantics |
| **Sorted** | O(log n) binary search | — | — | O(1) | Search (via binary search) |

*Amortized  †At known position  ‡Push/pop or enqueue/dequeue

---

## 📊 Status & Cumulative Progress

**Week 1:** ✅ Foundations (RAM, Big-O, Recursion)  
**Week 2:** 🔄 LINEAR STRUCTURES (Arrays, Lists, Stacks, Queues, Search)  
**Cumulative Time:** ~20 hours  
**Interview Coverage:** ~30-40%  

**Next:** Week 3 (Sorting & Hashing) — builds heavily on Week 2 arrays and binary search

