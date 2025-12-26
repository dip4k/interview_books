# Week 7: Complete Support Package (All 5 Files Combined)

## FILE 1: CHECKLIST & PROGRESS TRACKING

### Week 7 Daily Progress Tracker

**Day 1: Dijkstra's Algorithm**

Reading Progress (mark as you complete):
- [ ] Section 1 - The Why (motivation & context)
- [ ] Section 2 - The What (mental model)
- [ ] Section 3 - The How (implementation)
- [ ] Section 4 - Visualization (traced examples)
- [ ] Section 5 - Critical Analysis (complexity)
- [ ] Section 6 - Real System Integration (applications)
- [ ] Section 7 - Concept Crossovers (connections)
- [ ] Section 8 - Mathematical & Theoretical (proofs)
- [ ] Section 9 - Algorithmic Design Intuition (why works)
- [ ] Section 10 - Knowledge Check (questions)
- [ ] Section 11 - Retention Hook (memory aid)
- [ ] Section 12 - Cognitive Layer (5 lenses)

Confidence Ratings (1-5, with 5 = expert):
- Understand algorithm: __/5
- Can implement from scratch: __/5
- Know when to use vs Bellman-Ford: __/5
- Understand priority queue optimization: __/5
- Overall mastery: __/5

Hands-on Tasks:
- [ ] Implement Dijkstra from scratch
- [ ] Trace example by hand (at least 3 nodes)
- [ ] Solve 2 practice problems (LeetCode Network Delay Time, Minimum Cost)
- [ ] Optimize: try different heap implementations

Time Spent: __ minutes

Key Insights (write 3):
1. ________________________
2. ________________________
3. ________________________

Questions/Confusion:
- [ ] None - fully understood
- [ ] Have questions: ________________________

Knowledge Gaps:
- [ ] None
- [ ] Gaps: ________________________

External Resources Explored:
- [ ] YouTube video (which): ________________________
- [ ] Blog/article (which): ________________________
- [ ] Practice site problems done: __

---

**Day 2: Bellman-Ford & Floyd-Warshall**

(Same structure as Day 1)

Reading Progress: __/12 sections
Confidence: __/5
Tasks Completed: __/4
Time Spent: __ minutes
Key Insights: 3 written
Questions: [None / Listed]
Gaps: [None / Listed]
Resources: Listed

---

**Day 3: Minimum Spanning Trees**

(Same structure)

---

**Day 4: Network Flow I**

(Same structure)

---

**Day 5: Network Flow II**

(Same structure)

---

### Weekly Summary

Total reading time: __ minutes (goal: 450 min = 7.5 hours)
Total practice time: __ minutes (goal: 180 min = 3 hours)
Total time: __ minutes (goal: 630 min = 10.5 hours)

Average daily confidence: __/5
Overall week mastery: __/5

Topics fully mastered: [list]
Topics need more work: [list]
Breakthrough moments: [describe]

Success Criteria Met:
- [ ] All 11 sections read per topic
- [ ] 2+ practice problems per topic
- [ ] Average confidence > 3.5/5
- [ ] Can explain to someone else
- [ ] Ready for Week 8

---

## FILE 2: SUMMARY & QUICK REFERENCE

### One-Liner Essence (memorize these)

1. **Dijkstra:** "Always visit nearest unvisited node; O((V+E) log V) with heap"
2. **Bellman-Ford:** "Relax edges V-1 times; detects negative cycles; O(VE)"
3. **Floyd-Warshall:** "Three nested loops; O(V³); all-pairs shortest path"
4. **Kruskal's:** "Sort edges; union-find; O(E log E)"
5. **Prim's:** "Grow tree from start; min-heap; O((V+E) log V)"
6. **Max Flow:** "Find augmenting paths; push bottleneck; O(VE²) with BFS"
7. **Min Cut:** "Remove edges to disconnect; equals max flow"
8. **Bipartite Matching:** "Model as flow with unit capacities"

### Complexity Comparison Table

| Algorithm | Time | Space | When to Use |
|-----------|------|-------|------------|
| Dijkstra | O((V+E)logV) | O(V) | Single-source, non-negative |
| Bellman-Ford | O(VE) | O(V) | Single-source, negative allowed |
| Floyd-Warshall | O(V³) | O(V²) | All-pairs, small graphs |
| Kruskal's | O(ElogE) | O(V+E) | MST, sparse |
| Prim's | O((V+E)logV) | O(V+E) | MST, dense |
| Ford-Fulkerson | O(VE²) | O(V+E) | Max flow/matching |

### Decision Matrix

```
Problem: Single-source shortest path?
  No negative weights? → Use Dijkstra
  Has negative weights? → Use Bellman-Ford
  Need all-pairs? → Use Floyd-Warshall

Problem: Connect all nodes minimum cost?
  Sparse graph? → Use Kruskal's
  Dense graph? → Use Prim's
  
Problem: Maximum flow/matching?
  Max flow needed? → Use Ford-Fulkerson (or better variant)
  Min cut needed? → Run max flow, find reachable set
  Bipartite matching? → Model as flow (unit capacities)
```

### Common Mistakes to Avoid

1. **Dijkstra with negative weights:** WRONG! Graph structure violated
2. **Running Dijkstra V times instead of Floyd-Warshall:** Possible but slower for all-pairs
3. **Forgetting Union-Find in Kruskal's:** Slow cycle detection defeats purpose
4. **BFS for all edge weights equal:** Use it! Faster than Dijkstra
5. **Min Cut without running max flow first:** Must compute max flow first
6. **Forgetting flow conservation in networks:** Valid flow requires it

### Interview Quick Answers

**Q: When would you use Dijkstra?**
A: "When I need shortest path from one source to all others, and all edge weights are non-negative. Time O((V+E)logV) with heap."

**Q: Why not always use Floyd-Warshall?**
A: "Floyd-Warshall is O(V³), slower than Dijkstra O((V+E)logV) for sparse graphs. Also uses O(V²) space vs O(V)."

**Q: How does Bellman-Ford detect negative cycles?**
A: "After V-1 relaxations (which finds all shortest paths), if any edge can still be relaxed, a negative cycle exists."

**Q: What's minimum spanning tree used for?**
A: "Connecting all nodes with minimum cost. Applications: power lines, network infrastructure, data center routing."

**Q: Why does max flow equal min cut?**
A: "All flow must cross any cut separating source and sink. When max flow is found, the reachable set forms a cut with equal capacity."

### Concept Connections

```
Week 6 (Graphs) → Week 7 (Advanced)
  BFS/DFS: traversal
  Union-Find: used in Kruskal's
  Graph representation: foundation

Week 7 Internal Connections:
  Shortest paths (Days 1-2)
  Spanning trees (Day 3)
  Flow (Days 4-5)
  
  All use: Graph representations, greedy choice, optimal substructure

Week 7 → Week 8 (Specialized Structures)
  Still work with graphs
  But specialized structures (Tries, Segment Trees) for specific problems
```

---

## FILE 3: ROADMAP & TIME BUDGET

### Weekly Overview & Mission

**Goal:** Master advanced graph algorithms (weighted shortest paths, spanning trees, network flow)

**Why matters:** These algorithms solve real infrastructure, networking, and optimization problems

**Difficulty:** HARD (requires understanding multiple concepts)

**Time investment:** 25-30 hours (learning + practice)

### Phase-by-Phase Breakdown (5 Phases)

**Phase 1: Single-Source Shortest Paths (Days 1-2, 4.5 hours)**
- Learn Dijkstra's algorithm (priority queue, greedy)
- Learn Bellman-Ford (handles negative, detects cycles)
- Learn Floyd-Warshall (all-pairs, simple code)
- Compare and understand trade-offs

**Phase 2: Spanning Trees (Day 3, 3 hours)**
- Learn Kruskal's algorithm (union-find, greedy edge selection)
- Learn Prim's algorithm (growing tree, similar to Dijkstra)
- Understand when to use each
- Practice both implementations

**Phase 3: Basic Flow (Day 4, 3 hours)**
- Understand flow networks (capacities, constraints)
- Learn Ford-Fulkerson algorithm (augmenting paths)
- Understand why BFS (Edmonds-Karp) better than DFS
- Trace through examples carefully

**Phase 4: Advanced Flow (Day 5, 3 hours)**
- Min-cut finding (from max flow)
- Bipartite matching as flow
- Circulation with demands
- Problem reduction techniques

**Phase 5: Integration & Practice (2-3 hours)**
- Solve mixed problems
- Recognize which algorithm applies
- Optimize and improve implementations
- Prepare for interviews

### Hour-by-Hour Time Allocation

**Per day (assume 1.5 hours):**
- Reading/understanding (45 min)
- Working through examples (30 min)
- Coding practice (25 min)
- Total per day: 100 min

**Per day breakdown:**
- 0:00-0:45 Read all 12 sections
- 0:45-1:15 Trace examples, understand intuition
- 1:15-1:40 Code implementation, test

**Full week:**
- Days 1-5 reading: 375 minutes (6.25 hours)
- Days 1-5 practice: 125 minutes (2 hours)
- Days 1-5 total: 500 minutes (8.3 hours)
- Advanced problems: 180 minutes (3 hours)
- Total: 680 minutes (11.3 hours)

**Optimal schedule:**
- Day 1: 2 hours (algorithm depth)
- Day 2: 2.5 hours (2 algorithms)
- Day 3: 2 hours (2 similar algorithms)
- Day 4: 2 hours (flow basics)
- Day 5: 2 hours (advanced flow)
- Weekend: 2-3 hours practice
- Total: 12-13 hours

### Cross-Week Integration Points

**Week 6 → Week 7:**
- Union-Find (Week 6) used in Kruskal's
- BFS/DFS (Week 6) for finding paths
- Graph representation (Week 6) foundation

**Week 7 → Week 8:**
- Shortest paths used with specialized structures
- Tree concepts extend to Tries, Segment Trees
- Graph algorithms continue in later weeks

### Recovery Strategies (if behind)

If falling behind schedule:
1. **Skip Day 5 advanced topics** (bipartite matching, circulation) - come back later
2. **Focus on Dijkstra & Kruskal's** - most important
3. **Use video explanations** instead of reading all text
4. **Do fewer practice problems** but ensure depth

If ahead of schedule:
1. **Implement multiple variants** (Dinic's, push-relabel for flow)
2. **Solve harder problems** from competitive programming
3. **Explore real-world applications** (network design, image segmentation)

### Study Environment Setup

**Requirements:**
- Code editor (VS Code, PyCharm)
- Visualization tool (draw.io, paper & pencil)
- Practice platform (LeetCode, CodeSignal)
- Quiet space (2 hours uninterrupted)

**Optional:**
- Whiteboard for tracing
- Multiple monitors for visualizations
- Timer for practice problems

---

## FILE 4: Q&A PRACTICE QUESTIONS (50 Questions Total)

### Day 1: Dijkstra's Algorithm (10 Questions)

**⭐ Easy Questions:**

1. What does "shortest path" mean in context of Dijkstra's algorithm?
2. Why do we need a priority queue? Can't we just use a regular queue?
3. How does Dijkstra know it's finished?

**⭐⭐ Medium Questions:**

4. Why does Dijkstra fail on graphs with negative edge weights? Provide a counter-example.
5. What's the time complexity with binary heap vs array? Why is heap preferred?
6. How would you reconstruct the actual path (not just distances)?

**⭐⭐⭐ Hard Questions:**

7. Explain the "cut property" for shortest paths and why it justifies Dijkstra's greedy choice.
8. Compare Dijkstra vs Bellman-Ford: when would you use each?
9. Can you use Dijkstra on an unweighted graph? How? Why is BFS better?
10. Design a variant: what if edges have weights that change over time?

---

### Day 2: Bellman-Ford & Floyd-Warshall (10 Questions)

**⭐ Easy:**

1. What's the purpose of relaxing edges V-1 times in Bellman-Ford?
2. How does Bellman-Ford detect negative cycles?
3. What does Floyd-Warshall compute that Dijkstra doesn't?

**⭐⭐ Medium:**

4. Why is Floyd-Warshall O(V³) and when is that acceptable?
5. What's the relationship between the three shortest-path algorithms (Dijkstra, BF, FW)?
6. Can you prove why Bellman-Ford must relax exactly V-1 times?

**⭐⭐⭐ Hard:**

7. Implement Bellman-Ford with path reconstruction for negative cycle detection.
8. When would you run Dijkstra V times vs use Floyd-Warshall? Performance analysis.
9. What if a graph has a negative cycle not affecting the source? Does Bellman-Ford detect it?
10. Design a system using these three algorithms for real-time traffic (constantly changing weights).

---

### Day 3: Minimum Spanning Trees (10 Questions)

**⭐ Easy:**

1. What's the difference between a spanning tree and a minimum spanning tree?
2. Why must an MST have exactly V-1 edges?
3. Can there be multiple MSTs for the same graph?

**⭐⭐ Medium:**

4. Why does Kruskal's use Union-Find? What would happen without it?
5. Explain the "cut property" for MSTs.
6. When would you use Prim's over Kruskal's?

**⭐⭐⭐ Hard:**

7. Prove that Kruskal's algorithm always produces an MST using the cut property.
8. Implement Prim's algorithm using a priority queue and analyze time complexity.
9. Prove that if all edge weights are unique, the MST is unique.
10. Design an algorithm for finding a second minimum spanning tree.

---

### Day 4: Network Flow I (10 Questions)

**⭐ Easy:**

1. What's the difference between capacity and flow?
2. What's an augmenting path?
3. Why do we use residual graphs?

**⭐⭐ Medium:**

4. Explain flow conservation. Why is it needed?
5. What's the bottleneck in an augmenting path and why does it matter?
6. Why is BFS (Edmonds-Karp) better than DFS (basic Ford-Fulkerson)?

**⭐⭐⭐ Hard:**

7. Prove that Ford-Fulkerson terminates when using rational capacities.
8. Can Ford-Fulkerson loop infinitely with irrational capacities? Give an example.
9. Implement Edmonds-Karp (Ford-Fulkerson with BFS) and trace an example.
10. Design a flow network for a real problem (airline scheduling, data center routing).

---

### Day 5: Network Flow II (10 Questions)

**⭐ Easy:**

1. What's the relationship between max flow and min cut?
2. How do you find the min cut after computing max flow?
3. How can you model bipartite matching as a flow problem?

**⭐⭐ Medium:**

4. Prove that any flow value ≤ any cut capacity.
5. How would you handle circulation with demands and supplies?
6. What does a cut of capacity 0 mean? When can it happen?

**⭐⭐⭐ Hard:**

7. Implement bipartite matching using max flow and compare to direct algorithms.
8. Explain the project selection problem and how it reduces to min cut.
9. Prove the Max-Flow Min-Cut theorem.
10. Design an application: airline crew scheduling using network flow.

---

## FILE 5: COMPLETE INDEX & NAVIGATION

### File Structure Overview

**Instructional Files (5):**
- Week_7_Day_1_Dijkstra_Algorithm.md
- Week_7_Day_2_Bellman_Ford_Floyd_Warshall.md
- Week_7_Day_3_Minimum_Spanning_Trees.md
- Week_7_Day_4_Network_Flow_I.md
- Week_7_Day_5_Network_Flow_II.md

**Support Files (5):**
- Week_7_Checklist_Progress.md
- Week_7_Summary_Quick_Reference.md
- Week_7_Roadmap.md
- Week_7_QA_50_Questions.md
- Week_7_Complete_Index.md (this file)

**Guidelines File (1):**
- Week_7_Guidelines.md

### Quick Navigation by Algorithm

| Algorithm | File | Day | Sections | Practice |
|-----------|------|-----|----------|----------|
| Dijkstra | Day 1 | 1 | 12 | LeetCode Network Delay |
| Bellman-Ford | Day 2 | 2 | 12 | LeetCode Relax |
| Floyd-Warshall | Day 2 | 2 | 12 | LeetCode All Pairs |
| Kruskal's | Day 3 | 3 | 12 | LeetCode MST |
| Prim's | Day 3 | 3 | 12 | LeetCode Connecting Cities |
| Ford-Fulkerson | Day 4 | 4 | 12 | LeetCode Max Flow |
| Min Cut | Day 5 | 5 | 6 | LeetCode Min Cut |
| Bipartite Matching | Day 5 | 5 | 6 | LeetCode Matching |

### Daily Learning Path

**Recommended order within each day:**
1. Read The Why (context & motivation)
2. Read The What (intuitive understanding)
3. Study Visualization (traced examples)
4. Read The How (implementation)
5. Work through Knowledge Check
6. Code implementation
7. Solve 2 practice problems
8. Read rest of sections (deeper understanding)

### Complexity Reference Table

**Single-Source Shortest Path:**
- Dijkstra (non-negative): O((V+E)logV)
- Bellman-Ford (negative allowed): O(VE)
- BFS (unweighted): O(V+E)

**All-Pairs Shortest Path:**
- Floyd-Warshall: O(V³)
- Dijkstra V times: O(V(V+E)logV)
- Bellman-Ford V times: O(V²E)

**Minimum Spanning Tree:**
- Kruskal's: O(ElogE)
- Prim's (binary heap): O((V+E)logV)
- Prim's (Fibonacci heap): O(E + VlogV)

**Network Flow:**
- Ford-Fulkerson (DFS): O(|flow| × (V+E))
- Edmonds-Karp (BFS): O(VE²)
- Dinic's: O(V²E)
- Push-Relabel: O(V³) or O(V²√E)

### Problem Mapping

**LeetCode-style problems by algorithm:**

Dijkstra:
- Network Delay Time
- Minimum Cost to Reach Destination
- Path with Maximum Probability

Bellman-Ford:
- Cheapest Flights with K stops
- Detecting negative cycle variant

Floyd-Warshall:
- All Paths from Source to Target (with weights)
- Network Delay Time (all-pairs variant)

Kruskal's / Prim's:
- Minimum Cost to Connect All Cities
- Min Cost to Connect All Points
- Connecting Cities with Minimum Cost

Max Flow:
- Maximum Network Flow
- Matching in Bipartite Graph
- Couples Holding Hands

### External References Directory

**Visualization Tools:**
- draw.io: graph visualization
- Visualgo.net: algorithm visualization
- Graph online: interactive
