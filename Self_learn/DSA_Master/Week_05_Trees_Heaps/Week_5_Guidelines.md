# Week 5 Enhanced Guidelines - Master Overview

**Week:** 5 | **Focus:** Trees & Heaps Mastery  
**Difficulty:** 🔴 Hard | **Time:** 15-20 hours | **Interview Weight:** 25-30%

---

## 1️⃣ DAILY BREAKDOWN & TIME ALLOCATION

| Day | Topic | Core Time | Practice | Total | Outcomes |
|-----|-------|-----------|----------|-------|----------|
| **1** | Binary Tree Anatomy | 70 min | 40 min | 2.5 hrs | Understand tree structure, recursion |
| **2** | Tree Traversals | 75 min | 45 min | 2.5 hrs | Master 4 traversal methods |
| **3** | Binary Search Trees | 80 min | 50 min | 2.75 hrs | Implement search/insert/delete |
| **4** | Heaps & Priority Queues | 75 min | 45 min | 2.75 hrs | Understand priority vs sorted |
| **5** | Balanced Trees | 90 min | 60 min | 3 hrs | Rotations, rebalancing concept |
| **Integration** | Problem solving & review | - | 120+ min | 2-3 hrs | Solve 15+ mixed problems |

**Weekly Total:** 15-20 hours (recommended 3-4 hours/day)

---

## 2️⃣ LEARNING OBJECTIVES

### Knowledge Targets (Understanding) ✓

- [ ] **Tree Anatomy:** Nodes, edges, root, leaves, height, subtrees, recursive definition
- [ ] **Traversal Orders:** Preorder, inorder, postorder, level-order (when/why each)
- [ ] **BST Property:** Left < Parent < Right (and recursive application)
- [ ] **Inorder Corollary:** Inorder of BST = sorted values (fundamental)
- [ ] **Heap Property:** Parent ≥ children (max-heap) or ≤ (min-heap)
- [ ] **Balance Concept:** Why height ≈ log(n) matters (O(log n) vs O(n))
- [ ] **Rotations:** How left/right rotation preserves BST while rebalancing
- [ ] **Complexity:** Why O(log n) perfect, O(n) worst case (height dependent)

### Practical Skills (Can Do) ✓

- [ ] **Build Trees:** Create binary tree from values, draw on paper
- [ ] **Implement Traversals:** Recursive preorder, inorder, postorder, level-order (queue-based)
- [ ] **BST Search:** Find value in O(log n) assuming balanced
- [ ] **BST Insert:** Add node maintaining BST property
- [ ] **BST Delete:** Remove node (handle 0, 1, 2 children cases)
- [ ] **Heap Operations:** Insert (bubble-up), delete_root (bubble-down), build_heap
- [ ] **Tree Rotation:** Perform left/right rotation by hand, understand all 4 cases
- [ ] **Validate Trees:** Check if valid BST, valid AVL, valid heap

### Application Abilities (Where to Use) ✓

- [ ] **Problem Recognition:** When is tree structure optimal vs array vs hash table?
- [ ] **Algorithm Design:** How to solve problem using tree structure
- [ ] **Trade-off Decision:** When to use BST vs heap vs balanced tree
- [ ] **Interview Explanation:** Clearly communicate concepts in 1-2 minutes
- [ ] **Production Awareness:** Know MySQL, OS, languages use variants
- [ ] **Complexity Estimation:** Predict time/space before coding
- [ ] **Debug Tree Code:** Find and fix bugs in tree implementations

---

## 3️⃣ CORE CONCEPTS OVERVIEW

### Binary Tree Anatomy
**What it is:** Hierarchical structure where each node ≤ 2 children  
**Why it matters:** Foundation for O(log n) algorithms on hierarchical data  
**Key insight:** Recursively defined → recursion is natural  
**Complexity:** Operations O(h) where h = height (log n to n)

### Tree Traversals
**What they are:** 4 ways to visit all nodes in specific order  
**Why it matters:** Different orders reveal different properties  
**Key orders:**
- Preorder (parent first) → cloning trees
- Inorder (middle) → sorted BST values
- Postorder (parent last) → deleting trees
- Level-order (top-down) → BFS/breadth-first

**Complexity:** All O(n) time (must visit all nodes), O(h) space (recursion depth)

### Binary Search Trees
**What it is:** Tree maintaining left < parent < right everywhere  
**Why it matters:** Sorted + dynamic modification (search/insert/delete all O(log n) if balanced)  
**Key operations:**
- Search: follow left/right based on comparison
- Insert: find position, attach node
- Delete: 3 cases (0 children, 1 child, 2 children with successor)

**Complexity:** O(log n) balanced, O(n) skewed (degenerates to linked list)

### Heaps & Priority Queues
**What it is:** Tree prioritizing min/max element at root  
**Why it matters:** O(1) access to priority element, O(log n) insert/delete  
**Key insight:** Prioritized (not sorted), array-based, no search  

**Complexity:** Insert O(log n), delete O(log n), search O(n) ⚠️

### Balanced Trees
**What they are:** Auto-balancing variants (AVL, Red-Black)  
**Why it matters:** Guarantee O(log n) height regardless of insertion order  
**Key techniques:**
- AVL: strict |height difference| ≤ 1
- RB: looser color-based balance
- Rotations: local restructuring preserving BST

**Trade-off:** More rotations during insert (AVL) vs. slower insertions (RB)

---

## 4️⃣ RECOMMENDED LEARNING PATH

### Why This Order?

1. **Anatomy (Day 1) first:** Foundation for everything else
2. **Traversals (Day 2) second:** How to explore trees you build
3. **BST (Day 3) third:** Apply binary search thinking to trees
4. **Heaps (Day 4) fourth:** Different tree property, independent but important
5. **Balanced (Day 5) last:** Advanced, requires understanding previous concepts

### Building Blocks
```
Trees exist → (Day 1)
    ↓
We visit them → (Day 2)
    ↓
We organize them sorted → (Day 3)
    ↓
And prioritized → (Day 4)
    ↓
And keep them balanced → (Day 5)
```

### Daily Optimal Schedule

**Morning (1.5 hours):**
- 10 min: Review yesterday's concept
- 70-80 min: Read day's material
- 10-20 min: Take notes/digest

**Afternoon (1.5 hours):**
- 45-50 min: Hands-on implementation
- 30-40 min: Solve 2-3 problems
- 10-15 min: Reflect

**Optional Evening:** Review, extra problems if behind

---

## 5️⃣ COMMON MISTAKES TO AVOID

### Binary Tree Mistakes

| Mistake | Why Wrong | Fix | Impact |
|---------|-----------|-----|--------|
| Only checking immediate children in validation | Missing violations deeper | Check ALL descendants recursively | Wrong validation |
| Not handling null pointers | Crashes on None | Always check `if not node` first | Runtime error |
| Confusing height and depth | Different definitions | Height = path to deepest leaf | Wrong complexity analysis |
| Forgetting base cases in recursion | Infinite recursion | Always have `if not node: return` | Stack overflow |
| Unbalanced tree from sorted insert | Degenerates to list | Use balanced trees (coming) | O(n) instead of O(log n) |

### Traversal Mistakes

| Mistake | Why Wrong | Fix | Impact |
|---------|-----------|-----|--------|
| Wrong traversal order | Get wrong information | Pre/In/Post/Level for different needs | Incorrect output |
| Iterative preorder pushing left first | Gets wrong order | Push right THEN left (stack pops reverse) | Wrong traversal |
| Confusing iterative with recursive | Different mechanisms | Recursive uses call stack implicitly | Wrong implementation |

### BST Mistakes

| Mistake | Why Wrong | Fix | Impact |
|---------|-----------|-----|--------|
| Checking only vs immediate children in validation | Left of 5 should ALL be < 5 | Check bounds at every level | Invalid BST accepted |
| Wrong inorder successor in delete | Not maintaining order | Use min of right subtree | BST property broken |
| Not updating parent pointers | Tree becomes disconnected | Manage pointer updates carefully | Orphaned nodes |
| Forgetting delete with 2 children is complex | Easiest case looks simple | Handle 3 cases explicitly | Runtime errors |

### Heap Mistakes

| Mistake | Why Wrong | Fix | Impact |
|---------|-----------|-----|--------|
| Searching in heap expecting O(log n) | Heap not sorted | Must scan all: O(n) | Slow search |
| Wrong bubble-up direction | Violates heap property | Up for insert, down for delete | Heap property broken |
| Off-by-one in array index calculation | Can't find parent/children | Use (i-1)//2 for parent, 2i+1 for left | Memory errors |

### Balancing Mistakes

| Mistake | Why Wrong | Fix | Impact |
|---------|-----------|-----|--------|
| Not updating heights after insertion | Can't detect imbalance | Track height at every node | No rebalancing happens |
| Forgetting rotations preserve BST | Think rotation breaks order | Local operation, BST property maintained | Unnecessary complexity |
| Wrong rotation case | Right rotation fixes left-heavy | Know 4 cases: LL, RR, LR, RL | Doesn't rebalance |

---

## 6️⃣ PRACTICE PROBLEMS GUIDE

### By Difficulty Level

**Easy (5-7 problems, 20-30 min each):**
- Maximum depth of binary tree
- Minimum depth of binary tree
- Is balanced binary tree?
- Validate BST
- Invert binary tree
- Same tree
- Path sum (simple)

Sources: LeetCode (easy tag, tree tag)

**Medium (5-7 problems, 30-45 min each):**
- BST iterator
- Lowest common ancestor
- Serialize/deserialize binary tree
- Construct BST from preorder/inorder
- Kth smallest element in BST
- Convert sorted array to BST
- Heap problem: find median in stream

Sources: LeetCode (medium tag, tree/heap tag)

**Hard (3-5 problems, 45-60 min each):**
- Largest BST subtree
- Binary tree maximum path sum
- Serialize complex tree
- Tree reconstruction from multiple constraints
- Complex heap problem (top K elements)

Sources: LeetCode (hard tag), interview prep

### Problem-Solving Tips

1. **Understand problem first:** What's input, output, constraints?
2. **Choose structure:** Why tree? Could array work better?
3. **Choose technique:** Recursion, iteration, traversal method?
4. **Handle edge cases:** Null pointers, single node, empty tree
5. **Verify complexity:** Is O(log n) expected? Got it?
6. **Test thoroughly:** Sample input, edge cases, large input

---

## 7️⃣ INTERVIEW PREPARATION

### Common Questions by Topic

**Binary Trees:**
- "Explain a binary tree"
- "Difference between tree and graph"
- "How to find height of tree"
- "Are you familiar with tree traversals?"

**Traversals:**
- "Implement inorder traversal"
- "When would you use each traversal?"
- "Can you do this iteratively?"
- "What's the space complexity?"

**BSTs:**
- "Design a BST"
- "Implement search in BST"
- "Can you delete from BST?"
- "How would you validate a BST?"
- "Why use BST vs hash table?"

**Heaps:**
- "How is heap different from BST?"
- "Implement heap insert"
- "Why use heap for priority queue?"
- "Can you find median in stream?"

**Balanced Trees:**
- "Why do we need balancing?"
- "Explain tree rotations"
- "When does rebalancing trigger?"
- "AVL vs Red-Black?"

### Interview Tips

1. **Clarify ambiguities:** "Do you want recursive or iterative?"
2. **State assumptions:** "I'm assuming unique values?"
3. **Explain approach:** "I'll use DFS because..."
4. **Code cleanly:** Readable, proper indentation
5. **Test edge cases:** "Let me test with empty tree..."
6. **Explain complexity:** "Time O(n), space O(h)"
7. **Discuss trade-offs:** "Could also use hash table..."

### Follow-Up Questions to Expect

- "Can you do this in-place?"
- "What if tree is very large?"
- "Can you modify the structure?"
- "How would you handle duplicates?"
- "Can you do it iteratively instead?"

---

## 8️⃣ RESOURCES & REFERENCES

### Online Platforms

**Visualization:**
- VisuAlgo (visual algorithm animator): https://www.cs.usfca.edu/~galles/visualization/BST.html
- Sorting visualizer (includes tree sorts): https://www.cs.usfca.edu/~galles/visualization/Heapsort.html

**Problem Practice:**
- LeetCode Tree problems: https://leetcode.com/tag/binary-tree/
- LeetCode BST: https://leetcode.com/tag/binary-search-tree/
- LeetCode Heap: https://leetcode.com/tag/heap/
- HackerRank Trees: https://www.hackerrank.com/challenges/tree-height-of-a-binary-tree/cpp

**Learning:**
- GeeksforGeeks Binary Trees: https://www.geeksforgeeks.org/binary-tree-data-structure/
- GeeksforGeeks BST: https://www.geeksforgeeks.org/binary-search-tree-data-structure/
- GeeksforGeeks Heaps: https://www.geeksforgeeks.org/heap-data-structure/

### Recommended Books

- *Algorithm Design Manual* by Skiena (chapter on trees)
- *CLRS Introduction to Algorithms* (chapters 12-13)
- *Competitive Programming* (chapter on trees)

### Articles & Tutorials

- AVL Trees: https://www.geeksforgeeks.org/avl-tree-set-1-insertion/
- Red-Black Trees: https://en.wikipedia.org/wiki/Red%E2%80%93black_tree
- Heap Property: https://www.geeksforgeeks.org/binary-heap/

---

## 9️⃣ ASSESSMENT & SUCCESS CRITERIA

### Knowledge Assessment (Self-Rate 1-5)

- [ ] **Tree Structure:** Understanding of nodes, edges, height = ___/5
- [ ] **Traversals:** Can explain all 4 methods = ___/5
- [ ] **BST Property:** Left < parent < right everywhere = ___/5
- [ ] **Balanced Concept:** Why log(n) beats n = ___/5
- [ ] **Heap Priority:** When to use (vs BST) = ___/5
- [ ] **Rotation Mechanics:** Why local rebalances = ___/5

### Practical Skills (Can You...)

- [ ] Build tree from array by hand
- [ ] Implement preorder recursively
- [ ] Implement inorder iteratively
- [ ] Implement level-order with queue
- [ ] Implement BST search
- [ ] Implement BST insert
- [ ] Implement BST delete (all 3 cases)
- [ ] Implement heap insert (bubble-up)
- [ ] Implement heap delete (bubble-down)
- [ ] Perform left rotation by hand

### Confidence Targets

| Topic | Target | Current |
|-------|--------|---------|
| Tree Anatomy | 4/5 | ___/5 |
| Traversals | 4/5 | ___/5 |
| BST Ops | 4/5 | ___/5 |
| Heaps | 4/5 | ___/5 |
| Balancing | 3/5 | ___/5 |

### Success Checklist

- [ ] Understand structure, not just memorize
- [ ] Can explain to someone else clearly
- [ ] Can implement without looking at code
- [ ] Can identify when to use each structure
- [ ] Can solve 15+ problems across levels
- [ ] Confidence 4/5 minimum on most topics

---

## 🔟 CONNECTION TO FUTURE WEEKS

### Week 5.5: TIER 2 Strategic Patterns

**How Week 5 prepares:**
- Trees are special case of graphs
- DFS on trees = DFS on acyclic graphs
- BFS (level-order) = foundation for BFS on graphs
- Tree DP = simpler version of general DP

**Prerequisite:** Master trees first!

### Algorithms Weeks 6+

**Dijkstra:** Uses min-heap for "nearest unvisited"  
**Prim's MST:** Uses min-heap for "cheapest edge"  
**Huffman Coding:** Uses min-heap for "merge lowest frequency"  
**Heap Sort:** Direct application of heap structure  
**Dynamic Programming:** Often uses trees conceptually

### Why This Matters

Trees are the bridge from Week 1-4 (basics) to Weeks 5+ (advanced algorithms).

---

## 1️⃣1️⃣ FREQUENTLY ASKED QUESTIONS

**Q: Is Week 5 really that hard?**  
A: Yes, 25-30% of interviews are tree questions. Master this week!

**Q: Can I skip balanced trees?**  
A: Not recommended. Understanding balance is crucial for interviews.

**Q: Do I need to memorize all rotations?**  
A: No, but understand why they work. Most interviews ask understanding, not memorization.

**Q: What if I'm struggling with rotations?**  
A: Draw them by hand 10+ times. Kinesthetic learning helps!

**Q: Should I use Python heapq or implement from scratch?**  
A: Learn both. Understand mechanics, but use library in practice.

**Q: Are trees more important than arrays/strings?**  
A: Yes, ~30% vs ~25%. Tree mastery opens many doors.

**Q: How do I know when I'm ready for Week 5.5?**  
A: When you can solve medium tree problems independently.

**Q: Why learn both AVL and Red-Black?**  
A: Understand trade-offs. AVL in read-heavy systems, RB in write-heavy (Java).

**Q: Can I do Week 5 in less than 15 hours?**  
A: Possible if strong background, but 15-20 hours recommended for mastery.

---

## 1️⃣2️⃣ SCHEDULE & SUCCESS PATH

### Recommended Weekly Schedule

**Option 1: Full Time (4 hours/day × 5 days)**
- Day 1: 2.5 hours (read + hands-on)
- Day 2: 2.5 hours (read + hands-on)
- Day 3: 2.75 hours (read + hands-on)
- Day 4: 2.75 hours (read + hands-on)
- Day 5: 3 hours (read + hands-on)
- Weekend: 3-4 hours (problems + review)
- **Total: 19.5 hours**

**Option 2: Distributed (1.5-2 hours/day × 10 days)**
- Days 1-2: Anatomy + Traversals
- Days 3-4: BSTs
- Days 5-6: Heaps
- Days 7-8: Balanced Trees
- Days 9-10: Review + problems
- **Total: 20 hours**

### Key Milestones

**By End of Day 1:**
- [ ] Understand tree structure (recursion key)
- [ ] Can implement basic tree properties
- [ ] Confidence: 3-4/5

**By End of Day 2:**
- [ ] All 4 traversals working
- [ ] Understand when to use each
- [ ] Confidence: 4/5

**By End of Day 3:**
- [ ] BST search/insert/delete functional
- [ ] Solved 5 BST problems
- [ ] Confidence: 4/5

**By End of Day 4:**
- [ ] Heap operations functional
- [ ] Understand priority vs sorted
- [ ] Confidence: 4/5

**By End of Day 5:**
- [ ] Understand why rotations work
- [ ] Trace rebalancing by hand
- [ ] Confidence: 3-4/5

**By End of Week 5:**
- [ ] Solved 15+ total problems
- [ ] Confidence 4/5 minimum on all
- [ ] Ready for Week 5.5

### Success Path Visualization

```
Week 5 Start (Foundations)
    ↓
Days 1-2 (Tree concepts)
    ↓ (Check: confidence 4/5)
Days 3-4 (Applications)
    ↓ (Check: solved 10 problems)
Day 5 (Advanced concept)
    ↓ (Check: understand balance)
Week-End Review (Synthesis)
    ↓ (Check: solved 15+ problems)
Week 5 Complete (Ready for Week 5.5)
    ✅ Mastery achieved
```

### Week 5.5 Readiness Criteria

Before moving to Week 5.5, ensure:
- [ ] Comfortable with Days 1-5 concepts
- [ ] Confidence 4/5 minimum on each
- [ ] Solved 15+ practice problems
- [ ] Can explain each topic to someone
- [ ] Understand production usage
- [ ] Ready for graph generalization

---

**Week 5 Enhanced Guidelines**  
**Status:** Complete Reference  
**Version:** 1.0  
**Difficulty:** Hard  
**Time:** 15-20 hours  

**You're ready! Start with Day 1.** 🚀

