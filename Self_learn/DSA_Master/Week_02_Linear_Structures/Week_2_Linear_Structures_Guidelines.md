# Week 2: Linear Structures - Guidelines

**Week Focus:** Master fundamental data structures and understand memory behavior  
**Total Time Investment:** 10-12 hours (learning + practice)  
**Difficulty Level:** 🟡 Medium  
**Prerequisites:** Week 1 (Foundations, Big-O analysis)

---

## 📅 Daily Breakdown & Time Allocation

| Day | Topic | Time | Key Outcomes |
|-----|-------|------|--------------|
| **1** | Arrays | 100 min | Contiguous memory, cache locality, O(1) indexing, insertion/deletion |
| **2** | Dynamic Arrays | 105 min | Automatic growth, amortized analysis O(1) append, capacity management |
| **3** | Linked Lists | 95 min | Pointer-based structures, trade-offs, when useful (rarely), O(1) insertion |
| **4** | Stacks & Queues | 105 min | LIFO/FIFO ordering, ADTs, implementation, common patterns |
| **5** | Binary Search | 95 min | Logarithmic reduction on sorted data, O(log n) pattern, variants |

**Total Core Learning:** ~500 minutes (8.3 hours)  
**Practice & Consolidation:** ~2-3 hours  

---

## 🎯 Week 2 Learning Objectives

### By Week End, You Should:

**Knowledge:**
- [ ] Understand array memory layout and cache efficiency
- [ ] Know why dynamic arrays are efficient (amortized O(1))
- [ ] Understand linked list trade-offs vs arrays
- [ ] Know stack and queue ADTs and use cases
- [ ] Understand binary search requirements and variants

**Skills:**
- [ ] Implement dynamic array (resize logic)
- [ ] Implement singly/doubly linked list
- [ ] Implement stack and queue from arrays/linked lists
- [ ] Implement binary search (multiple variants)
- [ ] Analyze amortized complexity

**Application:**
- [ ] Choose between array/linked list based on operations
- [ ] Use stacks for problems requiring LIFO
- [ ] Use queues for BFS and level-order traversal
- [ ] Apply binary search to optimization problems
- [ ] Understand memory behavior and cache implications

---

## 📚 Core Concepts Overview

### Arrays
```
Layout: Contiguous memory, index-based access
Operations:
  - Access: O(1)
  - Insert/Delete: O(n) (shifting required)
  - Search: O(n) (or O(log n) if sorted)
  
Advantage: Fast access, cache-friendly
Disadvantage: Fixed size, expensive insertions
```

### Dynamic Arrays
```
Growth Strategy: Double capacity when full
Operations:
  - Append: O(1) amortized (why? total cost spreads)
  - Access: O(1)
  - Insert middle: O(n)
  
Amortized Analysis:
  - n appends cost O(n) total (not O(n²))
  - Average per append: O(1)
```

### Linked Lists
```
Layout: Pointer-based nodes
Operations:
  - Access: O(n) (must traverse)
  - Insert at head: O(1)
  - Insert middle: O(n) to find, then O(1) to insert
  - Delete: O(n) to find, then O(1) to delete
  
Use: When many insertions/deletions in middle (rare!)
      Usually arrays/dynamic arrays better
```

### Stacks & Queues
```
Stack (LIFO):
  - Operations: push, pop, peek (all O(1))
  - Use: Parenthesis matching, DFS, undo

Queue (FIFO):
  - Operations: enqueue, dequeue, peek (all O(1))
  - Use: BFS, task scheduling, breadth-first traversal
```

### Binary Search
```
Requirement: Sorted array
Time: O(log n) vs O(n) linear search
Pattern:
  - Find middle
  - Compare to target
  - Eliminate half based on comparison
  
Variants: Exact match, first occurrence, last occurrence, closest value
```

---

## 🔄 Recommended Learning Path

**Best Order to Study:**

1. **Day 1:** Arrays
   - Understand memory layout
   - Learn cache locality
   - Practice indexing and iteration
   - Understand O(1) access, O(n) insertion

2. **Day 2:** Dynamic Arrays
   - Understand growth strategy
   - Learn amortized analysis
   - Why O(1) append despite resizing
   - Trade space for time efficiency

3. **Day 3:** Linked Lists
   - Understand pointer-based structure
   - Compare with arrays (when better?)
   - Realize arrays usually better
   - Know use cases where actually useful

4. **Day 4:** Stacks & Queues
   - Implement from arrays
   - Understand ADT abstraction
   - Common patterns (matching, BFS)
   - Why LIFO/FIFO useful

5. **Day 5:** Binary Search
   - Understand logarithmic reduction
   - Implement basic version
   - Learn boundary handling
   - Practice variants (first, last, closest)

**Why This Order?**
- Arrays most basic (start there)
- Dynamic arrays extend arrays (natural follow-up)
- Linked lists show alternatives and trade-offs
- Stacks/Queues use arrays but with abstraction
- Binary search applies to sorted arrays

---

## ⚠️ Common Mistakes to Avoid

### Arrays

| Mistake | Fix |
|---------|-----|
| **Off-by-one errors** | Indices 0 to n-1, not 1 to n |
| **Modifying while iterating** | Create new array or use safe iteration |
| **Forgetting boundaries** | Check: 0 ≤ index < len(arr) |
| **Fixed size misconception** | Arrays fixed in most languages, but resizable in Python |

### Dynamic Arrays

| Mistake | Fix |
|---------|-----|
| **Think append is O(n)** | Amortized O(1), not O(n) |
| **Wrong growth factor** | Typical: double capacity (not add 1) |
| **Ignoring space waste** | Amortized analysis accounts for it |

### Linked Lists

| Mistake | Fix |
|---------|-----|
| **Using for random access** | O(n) each time, bad performance |
| **Forgetting to update pointers** | Must change .next after insertion/deletion |
| **Not handling edge cases** | Empty list, single node, last node |

### Stacks & Queues

| Mistake | Fix |
|---------|-----|
| **Pop from empty** | Check if empty before pop/dequeue |
| **Using list.pop(0) for queue** | O(n)! Use deque or implement circular |
| **Mixing LIFO/FIFO** | Stack: LIFO (last in first out), Queue: FIFO |

### Binary Search

| Mistake | Fix |
|---------|-----|
| **Array not sorted** | Binary search requires sorted array |
| **Off-by-one in mid** | Use mid = (left + right) // 2 |
| **Wrong comparison** | Think about what to do when found |
| **Infinite loop** | Move left or right every iteration |

---

## 🎓 Practice Problems Guide

### Array Problems

**Easy:**
- Find maximum element
- Reverse array
- Remove duplicates (sorted)
- Time: 15-20 min

**Medium:**
- Rotate array
- Merge sorted arrays
- Find peak element
- Time: 25-40 min

### Linked List Problems

**Easy:**
- Reverse linked list
- Merge two sorted lists
- Middle of linked list
- Time: 20-30 min

**Medium:**
- Detect cycle
- Remove nth node
- Reorder list
- Time: 30-45 min

### Stack & Queue Problems

**Easy:**
- Valid parentheses
- Min stack
- Implement queue with stacks
- Time: 15-25 min

**Medium:**
- Largest rectangle in histogram
- Daily temperatures
- BFS using queue
- Time: 30-45 min

### Binary Search Problems

**Easy:**
- Binary search
- Search insert position
- First bad version
- Time: 15-20 min

**Medium:**
- Search rotated array
- Find first/last position
- Search 2D matrix
- Time: 25-40 min

**Sources:** LeetCode, GeeksforGeeks, HackerRank

---

## 💼 Interview Preparation

### Common Week 2 Questions

**Arrays:**
- "How would you reverse an array in-place?"
- "What's the difference between array and linked list?"
- "How does dynamic array resizing work?"

**Linked Lists:**
- "Implement reverse linked list"
- "Detect cycle in linked list"
- "Merge two sorted linked lists"

**Stacks & Queues:**
- "Implement stack/queue from array"
- "Valid parentheses matching"
- "Implement BFS using queue"

**Binary Search:**
- "Implement binary search"
- "Find boundary in array"
- "Search in rotated sorted array"

### Interview Tips
1. **Clarify constraints:** "In-place? Duplicates? Memory limit?"
2. **Discuss trade-offs:** "Array vs linked list - when each?"
3. **State assumptions:** "I'll assume sorted array for binary search"
4. **Test edge cases:** "Empty, single element, duplicates"
5. **Explain complexity:** "Time O(n), space O(1)"

---

## 🔗 Resources & References

### Online Platforms
- **LeetCode:** Array, linked list, stack/queue problems
- **GeeksforGeeks:** Data structure tutorials with code
- **HackerRank:** Data structure courses
- **Khan Academy:** CS fundamentals

### Visualization Tools
- **VisuAlgo:** https://www.cs.usfca.edu/~galles/visualization/ (Arrays, lists)
- **Python Tutor:** https://pythontutor.com (step-by-step execution)
- **Algorithm Visualizer:** https://algorithm-visualizer.org/

### Recommended Books
- "Introduction to Algorithms" - CLRS (Chapter 10-11)
- "Cracking the Coding Interview" - Chapter 2
- "The Algorithm Design Manual" - Skiena (Chapter 3)

---

## ✅ Assessment & Success Criteria

### Knowledge Check
- [ ] Understand array memory layout and O(1) indexing
- [ ] Know why dynamic array append is O(1) amortized
- [ ] Understand linked list trade-offs with arrays
- [ ] Know when to use stack (LIFO) vs queue (FIFO)
- [ ] Understand binary search requirement (sorted)

### Practical Skills
- [ ] Implement dynamic array with resize logic
- [ ] Implement singly linked list (insert, delete, traverse)
- [ ] Implement stack from array
- [ ] Implement queue from array (circular or deque)
- [ ] Implement binary search (3+ variants)

### Confidence Targets
| Data Structure | Target |
|---|---|
| Arrays | 5/5 |
| Dynamic Arrays | 4-5/5 |
| Linked Lists | 4/5 |
| Stacks | 4-5/5 |
| Queues | 4-5/5 |
| Binary Search | 4/5 |
| Overall Week 2 | 4/5 |

---

## 📊 Connection to Future Weeks

### Week 3: Sorting & Hashing
```
Week 2 Linear structures and binary search
    ↓
Week 3 Sorting works on arrays, hashing tables store in arrays
    ↓
Understanding arrays critical for Week 3
```

### Week 4: Problem-Solving Patterns
```
Week 2 Arrays, stacks, queues
    ↓
Week 4 Two pointers on arrays, sliding window on arrays
    ↓
Mastery of arrays enables optimization patterns
```

### Week 5+: Trees & Graphs
```
Weeks 1-2 Fundamentals & Linear Structures
    ↓
Weeks 5+ Trees (linked nodes), Graphs (arrays/hashing)
    ↓
Both use concepts from Week 2
```

---

## ❓ Frequently Asked Questions

### Q1: When should I use linked list instead of array?

**A:** Rarely! Only when: (1) many insertions/deletions at beginning, AND (2) never random access. Usually dynamic array better.

### Q2: Is amortized O(1) same as guaranteed O(1)?

**A:** No. Single append might be O(n) (resizing), but average O(1). Important distinction for time-sensitive applications.

### Q3: Why is cache locality important?

**A:** Arrays contiguous in memory = better CPU cache behavior. Linked lists scattered = many cache misses. Practical difference, not Big-O.

### Q4: Should I memorize binary search code?

**A:** Understand the pattern. Many variants (closed-closed, closed-open, open-open bounds). Practice, don't memorize.

### Q5: Can I use stack/queue without implementing?

**A:** Yes, use built-in (deque in Python). But interview often asks implementation, showing you understand ADT.

### Q6: Do I need doubly linked lists?

**A:** Know the concept. Rarely needed in interviews unless specifically asked. Singly sufficient for most problems.

---

## 🎯 Before Moving to Week 3

**Checklist:**
- [ ] Understand array memory layout and O(1) indexing
- [ ] Implement dynamic array with resize logic
- [ ] Implement linked list (insert, delete, reverse)
- [ ] Implement stack and queue from arrays
- [ ] Implement binary search (4+ variants)
- [ ] Solve 15+ problems across all structures
- [ ] Overall confidence: 4/5 or higher

**If not ready:**
- Review weak data structures
- Implement again from scratch
- Solve 10+ more practice problems
- Don't rush to Week 3

---

## 📝 Week 2 Quick Summary

| Structure | Access | Insert/Delete Head | Insert/Delete Mid | Space |
|---|---|---|---|---|
| **Array** | O(1) | O(n) | O(n) | O(n) |
| **Dynamic Array** | O(1) | O(n) | O(n) | O(n) amortized |
| **Linked List** | O(n) | O(1) | O(n) to find | O(n) |
| **Stack** | O(1) peek | O(1) | - | O(n) |
| **Queue** | O(1) peek | O(1) | - | O(n) |

---

**Status:** Week 2 Ready for Study ✓  
**Expected Completion:** 1 week focused study  
**Success Rate:** 85%+ with consistent practice  
**Cumulative Progress:** 25-30% of total curriculum

