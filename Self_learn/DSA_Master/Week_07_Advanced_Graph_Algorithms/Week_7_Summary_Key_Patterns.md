# Week 7: Summary & Key Patterns

**Week:** 7 | **Topic:** Advanced Graph Algorithms Summary  
**Time Investment:** 25-30 hours | **Interview Coverage:** 40-50%

---

## 🎯 WEEK OVERVIEW

Week 7 transitions from basic graph exploration to weighted graph optimization. Five fundamental algorithms solve different optimization problems on weighted graphs.

**Learning Arc:**
```
Day 1: Single-source shortest path (non-negative) → Dijkstra
Day 2: Single-source & all-pairs (negative allowed) → Bellman-Ford, Floyd-Warshall
Day 3: Minimum spanning tree → Kruskal's, Prim's
Day 4: Maximum flow basics → Ford-Fulkerson, Edmonds-Karp
Day 5: Flow applications → Min-cut, Bipartite Matching, Min-cost Flow
```

---

## 🔑 KEY ALGORITHMS AT A GLANCE

### Algorithm Comparison Table

| Algorithm | Problem | Time | Space | When Use |
|-----------|---------|------|-------|----------|
| **Dijkstra** | Single-source shortest path | O((V+E)log V) | O(V+E) | Non-negative weights |
| **Bellman-Ford** | Single-source, negative weights | O(V×E) | O(V+E) | Negative weights required |
| **Floyd-Warshall** | All-pairs shortest path | O(V³) | O(V²) | Small graphs, all pairs needed |
| **Kruskal's** | Minimum spanning tree | O(E log E) | O(V+E) | Sparse graphs, simplicity |
| **Prim's** | Minimum spanning tree | O((V+E) log V) | O(V+E) | Dense graphs, efficiency |
| **Ford-Fulkerson** | Maximum flow framework | O(E × max_flow) | O(V+E) | With DFS, not polynomial |
| **Edmonds-Karp** | Maximum flow (polynomial) | O(V×E²) | O(V+E) | Safe choice, guaranteed polynomial |

---

## 💡 MENTAL MODELS FOR EACH DAY

### Day 1: Dijkstra's "Expanding Ripples"
```
Imagine ripples expanding from source:
  Wave 1: Reaches immediate neighbors
  Wave 2: Reaches second-nearest
  Order of reaching = order Dijkstra visits
  
Why it works: Greedy (always closest next) is optimal
              Because no negative weights "improve" distant paths
```

### Day 2: Bellman-Ford "Relaxation Iterations"
```
Like water flowing through network:
  Iteration 1: Find direct paths
  Iteration 2: Find paths through one intermediary
  Iteration 3: Find paths through two intermediaries
  ...
  Iteration V-1: Find longest shortest paths
  
Why V-1: Longest shortest path = V-1 edges
```

### Day 3: MST "Greedy Tree Building"
```
Kruskal: Build by picking cheapest edges (avoid cycles)
Prim: Grow from seed, always expand to nearest new node

Both optimal because of cut property:
  Minimum edge crossing any partition is in some MST
```

### Day 4: Ford-Fulkerson "Augmenting Paths"
```
Keep pushing more flow until stuck:
  1. Find path from source to sink in residual graph
  2. Push bottleneck amount along path
  3. Update residual (forward down, backward up)
  4. Repeat until no path
  
Why it works: Max-flow min-cut theorem guarantees optimality
```

### Day 5: Flow Applications "Problem Reduction"
```
Min-cut: Find bottleneck edges after max-flow
Bipartite matching: Set all capacities to 1
Min-cost flow: Add cost dimension to flow
```

---

## 🔗 ALGORITHM RELATIONSHIPS

```
                    Shortest Paths
                         |
                    /----+----\
                Dijkstra  |  Bellman-Ford
              (non-neg)   |  (negative)
                          |
                   Floyd-Warshall
                   (all-pairs)
                         |
                    Spanning Trees
                    (MST connects all)
                         |
                    /----+----\
                 Kruskal  | Prim
                (edge-based)(node-based)
                         |
                   Network Flow
                 (capacity-based routing)
                         |
                    /----+----\
                  Max-Flow  | Applications
                        | (min-cut, matching)
```

---

## 📊 PROBLEM SOLVING PATTERNS

### Pattern 1: When to Use Which Algorithm

```
Problem: Find shortest path between two cities
  → Dijkstra (fastest for single-source)

Problem: Find shortest path, some roads have negative value
  → Bellman-Ford (handles negative)

Problem: Shortest path from every city to every city
  → Floyd-Warshall (all-pairs)

Problem: Connect all cities with minimum road cost
  → MST (Kruskal or Prim)

Problem: Maximum flow of goods from warehouse to market
  → Max-flow (Ford-Fulkerson / Edmonds-Karp)

Problem: Match students to internships (one-to-one)
  → Flow-based bipartite matching
```

### Pattern 2: Graph Property Impact

```
Sparse (E ≈ V):
  Dijkstra: O(V log V) good
  Prim with heap: O(V log V) good
  Kruskal: O(V log V) good
  
Dense (E ≈ V²):
  Dijkstra: O(V² log V) bad
  Prim with heap: O(V² log V) okay
  Kruskal: O(V² log V) bad (sorting)
  Floyd-Warshall: O(V³) competitive
```

### Pattern 3: Capacity/Weight Properties

```
Non-negative weights:
  Use Dijkstra (fastest)
  
Negative weights, no negative cycles:
  Use Bellman-Ford (slower but works)
  
Negative weights + cycle detection needed:
  Use Bellman-Ford (detects cycles)
  
All-pairs needed (any weights):
  Use Floyd-Warshall
  
Capacities (flow problem):
  Use network flow algorithms
```

---

## 🎓 INTERVIEW PATTERNS

### Easy Level Interview Problems

```
1. Dijkstra Direct:
   - Network delay time
   - Minimum time visiting all nodes
   - Cheapest flight path

2. MST Recognition:
   - Connect cities with minimum cost
   - Number of operations to connect components

3. Flow Basics:
   - Maximum water flow (direct max-flow)
   - Network flow value calculation
```

### Medium Level Interview Problems

```
1. Dijkstra Variants:
   - Shortest path with obstacles
   - Path with minimum effort (weight variant)
   - Find K paths or K routes

2. MST Applications:
   - Minimum spanning tree with constraints
   - Redundancy analysis
   - Approximate traveling salesman

3. Bipartite Matching:
   - Student to project assignment
   - Maximum matching with unit capacities
```

### Hard Level Interview Problems

```
1. Min-Cut Recognition:
   - Vertex/edge cut problems
   - Network robustness analysis
   - Image segmentation conceptually

2. Min-Cost Flow:
   - Cost minimization with flow requirements
   - Optimal routing with transportation cost

3. Complex Flow:
   - Multiple commodity flows
   - Circulation with demands
   - Matching with preferences
```

---

## ⚠️ COMMON MISTAKES & FIXES

### Mistake 1: Using Dijkstra with Negative Weights
```
Wrong: Always use Dijkstra
Fix: Check for negative weights first
     Non-negative → Dijkstra
     Negative → Bellman-Ford
```

### Mistake 2: Implementing Ford-Fulkerson Without BFS
```
Wrong: Use DFS for augmenting paths
Problem: Can be O(E × max_flow) — not polynomial!
Fix: Use BFS (Edmonds-Karp) for polynomial-time guarantee
     O(V × E²)
```

### Mistake 3: Forgetting Residual Graph
```
Wrong: Just track current flow
Problem: Can't reroute to find better solutions
Fix: Maintain residual graph with:
     - Forward edges (remaining capacity)
     - Backward edges (ability to undo flow)
```

### Mistake 4: Overcomplicating Bipartite Matching
```
Wrong: Design custom matching algorithm
Problem: Complex and error-prone
Fix: Convert to flow problem (standard reduction)
     - Source to left (cap 1)
     - Left to right (cap 1)
     - Right to sink (cap 1)
     - Max-flow = max matching
```

### Mistake 5: Not Recognizing Flow Problems in Disguise
```
Common disguises:
  - Bipartite matching → recognize and use flow
  - Min-cut/vertex cut → recognize max-flow min-cut
  - Assignment problems → often flow-based
  
Strategy: Look for capacity constraints + optimization
         If present, likely flow problem
```

---

## 🧠 COGNITIVE INSIGHTS FROM WEEK

### Computational Reality vs Theory

```
Theory says:
  All O(E log V) algorithms same speed

Reality shows:
  - Dijkstra: excellent cache behavior
  - Bellman-Ford: poor cache behavior
  - Floyd-Warshall: mediocre cache behavior
  
Implementation matters! Constants hidden in Big-O
```

### Psychological Insights

```
Students often believe:
  1. "Algorithm with better O() always faster"
  2. "Greedy = suboptimal"
  3. "Flow = only for fluid dynamics"

Reality:
  1. Constants matter; must consider hardware
  2. Greedy optimal with right choice of "minimum"
  3. Flow = fundamental optimization (many problems reducible)
```

### Design Trade-offs

```
Kruskal vs Prim:
  Not just complexity difference
  Different algorithmic ideas (edge-based vs node-based)
  Same result, different path to solution

Dijkstra vs Floyd-Warshall:
  Dijkstra: faster for single-source, sparse
  Floyd-Warshall: simpler code, O(V³) for all-pairs
  Choose based on problem + graph structure
```

### AI/ML Connections

```
Week 7 algorithms appear in:
  - Dijkstra: pathfinding in games, robots
  - Bellman-Ford: value iteration in RL
  - MST: clustering, hierarchical structures
  - Max-flow: attention patterns, optimal transport
  
Modern ML extensively uses graph algorithms
```

---

## 📈 MASTERY PROGRESSION

### Level 1: Can Implement (Days 1-3)
- Implement Dijkstra from scratch
- Implement Kruskal with Union-Find
- Implement Prim with heap
- Understanding grows with implementation

### Level 2: Can Apply to New Problems (Days 4-5)
- Recognize when to use each algorithm
- Choose between alternatives
- Understand trade-offs
- Adapt algorithms for problem variants

### Level 3: Can Analyze & Optimize
- Understand why each algorithm works (cut property, etc.)
- Predict real-world performance (cache effects, etc.)
- Optimize implementations
- Parallelize where possible

### Level 4: Can Teach & Mentor
- Explain to others without notes
- Answer "why" questions deeply
- Provide intuition with mental models
- Guide others through problem-solving

---

## 🎯 WEEK 7 SUCCESS CHECKLIST

### Foundational Understanding ✓
- [ ] Understand 5 core algorithms deeply
- [ ] Know when to use each
- [ ] Grasp theoretical foundation
- [ ] See real-world applications

### Implementation Skills ✓
- [ ] Can code Dijkstra
- [ ] Can code Bellman-Ford
- [ ] Can code Kruskal with Union-Find
- [ ] Can code Ford-Fulkerson with BFS
- [ ] Can convert bipartite to flow

### Cognitive Integration ✓
- [ ] Understand hardware implications
- [ ] Know common misconceptions
- [ ] See design trade-offs
- [ ] Connect to AI/ML
- [ ] Appreciate historical evolution

### Interview Readiness ✓
- [ ] Can solve easy problems in 5-10 min
- [ ] Can solve medium problems in 15-20 min
- [ ] Can articulate trade-offs in interview
- [ ] Can handle follow-up questions
- [ ] Can discuss optimizations

---

## 🚀 NEXT WEEK BRIDGE (Week 8)

Week 8: Specialized Structures
- Tries: prefix trees for string search
- Segment Trees: range query data structures
- Fenwick Trees: efficient prefix sums
- Suffix structures: suffix arrays, trees

**Connection to Week 7:**
- Week 7: How to route (graphs, flow)
- Week 8: How to organize (specialized structures)
- Together: Advanced problem-solving toolkit

---

## 📚 RECOMMENDED REVIEW

### Quick Review (30 minutes)
1. Look at algorithm comparison table
2. Review decision tree for algorithm choice
3. Skim real-world application examples

### Deep Review (2 hours)
1. Re-read "The Why" for each day
2. Review examples and visualizations
3. Trace through one problem for each algorithm
4. Understand cognitive layers (5 perspectives)

### Before Interview Prep (ongoing)
1. Solve 3-5 problems per algorithm
2. Time yourself (should get faster)
3. Analyze your mistakes
4. Review trade-offs with your solutions

---

**Week 7 Complete!** ✅

**Status:** Ready to proceed to Week 8 (Specialized Structures)  
**Coverage:** 40-50% of interview questions  
**Cumulative:** 75-80% interview prep after Week 4.5 + Week 6 + Week 7  

