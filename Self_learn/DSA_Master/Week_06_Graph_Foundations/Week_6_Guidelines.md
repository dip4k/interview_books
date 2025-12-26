# Week 6 Enhanced Guidelines - Master Overview

**Week:** 6 | **Focus:** Graph Foundations Mastery  
**Difficulty:** 🔴 Hard | **Time:** 25-30 hours | **Interview Weight:** 40-60%

---

## 1️⃣ WEEK 6 MISSION

Master five graph algorithms covering **40-60% of graph interview problems**.

From optimization (Week 5.5) → graph foundations (Week 6) → advanced algorithms (Week 7).

---

## 2️⃣ THE FIVE TECHNIQUES AT A GLANCE

| Technique | Problem | Solution | Time | Space | Interview % |
|-----------|---------|----------|------|-------|------------|
| **Graph Repr.** | Store graphs | Matrix/List | - | O(n²) or O(n+m) | Foundation |
| **BFS** | Shortest path | Queue, level-by-level | O(V+E) | O(V) | 15-20% |
| **DFS** | Connectivity | Stack, recursive | O(V+E) | O(V) | 20-25% |
| **Topo Sort** | Ordering DAG | DFS/Kahn's | O(V+E) | O(V) | 10-15% |
| **Union-Find** | Components | Parent + compression | O(α(n)) | O(V) | 10-15% |

---

## 3️⃣ DAILY BREAKDOWN & TIME ALLOCATION

**Phase 1: Foundations (Days 1-3)** - 9 hours
- Day 1 Representations: 3 hrs
- Day 2 BFS: 3 hrs
- Day 3 DFS: 3 hrs

**Phase 2: Advanced (Days 4-5)** - 6 hours
- Day 4 Topological Sort: 3 hrs
- Day 5 Union-Find: 3 hrs

**Phase 3: Mastery (10-15 hours)**
- Problem solving sprint
- 20+ problems total
- Interview simulation

---

## 4️⃣ LEARNING OBJECTIVES

### Knowledge (Understanding)
- [ ] Two graph representations and trade-offs
- [ ] BFS for shortest paths in unweighted graphs
- [ ] DFS for connectivity and exploration
- [ ] Topological sort for DAGs and dependencies
- [ ] Union-Find for components and near-O(1) operations

### Skills (Can Do)
- [ ] Code all 5 algorithms from scratch
- [ ] Choose representation for problem
- [ ] Implement BFS with distance tracking
- [ ] Implement DFS (recursive & iterative)
- [ ] Implement both topological sort methods
- [ ] Implement Union-Find with optimizations

### Application (Where to Use)
- [ ] Recognize algorithm from problem statement
- [ ] Solve interview problems in 20-30 minutes
- [ ] Handle edge cases (disconnected, cycles, etc.)
- [ ] Discuss complexity and trade-offs
- [ ] Suggest optimizations

---

## 5️⃣ PATTERN RECOGNITION FRAMEWORK

### Decision Tree

```
Graph problem?

├─ Find shortest path (unweighted)?
│  └─ BFS (Day 2)
├─ Need to explore deeply or backtrack?
│  └─ DFS (Day 3)
├─ Need to order tasks with dependencies?
│  └─ Topological Sort (Day 4)
├─ Need to find connected components?
│  └─ Union-Find (Day 5)
├─ How to store graph?
│  ├─ Dense (>20% edges)? → Matrix
│  └─ Sparse (<5% edges)? → Adjacency List
└─ Still not sure?
   └─ Reference Decision Matrix
```

### Keywords Recognition

**BFS triggers:**
- Shortest path, level-by-level, distance, closest, degree

**DFS triggers:**
- All paths, backtrack, connectivity, cycle, deep exploration

**Topo Sort triggers:**
- Dependencies, ordering, prerequisites, DAG, scheduling

**Union-Find triggers:**
- Connected, components, grouping, merging, sets

**Representation triggers:**
- Dense vs sparse, O(1) edge lookup, memory constraint

---

## 6️⃣ COMMON MISTAKES & HOW TO AVOID

| Mistake | Why Wrong | Prevention |
|---------|-----------|-----------|
| Forget visited set in BFS | Infinite loop | Always mark visited immediately |
| Use BFS on weighted graph | Doesn't account for weights | Use Dijkstra for weighted |
| DFS without base case | Stack overflow | Check visited/base case |
| Topological sort on cyclic graph | Invalid result | Verify DAG first or detect cycle |
| Union-Find without optimizations | O(n) instead of O(α(n)) | Always use path compression + union by rank |
| Adjacency matrix for sparse | Memory explosion | Use adjacency list for sparse graphs |

---

## 7️⃣ INTERVIEW PREPARATION

### 30-Second Explanations

**Graph Representations:**
> "For sparse graphs I use adjacency list (O(n+m) space). For dense graphs or when O(1) edge lookup critical, I use matrix (O(n²) space)."

**BFS:**
> "BFS explores level-by-level using a queue. First time we reach a node is guaranteed shortest distance. Time: O(V+E), Space: O(V)."

**DFS:**
> "DFS explores deep using recursion (or explicit stack). Finds all connected nodes and can detect cycles. Time: O(V+E), Space: O(V) call stack."

**Topological Sort:**
> "For DAGs, reverse DFS finishing order gives topological sort. Alternatively, Kahn's algorithm removes nodes with in-degree 0. Both O(V+E)."

**Union-Find:**
> "Path compression + union by rank gives O(α(n)) ≈ O(1) amortized. Used for components, cycle detection, and Kruskal's MST."

### Code in 5 Minutes

- Graph representation: 2-3 lines
- BFS: 8-10 lines
- DFS: 6-8 lines
- Topological: 10-12 lines
- Union-Find: 15-20 lines (with optimizations)

### Solve in 20-30 Minutes

- Easy problems: 15-20 min
- Medium problems: 20-30 min
- Hard problems: 30-45 min

---

## 8️⃣ PRACTICE PROGRESSION

### Week 6 Problem Target: 20+ Total

**By Technique:**
- Graph representations: 2-3 problems
- BFS: 3-5 problems
- DFS: 3-5 problems
- Topological sort: 2-3 problems
- Union-Find: 3-5 problems

**By Difficulty:**
- Easy: 7-10 problems (basics)
- Medium: 7-9 problems (typical interviews)
- Hard: 2-3 problems (advanced)

**Recommended Sources:**
- LeetCode (primary)
- HackerRank (alternative)
- Company-specific archives

---

## 9️⃣ RESOURCES & EXTERNAL LINKS

**Visualization:**
- https://www.cs.usfca.edu/~galles/visualization/BFS.html (BFS)
- https://www.cs.usfca.edu/~galles/visualization/DFS.html (DFS)

**Practice:**
- LeetCode Graph tag: 600+ problems
- HackerRank: Good explanations

**Reference:**
- [85] Summary (quick lookup)
- [79-83] Instructional files
- [87] Q&A with answers

---

## 🔟 ASSESSMENT & SUCCESS CRITERIA

### Knowledge Assessment (Rate 1-5)

| Concept | Rating |
|---------|--------|
| Graph representations | ___/5 |
| BFS understanding | ___/5 |
| DFS understanding | ___/5 |
| Topological sort | ___/5 |
| Union-Find | ___/5 |

**Target:** 4/5 on all

### Practical Skills (Can You...)

- [ ] Implement adjacency matrix from scratch in < 2 min
- [ ] Implement adjacency list from scratch in < 2 min
- [ ] Code BFS from scratch in < 5 min
- [ ] Code DFS from scratch in < 5 min
- [ ] Code topological sort from scratch in < 7 min
- [ ] Code Union-Find from scratch in < 10 min

### Interview Readiness (Pre-Interview)

- [ ] Explain each technique in 30 sec
- [ ] Solve easy problems in 15 min
- [ ] Solve medium problems in 25 min
- [ ] Recognize which algorithm(s) apply
- [ ] Write production-quality code
- [ ] Discuss optimizations

---

## 1️⃣1️⃣ WEEK 6 INTEGRATION POINTS

### With Week 5.5 (Optimization)
- Week 5.5 optimized arrays
- Week 6 builds on data structures
- Both require choosing right structure for algorithm

### With Week 7 (Advanced Graphs)
- Dijkstra = BFS + priority queue
- Bellman-Ford = relaxation via DFS/BFS
- MST algorithms use Union-Find
- Advanced problems combine multiple techniques

### With Interviews
- Week 6 covers 40-60% of graph problems
- Essential for Google, Meta, Amazon, Microsoft
- Tests understanding of graphs + algorithms

---

## 1️⃣2️⃣ WEEK 6 TO WEEK 7 TRANSITION

### Before Moving to Week 7, Verify:

✅ **Readiness Checklist:**
- [ ] Understand all 5 techniques conceptually
- [ ] Confidence 4/5 on Days 1-5
- [ ] Solved 20+ problems across all techniques
- [ ] Can recognize algorithm from problem statement
- [ ] Can code from scratch in allotted time
- [ ] Can explain algorithms clearly

✅ **Performance Targets:**
- [ ] Easy problems: 90% success
- [ ] Medium problems: 70% success
- [ ] Hard problems: 50% success
- [ ] Average time within limits

✅ **Confidence Levels:**
- [ ] Overall confidence: 4/5
- [ ] Ready for advanced graph problems: YES

### If Not Ready:
1. Identify weak technique(s)
2. Review specific instructional file
3. Solve 5+ problems on weak technique
4. Return to readiness checklist

### If Ready:
→ Proceed to Week 7 (Advanced Graph Algorithms)

---

## 📝 FINAL SUMMARY

| Dimension | Week 6 |
|-----------|--------|
| **Topics** | 5 graph algorithms |
| **Time** | 25-30 hours |
| **Problems** | 20+ required |
| **Difficulty** | Hard |
| **Interview %** | 40-60% of graph problems |
| **Key Skill** | Pattern recognition for graphs |
| **Next Step** | Week 7 (Advanced) |

---

## ✅ SUCCESS DEFINITION

**You've mastered Week 6 when:**

1. **Knowledge:** Can explain all 5 algorithms in detail
2. **Skills:** Can code all 5 from scratch quickly
3. **Application:** Can recognize which algorithm(s) apply
4. **Proficiency:** Can solve medium/hard problems consistently
5. **Speed:** Can solve problems within time limits
6. **Confidence:** Feel 4/5 confidence on each technique

---

**Week 6 Enhanced Guidelines Complete**  
**Status:** Ready for learning  
**Goal:** Master graph foundations  
**Outcome:** 40-60% interview coverage  

**Let's master graphs!** 🚀

