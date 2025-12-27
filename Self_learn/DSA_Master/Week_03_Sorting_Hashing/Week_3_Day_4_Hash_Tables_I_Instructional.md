# Week 3, Day 4: Hash Tables I

## 🗓 Metadata
**Week:** 3 | **Day:** 4 of 5 | **Topic:** Hash Tables I  
**Difficulty:** 🔴 Hard | **Time:** 90-120 minutes

---

## 1️⃣ THE WHY — Engineering Motivation

**Real-World Problem:**
Array lookup is O(1) by index. But what if we need to find by key (name, email, ID)? Sorting then binary search is O(n log n). Hash tables give O(1) average.

**Design Problems Solved:**
- O(1) average search/insert/delete
- Key-value mapping
- Foundation for caches, databases, symbol tables
- Anagrams, duplicates, frequency counting problems

**Real System Usage:**
- **Databases:** Indexing via hash tables
- **Compilers:** Symbol tables (variable lookup)
- **Caches:** Redis, memcached
- **Python:** dict type, set type

---

## 2️⃣ THE WHAT — Mental Model & Intuition

**Core Analogy:**
Hash function is a shortcut. Instead of searching, compute which bucket the key belongs to directly.

```
Key → Hash Function → Bucket Index
Name "Alice" → hash("Alice") % 10 = 3
Look in bucket 3 → find Alice directly
```

**Three Components:**
1. **Hash Function:** Convert key to index (0 to capacity-1)
2. **Bucket/Slot:** Storage location for values
3. **Collision Resolution:** What if two keys hash to same bucket?

---

## 3️⃣ THE HOW — Mechanical Walkthrough

**Hash Function Basics:**
```
Simple hash for strings:
  hash(s) = (s[0] + s[1] + ... + s[n-1]) % capacity
  
Hash for integers:
  hash(x) = x % capacity
  
Goal: Distribute keys uniformly across buckets
```

**Insert:**
```
insert(key, value):
  index = hash(key) % capacity
  buckets[index] = (key, value)  // with collision resolution
```

**Search:**
```
search(key):
  index = hash(key) % capacity
  look in buckets[index] for key
```

---

## 4️⃣ VISUALIZATION — Simulation & Examples

**Hash Table with chaining (n=10):**
```
Bucket 0: [("Alice", 25)] → [("Kim", 30)]
Bucket 1: []
Bucket 2: [("Bob", 28)]
Bucket 3: [("Charlie", 35)]
...

Search "Alice":
  hash("Alice") % 10 = 0
  Check bucket 0 → find Alice → O(1) average
```

---

## 5️⃣ CRITICAL ANALYSIS — Performance & Robustness

| Operation | Average | Worst |
|-----------|---------|-------|
| **Search** | O(1) | O(n) |
| **Insert** | O(1) | O(n) |
| **Delete** | O(1) | O(n) |

**Average case:** Good hash function, low load factor  
**Worst case:** All keys hash to same bucket (O(n) chain)  
**Load Factor:** α = n/m (n keys, m buckets). Keep α < 0.75

---

## 6️⃣ REAL SYSTEM INTEGRATION

**C++ unordered_map, Java HashMap, Python dict:** All use hash tables  
**Database indexing:** B-tree for range, hash for equality  
**Distributed systems:** Consistent hashing for load balancing  

---

## 7️⃣ CONCEPT CROSSOVERS

**Builds on:** Arrays (buckets), hashing  
**Built by:** Bloom filters, cuckoo hashing  

---

## 8️⃣ MATHEMATICAL & THEORETICAL PERSPECTIVE

**Universal Hashing:**
For a good hash function, collision probability ≈ 1/m for any two keys.

With chaining: expected chain length = α = n/m (load factor)
Search cost: O(1 + α)

---

## 9️⃣ ALGORITHMIC DESIGN INTUITION

**When to use:** Need O(1) average key lookup, order doesn't matter  
**When NOT to use:** Need sorted order (use tree), or small n (array/linear search sufficient)

---

## 🔟 KNOWLEDGE CHECK — Socratic Reasoning

**Q1:** Why can hash table degrade to O(n) worst-case if hash function creates collisions?

**Q2:** Why is load factor α = n/m important?

**Q3:** Can you use a hash table for a problem requiring sorted output?

**Q4:** What makes a good hash function?

---

## 1️⃣1️⃣ RETENTION HOOK

**One-Liner:**
> **Hash Tables: O(1) average via key → index mapping. Collisions degrade to O(n) worst-case.**

