# Week 3, Day 5: Hash Tables II — Implementation Variants

## 🗓 Metadata
**Week:** 3 | **Day:** 5 of 5 | **Topic:** Hash Tables — Chaining vs Open Addressing, Real Implementations  
**Category:** Hash Data Structures | **Difficulty:** 🟡 Medium  
**Prerequisites:** Week 3 Day 4 (Hash Tables I fundamentals)  
**Time:** 150-180 minutes | **Status:** 🔍 In Study

---

## 1️⃣ THE WHY — Engineering Motivation

### Real-World Problem
Different collision handling strategies for different use cases. Chaining simple but uses extra memory (linked lists). Open addressing saves space but more complex. Must understand trade-offs. Python uses open addressing, Java uses chaining with bucket arrays.

### Design Problems Solved
- **Memory-efficient hashing** (open addressing)
- **Simple collision handling** (chaining)
- **Cache-friendly storage** (open addressing better for modern CPUs)
- **Deletion support** (chaining easier)
- **Rehashing strategies** (resize and rehash entire table)
- **Double hashing** (reduce clustering in open addressing)
- **Quadratic probing** (different collision pattern)

### Real System Usage
- **Python dict:** Open addressing with quadratic probing
- **Java HashMap:** Chaining with bucket arrays
- **C++ unordered_map:** Chaining (implementation dependent)
- **Bloom filters:** Open addressing variants
- **Consistent hashing:** Distributed systems
- **Cuckoo hashing:** Guarantees O(1) with limited probing

### Why Chaining vs Open Addressing Matters
**Different design choices yield different performance profiles.** Chaining memory-inefficient but simple. Open addressing faster for modern CPUs with good cache, but complex. Must know both to evaluate systems.

---

## 2️⃣ THE WHAT — Mental Model & Intuition

### Core Analogies

**Chaining:** Multiple books on same shelf, linked together. Adding book: append to chain. Finding book: follow chain until found.

**Open Addressing:** Assigned seating. If seat taken, find next available (probing pattern). Adding person: sit in first free seat following pattern. Finding person: check pattern until found.

### Key Differences

| Aspect | Chaining | Open Addressing |
|--------|----------|-----------------|
| **Collision** | Create chain/list | Probe for empty slot |
| **Space** | O(m + n) (extra lists) | O(m) (array only) |
| **Load Factor** | Can exceed 1 | Limited to < 1 |
| **Cache** | Poor (pointer following) | Good (linear memory) |
| **Deletion** | Easy (remove node) | Hard (mark tombstone) |
| **Clustering** | Minimal | Possible (primary) |

---

## 3️⃣ THE HOW — Mechanical Walkthrough

### Chaining Collision Handling

```
INSERT_CHAINING(key, value):
  bucket = HASH(key) % TABLE_SIZE
  node = CREATE_NODE(key, value)
  INSERT_AT_HEAD(table[bucket], node)  // O(1)

LOOKUP_CHAINING(key):
  bucket = HASH(key) % TABLE_SIZE
  current = table[bucket]
  While current != NULL:
    if current.key == key:
      return current.value
    current = current.next
  return NOT_FOUND

Time: O(1) insert, O(1 + chain_length) lookup
```

### Open Addressing (Linear Probing)

```
INSERT_OPEN(key, value):
  hash_value = HASH(key)
  i = 0
  While true:
    index = (hash_value + i) % TABLE_SIZE
    if table[index] is EMPTY or TOMBSTONE:
      table[index] = (key, value)
      return
    if table[index].key == key:
      table[index].value = value  // Update
      return
    i++  // Probe next position

LOOKUP_OPEN(key):
  hash_value = HASH(key)
  i = 0
  While true:
    index = (hash_value + i) % TABLE_SIZE
    if table[index] is EMPTY:
      return NOT_FOUND
    if table[index].key == key and table[index] not TOMBSTONE:
      return table[index].value
    i++

DELETE_OPEN(key):
  Find key via lookup
  Mark as TOMBSTONE (can't delete, would break lookup chain)
```

### Double Hashing

```
DOUBLE_HASH(key, value):
  hash1 = HASH1(key)
  hash2 = HASH2(key)  // Different function, relatively prime to table size
  i = 0
  While true:
    index = (hash1 + i * hash2) % TABLE_SIZE
    if table[index] is EMPTY:
      table[index] = (key, value)
      return
    i++

Advantage: Reduces primary/secondary clustering
Cost: Second hash computation
```

---

## 4️⃣ VISUALIZATION — Simulation & Examples

### Example: Chaining vs Open Addressing on Same Data

```
Insert: 3, 8, 13, 6, 11 (hash % 5)

CHAINING:
[0] → NULL
[1] → 6 → NULL
[2] → NULL
[3] → 13 → 8 → 3 → NULL  (chains built at index 3)
[4] → 11 → NULL

OPEN ADDRESSING (Linear):
Initial: [_, _, _, _, _]
Insert 3 (3%5=3): [_, _, _, 3, _]
Insert 8 (8%5=3, taken): try (3+1)%5=4: [_, _, _, 3, 8]
Insert 13 (13%5=3, taken): try (3+1)%5=4, taken: try (3+2)%5=0: [13, _, _, 3, 8]
Insert 6 (6%5=1): [13, 6, _, 3, 8]
Insert 11 (11%5=1, taken): try (1+1)%5=2: [13, 6, 11, 3, 8]

Result: [13, 6, 11, 3, 8] (all filled, primary clustering at index 3-4)

Lookup 8:
  8%5=3 (occupied, key=3): continue
  (3+1)%5=4 (occupied, key=8): FOUND
  2 probes needed
```

---

## 5️⃣ CRITICAL ANALYSIS — Performance & Robustness

### Complexity Comparison

| Operation | Chaining (avg) | Chaining (worst) | Open Addr (avg) | Open Addr (worst) |
|-----------|----------------|-----------------|-----------------|-------------------|
| **Lookup** | O(1 + α) | O(n) | O(1/(1-α)) | O(n) |
| **Insert** | O(1 + α) | O(n) | O(1/(1-α)) | O(n) |
| **Delete** | O(1 + α) | O(n) | O(1/(1-α)) with tombstone | O(n) |

Where α = load factor (n/m for chaining, max 1 for open addressing)

### Clustering in Open Addressing
- **Primary clustering:** Long probe sequences from same hash
- **Secondary clustering:** Different keys produce same probe sequence
- **Double hashing reduces both:** Different hash2 creates different probes
- **Quadratic probing:** i² instead of i (reduces primary)

---

## 6️⃣ REAL SYSTEM INTEGRATION

1. **Python 3.6+:** Uses open addressing, quadratic probing, compact dict format
2. **Java HashMap:** Chaining with bucket arrays, red-black trees if chain > 8
3. **C++ unordered_map:** Implementation-dependent (often chaining)
4. **Bloom filters:** Specialized open addressing for membership testing
5. **Consistent hashing:** Distributed systems, minimizes rehashing
6. **Cuckoo hashing:** Guarantees O(1) with limited probes
7. **Perfect hashing:** Zero collisions when key set known

---

## 7️⃣ CONCEPT CROSSOVERS

**Builds On:** Chaining and open addressing both variations of hash tables

**Built Upon By:** Distributed hashing, cuckoo hashing, consistent hashing, bloom filters

---

## 8️⃣ MATHEMATICAL PERSPECTIVE

### Expected Lookup Cost (Chaining)
```
E[lookup] = 1 + α  (where α = n/m = load factor)
Example: α = 0.5 → E[lookup] = 1.5 comparisons
```

### Expected Lookup Cost (Open Addressing)
```
E[lookup] = 1/(1-α)  (only valid for α < 1)
Example: α = 0.5 → E[lookup] ≈ 2 probes
Example: α = 0.9 → E[lookup] ≈ 10 probes
```

---

## 9️⃣ ALGORITHMIC DESIGN INTUITION

### When to Use Chaining
✅ Load factor can exceed 1  
✅ Deletion is frequent  
✅ Simplicity valued over cache  
✅ Unknown dataset size

### When to Use Open Addressing
✅ Cache efficiency critical  
✅ Memory tight  
✅ Load factor < 0.75  
✅ Deletion rare

---

## 🔟 KNOWLEDGE CHECK

**Q1: Why is primary clustering a problem in open addressing?**
**Q2: Why can't load factor exceed 1 in open addressing?**
**Q3: How does double hashing prevent clustering?**

---

## 1️⃣1️⃣ RETENTION HOOK

**One-Liner:**
> **Chaining stores collisions in lists; open addressing probes for empty slots. Trade memory (chaining) for cache efficiency (open).**

**Mnemonic:** **"Chaining = Lists, Probing = Slots"**

### 5 Cognitive Lenses

| **Computational** | Chaining: pointer dereference (cache miss). Open: array access (cache hit). Modern CPUs favor open addressing. |
| **Psychological** | Chaining intuitive, open addressing conceptually harder (primary clustering). |
| **Design Trade-off** | Space vs cache: chaining uses extra space for pointers but simpler code. |
| **AI/ML Analogy** | Chaining like multi-head attention (multiple chains). Open like single-head (one probe path). |
| **Historical Context** | Chaining classical (Knuth 1963), but modern CPUs revived open addressing interest. |

---

**Status:** ✅ Complete  
**Week 3 Mastery:** All 5 sorting + hashing patterns complete

