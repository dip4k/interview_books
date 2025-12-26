# Week_2_Checklist.md

## ✅ Week 2 Progress Checklist — Linear Structures

| Day | Topic                              | Core Goals                                                                 | Status | Confidence (1–5) | Notes / Next Steps |
|-----|------------------------------------|-----------------------------------------------------------------------------|--------|------------------|--------------------|
| 1   | Arrays                             | Understand contiguous layout, cache locality, O(1) indexing                | ✅     | 4.5              | Revisit row vs column major after 1 week |
| 2   | Dynamic Arrays                     | Master amortized analysis, growth factors, pointer invalidation            | ✅     | 4.0              | Practice reserve/shrink benchmarks       |
| 3   | Linked Lists                       | When they’re useful (intrusive, O(1) splice), why cache-unfriendly         | ✅     | 3.8              | Drill sentinel patterns, intrusive list usage |
| 4   | Stacks & Queues                    | ADT semantics, array vs linked implementations, circular buffer mechanics  | ✅     | 4.2              | Implement bounded queue with backpressure |
| 5   | Binary Search                      | Maintain invariants, handle duplicates, predicate search                   | ✅     | 4.6              | Solve rotated-array & parametric problems |

### Weekly Milestones
- [x] Completed all five Day topics using 11-section framework  
- [x] Logged conceptual gaps (arrays: row-major; dyn arrays: amortized spikes; linked list: sentinel use; stack/queue: circular wrap; binary search: overflow)  
- [x] Practiced at least one implementation per topic  
- [ ] Schedule spaced repetition session (recommended: 2026-01-02)

### Review Scheduling (Spaced Repetition Plan)
| Topic             | 48-hour Review | 1-Week Review | 1-Month Review |
|-------------------|----------------|---------------|----------------|
| Arrays            | 2025-12-28     | 2026-01-04    | 2026-01-27     |
| Dynamic Arrays    | 2025-12-29     | 2026-01-05    | 2026-01-28     |
| Linked Lists      | 2026-01-01     | 2026-01-08    | 2026-02-01     |
| Stacks & Queues   | 2026-01-01     | 2026-01-08    | 2026-02-01     |
| Binary Search     | 2026-01-02     | 2026-01-09    | 2026-02-02     |

### Practice & Implementation Log
- Arrays vs Linked Lists traversal benchmark ✔️  
- Dynamic array resize experiment (growth factors 1.25, 1.5, 2.0) ✔️  
- Linked list intrusive “list_head” prototype ✖️ (schedule next week)  
- Queue circular buffer implementation ✔️  
- Binary search lower/upper bound unit tests ✔️  

### Action Items for Week 3
- Refresh linked list sentinel handling before tackling tree nodes (Week 5)  
- Continue using explicit stacks for DFS exercises to reinforce queue/stack ADTs  
- Keep profiling linear scan vs binary search to internalize crossover thresholds  