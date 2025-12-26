# Hash Tables I: Fundamentals, Functions & Collision Theory

## 🗓 Metadata
**Topic:** Hash Functions, Load Factor, Direct Addressing  
**Week:** Week 3  
**Day:** Day 4 of 5  
**Category:** Hash Table Foundations  
**Difficulty:** 🟡 Medium  
**Status:** 🔍 In Study  
**Last Reviewed:** —  
**Confidence Level (1–5):** —/5  

---

## 1️⃣ The Why — Engineering Motivation

### Real-World Problem

**Sorting is O(n log n). Can we do better?**

Answer: **Different problem.**

Sorting organizes elements for sequential access. But sometimes we need instant lookup:
- Dictionary lookup: Find definition instantly, not by scanning dictionary
- Database search: Locate user by ID instantly, not by scanning all users
- Cache: Find cached result instantly, not by checking all cache entries
- Symbol table: Find variable type instantly in compiler, not by searching

**The demand:** Given a key, find its value in O(1) time (not O(log n), not O(n)).

### Design Problem Solved

**Hash Table Solution:**
- ✅ O(1) average lookup (vastly different from sorting!)
- ✅ O(1) average insertion
- ✅ O(1) average deletion
- ❌ Requires hash function design (not straightforward)
- ❌ Space overhead and collisions (unavoidable)

### Real-World Applications

1. **Caches:** CPU cache, web browser cache, CDN — all use hash tables
2. **Databases:** Indexes on primary keys use hash tables
3. **Compilers:** Symbol tables map variable names to types/offsets
4. **Operating Systems:** Page tables map virtual → physical addresses (must be O(1)!)
5. **Cryptography:** Hash functions for digital signatures, checksums
6. **Deduplication:** Finding duplicate files using content hashes

### Trade-off Introduced

| Aspect | Hash Table | Sorted Array | Binary Search Tree |
|--------|-----------|-------------|-------------------|
| **Lookup** | O(1) average | O(log n) | O(log n) |
| **Insert** | O(1) average | O(n) | O(log n) amortized |
| **Delete** | O(1) average | O(n) | O(log n) |
| **Range** | ❌ Can't | ✓ Easy | ✓ Easy |
| **Order** | ❌ No order | ✓ Sorted | ✓ Sorted |
| **Worst** | O(n) with bad hash | Always O(log n) | O(n) unbalanced |

---

## 2️⃣ The What — Mental Model & Intuition

### Core Analogy: Library Checkout System

**Mental Model:** Imagine a library with 10,000 books but a checkout desk with only 100 spots.

**Direct Addressing:**
```
Checkout desk has 100 numbered spots (0-99)

Book with ISBN 2847501 goes to spot: 2847501 mod 100 = 1
Book with ISBN 3956201 goes to spot: 3956201 mod 100 = 1  ← Collision!
Book with ISBN 4182503 goes to spot: 4182503 mod 100 = 3

Fast lookup: "Where's book with ISBN 2847501?" → Check spot 1
```

**Why this works:**
- Instead of searching all 10,000 books, check only 1 spot
- If multiple books at same spot (collision), scan that small pile
- Average case: Very fast

**The key insight:** Trade space (100 spots for 10,000 books) for speed (O(1) vs O(n)).

### Visual Representation

```
HASH TABLE (Size 11):

Index:  0   1   2   3   4   5   6   7   8   9  10
Value: [ ]  [7] [ ]  [3]  [1]  [ ]  [9]  [ ]  [ ]  [5]  [2]

Hash function: h(key) = key mod 11

Insert 7:    h(7) = 7 mod 11 = 7  → spot 7
Insert 3:    h(3) = 3 mod 11 = 3  → spot 3
Insert 1:    h(1) = 1 mod 11 = 1  → spot 1
Insert 14:   h(14) = 14 mod 11 = 3 → spot 3 (collision with 3!)
                                     → handle collision (next topic)

LOOKUP: "Do we have 7?"
        h(7) = 7 → Check spot 7 → Found! O(1)

LOOKUP: "Do we have 100?"
        h(100) = 100 mod 11 = 1 → Check spot 1 → Found 7? No. O(1)
```

### Core Invariants

**Hash Table Property:**
- For key k, store value at index h(k)
- To find key k, compute h(k) and check that index
- If collisions exist, handle them with strategy (chaining or open addressing)

---

## 3️⃣ The How — Mechanical Walkthrough

### Hash Function Design

**Requirements:**
1. **Deterministic:** Same key always produces same hash
2. **Fast:** O(1) computation, not O(n)
3. **Uniform distribution:** Keys spread evenly across table
4. **Unpredictable:** Small changes in input produce large changes in output

**Examples:**

**Integer Hashing (Simple):**
```
h(key) = key mod table_size

Example: table_size = 11
h(7) = 7 mod 11 = 7
h(18) = 18 mod 11 = 7 (collision!)
h(29) = 29 mod 11 = 7 (collision!)

Problem: If key is multiple of 11, all go to spot 0
Solution: Use prime number for table_size → better distribution
```

**Integer Hashing (Better):**
```
h(key) = (a × key + b) mod table_size

Where a, b are carefully chosen constants
Example: a = 7, b = 5, table_size = 11
h(7) = (7×7 + 5) mod 11 = 54 mod 11 = 10
h(18) = (7×18 + 5) mod 11 = 131 mod 11 = 10 (still collision, but less likely)
```

**String Hashing (FNV-1a Hash):**
```
hash = 2166136261  // FNV offset basis
for each byte in string:
    hash ^= byte
    hash *= 16777619  // FNV prime

Example: hash("cat")
Initial: hash = 2166136261
c (99):  hash = (2166136261 XOR 99) * 16777619 = ...
a (97):  hash = (result XOR 97) * 16777619 = ...
t (116): hash = (result XOR 116) * 16777619 = ...
Final:   hash mod table_size
```

**Why FNV works:**
- XOR mixes bits
- Multiplication by large prime spreads bits
- Small changes in input cause avalanche effect in output

### Load Factor and Resizing

**Load Factor Definition:**
```
α (alpha) = n / m

Where:
n = number of items in table
m = size of table
```

**Interpretation:**
- α = 0.5: Table is 50% full on average
- α = 1.0: Table is 100% full on average (too crowded!)
- α = 2.0: Table is 200% full (lots of collisions!)

**Standard Practice:**
```
If α > 0.75:
    Resize table to 2m or larger prime
    Rehash all items: for each item, compute new hash in larger table
    Time: O(n) for all items (but rare, only when α exceeds threshold)
```

**Why resize:**
```
As α grows, collisions increase exponentially
With chaining: average chain length = α
With open addressing: search cost = 1 / (1 - α)

α = 0.5: avg chain = 0.5, search cost = 2
α = 0.75: avg chain = 0.75, search cost = 4
α = 1.0: avg chain = 1.0, search cost = ∞ (table full, must resize)
```

**Dynamic Resizing Sequence:**
```
Start: size = 11, α = 0
Insert 1 item: size = 11, α = 0.09
Insert 2 items: size = 11, α = 0.18
...
Insert 8 items: size = 11, α = 0.73 (still okay)
Insert 9 items: size = 11, α = 0.82 → Resize to 23, rehash all 9 items
Now: size = 23, α = 0.39 (comfortable)
```

---

## 4️⃣ Visualization — Simulation & Examples

### Example 1: Building Hash Table with Integer Keys

**Scenario:** Insert numbers [7, 18, 29, 14, 23] into hash table of size 11

**Hash function:** h(k) = k mod 11

**Insert 7:**
```
h(7) = 7 mod 11 = 7
Table[7] = 7

Index:  0  1  2  3  4  5  6  7  8  9  10
Value: [ ][ ][ ][ ][ ][ ][ ][7][ ][ ][ ]
```

**Insert 18:**
```
h(18) = 18 mod 11 = 7
Table[7] is occupied! → Collision!
(We'll handle this with chaining in Day 5)
For now, pretend we handle it: Place 18 somewhere nearby
```

**Insert 29:**
```
h(29) = 29 mod 11 = 7
Another collision at 7!
```

**Insert 14:**
```
h(14) = 14 mod 11 = 3
Table[3] = 14

Index:  0  1  2  3  4  5  6  7  8  9  10
Value: [ ][ ][ ][14][ ][ ][ ][7,18,29][ ][ ][ ]
```

**Insert 23:**
```
h(23) = 23 mod 11 = 1
Table[1] = 23

Index:  0  1  2  3  4  5  6  7  8  9  10
Value: [ ][23][ ][14][ ][ ][ ][7,18,29][ ][ ][ ]
```

**Observation:** Many collisions at index 7! This is the distribution problem.

### Example 2: String Hashing

**Scenario:** Hash the word "hello" to a table of size 11

**Simple hash (just sum of ASCII values):**
```
ASCII values: h=104, e=101, l=108, l=108, o=111
Sum: 104 + 101 + 108 + 108 + 111 = 532
h("hello") = 532 mod 11 = 4

But: "olleh" also sums to 532! → Collision for permutations
Solution: Weight positions: 104*1 + 101*2 + 108*3 + 108*4 + 111*5
```

**Better hash (polynomial rolling hash):**
```
hash = 0
for each char in "hello":
    hash = (hash * 31 + ASCII(char)) mod table_size

h = 0
h('h'): h = (0 * 31 + 104) mod 11 = 104 mod 11 = 5
h('e'): h = (5 * 31 + 101) mod 11 = 256 mod 11 = 3
h('l'): h = (3 * 31 + 108) mod 11 = 201 mod 11 = 3
h('l'): h = (3 * 31 + 108) mod 11 = 201 mod 11 = 3
h('o'): h = (3 * 31 + 111) mod 11 = 204 mod 11 = 6

Final: h("hello") = 6
```

---

## 5️⃣ Critical Analysis — Performance & Robustness

### Complexity Analysis

| Operation | Average Case | Worst Case |
|-----------|-------------|-----------|
| **Lookup** | O(1) | O(n) |
| **Insert** | O(1) | O(n) |
| **Delete** | O(1) | O(n) |
| **Resize** | O(n) amortized | O(n) |

**Why average case?**
- Good hash function + reasonable load factor → O(1) expected
- Bad hash function or poor luck → O(n) worst case

**Why worst case?**
- All n keys hash to same slot (pathological hash function)
- Every lookup scans all n items
- Probability decreases exponentially with good hash functions

### Birthday Paradox: Collision Intuition

**Question:** In a hash table with m slots, how many items until a collision?

**Answer:** Surprisingly few! √m expected collisions.

**Birthday Paradox Example:**
```
Hash table size m = 365 (like birthdays in a year)
Probability of collision with 23 people ≈ 50%

Hash table size m = 1,000,000
Expected first collision at √1,000,000 = 1,000 items
Not 1,000,000 items!
```

**Math:**
```
Probability of no collision with k items:
P(no collision) = (m/m) × ((m-1)/m) × ((m-2)/m) × ... × ((m-k+1)/m)
                ≈ e^(-k²/(2m))

First collision expected when: k ≈ √(πm/2) ≈ √m
```

**Implications:**
```
m = 10^6 slots
Expect collision at √10^6 ≈ 1,000 items
Not 10^6 items!

So: table size should be at least 2-4× expected item count
With α = 0.25-0.5, stay well below collision threshold
```

### When Hash Tables Fail

**Bad Hash Function:**
```
h(k) = 0  for all k  (always returns 0)

Result: All items go to slot 0
        O(n) lookup time (must scan all items)
```

**Poor Load Factor Management:**
```
Start with m = 11, insert 100 items, never resize
Result: α = 9.09 (9 items per slot on average!)
        O(n) operations (huge chains or open addressing probe length)
```

**Hash Function Vulnerabilities:**
```
Adversary knows your hash function and table size
Sends carefully crafted keys to cause collisions

Example: h(k) = k mod m
Adversary sends: m, 2m, 3m, 4m, ...
All hash to slot 0!
```

---

## 6️⃣ Real System Integration

### Operating System: Virtual Memory

**Memory addressing: Virtual → Physical**

```
Virtual address: 0x7FFF0000  (32-bit)
Need to find: corresponding physical address

Page table is a hash table!

h(virtual_page) = physical_frame

Every memory access triggers this lookup!
Must be O(1) — cannot afford O(log n) or O(n)

If page table were O(log n):
1 memory access becomes 1 + log n = 1 + 20 = 21 accesses
21× slowdown! (logarithm is terrible here)
```

**Why must hash tables be used:**
- Every CPU instruction does memory accesses
- Need immediate translation from virtual to physical
- O(1) hash table lookup is the only acceptable solution

### Compiler: Symbol Table

**C code:**
```c
int x = 5;
float y = 3.14;
printf("%d", x);  // Lookup: what is x?
```

**Symbol table (hash table):**
```
Lookup "x":
  h("x") = hash of "x" mod table_size
  Find: type=int, offset=100, scope=global
  Return type information ✓
  O(1) lookup!
```

**Why efficient:**
- Compiler needs to look up thousands of variables
- Each lookup must be instant (part of compilation time)
- Hash table is perfect for this

### Database Indexing

**SQL:**
```sql
SELECT * FROM users WHERE user_id = 42;
```

**Without index:** Scan all 1 million users → O(n)  
**With hash index:** h(42) → O(1) lookup

**Trade-off:**
```
Space: Keep extra hash table structure (+10-20% disk space)
Time: Instant lookup instead of full scan

Worth it!
```

---

## 7️⃣ Concept Crossovers

### Builds On

**Previous concepts:**
- Basic algorithms (insertion)
- Arrays (underlying storage)
- Complexity analysis

### Builds Toward

**Future applications:**
- **Week 4:** Sliding window uses hash tables for frequency counting
- **Week 5:** BST vs Hash Table trade-offs
- **Week 11:** Dynamic programming uses hash tables for memoization
- **Hashing as cryptography:** Digital signatures, blockchain

### Concept Connections

**Hash Tables vs Arrays:**
```
Arrays:          Direct access by index, sequential storage
Hash Tables:     Direct access by key (computed index)
Trade-off:       Arrays are simpler but require keys to be integers 0...m-1
                 Hash tables work with any key type
```

**Hash Tables vs Sorted Data:**
```
Sorted array:    O(log n) lookup with binary search, can range query
Hash table:      O(1) lookup, can't range query
Choice:          When you need speed and only exact lookup, hash table wins
```

---

## 8️⃣ Mathematical & Theoretical Perspective

### Formal Definition: Hash Function

**Definition:**
A hash function h: U → {0, 1, ..., m-1} maps a universe U of keys to m slots.

**Properties:**
1. **Efficiency:** h(k) is computable in O(1) time
2. **Determinism:** h(k) always returns same value
3. **Uniformity:** For random keys, h(k) uniform distribution

**Mathematical Analysis:**
```
Universe U: All possible keys (may be very large or infinite)
Table size m: Fixed size (typically 11, 23, 47, ...)
Expected chain length: α = n/m

With good hash function:
E[chain length] = α (provably optimal)
E[lookup time] = O(1 + α)
```

### Proof: Birthday Paradox

**Claim:** With m slots and k = √(πm/2) items, collision probability ≈ 50%.

**Proof Sketch:**

Probability of NO collision:
```
P(no collision) = (m/m) × ((m-1)/m) × ((m-2)/m) × ... × ((m-k+1)/m)
                ≈ ∏[i=0 to k-1] (1 - i/m)
                ≈ e^(-∑ i/m)
                = e^(-k(k-1)/(2m))
                ≈ e^(-k²/(2m))
```

When k² ≈ 2m:
```
e^(-k²/(2m)) ≈ e^(-1) ≈ 0.37

So P(collision) ≈ 1 - 0.37 = 0.63 (63% with k = √(2m))
```

---

## 9️⃣ Algorithmic Design Intuition

### When to Use Hash Tables

**Use Hash Tables when:**
1. **Fast lookup needed** (O(1) is critical)
2. **Any key type** (integers, strings, objects)
3. **Exact match queries** only (not range queries)
4. **Memory abundant** (space for overhead okay)

**Examples:**
```
Dictionary: "Find definition of word" → Hash table O(1)
Cache: "Is value in cache?" → Hash table O(1)
De-duplication: "Have we seen this item?" → Hash table O(1)
```

### When NOT to Use Hash Tables

**Avoid when:**
1. ❌ **Range queries needed** ("All users aged 18-25?")
2. ❌ **Memory is scarce** (hash tables use extra space)
3. ❌ **Worst-case guarantees needed** (O(n) worst case unacceptable)
4. ❌ **Data is mostly pre-sorted** (sorted structure better)

### Decision Framework

```
Do you need any-key lookup?
  → YES: Use hash table (O(1))
  → NO: Use sorted array (O(log n)) or BST (O(log n))

Is exact-match enough?
  → YES: Hash table is perfect
  → NO: Need sorted structure for range queries

Is space abundant?
  → YES: Hash table (accepts space overhead)
  → NO: Sorted array is space-efficient
```

---

## 🔟 Knowledge Check — Socratic Reasoning

**Question 1: Why is direct addressing (using key as index) not always possible?**

Your reasoning:
- If keys are 0 to m-1, just use array[key]
- But what if keys are large (social security numbers, UUIDs)?
- What if keys are strings (names)?
- Why can't we create an array of size 10^10?
- How does hashing solve this problem?

**Hint:** Space complexity. Creating array[10^10] uses too much memory.

---

**Question 2: The birthday paradox says collision at √m items. Why isn't this a problem?**

Your reasoning:
- With m = 10^6 slots, expect collision at √10^6 = 1000 items
- Seems like you can only safely store 1000 items
- But databases store millions in hash tables!
- How do they handle collisions?
- What's the strategy to keep collisions manageable?

**Hint:** They resize the table! Maintain α = n/m < 0.75.

---

**Question 3: Why must virtual memory address translation be O(1), not O(log n)?**

Your reasoning:
- O(log n) seems acceptable (binary search is fast)
- But every CPU instruction does memory access
- How much slower does program run if each access becomes 20 accesses?
- Why can't we afford O(log n) here?
- What does this say about real-system constraints?

**Hint:** Constant factor matters when it's multiplied by billions of accesses.

---

**Question 4: Prove that a hash table with good hash function has O(1) expected lookup.**

Your reasoning:
- With load factor α = n/m
- Expected chain length with chaining = α
- Each element added: expected cost O(1)
- Why is this true on average?
- What happens in worst case?

**Hint:** Chaining strategy (Day 5) determines this.

---

**Question 5: Given limited memory, would you use many small hash tables or one large hash table?**

Your reasoning:
- Small tables: Low collision probability, but many tables
- Large table: High memory, but fewer collisions
- Trade-off between space and collision handling complexity
- What's the practical choice?

**Hint:** Think about the birthday paradox threshold.

---

## 1️⃣1️⃣ Retention Hook — Memory Anchors

### One-Line Essence

> **Hash tables achieve O(1) average lookup by computing index from key. Load factor α = n/m controls collision probability. Resize when α exceeds threshold. Not a sorting data structure; a lookup data structure.**

### Mnemonic: "HASH"

- **H**ash: Function that maps keys to indices
- **A**verage: O(1) expected time
- **S**pace: Trade memory for speed
- **H**andling: Collisions are unavoidable

### Visual Cue

```
HASH TABLE:
Input (key) → Hash function → Index → Value

VIRTUAL MEMORY:
Virtual address → Page table (hash table) → Physical address

BIRTHDAY PARADOX:
m slots
√m items → collision likely
Keep α = n/m < 0.75 → avoid many collisions
```

---

## 📚 Supplementary Data

### Hash Function Quality Check

```
Test hash function on sample keys:

h("apple") = ?
h("banana") = ?
h("cherry") = ?
h("apple2") = ? (small change in input)

Good hash: All spread out, small input change gives large output change
Bad hash: Clusters, similar keys hash near each other
```

### Load Factor in Practice

```
Language      | Default | Resizing trigger
Python dict   | 0.67    | When α > 0.67
Java HashMap  | 0.75    | When α > 0.75
C++ unordered_map | ~1.0 | Varies

All avoid high load factors to minimize collisions
```

---

## 🔗 External References

1. **Visualization:**
   - Hash Table Visualizer: https://www.cs.usfca.edu/~galles/visualization/HashTable.html

2. **Real Implementations:**
   - Python dict: https://docs.python.org/3/library/stdtypes.html#dict
   - Java HashMap: https://docs.oracle.com/javase/8/docs/api/java/util/HashMap.html
   - C++ unordered_map: https://en.cppreference.com/w/cpp/container/unordered_map

3. **Hash Functions:**
   - FNV Hash: http://www.isthe.com/chongo/tech/comp/fnv/
   - MurmurHash: https://en.wikipedia.org/wiki/MurmurHash

---

**Word Count:** ~2,400  
**Reading Time:** ~60 minutes  
**Status:** ✅ Complete with all 11 sections + supplementary material
