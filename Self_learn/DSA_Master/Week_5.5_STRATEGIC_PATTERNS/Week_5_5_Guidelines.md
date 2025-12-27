# Week 5.5 (Tier 2): Strategic Patterns — Guidelines

## 📅 Daily Breakdown & Time Allocation

**Total Week:** 9-10.5 hours (3 hours per day)

| Day | Topic | Time | Focus | Coverage |
|-----|-------|------|-------|----------|
| **1** | Difference Array | 3h | Range updates, O(n+k) optimization | 10-15% |
| **2** | In-Place Replacement | 3h | Space optimization, O(1) extra | 8-12% |
| **3** | Deque Operations | 3h | Sliding window, O(n) max/min | 5-10% |
| **Weekend** | Integration & Review | 1-1.5h | Pattern combinations, strategy | — |

**Total:** 9-10.5 hours, 3 critical strategic patterns

---

## 🎯 Learning Objectives

### By End of Week 5.5
- [ ] Master difference array for range updates (10-15% problems)
- [ ] Implement in-place replacement O(1) space (8-12% problems)
- [ ] Solve sliding window max/min with deque O(n) (5-10% problems)
- [ ] Recognize which Tier 2 pattern fits each problem
- [ ] Understand when Tier 2 patterns beat alternatives
- [ ] Solve 80-88% of interview problems (cumulative)

---

## 📚 Core Concepts

**Concept 1: Batch Processing with Boundaries**  
Mark problem boundaries instead of processing all elements. Transform O(n×k) to O(n+k).

**Concept 2: Two-Pointer Space Optimization**  
Modify arrays in-place with O(1) extra space. Read ahead, write selectively.

**Concept 3: Monotonic Data Structure**  
Maintain decreasing/increasing order in deque. Front always contains best element (max/min).

---

## 🔄 Recommended Learning Path

**Morning (90 min):** Read instructional, trace examples, understand mechanics  
**Afternoon (60 min):** Answer Socratic questions, solve 3-4 problems, implement from scratch  
**Evening (30 min):** Review checklist, rate confidence, compare to alternatives

---

## ⚠️ Common Mistakes to Avoid

**Mistake 1: "Difference array is just another data structure"**  
Reality: It's an optimization technique transforming O(n×k) to O(n+k) by inverting the problem.

**Mistake 2: "In-place only for memory savings"**  
Reality: Interview gold standard. Shows algorithmic mastery and pointer manipulation skill.

**Mistake 3: "Deque is just a queue"**  
Reality: Double-ended with unique properties. Monotonic deque is specialized pattern.

**Mistake 4: "Can use heap/segment tree instead of deque"**  
Reality: They work (O(n log n)) but deque is O(n) optimal for this pattern.

**Mistake 5: "Tier 2 patterns are less important than Tier 1"**  
Reality: +10-12% coverage. Takes cumulative 80-88%. Many hard interview problems use these.

---

## 🎓 Practice Problems Guide

### Difference Array (8+ problems)
1. Range Addition
2. Hotel Bookings II (count occupied rooms)
3. Difference Array Queries (range add, point query)
4. Shift Queries
5. Conflict Detection (overlapping intervals)
6. Range Increment
7. Event Scheduling (mark availability)
8. 2D Difference Array (rectangle updates on grid)

### In-Place Replacement (8+ problems)
1. Remove Duplicates from Sorted Array
2. Remove Element (by value)
3. Remove Vowels from String
4. Move Zeroes to End
5. Duplicate Zeros
6. Valid Mountain Array (in-place check)
7. Partition Labels
8. Shift Zeros (move to end in-place)

### Deque Operations (8+ problems)
1. Sliding Window Maximum
2. Sliding Window Minimum
3. First Negative Integer in Every Window
4. Building a Bigger Window
5. Maximize Sum of k Elements
6. Optimal Position for Service Center
7. Shortest Subarray with Sum at Least K
8. Min Index Sum of Two Lists (deque variant)

---

## 💼 Interview Preparation

**Tier 2 Coverage:** 80-88% of interview problems (combined with Tier 1 + foundational weeks)

**Interview Strategy:**
1. Identify problem category (range update? space optimization? sliding window?)
2. Check if Tier 2 pattern applies
3. Understand when pattern beats alternatives
4. Implement cleanly with edge cases
5. Explain time/space trade-offs

**When Tier 2 Matters Most:**
- Hard problems often combine Tier 1 + Tier 2
- Space optimization highly valued (O(1) → interview gold)
- Optimization patterns show deep understanding
- Real systems use these (booking systems, streaming, trading)

---

## 🔗 Connection to Other Weeks

**Week 4.5 (Tier 1):** Hash (70%), Monotonic (20%), Merge (30%), Partition (15%), Kadane (10%)  
**Week 5 (Trees):** Hierarchical structures, ordered access, priority queues  
**Week 5.5 (Tier 2):** Range updates (10-15%), space optimization (8-12%), sliding window (5-10%)  
**Week 6+ (Graphs, etc.):** Build on these patterns for complex algorithms

---

## ❓ Frequently Asked Questions

**Q: Do I need to master all 3 Tier 2 patterns?**
A: Yes. Each covers 5-15% of problems. Together 80-88%.

**Q: Can I skip Tier 2 and go to Week 6?**
A: Possible, but many hard problems use these. Recommended to do Tier 2.

**Q: How long does Tier 2 take?**
A: 9-10.5 hours (3 hours per day). Faster than full weeks (12-14 hours).

**Q: Is in-place replacement really that important?**
A: Yes. Interviews heavily prefer O(1) space. Critical for embedded/real-time systems.

**Q: When do I use difference array vs segment tree?**
A: Difference array: batch range updates, one reconstruction. Segment tree: mixed updates + queries.

**Q: How do I extend deque to 2D sliding window?**
A: Use 2D deque (nested deques or custom structure). More complex but same principle.

---

## ✅ Before Proceeding to Week 6

- [ ] Rate 4/5 or higher on all 3 days
- [ ] Can recognize pattern instantly from problem statement
- [ ] Can implement without looking at notes
- [ ] Understand when each pattern is optimal
- [ ] Understand time/space trade-offs

