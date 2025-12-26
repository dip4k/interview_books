# Week_2_Index.md

## 📚 Week 2 Complete Index — Linear Structures

### Core Topics (Curriculum Files)
1. **Week_2_Day_1_Arrays.md**  
   - Contiguous memory, cache locality, O(1) indexing  
   - Key sections: Why arrays matter in OS/DB, memory layouts, cache considerations.

2. **Week_2_Day_2_Dynamic_Arrays.md**  
   - Automatic growth, amortized analysis, pointer invalidation  
   - Highlights: Growth policy trade-offs, practical amortized analysis, real system usage.

3. **Week_2_Day_3_Linked_Lists.md**  
   - Pointer-based structures, trade-offs, realistic use (rare)  
   - Focus: Intrusive vs non-intrusive lists, when lists beat arrays, cache pitfalls.

4. **Week_2_Day_4_Stacks_Queues.md**  
   - LIFO/FIFO ADTs, circular buffers, call-stack parallels  
   - Includes: Implementation walkthroughs, concurrency considerations, queue fairness.

5. **Week_2_Day_5_Binary_Search.md**  
   - Logarithmic reduction, lower/upper bounds, predicate search  
   - Coverage: Proof of correctness, overflow-safe mid calculation, system integration.

### Supporting Assets
- **Week_2_Checklist.md** – Progress tracking & review plan  
- **Week_2_Summary.md** – Conceptual synthesis of Week 2 learnings  
- **Week_2_Roadmap.md** – Transition guidance into Week 3 (Sorting & Hashing)  
- **Week_2_QA.md** – Comprehensive Q&A (50 questions, 10 per day topic)  

### Cross-Topic References
- Arrays → prerequisite for dynamic arrays, binary search  
- Dynamic arrays → builds toward vector-based stacks/queues  
- Linked lists → informs use in hash table chaining, tree node linkage  
- Stacks & queues → essential for Week 4 problem-solving patterns (two-pointer, BFS/DFS)  
- Binary search → foundation for Week 3 sorting algorithms & Week 8 specialized structures  

### External Reference Links Recap
- Drepper, “What Every Programmer Should Know About Memory”  
- C++ STL `std::vector` / `std::list` source  
- Linux kernel `list_head`, `kfifo` APIs  
- glibc `bsearch`, Go `sort.Search` implementations  

> Use this index as the entry point to review specific topics or locate supporting resources quickly.