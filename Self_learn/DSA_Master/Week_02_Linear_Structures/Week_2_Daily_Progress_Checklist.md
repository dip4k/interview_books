# Week 2: Daily Progress Checklist

## 📋 DAY 1: Arrays

### Morning Objectives
- [ ] Understand direct addressing: arr[i] at address base + i×size
- [ ] Understand O(1) access via arithmetic
- [ ] Understand O(n) insertion/deletion via shifting
- [ ] Recognize cache-friendly sequential access

### Core Learning
- [ ] Read: Week_2_Day_1_Arrays_Instructional.md (sections 1-11)
- [ ] Trace: 5 array operations by hand
- [ ] Analyze: Complexity table for all operations

### Practice Problems
- [ ] Explain why array access is O(1)
- [ ] Calculate address for arr[i] given base and size
- [ ] Trace insertion with shifting
- [ ] Predict cache performance for sequential vs random

### Mastery Checklist
- [ ] Can explain RAM model → direct addressing → O(1)
- [ ] Can trace any operation by hand
- [ ] Understand why cache matters
- [ ] Know when to use arrays

**Confidence Rating**: ___ / 5

---

## 📋 DAY 2: Dynamic Arrays

### Morning Objectives
- [ ] Understand exponential growth strategy (2x doubling)
- [ ] Understand amortized analysis
- [ ] Know resize cost: occasional O(n), amortized O(1) per append
- [ ] Understand capacity vs size

### Core Learning
- [ ] Read: Week_2_Day_2_Dynamic_Arrays_Instructional.md
- [ ] Trace: Sequence of appends showing resizes
- [ ] Calculate: Total cost for n appends

### Practice Problems
- [ ] Prove amortized O(1) for doubling growth
- [ ] Calculate resize times for n=1000
- [ ] Compare doubling vs linear growth cost
- [ ] Identify memory overhead

### Mastery Checklist
- [ ] Can explain doubling strategy clearly
- [ ] Can derive O(1) amortized from first principles
- [ ] Understand why exponential beats linear
- [ ] Know resize pauses happen occasionally

**Confidence Rating**: ___ / 5

---

## 📋 DAY 3: Linked Lists

### Morning Objectives
- [ ] Understand pointer-chasing: O(n) access
- [ ] Understand relink: O(1) insertion at known position
- [ ] Recognize cache-unfriendly scattered memory
- [ ] Know when lists are appropriate (undo/redo, allocators, LRU)

### Core Learning
- [ ] Read: Week_2_Day_3_Linked_Lists_Instructional.md
- [ ] Trace: Access and insertion operations
- [ ] Visualize: Node layout in memory

### Practice Problems
- [ ] Trace access to node at position i
- [ ] Trace insertion at known position
- [ ] Explain "O(1) IF you have pointer" caveat
- [ ] Compare cache performance vs arrays

### Mastery Checklist
- [ ] Can explain pointer-chasing cost
- [ ] Understand O(1) insertion requires known position
- [ ] Know cache impact (50x slower than arrays)
- [ ] Know rare use cases

**Confidence Rating**: ___ / 5

---

## 📋 DAY 4: Stacks & Queues

### Morning Objectives
- [ ] Understand LIFO: Last In First Out
- [ ] Understand FIFO: First In First Out
- [ ] Know push/pop/enqueue/dequeue are O(1)
- [ ] Recognize use cases (undo, scheduling, BFS)

### Core Learning
- [ ] Read: Week_2_Day_4_Stacks_Queues_Instructional.md
- [ ] Implement: Stack using array
- [ ] Implement: Queue using circular buffer
- [ ] Trace: Operations step by step

### Practice Problems
- [ ] Implement stack.push, pop, peek correctly
- [ ] Implement queue.enqueue, dequeue, peek correctly
- [ ] Trace sequence of stack operations
- [ ] Trace sequence of queue operations
- [ ] Solve: Queue using two stacks (bonus)

### Mastery Checklist
- [ ] Can implement both correctly from scratch
- [ ] Can trace by hand
- [ ] Understand LIFO vs FIFO difference
- [ ] Know real-world uses

**Confidence Rating**: ___ / 5

---

## 📋 DAY 5: Binary Search

### Morning Objectives
- [ ] Understand divide-and-conquer: eliminate half each step
- [ ] Understand O(log n) complexity derivation
- [ ] Know precondition: array MUST be sorted
- [ ] Recognize use cases (database lookup, git bisect)

### Core Learning
- [ ] Read: Week_2_Day_5_Binary_Search_Instructional.md
- [ ] Trace: Search for multiple targets on same array
- [ ] Derive: T(n) = T(n/2) + O(1) = O(log n)

### Practice Problems
- [ ] Trace binary search on [10,20,30,40,50] for target=30
- [ ] Trace search for target not found
- [ ] Calculate comparisons needed for n=1,000,000
- [ ] Identify what breaks if array unsorted
- [ ] Implement recursive vs iterative

### Mastery Checklist
- [ ] Can trace by hand without errors
- [ ] Can derive O(log n) from recurrence
- [ ] Understand precondition (SORTED!) is critical
- [ ] Know when binary search applies

**Confidence Rating**: ___ / 5

---

## 🔄 WEEKLY INTEGRATION & SYNTHESIS (3 hours)

### Step 1: Structure Comparison (60 min)
- [ ] Complete comparison table (access, insert, delete, space, cache)
- [ ] Create mental model for each structure
- [ ] List 3+ real-world examples per structure

### Step 2: Problem-Solving Practice (90 min)
- [ ] Solve 5 mixed problems (one per topic)
- [ ] Choose structure BEFORE coding
- [ ] Trace solutions step by step
- [ ] Identify operations used

### Step 3: Mastery Verification (45 min)
- [ ] Rate confidence on each day (1-5)
- [ ] Answer open-ended questions per day
- [ ] Identify weak areas
- [ ] Plan additional practice

### Step 4: Interview Prep (45 min)
- [ ] Answer: "When do you use array vs list?"
- [ ] Answer: "What's amortized complexity?"
- [ ] Answer: "Binary search precondition?"
- [ ] Answer: "Cache impact on performance?"

---

## 📊 DAILY SELF-ASSESSMENT

| Day | Topic | Understanding | Application | Confidence | Notes |
|-----|-------|---|---|---|---|
| **1** | Arrays | ___ | ___ | ___ / 5 | |
| **2** | Vectors | ___ | ___ | ___ / 5 | |
| **3** | Lists | ___ | ___ | ___ / 5 | |
| **4** | Stack/Queue | ___ | ___ | ___ / 5 | |
| **5** | BinarySearch | ___ | ___ | ___ / 5 | |

**Target:** 4/5 or higher on all before Week 3

---

## ⚠️ RED FLAGS (Need More Practice)

- ❌ "I don't understand why array access is O(1)"
- ❌ "Amortized complexity still confuses me"
- ❌ "When would I use linked lists?"
- ❌ "Can't implement binary search without looking it up"
- ❌ "Don't know difference between stack and queue"
- ❌ "Can't analyze complexity of operations"

**Action:** Spend 1-2 more days on weak areas before proceeding to Week 3.

---

## ✅ WEEK 2 COMPLETION CHECKLIST

### Knowledge Check
- [ ] Can explain direct addressing (address = base + i × size)
- [ ] Can explain amortized O(1) append
- [ ] Can explain pointer-chasing O(n) access
- [ ] Can distinguish LIFO (stack) from FIFO (queue)
- [ ] Can explain why binary search needs sorted array

### Skills Check
- [ ] Can analyze array operation complexity
- [ ] Can trace vector resizing
- [ ] Can implement stack and queue from scratch
- [ ] Can trace binary search by hand
- [ ] Can choose right structure for problem

### Judgment Check
- [ ] Can choose array vs vector for problem
- [ ] Can choose array vs list vs stack vs queue
- [ ] Can identify cache impact
- [ ] Can optimize structure choice
- [ ] Can explain trade-offs

---

## 📈 Week 2 Summary

**Time Invested:** ~10-12 hours (2-2.5 per day)  
**Topics Mastered:** 5 fundamental structures + binary search  
**Problems Solved:** 40-50 practice problems  
**Real Systems Analyzed:** 20+ examples  

**Result:** Ready for Week 3 with solid linear structure foundation.

**Next:** Week 3 (Sorting & Hashing) builds directly on arrays and binary search.

---

## 🎓 Final Sign-Off

**I am ready to move to Week 3:** YES / NO

If YES: Proceed to Week 3  
If NO: Identify weak areas and spend 1-2 more days practicing before proceeding.

