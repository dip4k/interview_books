## 📚 The Curriculum

### Week 1: Foundations
**Goal:** Understand how computers actually work and how to measure algorithm efficiency.
* **Day 1: RAM Model & Pointers** — The computational model all analysis assumes.
* **Day 2: Asymptotic Analysis** — Why Big-O matters and how it's derived.
* **Day 3: Space Complexity** — Space Complexity — Memory usage, Stack vs Heap, space trade-offs.
* **Day 4: Recursion I** — Stack frames, base cases, intuitive understanding.
* **Day 5: Recursion II** — Advanced recursion, tail recursion, mutual recursion.
* **Why:** Prerequisites for understanding why specific structures are efficient or slow.

### Week 2: Linear Structures
**Goal:** Master fundamental data structures and understand memory behavior.
* **Day 1: Arrays** — Contiguous memory, cache locality, O(1) indexing.
* **Day 2: Dynamic Arrays** — Automatic growth, amortized analysis.
* **Day 3: Linked Lists** — Pointer-based structures, trade-offs, when they're useful (rarely).
* **Day 4: Stacks & Queues** — LIFO/FIFO ordering, ADTs.
* **Day 5: Binary Search** — Logarithmic reduction on sorted data.
* **Why:** The building blocks for all advanced structures.

### Week 3: Sorting & Hashing
**Goal:** Master sorting algorithms and understand hash tables deeply.
* **Day 1: Elementary Sorts** — Bubble, insertion, selection;understand the limits.
* **Day 2: Merge Sort & Quick Sort** — Divide-and-conquer sorting; analyze both.  
* **Day 3: Heap Sort & Variants** — Heapify, in-place sorting.
* **Day 4: Hash Tables I** — Hash functions, collision theory, load factor.
* **Day 5: Hash Tables II** — Chaining vs open addressing;real implementations.
* **Why:** Sorting is ubiquitous. Hash tables are fundamental. Combined, they explain indexing.

### Week 4: Problem-Solving Patterns
**Goal:** Learn systematic techniques for solving many problem types.
* **Day 1: Two Pointers** — Strategy and application, When and why this technique works.
* **Day 2: Sliding Window (Fixed)** — Fixed-size window over array.
* **Day 3: Sliding Window (Variable)** — Dynamic window for optimization.
* **Day 4: Prefix Sums** — Trade space for time in range queries.
* **Day 5: Cycle Detection** — Floyd's algorithm, graph cycles.
* **Why:** You now have data structures. These patterns show how to use them effectively.

### ⭐ Week 4.5: TIER 1 - CRITICAL PROBLEM-SOLVING PATTERNS
**Goal:** Master essential patterns that solve 70-80% of interview problems. Building on Weeks 1-4 foundations.
* **Why:** These provide the highest ROI for interview readiness.
* **Day 1: Hash Map / Hash Set**
- Interview Usage: 70% of all interview problems!
- Key Concept: O(1) average-case lookup and insertion via hashing
- Real Problems: Two sum, anagrams, duplicates, frequency counting
- Why Essential: Foundation for almost every advanced problem

* **Day 2: Monotonic Stack**
- Interview Usage: 20-30% of stack problems
- Key Concept: Maintain monotonic order while processing
- Real Problems: Next greater element, trapping rain water, largest rectangle
- Why Essential: Unique pattern enabling medium/hard problems

* **Day 3: Merge Operations**
- Interview Usage: 30% of array/list problems
- Key Concept: Combine sorted structures in O(n) time
- Real Problems: Merge sorted arrays, merge sorted lists, merge K lists
- Why Essential: Foundation for merge sort and multi-way operations

* **Day 4 (Part A): Partition**
- Interview Usage: 15% of array problems
- Key Concept: In-place segregation using two pointers
- Real Problems: Move zeroes, Dutch National Flag, quicksort partitioning
- Why Essential: Space optimization and quicksort foundation

* **Day 4 (Part B): Kadane's Algorithm**
- Interview Usage: 10% of DP/array problems
- Key Concept: Maximum subarray using dynamic programming
- Real Problems: Maximum subarray, maximum product subarray
- Why Essential: Classic DP pattern, foundation for advanced DP

### Week 5: Trees & Heaps
**Goal:** Master hierarchical data structures.
* **Day 1: Binary Tree Anatomy** — Structure, properties, traversal foundations.
* **Day 2: Tree Traversals** — Inorder, preorder, postorder, level-order.
* **Day 3: Binary Search Trees** — Maintaining sorted order, search/insert/delete.
* **Day 4: Heaps & Priority Queues** — Complete binary trees, heap property.
* **Day 5: Balanced Trees** — AVL, Red-Black trees; when needed.
* **Why:** Trees are everywhere (DOM, file systems, databases). Understanding them deeply is essential.

### 🟡 Week 5.5: TIER 2 - STRATEGIC PATTERNS
**Goal:** Extend coverage to 80-88%.
**When** : Week 5.5, after Week 5 consolidation
* **Day 1: Difference Array**
- Interview Usage: 10-15% of range update problems
- Key Concept: Inverse of prefix sums for O(n+k) efficiency
- Real Problems: Range addition, hotel bookings, shift queries
- Why Important: Optimizes O(n×k) to O(n+k) for range updates

* **Day 2: In-Place Replacement**
- Interview Usage: 8-12% of array manipulation problems
- Key Concept: Modify arrays in-place with O(1) extra space
- Real Problems: Remove duplicates, remove element, remove vowels
- Why Important: Space optimization (interview preference for O(1) space)

* **Day 3: Deque Operations**
- Interview Usage: 5-10% of sliding window problems
- Key Concept: Double-ended queue for optimal window operations
- Real Problems: Sliding window maximum, sliding window minimum
- Why Important: Optimizes O(n log n) to O(n) for sliding window
* **Why:** Optimization techniques frequently requested in intermediate/hard interviews.

### Week 6: Graph Foundations
**Goal:** Graph representations and fundamental traversals.
* **Day 1: Graph Representations** — Adjacency matrix vs list; when each is best.
* **Day 2: Breadth-First Search** — Level-by-level exploration, shortest paths.
* **Day 3: Depth-First Search** — Recursive exploration, topological sorting.
* **Day 4: Topological Sort** — DAG ordering, dependency resolution.
* **Day 5: Union-Find** — Disjoint set forest; near-constant time operations.
* **Why:** Graphs model relationships (networks, web, social graphs). Graph algorithms are fundamental.

### Week 7: Advanced Graph Algorithms
**Goal:** Weighted graphs and network flow.
* **Day 1: Dijkstra's Algorithm** — Shortest path with weights, greedy approach.
* **Day 2: Bellman-Ford & Floyd-Warshall** — Negative weights, all-pairs distances.
* **Day 3: Minimum Spanning Trees** — Kruskal's and Prim's algorithms.
* **Day 4: Network Flow I** — Max flow basics, Ford-Fulkerson.
* **Day 5: Network Flow II** — Min cut, bipartite matching, advanced flow.
* **Why:** Building on graph basics; now handle weighted and flow problems. Critical for routing and optimization problems.

### Week 8: Specialized Structures
**Goal:** Learn advanced indexing structures.
* **Day 1: Tries** — Prefix trees for string searching.
* **Day 2: Segment Trees I** — Range query data structure, lazy propagation basics.
* **Day 3: Segment Trees II** — Advanced segment tree techniques.
* **Day 4: Fenwick Trees** — Binary indexed trees for range queries.
* **Day 5: Suffix Structures** — Suffix arrays, suffix trees for string problems.
* **Why:** Powerful tools for specific string and range classes.

### Week 9: String & Math Algorithms
**Goal:** Master string matching and mathematical algorithms.
* **Day 1: String Matching: KMP Algorithm** — Knuth-Morris-Pratt algorithm.
* **Day 2: String Matching: Rabin-Karp** — Rolling hash.
* **Day 3: Number Theory** — Primes, GCD, modular arithmetic foundations
* **Day 4: Modular Arithmetic** — Modular exponentiation, inverse, Chinese Remainder Theorem.
* **Day 5: Computational Geometry** — Convex hull, intersections.
* **Why:** Fundamentals for cryptography and text processing. String and math problems appear frequently. KMP is elegant. Number theory underlies many problems.

### Week 10: Greedy & Backtracking
**Goal:** Learn greedy and backtracking paradigms.
* **Day 1: Greedy Paradigm** — When greedy works, exchange arguments, examples.
* **Day 2: Backtracking I** — Constraint satisfaction, pruning strategies.
* **Day 3: Backtracking II** — Advanced backtracking problems.
* **Day 4: Pruning & Optimization** — Search space reduction, Techniques for faster search.
* **Day 5: Divide and Conquer** — Recursive problem decomposition strategy.
* **Why:** Two fundamental problem-solving paradigms. Many interview problems use these.

### Week 11: Dynamic Programming
**Goal:** Deep mastery of DP.
* **Day 1: DP Philosophy** — Optimal substructure, memoization, when DP applies.
* **Day 2: 1D DP** — Linear DP problems (coins, climb stairs, etc.).
* **Day 3: Classic Patterns** — Longest increasing subsequence, edit distance, knapsack.
* **Day 4: 2D/Sequence DP** — Matrix DP, string DP problems.
* **Day 5: Advanced DP** — DP on trees, digit DP, bitmask DP.
* **Why:** DP is the hardest paradigm to learn. Dedicating a full week ensures deep mastery.

### Week 12: Interview Mastery & Integration
**Goal:** Solve complex problems by integrating multiple concepts.
* **Day 1: Merge Intervals** — Interval problems, sweep line algorithms.
* **Day 2: Monotonic Stack (Advanced)** — Stack-based techniques refinement.
* **Day 3: Cyclic Sort** — In-place array rearrangement.
* **Day 4: Matrix Problems (Advanced)** — Complex matrix traversal.
* **Day 5: System Review & Integration** — Integration of concepts, Bringing it all together.
* **Why:** These are complex problem types that require integrating multiple concepts. The capstone week.

### 🟢 Week 13+: TIER 3 - GOOD-TO-KNOW PROBLEM-SOLVING PATTERNS
**Goal:** Learn extension patterns and specialized techniques. +5-8% interview coverage (85-95% cumulative).
* **Pattern 1: Fast & Slow Pointers (Extended)**
- Interview Usage: 3-5% of linked list problems
- Key Concept: Two pointers at different speeds for various operations
- Real Problems: Middle of linked list, partition list, palindrome linked list, reorder list
- Why Good-to-Know: Extends basic pointer pattern beyond cycle detection

**Pattern 2: Reverse & Two Pointers**
- Interview Usage: 5-8% of string/array problems
- Key Concept: Reversal and two-pointer merging strategies
- Real Problems: Reverse string, reverse words, two sum sorted array, container with most water
- Why Good-to-Know: String/array manipulation extensions

**Pattern 3: Matrix Traversal**
- Interview Usage: 3-5% of matrix problems
- Key Concept: Spiral, zigzag, diagonal traversal patterns
- Real Problems: Spiral matrix, zigzag traversal, diagonal traversal, rotate matrix
- Why Good-to-Know: 2D array navigation patterns

**Pattern 4: Conversion & Encoding**
- Interview Usage: 2-3% of string problems
- Key Concept: String compression and encoding techniques
- Real Problems: String compression, run-length encoding, decode string, encode and decode
- Why Good-to-Know: String manipulation and space optimization

* **Why:** Completes the toolkit for niche or "good-to-know" scenarios.

### Weeks 14-16: Advanced Mastery (Optional)
**Goal:** Continued practice and depth.
* Focus on re-applying Week 12 concepts to harder constraints.
* Deep dive into previously identified weak points.
* Mock interview simulation.