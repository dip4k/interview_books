# Week 3, Day 4: Hash Tables I — Fundamentals

## 🗓 Metadata
**Week:** 3 | **Day:** 4 of 5 | **Topic:** Hash Tables, Hash Functions, Collision Theory  
**Category:** Hash Data Structures | **Difficulty:** 🟡 Medium  
**Prerequisites:** Week 1-2 (Arrays, Big-O), Basic modulo arithmetic  
**Time:** 120-150 minutes | **Status:** 🔍 In Study

---

## 1️⃣ THE WHY — Engineering Motivation

### Real-World Problem
Fast lookups: find user by email (O(1) vs O(n)), check if username exists instantly, cache data with keys. Arrays need full scan. Hash tables promise O(1) average lookup. Essential for databases, compilers, caches, file systems.

### Design Problems Solved
- **Constant-time lookup** (dictionary/map operations)
- **Duplicate detection** (has this user been seen?)
- **Caching** (store computed results by key)
- **Deduplication** (remove duplicates efficiently)
- **Frequency counting** (count word occurrences)
- **Anagrams/grouping** (group similar items)
- **Symbol tables** (compiler variable lookup)

### Real System Usage
- **Database indexes:** Hash indexes for equality queries
- **CPU caches:** Mapping memory addresses to cache lines
- **File systems:** Inode lookup by number
- **Web servers:** Session storage by session ID
- **Compilers:** Symbol table (variable/function names)
- **Networking:** IP route lookups
- **Spell checking:** Dictionary of valid words

### Why Hash Tables Matter
**O(1) average lookup breaks linear search barrier.** Understanding hash functions and collision handling separates competent from expert engineers. Crucial for optimization.

---

## 2️⃣ THE WHAT — Mental Model & Intuition

### Core Analogy
**Hash table:** Library with books. Hash function = convert book name to shelf number. Collision = multiple books for same shelf (use chaining or open addressing). Load factor = how full (n/m).

### Key Invariants
1. **Hash Function Invariant:** Same key always maps to same bucket
2. **Collision Invariant:** Different keys may map to same bucket (must handle)
3. **Load Factor Invariant:** n/m ≤ 0.75 keeps performance good (rehash if exceeded)
4. **Probe Invariant:** Open addressing probes available slots following pattern

### Visual Representation

```
HASH TABLE (Chaining):
Hash function: h(key) = key % 5

Buckets:
[0] → NULL
[1] → 6 → 11 → NULL  (6 and 11 collided, chained)
[2] → 7 → NULL
[3] → 3 → 13 → NULL
[4] → 4 → 9 → NULL

Load factor = 7 items / 5 buckets = 1.4

OPEN ADDRESSING (Linear Probing):
Hash function: h(key, i) = (h(key) + i) % 5

Insert 3, 8, 13, 6, 11:
h(3) = 3 % 5 = 3 → [3, _, _, 3, _]
h(8) = 8 % 5 = 3 → collision, try 4 → [3, _, _, 3, 8]
h(13) = 13 % 5 = 3 → collision, try 4 → occupied, try 0 → [13, _, _, 3, 8]
h(6) = 6 % 5 = 1 → [13, 6, _, 3, 8]
h(11) = 11 % 5 = 1 → collision, try 2 → [13, 6, 11, 3, 8]

Load factor = 5/5 = 1.0 (full!)
```

---

## 3️⃣ THE HOW — Mechanical Walkthrough

### Hash Table with Chaining

```
INSERT(key, value):
  hash_value = HASH_FUNCTION(key)
  bucket_index = hash_value % table_size
  
  // Append to chain (or update if exists)
  node = CREATE_NODE(key, value)
  INSERT_AT_HEAD(table[bucket_index], node)

LOOKUP(key):
  hash_value = HASH_FUNCTION(key)
  bucket_index = hash_value % table_size
  
  current = table[bucket_index]
  While current != NULL:
    if current.key == key:
      return current.value
    current = current.next
  
  return NOT_FOUND

DELETE(key):
  hash_value = HASH_FUNCTION(key)
  bucket_index = hash_value % table_size
  
  DELETE_FROM_CHAIN(table[bucket_index], key)

Time: O(1) average lookup, O(n) worst (all in one bucket)
Space: O(m + n) where m = table size, n = items
```

### Hash Function Design

```
SIMPLE_HASH(string_key):
  hash_value = 0
  For each character c in string_key:
    hash_value = (hash_value * 31 + ASCII(c)) % LARGE_PRIME
  return hash_value

Properties:
- Deterministic (same input, same output)
- Uniform distribution (minimize collisions)
- Fast to compute (O(key_length))
- Avalanche effect (small change in key → big change in hash)
```

---

## 4️⃣ VISUALIZATION — Simulation & Examples

### Example 1: Hash Table Building

```
Insert keys: "apple" (5), "banana" (6), "cherry" (6), "date" (4)

Hash function: sum of ASCII values % 5

"apple": 97+112+112+108+101 = 530 % 5 = 0
"banana": 98+97+110+97+110+97 = 609 % 5 = 4
"cherry": 99+104+101+114+114+121 = 653 % 5 = 3
"date": 100+97+116+101 = 414 % 5 = 4

Table:
[0] → apple
[1] → NULL
[2] → NULL
[3] → cherry
[4] → banana → date (chained)

Load factor = 4/5 = 0.8 (good)
```

---

## 5️⃣ CRITICAL ANALYSIS — Performance & Robustness

| Operation | Average | Worst | Notes |
|-----------|---------|-------|-------|
| **Lookup** | O(1) | O(n) | All keys in one bucket |
| **Insert** | O(1) | O(n) | Table full, collision chain long |
| **Delete** | O(1) | O(n) | Same as lookup |

### Load Factor Impact
- **α = n/m = 0.5:** Good performance, ~50% full
- **α = 0.75:** Threshold for rehashing
- **α = 1.0:** Average chain length = 1 (chaining), full (open addressing)
- **α > 1.0:** Chaining allows > 1, open addressing doesn't

### Collision Probability
By birthday paradox: with k items and m buckets, collision probability high when k ≈ √m. Even good hash functions have collisions; handling is critical.

---

## 6️⃣ REAL SYSTEM INTEGRATION

1. **Python dictionaries:** Hash tables with open addressing
2. **Java HashMap:** Chaining with bucket resizing
3. **Linux file cache:** Hash on inode number
4. **CPU cache:** Hash on memory address
5. **Bloom filters:** Probabilistic hash-based
6. **Consistent hashing:** Distributed systems
7. **Password hashing:** Cryptographic hash functions

---

## 7️⃣ CONCEPT CROSSOVERS

**Builds On:** Arrays, linked lists, modulo arithmetic  
**Built Upon By:** Hash maps, sets, caching, distributed hashing

---

## 8️⃣ MATHEMATICAL PERSPECTIVE

### Hash Function Properties
- **Universal hashing:** Probability of collision ≤ 1/m for any two keys
- **Perfect hashing:** Zero collisions (if key set known upfront)
- **Avalanche effect:** Each bit of output depends on every bit of input

---

## 9️⃣ ALGORITHMIC DESIGN INTUITION

✅ **Use hash tables when:**
- Average O(1) lookup needed
- Unknown data size (dynamic)
- Order doesn't matter

❌ **Avoid when:**
- Worst-case O(1) required (use balanced BST)
- Range queries needed (use sorted array/BST)
- Order matters

---

## 🔟 KNOWLEDGE CHECK

**Q1: Why do hash tables hash to index, not use key directly?**
**Q2: How do collisions affect performance?**
**Q3: Why rehash when load factor exceeds 0.75?**

---

## 1️⃣1️⃣ RETENTION HOOK

**One-Liner:**
> **Hash tables map keys to array indices via hash function, achieving O(1) average lookup by trading collisions for speed.**

**Mnemonic:** **"Hash = Divide & Index"** (divide by table size, use remainder as index)

### 5 Cognitive Lenses

| **Computational** | Hash function O(key_length), table O(m) space, lookup O(1) average with good distribution. |
| **Psychological** | Collision handling unintuitive; must understand chains/probing. Load factor concept not obvious. |
| **Design Trade-off** | Space vs time: more buckets (more space) → fewer collisions → faster lookups. |
| **AI/ML Analogy** | Feature hashing for dimensionality reduction. Hash collision like embedding collision. |
| **Historical Context** | Hash tables 1950s. Widely used in modern systems. Collisions handled by Knuth (chaining) and Brent (open addressing). |

---

**Status:** ✅ Sections 1-11 Complete  
**Next:** Day 5 (Hash Tables II - Chaining vs Open Addressing)

