# Week 2: Core Data Structures - Guidelines

**Week Focus:** Master fundamental data structures (Stacks, Queues, HashMaps, Heaps basics)  
**Total Time Investment:** 9-11 hours (learning + practice)  
**Difficulty Level:** 🟡 Medium  
**Prerequisites:** Week 1 (Array & String fundamentals)

---

## 📅 Daily Breakdown & Time Allocation

| Day | Topic | Time | Key Outcomes |
|-----|-------|------|--------------|
| **1** | Stacks Fundamentals | 90 min | LIFO, push/pop, common patterns |
| **2** | Queues Fundamentals | 90 min | FIFO, enqueue/dequeue, circular queues |
| **3** | Hash Tables/Maps | 95 min | Hash function, collision, lookup O(1) |
| **4** | Heaps & Priority Queues | 85 min | Min/max heaps, heap operations |
| **5** | Data Structure Integration | 80 min | Choose right structure, solve problems |

**Total Core Learning:** ~440 minutes (7.3 hours)  
**Practice & Consolidation:** ~3-4 hours  

---

## 🎯 Week 2 Learning Objectives

### By Week End, You Should:

**Knowledge:**
- [ ] Understand LIFO (Stack) concept
- [ ] Understand FIFO (Queue) concept
- [ ] Understand hashing and hash tables
- [ ] Understand heap data structure
- [ ] Know when to use each structure

**Skills:**
- [ ] Implement Stack from array
- [ ] Implement Queue from array
- [ ] Implement HashMap/Dictionary
- [ ] Implement Min/Max Heap
- [ ] Solve problems using right structure

**Application:**
- [ ] Use stacks for bracket matching
- [ ] Use queues for BFS
- [ ] Use hashes for duplicate detection
- [ ] Use heaps for top-k problems
- [ ] Choose structure based on requirements

---

## 📚 Core Concepts Overview

### Stack
```
Operations: push (add), pop (remove), peek (view top)
Order: LIFO (Last-In-First-Out)
Time: O(1) for all operations
Use Cases: Bracket matching, undo, function call stack
```

### Queue
```
Operations: enqueue (add rear), dequeue (remove front), peek
Order: FIFO (First-In-First-Out)
Time: O(1) for all operations
Use Cases: BFS, task scheduling, printer queue
```

### Hash Table/Map
```
Operations: insert, delete, lookup
Average Time: O(1) for all operations
Space: O(n) for n key-value pairs
Use Cases: Caching, frequency counting, deduplication
```

### Heap
```
Operations: insert, delete-min/max, heapify
Time: O(log n) for operations
Property: Parent ≤ (or ≥) children
Use Cases: Priority queues, top-k elements, sorting
```

---

## 🔄 Recommended Learning Path

**Best Order to Study:**

1. **Day 1:** Stacks Fundamentals
   - Understand LIFO concept
   - Implement from array
   - Practice basic operations
   - Solve bracket matching

2. **Day 2:** Queues Fundamentals
   - Understand FIFO concept
   - Implement from array
   - Learn circular queues
   - Apply to BFS concept

3. **Day 3:** Hash Tables
   - Understand hashing
   - Collision handling
   - Map/Dictionary implementation
   - Common use patterns

4. **Day 4:** Heaps & Priority Queues
   - Understand heap property
   - Build max/min heaps
   - Heap operations (insert, delete)
   - Priority queue applications

5. **Day 5:** Integration
   - Choose right structure
   - Combine structures
   - Solve complex problems

**Why This Order?**
- Stack and Queue are simple (start there)
- Hash Tables are critical (middle week)
- Heaps are more complex (after comfort)
- Integration uses all concepts

---

## ⚠️ Common Mistakes to Avoid

### Stack-Related

| Mistake | Fix |
|---------|-----|
| **Pop from empty stack** | Check if stack empty before pop |
| **Confusing push/pop order** | Remember: pop returns LIFO (last in) |
| **Using array append (slow)** | Use deque for O(1) operations |

### Queue-Related

| Mistake | Fix |
|---------|-----|
| **Dequeue from empty queue** | Check if queue empty |
| **Not using circular indexing** | Use (rear + 1) % size for wraparound |
| **Array shifting is O(n)** | Use deque or circular array |

### Hash Table-Related

| Mistake | Fix |
|---------|-----|
| **Ignoring collisions** | Use chaining or open addressing |
| **Bad hash function** | Use built-in hash, not naive modulo |
| **Key doesn't exist error** | Check key existence before access |

### Heap-Related

| Mistake | Fix |
|---------|-----|
| **Breaking heap property** | Heapify after insertion/deletion |
| **Parent-child index confusion** | left = 2i+1, right = 2i+2 (0-indexed) |
| **Using list pop (slow)** | Pop from end is O(1), others are O(n) |

---

## 🎓 Practice Problems Guide

### Stack Problems

**Easy:**
- Valid parentheses
- Min stack
- Reverse string using stack
- Time: 15-25 min

**Medium:**
- Largest rectangle in histogram
- Daily temperatures
- Evaluate RPN
- Time: 25-40 min

### Queue Problems

**Easy:**
- Implement queue
- Implement circular queue
- Moving average from stream
- Time: 15-25 min

**Medium:**
- Number of recent calls
- Dota2 Senate
- Time: 30-40 min

### Hash Table Problems

**Easy:**
- Two sum
- Contains duplicate
- Valid anagram
- Time: 15-20 min

**Medium:**
- LRU cache
- Group anagrams
- Top K frequent
- Time: 30-45 min

### Heap Problems

**Easy:**
- Last stone weight
- Kth largest element
- Time: 20-30 min

**Medium:**
- Top K frequent elements
- Merge K sorted lists
- Time: 35-50 min

**Sources:** LeetCode (Easy/Medium), GeeksforGeeks, HackerRank

---

## 💼 Interview Preparation

### Common Week 2 Questions

**Stack:**
- "How to implement stack with min/max?"
- "Reverse a string using stack"
- "Valid parentheses matching"

**Queue:**
- "Implement queue with two stacks"
- "BFS - when to use queue?"
- "Circular queue implementation"

**Hash Table:**
- "Implement hash table from scratch"
- "Handle collisions"
- "Design LRU cache"

**Heap:**
- "Implement min/max heap"
- "Top K elements"
- "Merge K sorted arrays"

### Interview Tips
1. **Clarify requirements:** "What about duplicates? Update operations?"
2. **Discuss trade-offs:** "Stack vs array? Time vs space?"
3. **Handle edge cases:** "Empty, single element, duplicates"
4. **Explain space complexity:** "Hash table uses O(n) space"
5. **Show implementation:** Code clean, readable, tested

---

## 🔗 Resources & References

### Online Platforms
- **LeetCode:** Stack, Queue, Hash Table, Heap problems
- **GeeksforGeeks:** Data structure tutorials
- **VisuAlgo:** Data structure visualization

### Visualization Tools
- **VisuAlgo (Stack/Queue):** https://www.cs.usfca.edu/~galles/visualization/
- **Python Tutor:** https://pythontutor.com

### Recommended Books
- "Introduction to Algorithms" - CLRS (Chapter 10-11)
- "Cracking the Coding Interview" - Chapter 3 (Stacks and Queues)
- "The Algorithm Design Manual" - Skiena (Chapter 3)

---

## ✅ Assessment & Success Criteria

### Knowledge Check
- [ ] Understand when to use Stack vs Queue
- [ ] Know O(1) operations for each structure
- [ ] Understand hash function and collisions
- [ ] Know heap property and operations
- [ ] Can choose right structure for problem

### Practical Skills
- [ ] Implement Stack from array
- [ ] Implement Queue from array
- [ ] Implement HashMap manually
- [ ] Build Min/Max Heap
- [ ] Use built-in data structures efficiently

### Confidence Targets
| Structure | Target |
|-----------|--------|
| Stack | 5/5 |
| Queue | 4-5/5 |
| Hash Table | 4/5 |
| Heap | 3-4/5 |
| Integration | 3-4/5 |
| Overall Week 2 | 4/5 |

---

## 📊 Connection to Future Weeks

### Week 3: Sorting Applications
```
Week 2 Data Structures
    ↓
Week 3 Sorting uses Heaps for Heap Sort
    ↓
Understanding heap structure essential
```

### Week 4: Optimization Patterns
```
Week 2 Hash Tables, Stacks, Queues
    ↓
Week 4 Two pointers, sliding window (often with sets/maps)
    ↓
Must understand hash table efficiency
```

### Week 5+: Advanced Algorithms
```
Weeks 1-2 Fundamentals & Data Structures
    ↓
Weeks 5+ Greedy, DP, Graphs (all use data structures)
    ↓
Comfortable with all structures → solve advanced problems
```

---

## ❓ Frequently Asked Questions

### Q1: Why implement data structures if languages have them?
**A:** Interviews often ask. Understanding implementation shows mastery. Plus, you can optimize (like designing LRU cache).

### Q2: When would I use Stack vs Array?
**A:** Stack when you need LIFO order. Array when you need random access. Stack has cleaner semantics.

### Q3: What about Queue implementation? Isn't deque better?
**A:** Yes! Use deque. But understand why (O(1) operations). Interview might ask array-based implementation.

### Q4: Can I use Python's deque for both Stack and Queue?
**A:** Yes! append/pop for stack, appendleft/pop for queue. But understand underlying implementation.

### Q5: Is understanding collision handling important?
**A:** Very! Shows deep understanding. Common follow-up: "How to handle collisions?" or "Design hash table"

### Q6: When to use Heap vs Sorted Array?
**A:** Heap for dynamic top-k. Sorted array if all data upfront. Heap: O(log n) insert/delete, Array: O(1) access.

---

## 🎯 Before Moving to Week 3

**Checklist:**
- [ ] Implement all 4 data structures from scratch
- [ ] Solve 3-5 problems per structure (12-20 total)
- [ ] Understand when to use each structure
- [ ] Can compare trade-offs (time, space, use case)
- [ ] Feel confident implementing and using them
- [ ] Overall confidence: 4/5 or higher

**If not ready:**
- Review structure implementation
- Solve more practice problems (5 per structure)
- Don't rush to Week 3

---

## 📝 Week 2 Quick Summary

| Structure | Core Operations | Time | Use When |
|-----------|-----------------|------|----------|
| **Stack** | push, pop, peek | O(1) | LIFO needed |
| **Queue** | enqueue, dequeue, peek | O(1) | FIFO needed |
| **Hash Table** | insert, delete, lookup | O(1) avg | Fast lookup needed |
| **Heap** | insert, delete-min/max | O(log n) | Priority order needed |

---

**Status:** Week 2 Ready for Study ✓  
**Expected Completion:** 1 week focused study  
**Success Rate:** 90%+ with consistent practice  

