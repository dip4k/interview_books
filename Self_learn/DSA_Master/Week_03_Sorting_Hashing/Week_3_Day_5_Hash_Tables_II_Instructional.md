# Week 3, Day 5: Hash Tables II

## 🗓 Metadata
**Week:** 3 | **Day:** 5 of 5 | **Topic:** Hash Tables II  
**Difficulty:** 🔴 Hard | **Time:** 90-120 minutes

---

## 1️⃣ THE WHY — Engineering Motivation

**Real-World Problem:**
Hash table chains can get long (collisions). Two approaches: chaining vs open addressing. Which is better?

**Design Problems Solved:**
- Collision resolution strategies
- Load factor and rehashing
- Practical hash table implementations
- Trade-offs between chaining and probing

---

## 2️⃣ THE WHAT — Mental Model & Intuition

### Chaining
**Analogy:** Each bucket is a linked list. Collisions go on the chain.

```
Bucket 0: [("Alice", 25)] → [("Bob", 28)] → [("Kim", 30)]
Bucket 1: [("Charlie", 35)]
Bucket 2: []
```

### Open Addressing
**Analogy:** Find empty slot nearby if bucket occupied. Probe: linear, quadratic, double-hash.

```
Index: 0     1     2     3     4     5
Data:  Alice -     Bob   -     -     Kim

If slot occupied, probe next slot (linear: i+1, quadratic: i+1², i+4², i+9², etc.)
```

---

## 3️⃣ THE HOW — Mechanical Walkthrough

**Chaining Insert:**
```
insert(key, value):
  index = hash(key) % capacity
  append (key, value) to linked list at buckets[index]
```

**Open Addressing Insert (linear probing):**
```
insert(key, value):
  index = hash(key) % capacity
  i = 0
  while buckets[(index + i) % capacity] is occupied:
    i++
  buckets[(index + i) % capacity] = (key, value)
```

**Rehashing:**
```
if load_factor > threshold (e.g., 0.75):
  new_capacity = 2 × old_capacity
  rehash all entries to new table
```

---

## 4️⃣ VISUALIZATION — Simulation & Examples

**Chaining with insertions:**
```
Insert ("Alice", 25) → Bucket 0
Insert ("Bob", 28) → Bucket 0 (collision!)
  Bucket 0: Alice → Bob

Insert ("Charlie", 35) → Bucket 3
  Bucket 3: Charlie
```

**Linear Probing with insertions:**
```
Array size 5.

Insert ("Alice", 25) → hash=0 → index 0
  [Alice, -, -, -, -]

Insert ("Bob", 28) → hash=0 → index 0 occupied → try 1
  [Alice, Bob, -, -, -]

Insert ("Charlie", 35) → hash=0 → indices 0,1 occupied → try 2
  [Alice, Bob, Charlie, -, -]
```

---

## 5️⃣ CRITICAL ANALYSIS — Performance & Robustness

**Chaining:**
- Advantages: Simple, works well with rehashing, deletions easy
- Disadvantages: Extra memory for pointers, cache-unfriendly

**Open Addressing:**
- Advantages: Better cache, no extra pointers
- Disadvantages: Deletions tricky (need tombstones), clustering

**Rehashing:** O(n) operation, done occasionally (amortized O(1))

---

## 6️⃣ REAL SYSTEM INTEGRATION

**Python dict:** Open addressing with quadratic probing  
**Java HashMap:** Chaining with linked lists  
**C++ unordered_map:** Implementation-dependent (chaining or probing)  

---

## 7️⃣ CONCEPT CROSSOVERS

**Builds on:** Hash Tables I, collision theory  
**Used in:** Caches, databases, symbol tables  

---

## 8️⃣ MATHEMATICAL & THEORETICAL PERSPECTIVE

**Birthday Paradox:** With m buckets and n keys, expect collisions when n ≈ √m  
**Load Factor:** α = n/m. For chaining, avg chain length = α.  
**Clustering (open addressing):** Primary clustering reduces effective capacity

---

## 9️⃣ ALGORITHMIC DESIGN INTUITION

**When to use chaining:** Frequent deletions, extra space acceptable  
**When to use open addressing:** Cache matters, deletions rare  

---

## 🔟 KNOWLEDGE CHECK — Socratic Reasoning

**Q1:** Why is rehashing necessary and what's its cost?

**Q2:** Open addressing has primary clustering. What's that and why does it hurt?

**Q3:** Can you delete from open addressing without breaking searches?

**Q4:** Load factor 0.75 vs 0.5 vs 0.9 — which is better and why?

---

## 1️⃣1️⃣ RETENTION HOOK

**One-Liner:**
> **Hash Tables II: Chaining (simple, pointers) vs Open Addressing (cache-friendly, clustering). Rehashing keeps O(1) amortized.**

---

**Supplementary:** Practice implementing both strategies

