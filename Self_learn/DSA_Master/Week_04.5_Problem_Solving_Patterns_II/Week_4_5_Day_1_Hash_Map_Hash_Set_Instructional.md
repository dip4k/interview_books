# Week 4.5, Day 1: Hash Map / Hash Set

## 🗓 Metadata
**Week:** 4.5 (Tier 1) | **Day:** 1 of 5 | **Topic:** Hash Map / Hash Set  
**Category:** Critical Problem-Solving Patterns | **Difficulty:** 🟡 Medium  
**Prerequisites:** Week 1-4 (Foundations, Linear Structures, Sorting & Hashing, Problem Patterns)  
**Time:** 90-120 minutes | **Status:** 🔍 In Study  
**Interview Coverage:** **70% of ALL interview problems!**

---

## 1️⃣ THE WHY — Engineering Motivation

**Real-World Problem:**
You have 1 million user IDs, need to find duplicates instantly. Naive: O(n²) nested loops. Better: store in hash set, O(1) lookup per ID.

**Design Problems Solved:**
- Instant membership checking (is element in set?)
- Frequency counting without sorting
- Finding pairs/groups with properties
- Caching results (memoization in DP)
- De-duplicating data streams
- Building indices for fast retrieval

**Real System Usage:**
- **Databases:** Hash indexes for O(1) lookups (PostgreSQL, MySQL hash tables)
- **Caching:** Redis hash maps for O(1) cache hits
- **Compilers:** Symbol tables (variable/function names → memory addresses)
- **Operating Systems:** Page tables (virtual address → physical address mapping)
- **Graphics:** Texture caching, material ID lookup
- **Networking:** DNS caching (domain → IP address)

**Why Hash Maps/Sets Matter:**
Hash-based data structures are foundational. They appear in 70% of interview problems because:
- Most problems need fast lookup
- Hash maps eliminate O(n) lookups
- Enable O(n) solutions instead of O(n²)
- Building block for advanced techniques (monotonic stack uses deque + hash, DP uses memoization hash)

---

## 2️⃣ THE WHAT — Mental Model & Intuition

**Core Analogy:**
Think of a hash set like a **library with perfect address system**. Instead of searching shelves (O(n)), you hash the book title to get its exact shelf location (O(1)).

```
Hash Set: ["alice", "bob", "charlie"]
lookup("bob"):
  hash("bob") = 42  ← hash function
  check shelf 42  ← direct access
  Found! O(1)
```

**Hash Map: Same idea, but store key-value pairs**
```
Hash Map: {"alice": 25, "bob": 30, "charlie": 28}
lookup("alice"):
  hash("alice") = 17
  check shelf 17  → ("alice", 25)
  Found! O(1)
```

**Key Invariants:**
- Hash function maps any input to fixed range (0 to table size - 1)
- Same input always produces same hash
- Different inputs may hash to same location (collision)
- Good hash functions distribute inputs evenly
- Collision resolution: chaining (linked list) or open addressing (probe)

**Visual Representation:**
```
Hash Table (size 10):
Index:  0   1   2   3   4   5   6   7   8   9
      [   ] ["a"][ ] ["b"][ ] ["c"][ ] [ ] ["d"][ ]
      
Insert "e": hash("e") = 4
      [   ] ["a"][ ] ["b"]["e"]["c"][ ] [ ] ["d"][ ]
      
Lookup "b": hash("b") = 3 → Found at index 3 ✓
```

---

## 3️⃣ THE HOW — Mechanical Walkthrough

**State:**
- `table`: array of size N (hash table)
- `hash_function`: maps key to index (0 to N-1)
- `collision_resolution`: how to handle collisions

**Operation 1: Insert (Hash Map)**
```
1. hash_value = hash(key) % table_size
2. Go to table[hash_value]
3. If empty, insert (key, value)
4. If occupied (collision):
     a) Chaining: append to linked list
     b) Open addressing: probe next empty spot
5. Time: O(1) average, O(n) worst (all collisions)
6. Space: O(n) for n elements
```

**Operation 2: Lookup**
```
1. hash_value = hash(key) % table_size
2. Go to table[hash_value]
3. Check if key exists
4. Return value or not found
5. Time: O(1) average, O(n) worst (collision chain)
```

**Operation 3: Delete**
```
1. hash_value = hash(key) % table_size
2. Find key in table[hash_value]
3. Remove it
4. Time: O(1) average, O(n) worst
```

**Memory Behavior:**
- Hash tables use contiguous memory (good cache locality when sparse)
- Collisions move to linked lists (bad cache locality)
- Load factor = n / table_size. When > 0.75, rehash to larger table (O(n) operation, but amortized O(1) per insertion)

---

## 4️⃣ VISUALIZATION — Simulation & Examples

**Example 1: Two Sum (find pair summing to target)**
```
Array: [2, 7, 11, 15], target = 9

Step 1: seen = {}
  Process 2: seen = {2}
  Process 7: 9-7=2, check seen: YES! → Return [2,7]
  
Time: O(n), Space: O(n)
vs naive: O(n²)
```

**Example 2: Anagrams (group by character frequency)**
```
Words: ["eat", "tea", "ate", "bat", "tab"]

Approach: hash by sorted letters
  "eat" → sorted: "aet" → key
  "tea" → sorted: "aet" → same key!
  "ate" → sorted: "aet" → same key!
  "bat" → sorted: "abt" → different key
  "tab" → sorted: "abt" → same key as "bat"

Result: {"aet": ["eat", "tea", "ate"], "abt": ["bat", "tab"]}

Time: O(n × k log k) where k = max word length
```

**Example 3: Frequency Counter**
```
String: "abracadabra"

Process each character:
  'a': freq = 1
  'b': freq = 1
  'r': freq = 1
  'a': freq = 2 (already in hash)
  ...
  
Result: {'a': 5, 'b': 2, 'r': 2, 'c': 1, 'd': 1}

Time: O(n), Space: O(unique characters)
```

---

## 5️⃣ CRITICAL ANALYSIS — Performance & Robustness

| Operation | Best | Average | Worst | Notes |
|-----------|------|---------|-------|-------|
| **Insert** | O(1) | O(1) | O(n) | Worst when all hash to same bucket |
| **Lookup** | O(1) | O(1) | O(n) | Same as insert |
| **Delete** | O(1) | O(1) | O(n) | Same as insert |
| **Rehash** | O(n) | O(n) | O(n) | When load factor exceeds threshold |

**Load Factor & Resizing:**
- Load factor = n / table_size
- When load_factor > 0.75, double table size and rehash
- Amortized: O(1) per insertion (spreading O(n) rehash over n insertions)

**Real Memory Behavior:**
- Empty hash table wastes space (typical load factor 0.5-0.75)
- Collisions force linked list traversal (bad cache locality)
- Good hash function distributes evenly (minimal collisions)
- Python dicts use open addressing (faster than chaining)

**Edge Cases & Failure Modes:**
- **Bad hash function:** All keys hash to same bucket → O(n) operations
- **Integer overflow:** Hash code might overflow, need modulo
- **Null keys:** Many languages allow null as key (Python dict allows None)
- **Floating point keys:** Risky due to precision, use integers or strings
- **Memory pressure:** Large hash tables consume memory

**When Complexity Analysis Breaks Down:**
- Worst case O(n) happens rarely in practice
- Hash function quality matters (cryptographic vs simple)
- Rehashing cost is amortized, not per operation
- Load factor determines true performance (not just table size)

---

## 6️⃣ REAL SYSTEM INTEGRATION

**Operating Systems:**
Linux kernel uses hash tables for:
- Process scheduling (PID → process control block)
- File descriptors (fd → file structure)
- Memory management (virtual address → physical page mapping in TLB misses)

**Databases:**
PostgreSQL uses hash indexes for:
- SELECT by exact key (no range queries)
- O(1) lookup instead of B-tree O(log n)
- Hash collisions handled with chaining

**Compilers:**
Symbol tables use hash maps:
- Variable name → type, scope, memory location
- Function name → arity, return type, code location
- Enables O(1) identifier lookup during compilation

**Networking:**
- DNS caching: domain name → IP address
- ARP caching: IP address → MAC address
- Bloom filters (probabilistic hash sets) for fast existence checks

**Graphics Engines:**
- Texture caches: texture ID → GPU memory pointer
- Material library: material name → material properties
- Shader compilation caching: source code hash → compiled binary

---

## 7️⃣ CONCEPT CROSSOVERS

**Builds On:**
- Arrays (hash table is array underneath)
- Linked lists (collision resolution via chaining)
- Hash functions (mathematical foundation)

**Built Upon By:**
- Monotonic Stack (uses hash map for O(1) lookups)
- Memoization in DP (hash map stores computed results)
- Graph algorithms (adjacency lists use hash maps)
- All pattern-finding algorithms

**Used In Algorithms:**
- Two pointer with hash: Two Sum, 3Sum
- Sliding window with hash: Longest substring without repeat
- Merge with hash: Find common elements
- Graph algorithms: DFS/BFS use hash for visited set
- Dynamic programming: Memoization uses hash map

**Combinations with Other Techniques:**
- Hash + sorting: Group anagrams
- Hash + heaps: Find top K frequent elements
- Hash + graph: Detect cycles in undirected graphs
- Hash + DP: Count unique solutions

---

## 8️⃣ MATHEMATICAL & THEORETICAL PERSPECTIVE

**Formal Definition:**
Hash table with n elements, table size m:
- Load factor λ = n / m
- Hash function h: keys → [0, m-1]
- Expected lookup time: O(1 + λ) with good distribution
- With chaining: O(1 + λ) average case
- With open addressing: O(1 / (1 - λ)) average case

**Hash Function Properties:**
1. **Deterministic:** h(x) always produces same output
2. **Uniform distribution:** Each bucket equally likely
3. **Fast computation:** O(1) time to compute

**Collision Probability (Birthday Paradox):**
- With m buckets and n items, expected collisions ≈ n² / (2m)
- When n ≈ √m, collisions become likely
- λ > 0.75 → rehash to larger table

**Amortized Analysis:**
- Total cost of n insertions with rehashing = O(n)
- Average cost per insertion = O(1)
- Rehashing cost O(n) is amortized over n insertions

---

## 9️⃣ ALGORITHMIC DESIGN INTUITION

**When to Use Hash Map/Set:**

✅ **Use Hash Map When:**
- Need O(1) membership checking (exact key)
- Counting frequencies
- Storing key-value pairs
- Grouping elements by property
- Memoization in DP
- Building indices

✅ **Use Hash Set When:**
- Only need to check membership (not values)
- De-duplicating
- Finding unique elements
- Checking if element seen before

❌ **DON'T Use Hash When:**
- Need range queries (use B-tree or sorted array)
- Need order preservation (use sorted map)
- Keys are complex objects (use tree-based)
- Worst-case O(n) unacceptable (use balanced tree)
- Memory very limited (tree uses less space per collision)

**Real-World Trade-offs:**
- **Hash vs Tree:** Hash faster (O(1) vs O(log n)) but tree ordered
- **Chaining vs Open Addressing:** Chaining flexible (delete easy), open addressing cache-friendly
- **Load Factor:** High load → more collisions, low load → wasted space

**Anti-patterns:**
- ❌ Using mutable objects as keys (hash changes if object modified)
- ❌ Hash table with bad distribution (all collisions)
- ❌ Not resizing when load factor gets too high
- ❌ Using floating point as key (precision issues)

---

## 🔟 KNOWLEDGE CHECK — Socratic Reasoning

**Q1:** Two Sum finds a pair in O(n). Why can't we do this faster than O(n)?

**Q2:** Why must hash function output be deterministic? What breaks if it's random?

**Q3:** If all n items hash to same bucket, what's the time complexity of lookup?

**Q4:** Load factor 0.5 vs 0.9: which uses more memory, which has faster lookup?

**Q5:** Can you delete items efficiently from an open addressing hash table? Why or why not?

---

## 1️⃣1️⃣ RETENTION HOOK — Memory Anchors

**One-Liner:**
> **Hash Map: O(1) average lookup via hash function → index mapping. Foundation for 70% of interview problems.**

**Mnemonic:** "H.A.S.H." → Hash function, Amortized O(1), Store key-value, Handle collisions

**Cognitive Lenses:**

| **Computational** | Hash reduces search from O(n) to O(1) by avoiding linear scan. CPU cache misses on collisions. |
| **Psychological** | Natural intuition: book title → shelf location (not linear search). |
| **Design Trade-off** | Space vs time: more memory (load factor 0.5) → fewer collisions → faster. |
| **AI/ML Analogy** | Similar to embedding vectors: hash key → feature vector → table lookup. |
| **Historical Context** | Earliest hash tables (1953, UNIVAC). Donald Knuth popularized analysis. |

---

## Supplementary Outcomes

**Practice Problems (10+):**
1. Two Sum
2. Contains Duplicate
3. Valid Anagram
4. Group Anagrams
5. Majority Element
6. Ransom Note
7. Happy Number
8. Word Pattern
9. Isomorphic Strings
10. Find All Anagrams in a String

**Interview Q&A Highlights:**
- Why O(1) and not O(log n)?
- Collision resolution strategies
- Why rehash at load factor 0.75?
- Mutable vs immutable keys
- Custom objects as keys

**Common Misconceptions:**
- ❌ "Hash table always O(1)" → ✅ Average O(1), worst O(n)
- ❌ "No collisions with good hash" → ✅ Collisions always possible (pigeonhole principle)
- ❌ "Larger table = fewer collisions" → ✅ Load factor matters, not absolute size

