# Week 7: Interview Q&A Reference

**Week:** 7 | **Topic:** Advanced Graph Algorithms Q&A  
**Use:** For quick lookup during interview prep or after problem-solving

---

## DIJKSTRA'S ALGORITHM Q&A

**Q: Why does Dijkstra fail on negative weights?**
A: Dijkstra assumes once a node is visited, its shortest distance is finalized. With negative weights, a later path might improve via a negative edge, violating this assumption.

**Q: How would you find shortest path to a specific node (not all)?**
A: Stop early when that node is visited/popped from heap. Algorithm still works; you're done when you extract that node.

**Q: Why use min-heap instead of sorted list?**
A: Extract-min: heap O(log V) vs sorted list O(V). For E edge relaxations, total time is O(E log V) vs O(E × V). Huge difference!

**Q: What if graph disconnected?**
A: Unreached nodes remain at infinity. This is correct—they're unreachable. Return "impossible" for those nodes.

**Q: How to reconstruct actual path (not just distance)?**
A: Use parent pointers. When updating distance to v, record parent[v] = u. Trace back from destination to source using parent pointers.

---

## BELLMAN-FORD & FLOYD-WARSHALL Q&A

**Q: Why V-1 relaxations enough for Bellman-Ford?**
A: Longest shortest path = V-1 edges (visiting each node once). By V-1 iterations, all such paths found. If Vth iteration still improves, a negative cycle exists.

**Q: How to detect negative cycle?**
A: After V-1 relaxations, try relaxing all edges once more. If any edge can still be relaxed, negative cycle exists.

**Q: Why is Floyd-Warshall order-dependent (k must go outer)?**
A: Must process k in order to ensure dist[i][k] and dist[k][j] already use nodes 0..k-1. If k not outer, intermediate nodes not yet available.

**Q: When would Floyd-Warshall beat Bellman-Ford?**
A: Dense graphs. Floyd-Warshall O(V³), Bellman-Ford O(V × E). If E = V², then V³ < V × V² = V³ (same), but Floyd-Warshall simpler code. For E > V²: Floyd-Warshall better.

**Q: What's the time complexity of running Dijkstra V times vs Floyd-Warshall?**
A: Dijkstra V times: O(V × (V+E) log V) = O(V² log V) for sparse. Floyd-Warshall: O(V³). Dijkstra wins for sparse.

---

## MINIMUM SPANNING TREES Q&A

**Q: Why does Kruskal's not create cycles?**
A: Union-Find detects when endpoints already connected. If they're in same component (already connected), adding edge would create cycle. We skip it.

**Q: Why does Prim's always pick available minimum edge?**
A: By induction. If tree so far is part of some MST, adding minimum edge from tree to non-tree maintains optimality (by cut property).

**Q: Can MST be non-unique?**
A: Yes, if multiple edges have same weight. Different MSTs can exist with same total cost. All have cost = minimum possible.

**Q: How to verify an MST is optimal?**
A: Check all edges follow cut property. For each edge in MST, removing it should increase total cost. Also: no cycle, connects all V nodes, has V-1 edges.

**Q: When to use Kruskal vs Prim?**
A: Kruskal: sparse graphs, simpler to code (sort + union-find). Prim: dense graphs, more efficient. Both correct; choice is preference + graph structure.

---

## MAXIMUM FLOW Q&A

**Q: Why do we need backward edges in residual graph?**
A: To reroute flow! Backward edge (capacity = current flow) represents ability to undo previous routing. Allows finding better paths via rerouting.

**Q: What's bottleneck capacity on a path?**
A: Minimum residual capacity on any edge in the path. You can only push as much flow as the tightest edge allows.

**Q: How does BFS improve Ford-Fulkerson?**
A: BFS finds shortest augmenting path. Shortest path = fewest edges = limits rerouting iterations to O(V×E) instead of unbounded. Edmonds-Karp is polynomial.

**Q: Can maximum flow be non-integer with integer capacities?**
A: No. Integrality theorem: integer capacities guarantee integer flow. Ford-Fulkerson preserves integer invariant throughout.

**Q: What if no augmenting path exists?**
A: Maximum flow reached. No more flow can be pushed from source to sink. The algorithm terminates with optimal result.

**Q: What's the difference between Ford-Fulkerson and Edmonds-Karp?**
A: Ford-Fulkerson is framework (can use any pathfinding). Edmonds-Karp uses BFS for pathfinding, guaranteeing polynomial-time O(V×E²).

---

## MIN-CUT & ADVANCED FLOW Q&A

**Q: How to find min-cut after max-flow?**
A: Run BFS/DFS from source in residual graph (only following edges with capacity > 0). Reached nodes = S (source side). Min-cut = all edges from S to T.

**Q: Why does min-cut equal max-flow?**
A: By max-flow min-cut theorem. After max-flow, edges from source-side to sink-side in residual must all be saturated (flow = capacity), and no path exists. Cut capacity = flow value.

**Q: How does bipartite matching convert to flow?**
A: Build network: source → left (cap 1) → right (cap 1) → sink (cap 1). Max-flow = max matching size. Unit capacities ensure each node used once.

**Q: How to find maximum matching in bipartite graph?**
A: Convert to flow problem (as above), run Edmonds-Karp. Time: O(√(L+R) × E) with Hopcroft-Karp specialization.

**Q: What's König's theorem?**
A: In bipartite graphs, minimum vertex cover size = maximum matching size. Consequence: can compute vertex cover using max-flow algorithms.

**Q: When would min-cost max-flow be needed?**
A: When minimizing cost matters while maintaining maximum flow. Example: route packages on cheapest paths while maximizing throughput. Uses successive shortest path (Bellman-Ford each iteration).

---

## ALGORITHM CHOICE Q&A

**Q: I need shortest paths. How do I choose algorithm?**
A: Check weights: Non-negative? → Dijkstra. Negative but no cycles? → Bellman-Ford. Need all-pairs? → Floyd-Warshall.

**Q: I have dense graph with negative weights. Which algorithm?**
A: Floyd-Warshall O(V³) likely best. Bellman-Ford O(V×E) = O(V³) for dense anyway. Floyd-Warshall simpler code.

**Q: I need to connect all nodes with minimum cost.**
A: MST problem. Sparse? → Kruskal's. Dense? → Prim's. Both O(E log E) - O((V+E) log V) respectively.

**Q: I have capacity constraints and need to maximize something.**
A: Flow problem! Apply max-flow. If disguised (matching, min-cut), recognize and convert.

**Q: Which flow algorithm should I use?**
A: Edmonds-Karp (BFS-based Ford-Fulkerson) for guaranteed polynomial-time O(V×E²). Simple implementation, safe choice.

---

## COMPLEXITY Q&A

**Q: Is O(E log E) always better than O((V+E) log V)?**
A: Not always. Dense graph (E = V²): E log E = V² log V > (V+E) log V = V² log V (essentially same). Sparse (E = V): E log E = V log V < (V+E) log V = V log V (essentially same). Other factors matter.

**Q: When is O(V³) acceptable?**
A: When V ≤ 500 roughly. V=500: 125M operations ≈ 0.1s. V=1000: 1B operations ≈ 1s. V=5000: 125B operations ≈ 125s (too slow).

**Q: How do I predict algorithm runtime?**
A: Estimate V and E from problem. Calculate operations count. Roughly 10^8-10^9 operations per second on modern machines. Then estimate time.

---

## COMMON PITFALL Q&A

**Q: I used Dijkstra and got wrong answer. Why?**
A: Likely negative weights. Dijkstra assumes non-negative. Check problem statement. If negative weights exist, use Bellman-Ford.

**Q: My Ford-Fulkerson is too slow. What's wrong?**
A: Probably using DFS instead of BFS. DFS doesn't guarantee polynomial-time. Switch to BFS (Edmonds-Karp). Huge speedup for large networks.

**Q: I forgot what algorithm to use. How do I decide?**
A: Ask: (1) Single-source or all-pairs? (2) Weights negative? (3) Shortest path or spanning tree? (4) Capacity constraints? Answers determine algorithm.

**Q: Graph disconnected. My algorithm fails. Bug?**
A: Not necessarily a bug. If asking for shortest path to disconnected node, it's unreachable (infinity). If asking for spanning tree of disconnected graph, impossible. Check problem requirements.

**Q: Should I implement from scratch in interview?**
A: Yes. Implement basic version correctly. Then optimize/add features if time. Correctness > optimization. Don't skip steps to save time.

---

## REAL-WORLD APPLICATION Q&A

**Q: When would I use Dijkstra in real job?**
A: GPS/maps navigation. Network routing. Game pathfinding. Any "find cheapest/shortest path" where costs are positive.

**Q: When would I use MST?**
A: Network design (telecom, electricity). Cluster analysis. Approximation algorithms. Any "connect all with minimum cost."

**Q: When would I use max-flow?**
A: Network capacity planning. Bipartite matching (job assignments). Image segmentation. Circulation problems. Harder to recognize but powerful.

**Q: Why do ML engineers need graph algorithms?**
A: Modern deep learning uses graphs heavily. GNNs, attention (flow-like), clustering (MST-based). Knowledge graphs use pathfinding. Recommendation systems use matching.

---

## INTERVIEW STRATEGY Q&A

**Q: How much time for each problem type?**
A: Easy (Dijkstra): 5-10 min. Medium (MST, matching): 15-20 min. Hard (min-cost flow, complex problem): 30-45 min.

**Q: Should I always use optimal algorithm?**
A: No. Use simplest correct algorithm first. If TLE, optimize. Interview values correctness + communication > premature optimization.

**Q: What if I forget algorithm details?**
A: Explain your approach clearly. Implement key idea. If needed, use slower algorithm correctly rather than guessing fast algorithm wrongly.

**Q: How to handle "I don't know" moment?**
A: Say "I recognize this might be [algorithm], but let me think through approach instead of guessing." Think out loud. Interviewer appreciates honesty.

---

**End of Week 7 Q&A Reference**  
**Use this for:** Quick lookup, last-minute review, interview prep  
**Next:** Full problem-solving walkthroughs and implementation guides

