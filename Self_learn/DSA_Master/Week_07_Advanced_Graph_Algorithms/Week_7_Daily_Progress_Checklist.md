# Week 7: Daily Progress Checklist

**Week:** 7 | **Topic:** Advanced Graph Algorithms  
**Difficulty:** Hard | **Time Investment:** 25-30 hours total  
**Prerequisites:** Week 6 (Graph Foundations)

---

## 📋 DAILY LEARNING CHECKLIST

### Day 1: Dijkstra's Algorithm (90 minutes)

**Learning Outcomes:**
- [ ] Understand why greedy choice works (non-negative weights)
- [ ] Can trace Dijkstra's algorithm by hand
- [ ] Know time complexity O((V+E) log V) with min-heap
- [ ] Understand priority queue implementation
- [ ] Can identify real-world applications (GPS, routing)

**Instructional Content:**
- [ ] Read all 12 sections (The Why through Cognitive Layer)
- [ ] Understand RAM model and hardware reality
- [ ] Grasp psychological misconceptions about "always use Dijkstra"
- [ ] See design trade-offs vs Bellman-Ford
- [ ] Connect to transformer attention (AI/ML analogy)

**Practice Problems:**
- [ ] Shortest path with weighted edges (basic)
- [ ] Network delay time (LeetCode 743)
- [ ] Path with minimum effort (weighted variant)
- [ ] Find city with smallest distance to all cities
- [ ] Minimum time to collect all apples (modified Dijkstra)

**Checkpoint Questions:**
1. Why does Dijkstra fail on negative weights?
2. How would you find shortest path to specific node (not all)?
3. Why use min-heap instead of sorted list?

---

### Day 2: Bellman-Ford & Floyd-Warshall (100 minutes)

**Learning Outcomes:**
- [ ] Understand Bellman-Ford relaxation concept
- [ ] Can detect negative cycles
- [ ] Know why Floyd-Warshall order matters (k-intermediate-node)
- [ ] Understand time complexity trade-offs
- [ ] Know when to use which algorithm

**Instructional Content:**
- [ ] Master Bellman-Ford relaxation (V-1 iterations)
- [ ] Understand Floyd-Warshall dynamic programming approach
- [ ] Grasp why both handle negative weights
- [ ] Learn about all-pairs vs single-source
- [ ] Understand computational lens: hardware cache behavior

**Practice Problems:**
- [ ] Network delay time with negative edges
- [ ] Find city with minimum cost to connect to all
- [ ] Currency exchange arbitrage detection
- [ ] All-pairs shortest path (Floyd-Warshall)
- [ ] Detect negative cycle

**Checkpoint Questions:**
1. Why V-1 relaxations enough for Bellman-Ford?
2. How to detect negative cycle?
3. When would Floyd-Warshall beat Bellman-Ford?

---

### Day 3: Minimum Spanning Trees (100 minutes)

**Learning Outcomes:**
- [ ] Understand MST problem (V-1 edges, minimum total, acyclic)
- [ ] Can implement Kruskal's with Union-Find
- [ ] Can implement Prim's with priority queue
- [ ] Know complexity trade-offs (sparse vs dense)
- [ ] Understand cut property proof of optimality

**Instructional Content:**
- [ ] Master Kruskal's edge-based approach
- [ ] Master Prim's node-based approach
- [ ] Understand Union-Find optimization (path compression, union by rank)
- [ ] Learn cut property (theoretical foundation)
- [ ] Understand real-world applications (network design, clustering)

**Practice Problems:**
- [ ] Connect all cities with minimum cost (classic MST)
- [ ] Number of operations to make network connected (variant)
- [ ] Optimize cable connection costs
- [ ] Find redundant edges (non-tree edges)
- [ ] MST-based clustering

**Checkpoint Questions:**
1. Why does Kruskal's not create cycles?
2. When to use Kruskal vs Prim?
3. How to verify MST optimality?

---

### Day 4: Network Flow I - Max Flow Basics (110 minutes)

**Learning Outcomes:**
- [ ] Understand max flow problem (capacity constraints, flow conservation)
- [ ] Can trace Ford-Fulkerson by hand
- [ ] Know why Edmonds-Karp is polynomial (BFS matters)
- [ ] Understand residual graph concept (forward + backward edges)
- [ ] Can implement basic max-flow

**Instructional Content:**
- [ ] Master Ford-Fulkerson framework (augmenting paths)
- [ ] Understand bottleneck capacity calculation
- [ ] Learn residual graph concept (critical for rerouting)
- [ ] Understand why BFS makes algorithm polynomial-time
- [ ] Learn real-world applications (routing, bipartite matching prep)

**Practice Problems:**
- [ ] Maximum water flow in network
- [ ] Network flow between source and sink
- [ ] Validate flow in graph (feasibility checking)
- [ ] Minimum cut finding
- [ ] Maximum disjoint paths

**Checkpoint Questions:**
1. Why do we need backward edges in residual graph?
2. What's bottleneck capacity?
3. How does BFS improve Ford-Fulkerson?

---

### Day 5: Network Flow II - Advanced Applications (120 minutes)

**Learning Outcomes:**
- [ ] Understand min-cut and max-flow min-cut theorem
- [ ] Can convert bipartite matching to flow problem
- [ ] Know min-cost max-flow applications
- [ ] Understand König's theorem implications
- [ ] Can apply flow to diverse problems

**Instructional Content:**
- [ ] Master min-cut finding algorithm
- [ ] Master bipartite matching reduction
- [ ] Understand max-flow min-cut theorem proof
- [ ] Learn min-cost max-flow (successive shortest paths)
- [ ] Understand real-world: network robustness, job placement, image segmentation

**Practice Problems:**
- [ ] Maximum bipartite matching (students to projects)
- [ ] Image segmentation using min-cut (conceptual)
- [ ] Maximum matching with constraints
- [ ] Minimum vertex cover (König's theorem)
- [ ] Stable matching variants

**Checkpoint Questions:**
1. How to find min-cut after max-flow?
2. How does bipartite matching convert to flow?
3. When would min-cost max-flow be needed?

---

## 🎯 WEEKLY INTEGRATION

### Cross-Day Patterns

**Shortest Paths Evolution:**
- Day 1: Non-negative weights (Dijkstra, greedy)
- Day 2: Negative weights (Bellman-Ford, DP), all-pairs (Floyd-Warshall)
- Pattern: Algorithm complexity increases with problem generality

**Trees & Graphs:**
- Day 3: MST (no cycles, minimum spanning)
- Day 4-5: Flow networks (cycles allowed, capacities matter)
- Pattern: Different problems, different properties

**Problem-Solving Progression:**
- Day 1: Find optimal single-source distances
- Day 2: Find optimal all-pairs distances or detect negative cycles
- Day 3: Find optimal tree connecting all nodes
- Day 4-5: Find optimal flow distribution with constraints

---

## 📊 WEEKLY TIME ALLOCATION (30 hours total)

| Activity | Hours | Breakdown |
|----------|-------|-----------|
| Instructional Reading | 8 | 1.5-2 per day |
| Problem Solving | 12 | 2-2.5 per day |
| Cognitive Integration | 4 | Review of multi-lens perspectives |
| Implementation Practice | 4 | Coding algorithms from scratch |
| Interview Simulation | 2 | Timed problem solving |
| **Total** | **30** | **5-6 hours per day** |

---

## ✅ MASTERY VERIFICATION

### After Day 1 (Dijkstra):
- [ ] Can implement from scratch
- [ ] Can explain to someone else
- [ ] Can solve 5+ variations
- [ ] Understand hardware implications
- [ ] Know when it's the right tool

### After Day 2 (Bellman-Ford & Floyd-Warshall):
- [ ] Understand when Dijkstra insufficient
- [ ] Can choose between three algorithms
- [ ] Understand all-pairs optimizations
- [ ] Can detect negative cycles

### After Day 3 (MST):
- [ ] Can implement both Kruskal and Prim
- [ ] Understand Union-Find optimizations
- [ ] Know real-world applications
- [ ] Can prove optimality via cut property

### After Day 4 (Max Flow Basics):
- [ ] Can trace Ford-Fulkerson manually
- [ ] Understand residual graph deeply
- [ ] Know complexity: Edmonds-Karp O(VE²)
- [ ] Can identify flow problems

### After Day 5 (Advanced Flow):
- [ ] Understand min-cut finding
- [ ] Can solve bipartite matching via flow
- [ ] Know when to use flow-based reduction
- [ ] Understand real-world applications

---

## 🚨 COMMON PITFALLS TO AVOID

1. **Day 1-2:** Confusing when to use Dijkstra vs Bellman-Ford
   - Fix: Non-negative = Dijkstra always
   - Fix: Negative weights = Bellman-Ford required

2. **Day 3:** Forgetting Union-Find optimization
   - Fix: Path compression + union by rank = O(α(V)) ≈ O(1)
   - Fix: Kruskal O(E log E), not O(E × E)

3. **Day 4:** Misunderstanding residual graph
   - Fix: Backward edges enable rerouting (not undoing)
   - Fix: Both forward and backward in residual

4. **Day 5:** Overcomplicating bipartite matching
   - Fix: Just set all capacities to 1
   - Fix: Source/sink trick makes it standard flow

---

## 📚 RECOMMENDED RESOURCES

**For Each Day:**

Day 1: Dijkstra
- Textbook: CLRS Chapter 24.3
- Visualization: pathfinding.visualizations.github.io
- Practice: LeetCode 743, 787, 1514

Day 2: Bellman-Ford & Floyd-Warshall
- Textbook: CLRS Chapter 24.1, 25.2
- Practice: LeetCode variations with negative weights
- Visualization: algorithm visualizers for relaxation

Day 3: MST
- Textbook: CLRS Chapter 23
- Visualization: MST visualizers (Kruskal vs Prim)
- Practice: MST problems in various forms

Day 4-5: Flow
- Textbook: CLRS Chapter 26
- Visualization: Flow network simulators
- Practice: LeetCode flow problems, bipartite matching

---

## 🎓 INTERVIEW PREPARATION

### Typical Interview Questions (Week 7)

**Easy (Days 1-2):**
- Shortest path in weighted graph (Dijkstra)
- Network delay time (Dijkstra variant)
- Cheapest flight (Dijkstra with K stops)

**Medium (Day 3):**
- Minimum spanning tree variations
- Connect cities with minimum cost
- Redundant connections (MST property)

**Hard (Days 4-5):**
- Maximum flow (direct or disguised)
- Bipartite matching (as flow problem)
- Min-cut (network robustness)

---

## ⏰ DAILY SCHEDULE

### Recommended Time Allocation Per Day

**Total:** 5-6 hours

```
0:00-1:30: Instructional reading (all 12 sections)
1:30-2:00: Active review of cognitive layers
2:00-4:30: Problem solving (2-3 problems)
4:30-5:00: Implementation from scratch
5:00-5:30: Reflection & connect to previous days
5:30-6:00: Prepare for next day (preview)
```

---

**Week 7: Complete Curriculum Checklist Ready**  
**Status:** Use this to track daily progress and weekly mastery  
**Next:** Weekly Summary & Integration Points

