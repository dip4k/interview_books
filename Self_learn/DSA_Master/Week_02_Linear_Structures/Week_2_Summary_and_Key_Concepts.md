# Week 2: Linear Structures - Summary & Key Concepts

**Week:** 2 | **Date:** December 27, 2025  
**Topics:** 5 (Arrays, Dynamic Arrays, Linked Lists, Stacks/Queues, Binary Search)  
**Total Content:** 25,000+ words across 5 days

---

## 🎯 QUICK REFERENCE

### Structure Comparison Table

| Aspect | Array | Dynamic | List | Stack | Queue |
|--------|-------|---------|------|-------|-------|
| **Access[i]** | O(1) | O(1) | O(n) | O(1) top | O(1) front |
| **Insert End** | O(n)* | O(1)† | O(n) | O(1) | O(1) |
| **Insert Mid** | O(n) | O(n) | O(1)‡ | - | - |
| **Delete Mid** | O(n) | O(n) | O(1)‡ | - | - |
| **Space** | O(n) | O(n) | O(n) | O(n) | O(n) |
| **Cache** | ✓ Good | ✓ Good | ✗ Bad | ✓ Good | ✓ Good |

*Fixed size: can't insert  
†Amortized  
‡If you have pointer

---

## 📚 CORE CONCEPTS RECAP

### Day 1: Arrays

**Key Insight:** Contiguous memory + address arithmetic = O(1) access

**How It Works:**
```
Memory:  [0] [1] [2] [3] [4]
         10  20  30  40  50
         
arr[i] address = base + i * sizeof(int)
arr[3] = 40 at address (base + 3*4)
```

**Complexity:**
- Access: O(1) via arithmetic
- Insert/Delete middle: O(n) shifting
- Sequential iteration: Cache-optimal

**When to Use:**
- Need O(1) random access
- Mostly reading, not modifying
- Cache performance critical

---

### Day 2: Dynamic Arrays

**Key Insight:** Automatic resizing with amortized O(1) append

**How It Works:**
```
Size: 3, Capacity: 4 → push_back(40) → O(1)
Size: 4, Capacity: 4 → push_back(50) → O(4) resize + O(1) insert

Doubling: 1 → 2 → 4 → 8 → 16 → ...
Resizes: O(log n) times for n elements
Total cost: O(n), amortized per push: O(1)
```

**Complexity:**
- Push: O(1) amortized
- Worst case: O(n) on resize
- Pop: O(1)

**When to Use:**
- Size unknown at compile-time
- Frequent appends
- Need cache-efficient access
- Default choice for variable-size collections

---

### Day 3: Linked Lists

**Key Insight:** Pointer-based structure enables O(1) insertion at known position

**How It Works:**
```
List: [10] → [20] → [30]
               ↓
Insert 25: [10] → [20] → [25] → [30]
Operation: 20.next = new_node; new_node.next = 30;
Cost: O(1) if you have pointer to 20
```

**Complexity:**
- Access: O(n) following pointers
- Insert at known: O(1) if you have pointer
- Insert at unknown: O(n) to search + O(1) insert
- Cache misses: Scattered memory = bad

**When to Use:**
- Frequent insertion/deletion at known positions
- Implement LRU cache (with hash map)
- Don't need random access
- (Rarely: arrays usually win despite cache issues)

---

### Day 4: Stacks & Queues

**Key Insight:** Abstract enforced ordering enables specific algorithms

**Stack (LIFO):**
```
Push:  [10, 20, 30, 40]  ← append
Pop:   [10, 20, 30]      ← remove 40 (last in)
```

**Queue (FIFO):**
```
Enqueue: [10, 20, 30, 40]  ← append at back
Dequeue: [20, 30, 40]      ← remove 10 (first in)
```

**Use Cases:**
- Stack: DFS, undo/redo, function calls, parenthesis matching
- Queue: BFS, job scheduling, message passing, printing

**Implementation:**
- Stack: Array with top pointer, O(1) push/pop
- Queue: Ring buffer (circular array) for O(1) dequeue

---

### Day 5: Binary Search

**Key Insight:** Divide-and-conquer on sorted arrays → O(log n)

**How It Works:**
```
arr = [10, 20, 30, 40, 50, 60, 70, 80, 90]
target = 60

Check middle (index 4): arr[4] = 50 < 60 → search right
Check middle (index 6): arr[6] = 70 > 60 → search left
Check middle (index 5): arr[5] = 60 == 60 → found!

3 comparisons instead of up to 9
```

**Complexity:**
- Time: O(log n)
- Space: O(1) iterative, O(log n) recursive
- Precondition: Array must be sorted!

**When to Use:**
- Large sorted sets (>1000 elements)
- Parametric binary search (find best X)
- Database indexes
- Price lookups

**Pitfalls:**
- Array not sorted → wrong answer
- mid = (left+right)/2 → integer overflow (fix: mid = left+(right-left)/2)
- Off-by-one errors → infinite loop or miss
- Duplicates → need special handling

---

## 🧠 5 COGNITIVE LENSES (Every Day)

### 🖥️ COMPUTATIONAL LENS

**How the computer actually executes:**

**Arrays:**
- Contiguous memory allows CPU prefetch
- Sequential scan: ~1 cache miss per 8 elements
- Random access: ~1 cache miss per element
- 100x difference in real performance

**Dynamic Arrays:**
- Doubling strategy keeps resize O(log n) total
- Amortized analysis: costs average out

**Linked Lists:**
- Every pointer dereference is unpredictable
- CPU can't prefetch → cache miss every access
- Kills performance despite O(1) theory

**Stacks/Queues:**
- Stack: LIFO enforces last-computed-first-used
- Queue: FIFO matches production flow
- Both cache-efficient if array-based

**Binary Search:**
- Eliminate half space per comparison
- Logarithmic → 30 comparisons for 1 billion

### 🧠 PSYCHOLOGICAL LENS

**How humans understand/think about it:**

**Arrays:**
- Intuitive: numbered slots
- O(1) access: instant retrieval
- O(n) insert: must renumber

**Dynamic Arrays:**
- Confusing: "O(1) amortized but sometimes O(n)?"
- Mental fix: Amortized = average cost over sequence

**Linked Lists:**
- Appealing: elegant pointer-based solution
- Trap: Students love theory, forget cache misses
- Mental fix: "Cache behavior dominates in practice"

**Stacks/Queues:**
- Intuitive: plates/lines (physical analogy)
- Stack: LIFO is backward from natural order
- Queue: FIFO matches intuition

**Binary Search:**
- Intuitive: phone book search
- Trap: Off-by-one and overflow errors
- Mental fix: Test carefully on edge cases

### 🔄 DESIGN TRADE-OFF LENS

**Fundamental decisions and trade-offs:**

**Array vs Dynamic:**
- Trade: Memory overhead for convenience
- When: Use dynamic if size varies wildly

**Array vs Linked:**
- Trade: Cache efficiency vs insertion at middle
- When: Almost never use list (cache kills performance)
- Exception: LRU cache (list + hash map)

**Stack vs Queue:**
- Trade: LIFO vs FIFO ordering
- When: Choose based on algorithm needs

**Sorted vs Unsorted:**
- Trade: O(n log n) sort once → O(log n) searches
- When: More than log n searches = sort is worth it

### 🤖 AI/ML ANALOGY LENS

**How this appears in machine learning:**

**Tensors (N-dimensional arrays):**
- Neural networks exclusively use arrays
- GPU requires contiguous memory
- Batch processing = sequential tensor access
- Linked lists impossible for tensor operations

**Hash maps:**
- Training: store embedding vectors efficiently
- Inference: O(1) lookup of learned weights

**Stacks/Queues:**
- Training: computational graph builds as stack of operations
- Backprop: reverse topological order (stack-like)

**Binary search:**
- Hyperparameter tuning: find optimal learning rate (parametric search)
- Tree models: B-tree node search during inference

### 📚 HISTORICAL CONTEXT LENS

**How these concepts evolved:**

**Arrays:**
- Inherent to Von Neumann architecture (1945)
- Addressable memory = arrays optimal
- Dominated for 70+ years

**Dynamic Arrays:**
- Vectors added to C++ STL (1994)
- Solved "fixed size" problem elegantly
- Now default in almost all languages

**Linked Lists:**
- Lisp invention (1958): cons cells
- Elegant in functional languages
- Proved slower than arrays in practice
- Still taught, rarely used

**Stacks/Queues:**
- Call stack: CPU hardware feature (1960s)
- Message queues: OS innovation (1970s)
- Now fundamental architectural pattern

**Binary Search:**
- Ancient technique (phone books)
- Knuth: Art of Computer Programming
- Still most important algorithm for interviews

---

## ✅ MASTERY CHECKLIST

### Knowledge (Recall)

- [ ] Explain O(1) array access via address arithmetic
- [ ] State complexity of each operation on each structure
- [ ] Define amortized analysis
- [ ] Describe how binary search eliminates half
- [ ] List preconditions for binary search

### Skills (Application)

- [ ] Implement array access, insert, delete
- [ ] Analyze complexity of any array operation
- [ ] Implement dynamic array with doubling
- [ ] Implement linked list insert/delete
- [ ] Implement stack and queue
- [ ] Implement binary search (iterative and recursive)

### Understanding (Explanation)

- [ ] Explain why cache misses matter more than Big-O
- [ ] Explain why linked lists rarely win in practice
- [ ] Explain amortized O(1) despite occasional O(n)
- [ ] Explain LIFO vs FIFO differences
- [ ] Explain why binary search requires sorted input

---

## 📊 PROBLEM DISTRIBUTION BY STRUCTURE

### Most Common in Interviews

1. **Arrays** - 40% of problems
   - Two pointers, sliding window, sorting variants
   
2. **Binary Search** - 15% of problems
   - Direct search, parametric search, rotated arrays
   
3. **Stacks/Queues** - 20% of problems
   - DFS/BFS graphs, monotonic stack, LRU cache
   
4. **Linked Lists** - 15% of problems
   - Reversal, merging, cycle detection
   
5. **Dynamic Arrays** - 10% of problems
   - Rarely alone, usually mixed with other structures

---

## 🎓 INTERVIEW PREPARATION

### Key Q&A Pairs (Sample)

**Q1: Why is array access O(1)?**
A: Address calculation: base + index*sizeof(type), all constant-time operations

**Q2: Why is dynamic array push_back O(1) amortized?**
A: Doubling strategy: resize O(log n) times total, average cost per push ≈ O(1)

**Q3: When would you use linked list over array?**
A: Rarely. Only when middle insertions outweigh cache misses (LRU cache with hash map)

**Q4: How do you implement queue in O(1) dequeue?**
A: Ring buffer: front++ and back++ mod capacity, no shifting needed

**Q5: What's the precondition for binary search?**
A: Array must be sorted! Without sorting, algorithm gives wrong answer

(See Week 2 Interview Q&A file for 60+ complete pairs)

---

## 🚀 PROGRESSION FRAMEWORK

### After Week 2, You Can:

✅ Analyze complexity of any linear data structure operation  
✅ Choose appropriate structure for given workload  
✅ Implement custom arrays, lists, stacks, queues  
✅ Identify and fix cache-related performance issues  
✅ Solve any problem using linear structures  
✅ Understand real systems (OS, databases, graphics)  

### Next: Week 3 (Sorting & Hashing)

You'll build on Week 2 by:
- Sorting arrays (various algorithms)
- Building hash tables (arrays with collision handling)
- Combining structures (hash map + linked list for LRU)

---

## Summary

**Week 2 mastery means understanding fundamental linear structures' trade-offs and choosing wisely. Arrays dominate due to cache efficiency; linked lists solve specific problems rarely; stacks/queues enforce ordering; binary search exploits sorted properties.**

**Most important insight:** Cache behavior matters more than Big-O for practical performance.

