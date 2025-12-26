# Week_2_Summary.md

## 📝 Week 2 Summary — Linear Structures Mastery

### High-Level Takeaways
- **Arrays anchor everything:** Contiguity provides O(1) indexing and cache-friendly iteration, forming the mental model for memory layout in systems.
- **Dynamic arrays trade spare capacity for amortized speed:** Doubling strategies balance reallocations, highlighting the difference between worst-case and amortized guarantees.
- **Linked lists are niche tools:** Excellent for O(1) splicing and intrusive data structures, but modern hardware penalizes pointer chasing; understanding when *not* to use them is critical.
- **Stacks and queues embody order constraints:** Recognizing that recursion uses stacks, BFS uses queues, and that ADTs abstract away implementation decisions prepares you for higher-level patterns.
- **Binary search formalizes logarithmic thinking:** Mastery requires respect for invariants, overflow-safe calculations, and variants (lower/upper bound, predicate search) common in indexing.

### Conceptual Gaps Addressed
- Arrays: Row-major vs column-major, cache line interactions  
- Dynamic arrays: Amortized analysis justification, pointer invalidation  
- Linked lists: Sentinel nodes, intrusive implementations, cache costs  
- Stacks & queues: Circular buffer wrap-around, bounded vs unbounded semantics  
- Binary search: Overflow handling, duplicates, monotonic predicate applications

### Skill Progress Metrics
| Skill Area                         | Baseline | After Week 2 | Evidence |
|-----------------------------------|----------|---------------|----------|
| Cache-aware thinking              | Low      | Medium        | Benchmarks comparing array vs list traversal |
| Amortized analysis intuition      | Low      | Medium        | Growth factor simulation documented |
| Pointer manipulation confidence   | Low      | Medium        | Linked list sentinel exercises (partial) |
| ADT abstraction & usage           | Medium   | High          | Stack/queue implementations & BFS practice |
| Logarithmic algorithm mastery     | Medium   | High          | Binary search variants, unit tests, predicate search |

### Practice Highlights
- Implemented array-backed stack and queue; measured wrap-around correctness.  
- Ran dynamic array growth experiments with different factors, confirming amortized O(1).  
- Benchmarked linked list vs array traversal to “feel” cache penalties.  
- Solved expression evaluation and BFS tasks to reinforce stack/queue ADT semantics.  
- Completed binary search unit tests including edge cases (empty, duplicates).

### Reflection Questions
- Can you walk through a binary search proof using loop invariants without referencing code?  
- How would you defend choosing a dynamic array over a linked list in a code review?  
- What hardware realities make arrays superior for most workloads today?  
- How would you enforce backpressure on a bounded queue in a high-load service?

### Next Steps
- Apply stack/queue patterns in Week 4 problem-solving techniques (e.g., sliding window).  
- Prepare for Week 3 by revisiting array-based sorting implementations (in-place vs stable).  
- Continue spaced repetition per the checklist to cement retention.

> Week 2 built the mental scaffolding for linear data handling. These foundations feed directly into sorting, hashing, and pattern recognition in upcoming weeks.