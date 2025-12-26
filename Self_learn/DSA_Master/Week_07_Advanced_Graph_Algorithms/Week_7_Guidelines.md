# Week 7: Enhanced Guidelines - Master Overview

**Week:** 7 | **Focus:** Advanced Graph Algorithms (Shortest Paths, Spanning Trees, Network Flow)  
**Difficulty:** HARD | **Time Investment:** 25-30 hours | **Interview Relevance:** Very High

---

## 1️⃣ DAILY BREAKDOWN & TIME ALLOCATION

### Weekly Schedule at a Glance

| Day | Topic | Core Learning | Practice | Total | Cumulative |
|-----|-------|---|---|---|---|
| 1 | Dijkstra's Algorithm | 45 min | 35 min | 80 min | 80 min |
| 2 | Bellman-Ford & Floyd-Warshall | 60 min | 40 min | 100 min | 180 min |
| 3 | Minimum Spanning Trees | 45 min | 35 min | 80 min | 260 min |
| 4 | Network Flow I | 50 min | 40 min | 90 min | 350 min |
| 5 | Network Flow II | 50 min | 40 min | 90 min | 440 min |
| Weekend | Advanced Practice & Integration | — | 120 min | 120 min | 560 min |
| **TOTAL** | **Week 7** | **250 min** | **310 min** | **560 min** | **560 min** |

### Time Allocation Rationale

**Core Learning (250 min = 4.2 hours):**
- Reading: 3.5 hours
- Visualization/tracing: 0.7 hours
- Why this: Deep conceptual understanding needed

**Practice (310 min = 5.2 hours):**
- Coding: 3 hours
- Problem solving: 2 hours
- Why this: Algorithms only learned through implementation

**Advanced (120 min = 2 hours):**
- Mixed problem types
- Complex scenarios
- Interview-level problems

**Total: 560 minutes = 9.3 hours** (within 25-30 hour week estimate including other activities)

### Daily Progression Logic

```
Day 1 (Dijkstra): Foundation
  ├─ Shortest path for one source
  ├─ Non-negative weights only
  └─ Greedy approach
  
Day 2 (Bellman-Ford + Floyd-Warshall): Variations
  ├─ Handles negative weights
  ├─ All-pairs variant
  └─ Trade-offs with Dijkstra
  
Day 3 (MSTs): Parallel concept
  ├─ Different optimization goal
  ├─ Similar greedy approach
  └─ Two different algorithms (Kruskal, Prim)
  
Day 4 (Flow I): New paradigm
  ├─ Capacity-based problems
  ├─ Augmenting path concept
  └─ Fundamental algorithm (Ford-Fulkerson)
  
Day 5 (Flow II): Applications
  ├─ Min cut (dual of max flow)
  ├─ Bipartite matching (special case)
  └─ Advanced reductions
```

---

## 2️⃣ LEARNING OBJECTIVES

### Knowledge Targets (What You'll Understand)

By end of Week 7, you should understand:

**Shortest Path Algorithms:**
- [ ] Why Dijkstra requires non-negative weights
- [ ] How priority queue makes Dijkstra efficient
- [ ] When to use Bellman-Ford vs Dijkstra vs Floyd-Warshall
- [ ] Proof that Dijkstra's greedy choice is optimal
- [ ] How to detect and handle negative cycles

**Minimum Spanning Trees:**
- [ ] Difference between spanning tree and MST
- [ ] Why MST has exactly V-1 edges
- [ ] Cut property and cycle property
- [ ] How Kruskal's and Prim's differ
- [ ] Why both produce same MST weight

**Network Flow:**
- [ ] Flow network constraints (capacity, conservation, skew symmetry)
- [ ] Augmenting path concept
- [ ] Why maximum flow = minimum cut (theorem)
- [ ] How to model matching as flow problem
- [ ] Reduction techniques for complex problems

### Practical Skills (What You Can Do)

**Implementation Skills:**
- [ ] Code Dijkstra from scratch with priority queue
- [ ] Code Bellman-Ford with negative cycle detection
- [ ] Code Floyd-Warshall (and understand when useful)
- [ ] Code Kruskal's with Union-Find
- [ ] Code Prim's with min-heap
- [ ] Code Ford-Fulkerson (Edmonds-Karp version)
- [ ] Find minimum cut from maximum flow
- [ ] Model bipartite matching as flow network
- [ ] Optimize for edge cases and special graphs

**Problem-Solving Skills:**
- [ ] Recognize shortest path vs MST vs flow problem
- [ ] Choose right algorithm for given problem
- [ ] Trace algorithms by hand on small examples
- [ ] Analyze time/space complexity
- [ ] Optimize implementations for performance
- [ ] Debug incorrect outputs

### Application Abilities (Where You'll Use It)

**Interview Contexts:**
- [ ] Answer "shortest path from A to B" problem
- [ ] Solve bipartite matching interview question
- [ ] Discuss min cut applications
- [ ] Explain when to use which shortest path algorithm
- [ ] Design system using these algorithms
- [ ] Optimize solution from naive to efficient

**Real-World Contexts:**
- [ ] GPS navigation system design
- [ ] Network routing protocol understanding
- [ ] Infrastructure planning (roads, power, networks)
- [ ] Resource allocation and matching problems
- [ ] Supply chain and logistics optimization

---

## 3️⃣ CORE CONCEPTS OVERVIEW

### Main Algorithms at a Glance

**Dijkstra's Algorithm**
```
Goal: Single-source shortest paths (non-negative weights)
Approach: Greedy - always pick nearest unvisited node
Time: O((V+E) log V) with binary heap
Why: Greedy optimal due to non-negative weights
When: GPS, network routing, game pathfinding
```

**Bellman-Ford Algorithm**
```
Goal: Single-source shortest paths (any weights)
Approach: Iterative relaxation V-1 times
Time: O(V × E)
Why: Detects negative cycles
When: When Dijkstra can't handle weights
```

**Floyd-Warshall Algorithm**
```
Goal: All-pairs shortest paths
Approach: DP - consider intermediate nodes
Time: O(V³)
Space: O(V²)
Why: Simple code, good for small dense graphs
When: Need all distances, small graphs only
```

**Kruskal's Algorithm**
```
Goal: Minimum spanning tree
Approach: Greedy - add minimum edges avoiding cycles
Time: O(E log E)
Uses: Union-Find for cycle detection
Why: Optimal by cut property
When: Sparse graphs, conceptually simpler
```

**Prim's Algorithm**
```
Goal: Minimum spanning tree
Approach: Grow tree from starting node
Time: O((V+E) log V)
Uses: Min-heap, similar to Dijkstra
Why: Optimal, good for dense graphs
When: Need incremental construction
```

**Ford-Fulkerson Algorithm**
```
Goal: Maximum flow in network
Approach: Find augmenting paths repeatedly
Time: O(|flow| × (V+E)) worst case, O(VE²) with BFS
Why: Optimal when no augmenting path exists
When: Flow networks, matching, circulation problems
```

### Prerequisites & Requirements

**Week 6 Knowledge Needed:**
- [ ] Graph representations (adjacency list/matrix)
- [ ] DFS and BFS traversals
- [ ] Union-Find data structure
- [ ] Basic graph properties

**Data Structures Used This Week:**
- [ ] Priority queue / Min-heap
- [ ] Adjacency list representation
- [ ] Union-Find (disjoint set)
- [ ] Residual graph (adjacency list with capacities)

**Mathematical Concepts:**
- [ ] Proof by contradiction
- [ ] Optimal substructure
- [ ] Greedy choice property
- [ ] Graph theory basics (paths, cycles, connectivity)

### When to Use Each (Decision Framework)

```
Given problem, ask:
1. Is it a shortest path problem?
   YES → Is it single-source or all-pairs?
   └─ Single-source → Dijkstra (non-neg) or Bellman-Ford (neg) or BFS (unweighted)
   └─ All-pairs → Floyd-Warshall (small) or Dijkstra V times (large)
   
2. Is it about connecting all nodes with minimum cost?
   YES → Minimum Spanning Tree
   └─ Sparse → Kruskal's (more intuitive)
   └─ Dense → Prim's (with Fibonacci heap)
   
3. Is it about maximizing or managing flow/capacity?
   YES → Network Flow Problem
   └─ Max flow → Ford-Fulkerson (or variants)
   └─ Min cut → Run max flow, find reachable set
   └─ Bipartite matching → Model as flow with unit capacities
   └─ Circulation with demands → Add supersource/sink
```

---

## 4️⃣ RECOMMENDED LEARNING PATH

### Why This Order?

**Days 1-2: Shortest Paths First**
- Rationale: These are most fundamental, taught in every CS program
- Build on: Graph traversal from Week 6
- Enable: Understanding of greedy algorithms with different constraints
- Progression: Simple (Dijkstra) → Complex (Bellman-Ford) → Complete (Floyd-Warshall)

**Day 3: Spanning Trees (Parallel Concept)**
- Rationale: Also greedy, same mathematical properties (cut property)
- Similarity: Both optimize on graphs with non-negative weights
- Difference: Optimize for different goals (paths vs connectivity)
- Builds intuition: Recognize different problem types

**Days 4-5: Network Flow (New Paradigm)**
- Rationale: Once comfortable with greedy, introduce new concept (augmenting paths)
- Prerequisites: Everything before (build on graph knowledge)
- Complexity: Highest level, combines multiple concepts
- Applications: Show power of reductions

### Phase-Based Learning

**Phase 1: Conceptual Understanding (Days 1-2)**
- Focus: Why algorithms work, not coding details
- Time: 50% reading, 30% visualization, 20% coding
- Goal: Understand intuition deeply

**Phase 2: Implementation Practice (Days 3-4)**
- Focus: Coding and optimization
- Time: 20% reading, 30% visualization, 50% coding
- Goal: Fluent implementation

**Phase 3: Advanced Application (Day 5)**
- Focus: Problem reduction and complex scenarios
- Time: 30% reading, 40% problem solving, 30% coding
- Goal: Recognize patterns and apply algorithms creatively

### Optimal Daily Schedule

**Option A: Intensive (1 topic per day, 2-2.5 hours)**
- Best for: Full-time learners, high commitment
- Day 1: 2.0 hours
- Day 2: 2.5 hours (2 algorithms)
- Day 3: 2.0 hours
- Day 4: 2.0 hours
- Day 5: 2.0 hours
- Weekend: 3.0 hours advanced

**Option B: Distributed (spread over 2 weeks)**
- Best for: Working professionals, part-time learners
- Days 1-2 of Week: Dijkstra
- Days 3-4 of Week: Bellman-Ford + Floyd-Warshall
- Day 5 of Week: MST + Flow intro
- Next Week: Complete Flow

**Option C: Compressed (3 days intensive)**
- Best for: Quick review, time-constrained
- Day 1: Dijkstra + Bellman-Ford + Floyd-Warshall (survey)
- Day 2: Kruskal's + Prim's
- Day 3: Ford-Fulkerson + Min Cut + Matching
- Next days: Deep practice

---

## 5️⃣ COMMON MISTAKES TO AVOID

### Critical Mistakes (Breaks Algorithm)

| Mistake | Why Wrong | How to Fix | Impact |
|---------|-----------|-----------|--------|
| Using Dijkstra on negative weights | Greedy assumption violated | Use Bellman-Ford instead | Wrong answer |
| Forgetting Union-Find in Kruskal's | Doesn't detect cycles | Use UF before adding edge | O(E²) instead of O(E log E) |
| Not implementing flow conservation | Flow rules violated | Check: inflow = outflow at each node | Invalid flow |
| Using BFS for weighted graphs | Ignores weights | Use Dijkstra instead | Wrong shortest path |
| Forgetting to update residual graph | Doesn't allow flow cancellation | Update both directions: u→v and v→u | Algorithm fails |

### Efficiency Mistakes (Correct but Slow)

| Mistake | Better Approach | Speedup |
|---------|------------------|---------|
| Running Bellman-Ford for all-pairs | Use Floyd-Warshall | 10-100x |
| Using array instead of heap in Dijkstra | Use binary heap | 10-100x |
| Sorting edges in Prim's each iteration | Use min-heap | 10x |
| Running Dijkstra V times instead of FW | Use Floyd-Warshall for all-pairs | 100-1000x |
| Finding min in Bellman-Ford naively | Track during iterations | 10x |

### Conceptual Mistakes (Logic Errors)

| Misconception | Reality | Correction |
|---|---|---|
| "All greedy algorithms are optimal" | Only with specific properties | Check cut property, exchange argument |
| "Floyd-Warshall always better for all-pairs" | O(V³) too slow for large graphs | Use Dijkstra V times for sparse |
| "MST is shortest path tree" | Different optimizations | Shortest path from source; MST overall |
| "Max flow can exceed source capacity" | Impossible | Conservation constraint prevents this |
| "Min cut is unique" | Multiple possible | But all have same minimum value |

---

## 6️⃣ PRACTICE PROBLEMS GUIDE

### Problem Organization by Difficulty

**Easy (Warm-up, 1 per algorithm)**
- Dijkstra: Network Delay Time (LeetCode 743)
- Bellman-Ford: Cheapest Flights (K stops) simplified
- Floyd-Warshall: Find City with Smallest Neighbors (LeetCode 1334)
- Kruskal's: Minimum Cost to Connect All Cities (LeetCode 1584)
- Prim's: Connecting Cities with Min Cost (variant)
- Flow: Simple max flow (custom)

**Medium (Core understanding, 3-4 per algorithm)**
- Dijkstra: Minimum Cost Path (LeetCode variants)
- Bellman-Ford: Negative cycle detection
- Floyd-Warshall: All pairs shortest (custom)
- Kruskal's/Prim's: MST with constraints
- Flow: Bipartite matching (matching problem)

**Hard (Mastery, 2-3 per algorithm)**
- Dijkstra: Path with Maximum Probability (LeetCode 1514)
- Bellman-Ford: Design system with negative costs
- Floyd-Warshall: Complex all-pairs with additional constraints
- MST: Variants (bottleneck MST, rectilinear MST)
- Flow: Project selection, image segmentation

### Problem Recommendations

**Total Problems for Week: 20-30**
- Dijkstra: 4 problems (easy-hard progression)
- Bellman-Ford: 3 problems
- Floyd-Warshall: 2 problems
- MST: 5 problems (Kruskal + Prim combined)
- Flow: 6-8 problems (including matching, min-cut)

**Time per Problem:**
- Easy: 15-20 min
- Medium: 30-40 min
- Hard: 45-60+ min

**Problem Sources:**
- LeetCode: 1300+ rating (these problems)
- GeeksforGeeks: Detailed explanations
- CodeSignal: Interactive practice
- InterviewBit: Real interview level

---

## 7️⃣ INTERVIEW PREPARATION

### Common Interview Questions by Level

**Junior Level (L3 at Big Tech):**
- "Implement Dijkstra's algorithm"
- "Find shortest path from A to B"
- "What's the difference between Dijkstra and Bellman-Ford?"
- "Implement MST (Kruskal's or Prim's)"

**Mid Level (L4 at Big Tech):**
- "Optimize given shortest path solution"
- "Handle negative weights in path problem"
- "Recognize and solve as MST problem"
- "Implement max flow or bipartite matching"
- "Discuss trade-offs: Kruskal vs Prim"

**Senior Level (L5+ at Big Tech):**
- "Design GPS routing system with real-time updates"
- "How would you solve this as max flow problem?"
- "Optimize for specific constraints (memory, time, network)"
- "Extend algorithm to handle new requirement"
- "Compare 3 different solutions, pick best for scenario"

### How These Topics Appear in Interviews

**Pattern 1: Direct Algorithm Implementation**
- Asked directly: "Implement Dijkstra"
- How to prepare: Code all 6 algorithms fluently
- Time: Usually 30-45 minutes

**Pattern 2: Problem Recognition**
- Not labeled: "Find shortest path"
- Must recognize: Which algorithm applies?
- How to prepare: Solve 20+ mixed problems
- Time: Includes problem solving + coding

**Pattern 3: System Design Component**
- Part of larger design: "Navigation system"
- Need algorithm knowledge: Why Dijkstra for this?
- How to prepare: Understand real-world applications
- Time: 5-15 minutes of 45-minute interview

**Pattern 4: Optimization Challenge**
- Start with solution: "Can you do better?"
- Must optimize: Suggest better algorithm
- How to prepare: Understand complexity trade-offs
- Time: Usually bonus/follow-up question

### Interview Tips & Strategies

**Before Coding:**
1. Clarify: Negative weights? Directed/undirected? Large graph?
2. Draw: Simple example (3-4 nodes)
3. Discuss: Which algorithm, why, complexity
4. Get feedback: "Does this approach work?"

**While Coding:**
1. Code cleanly: Use helper functions
2. Handle edge cases: Empty graph, single node, disconnected
3. Trace: Walk through example during coding
4. Explain: Narrate what you're doing

**After Coding:**
1. Test: Run on example, trace through
2. Verify: Check edge cases
3. Optimize: "Can I improve space or time?"
4. Discuss: Compare with alternatives

### Follow-Up Question Handling

**"Can you do it in O(log V) space?"**
→ Discuss trade-offs, might use different algorithm

**"What if graph is very large (billions of edges)?"**
→ Discuss preprocessing, distributed computing, approximations

**"What if requirements change?"**
→ Show flexibility, discuss which parts must change

**"How would you test this?"**
→ Unit tests, edge cases, stress tests, bench marking

### Trade-Off Discussion Guidance

**When to use Dijkstra vs Bellman-Ford:**
"Use Dijkstra for non-negative weights (faster O((V+E)logV)), Bellman-Ford for negative (O(VE) but handles negatives)."

**When to use MST vs shortest path:**
"MST minimizes total cost to connect all; shortest path minimizes cost to reach one node. Different goals, different algorithms."

**When to use Kruskal vs Prim:**
"Kruskal better for sparse graphs and conceptually simpler (sort edges); Prim better for dense graphs and when incremental construction needed."

**When to use Ford-Fulkerson vs specialized:**
"FF works for all flows; Dinic's faster (O(V²E)); Push-relabel faster still. Choose based on time constraints and implementation complexity."

---

## 8️⃣ RESOURCES & REFERENCES

### Online Learning Platforms

**Video Learning:**
- YouTube: "Dijkstra's algorithm explained" (William Fiset, Abdul Bari)
- Coursera: Algorithms courses (Princeton, UC San Diego)
- Udemy: Graph algorithms comprehensive courses
- YouTube: MIT OpenCourseWare (classic lectures)

**Interactive Practice:**
- LeetCode: 50+ problems, solutions, discussions
- CodeSignal: Interactive algorithm challenges
- HackerRank: Algorithm practice with visualizations
- Codeforces: Competitive programming (harder)

**Visualization Tools:**
- Visualgo.net: Algorithm visualization (highly recommended)
- Graph Online: Draw and solve interactively
- draw.io: Manual visualization and drawing
- Algorithm Visualizer: Browser-based visualizations

### Recommended Books

- "Introduction to Algorithms" (CLRS): Classic, comprehensive, proof-heavy
- "Algorithm Design Manual" (Skiena): Practical, real-world focus
- "Competitive Programming" (Halim): Interview-focused, concise

### Article References

- GeeksforGeeks: Detailed algorithm explanations and code
- Medium: Various graph algorithm walkthroughs
- Brilliant.org: Interactive problem-solving
- TopCoder: Tutorials and editorials

---

## 9️⃣ ASSESSMENT & SUCCESS CRITERIA

### Knowledge Check (Conceptual Understanding)

By end of week, you should answer "YES" to:

- [ ] I can explain Dijkstra's greedy choice without referring to notes
- [ ] I understand why Bellman-Ford handles negative weights
- [ ] I can prove MST correctness using cut property
- [ ] I understand max-flow min-cut theorem intuitively
- [ ] I can distinguish shortest path vs MST vs flow problems
- [ ] I know time complexity of all 6 main algorithms
- [ ] I can explain trade-offs between Kruskal vs Prim
- [ ] I understand when to use which shortest path algorithm
- [ ] I can model bipartite matching as a flow problem
- [ ] I understand flow conservation and residual graphs

### Practical Skills (Can You Do It?)

- [ ] Implement Dijkstra from scratch in 20 minutes
- [ ] Implement Bellman-Ford from scratch in 25 minutes
- [ ] Implement Floyd-Warshall from scratch in 10 minutes
- [ ] Implement Kruskal's (with Union-Find) in 20 minutes
- [ ] Implement Prim's from scratch in 20 minutes
- [ ] Implement Ford-Fulkerson (Edmonds-Karp) in 30 minutes
- [ ] Find min cut after running max flow
- [ ] Model bipartite matching as flow network
- [ ] Trace any algorithm on 4-node example
- [ ] Optimize a basic solution to efficient one

### Confidence Targets (Rate 1-5)

Target scores for each skill:
- Understanding algorithms: ≥ 4/5
- Implementation fluency: ≥ 4/5
- Problem recognition: ≥ 4/5
- Trade-off analysis: ≥ 3.5/5
- Interview readiness: ≥ 4/5
- Overall mastery: ≥ 4/5

### Mastery Indicators

You've achieved mastery when:
- ✓ Can implement any algorithm without reference
- ✓ Recognize problem types instantly
- ✓ Explain to others clearly
- ✓ Solve mixed problems correctly
- ✓ Optimize beyond basic solutions
- ✓ Handle edge cases confidently
- ✓ Discuss real-world applications
- ✓ Solve interview problems under time pressure

---

## 🔟 CONNECTION TO FUTURE WEEKS

### How Week 7 Builds Toward Future

**Week 8 (Specialized Structures): Direct Application**
- Tries: String problems sometimes use shortest path
- Segment Trees: Range queries related to MST weights
- Fenwick Trees: Used for advanced flow algorithms

**Week 9 (String & Math Algorithms): Related Techniques**
- KMP algorithm: Similar to shortest path (DP)
- Number theory: Used in flow algorithms (GCD, modular arithmetic)

**Week 10 (Greedy & Backtracking): Foundational Concepts**
- Greedy paradigm: Master these greedy algorithms first
- Exchange arguments: Prove greedy correctness (learned here)

**Week 11 (Dynamic Programming): Different Paradigm**
- Floyd-Warshall is DP: You've seen it here
- Optimal substructure: Key concept learned in Week 7

**Week 12 (Integration): Brings Everything Together**
- Complex problems often need shortest path + something else
- MST sometimes combined with other techniques
- Flow as component of larger solution

### Prerequisites for Week 8

**Must Know Before Week 8:**
- [ ] Dijkstra and when to use it
- [ ] Minimum spanning trees and algorithms
- [ ] Max flow basics (will extend in Week 8 context)
- [ ] How to model problems as graphs

**Nice to Know:**
- [ ] Bellman-Ford and negative weight handling
- [ ] Floyd-Warshall for all-pairs
- [ ] Advanced flow (matching, min-cut)

### Mastery Importance Rating

**Critical (absolutely master):**
- Dijkstra's algorithm (10/10) - appears everywhere
- Kruskal's or Prim's MST (9/10) - common in interviews
- Ford-Fulkerson max flow (8/10) - elegant, appears in reductions

**Very Important (strong understanding):**
- Bellman-Ford (7/10) - handles edge cases
- Floyd-Warshall (6/10) - all-pairs alternative
- Min cut / bipartite matching (7/10) - reductions

---

## 1️⃣1️⃣ FREQUENTLY ASKED QUESTIONS

### Q: Why learn both Kruskal's and Prim's if they give same result?

**A:** Different approaches teach different concepts:
- Kruskal: global greedy on edges (union-find thinking)
- Prim: local greedy from tree (Dijkstra-like thinking)
- Interviews ask both or ask which to use when
- Understand both deepens graph algorithm knowledge

### Q: When would I actually use Floyd-Warshall?

**A:** Mostly in specific scenarios:
- Small graphs (< 500 nodes)
- Need all-pairs distances
- Simple implementation preferred over efficiency
- In practice: less common (Dijkstra repeated or specialized algorithms)

### Q: Dijkstra vs Bellman-Ford on the same graph?

**A:** 
- If all weights non-negative: Dijkstra (much faster)
- If negative weights present: Must use Bellman-Ford
- Bellman-Ford slower but handles negative

### Q: Can you optimize Ford-Fulkerson beyond Edmonds-Karp?

**A:** Yes, several variants:
- Dinic's algorithm: O(V²E)
- Push-relabel: O(V³) or O(V²√E)
- But Edmonds-Karp good for learning and interviews

### Q: How to handle disconnected graphs?

**A:** Depends on algorithm:
- Dijkstra: Unreachable nodes stay at infinity (correct)
- MST: Kruskal handles naturally; produces forest
- Flow: Need path S to T (disconnected = no flow possible)

### Q: Why do we teach both Union-Find and MST together?

**A:** Union-Find essential for Kruskal's efficiency:
- Without UF: O(E²) (re-check cycles each time)
- With UF: O(E log E) (fast cycle detection)
- Learning union-find here = essential for other uses

### Q: What's the difference between min cut and edge connectivity?

**A:**
- Min cut: Remove edges to disconnect S from T (weighted)
- Edge connectivity: Minimum edges to remove to disconnect any two nodes (unweighted)
- Related concepts but different

### Q: How does max flow apply to real problems?

**A:** Many problems reduce to flow:
- Bipartite matching: assignments (students to courses)
- Image segmentation: find best boundary
- Supply/demand: circulation with constraints
- Project selection: profits and dependencies

### Q: Do I need to memorize all complexities?

**A:** Know these by heart:
- Dijkstra: O((V+E) log V)
- Bellman-Ford: O(VE)
- Floyd-Warshall: O(V³)
- Kruskal's: O(E log E)
- Prim's: O((V+E) log V)
- Ford-Fulkerson: O(VE²)

### Q: How to recognize problem type in interview?

**A:** Look for keywords:
- "shortest": Dijkstra/Bellman-Ford/Floyd-Warshall
- "minimum cost connect": MST (Kruskal/Prim)
- "maximum flow"/"capacity": Ford-Fulkerson or variant
- "matching"/"assignment": Often reduces to flow
- "minimum edges": Min cut problem

---

## 1️⃣2️⃣ SCHEDULE & SUCCESS PATH

### Recommended Weekly Schedule Options

**Option A: Intensive (9-10 hours)** ← Recommended

```
Monday: Day 1 (Dijkstra) - 2 hours
Tuesday: Day 2 (Bellman-Ford + Floyd-Warshall) - 2.5 hours
Wednesday: Day 3 (MST Kruskal + Prim) - 2 hours
Thursday: Day 4 (Ford-Fulkerson) - 2 hours
Friday: Day 5 (Min Cut + Matching) - 2 hours
Weekend: Advanced practice and integration - 2-3 hours
Total: 11-12 hours
```

**Option B: Distributed (12-15 hours)**

```
Week 1:
  Mon-Wed: Days 1-2 (Shortest paths deep dive)
  Thu-Fri: Day 3 (MST)
  
Week 2:
  Mon-Tue: Day 4-5 (Flow)
  Wed+: Practice
  
Total: Split into 2 weeks, 6-7 hours per week
```

**Option C: Compressed (5-6 hours)**

```
Day 1: Days 1-2 survey (Shortest paths, 2 hours)
Day 2: Day 3 (MST, 1.5 hours)
Day 3: Days 4-5 (Flow intro, 1.5 hours)
Weekend: Targeted practice (1 hour)
Total: 6 hours
**Trade-off:** Less depth, faster pace
```

### Key Milestones per Day

**Day 1 (Dijkstra):**
- ✓ Understand greedy choice property
- ✓ Implement and test
- ✓ Solve 2 practice problems
- ✓ Know when to use it

**Day 2 (Bellman-Ford + Floyd-Warshall):**
- ✓ Understand negative weight handling
- ✓ Implement both algorithms
- ✓ Compare performance characteristics
- ✓ Know all-pairs vs single-source

**Day 3 (MST):**
- ✓ Understand cut and cycle properties
- ✓ Implement Kruskal's and Prim's
- ✓ Know when to use each
- ✓ Practice on 2-3 problems

**Day 4 (Flow I):**
- ✓ Understand flow constraints
- ✓ Understand augmenting paths
- ✓ Implement Ford-Fulkerson
- ✓ Trace example carefully

**Day 5 (Flow II):**
- ✓ Find min cut from max flow
- ✓ Model bipartite matching as flow
- ✓ Solve matching problem using flow
- ✓ Understand problem reductions

### Success Path Visualization

```
Week 6 (Graphs)
  ↓
Dijkstra (Day 1) ← Start here
  ↓
Bellman-Ford & Floyd-Warshall (Day 2)
  ↓
MST: Kruskal's & Prim's (Day 3)
  ↓
Max Flow: Ford-Fulkerson (Day 4)
  ↓
Flow Applications: Min Cut, Matching (Day 5)
  ↓
Interview-Ready for Most Graph Problems
  ↓
Week 8 (Specialized Structures)
```

### Week Completion Checklist

- [ ] Read all 5 days instructional content (12 sections each)
- [ ] Implement all 6 main algorithms
- [ ] Solve 20-30 practice problems
- [ ] Trace 3+ examples by hand per algorithm
- [ ] Discuss trade-offs between algorithms
- [ ] Score ≥ 3.5/5 confidence on all topics
- [ ] Can solve mixed problem types
- [ ] Ready to move to Week 8

### Week 8 Readiness Criteria

You're ready for Week 8 if:
- ✅ Can implement Dijkstra in 20 minutes
- ✅ Understand MST concepts deeply
- ✅ Know max flow basics
- ✅ Can recognize algorithm from problem description
- ✅ Scored ≥ 75% on practice problems
- ✅ Feel confident explaining to others
- ✅ Understand real-world applications
- ✅ Ready for interview questions on these topics

---

## FINAL SUMMARY

**Week 7 teaches:** Advanced graph algorithms that solve real infrastructure, networking, and optimization problems

**Core learning:** Greedy algorithms with mathematical proofs of optimality

**Career impact:** Master these, and you'll solve 30-40% of interview problems at Big Tech

**Time investment:** 10-12 hours learning + practice this week

**Success metric:** Score 4/5+ confidence, solve interview-level problems

---

**Week 7 is CRITICAL. Master it.** ✅

