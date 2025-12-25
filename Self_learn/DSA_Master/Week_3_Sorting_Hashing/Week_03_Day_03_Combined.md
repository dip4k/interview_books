# 📘 WEEK 3 DAY 3: HASHING FUNDAMENTALS - Complete Learning Package

**Week 3, Day 3: Hash Tables and Hash Functions**

Generated: 2025-12-26 | Duration: 90 minutes | Difficulty: 🟡 Medium | Target: 4-5/5

---

## PART 1: MAIN CONTENT

### 1️⃣ The Why

**Problem:** Looking up data in array is O(n). Can we get O(1)?

**Insight:** Use value itself to compute storage location.

Real-world:
- **Caching:** O(1) lookup of cached values
- **Databases:** Hash indexes for fast queries
- **Compilers:** Symbol tables use hashing
- **Spell checkers:** Hashing dictionary words

**Performance:**
```
Array lookup: O(n)
Binary search: O(log n)
Hash table: O(1) average!
```

---

### 2️⃣ The What: Mental Model

**Hash Table Concept:**
```
Data: {"alice": 25, "bob": 30, "charlie": 22}

Array-based storage:
Index: 0    1    2
Data:  alice bob charlie

Lookup "bob" = scan all (O(n))

Hash table approach:
hash("alice") = 0
hash("bob") = 1
hash("charlie") = 2

Index: 0      1      2
Data:  alice  bob    charlie

Lookup "bob" = hash("bob")=1, check index 1 (O(1))
```

**Hash Function:**
- Takes key (any type)
- Produces array index
- Ideally, uniform distribution

```python
def simple_hash(key, size):
    return hash(key) % size

# "alice" → 12345 → 12345 % 10 = 5
# "bob" → 67890 → 67890 % 10 = 0
```

---

### 3️⃣ The How: Mechanics

**Hash Table Implementation:**
```python
class HashTable:
    def __init__(self, size=10):
        self.size = size
        self.table = [None] * size
    
    def hash(self, key):
        return hash(key) % self.size
    
    def insert(self, key, value):
        index = self.hash(key)
        self.table[index] = (key, value)
    
    def lookup(self, key):
        index = self.hash(key)
        if self.table[index]:
            return self.table[index][1]
        return None
```

**Collision Handling:**

```python
# Chaining: Store list at each index
class ChainedHashTable:
    def __init__(self, size=10):
        self.size = size
        self.table = [[] for _ in range(size)]
    
    def insert(self, key, value):
        index = self.hash(key)
        for i, (k, v) in enumerate(self.table[index]):
            if k == key:
                self.table[index][i] = (key, value)
                return
        self.table[index].append((key, value))
    
    def lookup(self, key):
        index = self.hash(key)
        for k, v in self.table[index]:
            if k == key:
                return v
        return None
```

---

### 4️⃣ Visualization

**Hash Table with Chaining:**
```
Keys: "alice", "bob", "charlie", "alice2"
Size: 3

hash("alice") = 0
hash("bob") = 1
hash("charlie") = 2
hash("alice2") = 0 (collision!)

Index 0: [("alice", 25), ("alice2", 26)]
Index 1: [("bob", 30)]
Index 2: [("charlie", 22)]

Lookup "alice":
  1. hash("alice") = 0
  2. Check index 0: list has 2 items
  3. Scan: ("alice", 25) - match!
  4. Return 25
```

**Hash Function Quality:**
```
Good hash function (uniform):
["alice"] → index 0
["bob"] → index 1
["charlie"] → index 2
(all distributed)

Bad hash function (many collisions):
["alice"] → index 0
["alice2"] → index 0
["alice3"] → index 0
(all hash to same bucket)
```

---

### 5️⃣ Critical Analysis

**Complexity:**

| Operation | Best | Average | Worst |
|-----------|------|---------|-------|
| Insert | O(1) | O(1) | O(n) |
| Lookup | O(1) | O(1) | O(n) |
| Delete | O(1) | O(1) | O(n) |

**Best case:** Good hash function, no collisions
**Average:** Good function, some collisions (few items per bucket)
**Worst:** All keys hash to same bucket (terrible function)

**Load Factor:**
```
λ = n / m (n items, m buckets)

λ < 1: Usually few collisions
λ ≈ 1: Some collisions
λ > 2: Many collisions, consider rehashing

Rehashing: When λ too high, create larger table, re-insert all
```

---

### 6️⃣ Real Systems

**Hash Tables Everywhere:**
- Python dict, Java HashMap, C++ unordered_map
- Database B-tree leaves sometimes use hashing
- Cache: CPU caches use hashing addresses
- Bloom filters: Probabilistic set membership

**Hash Function Design:**
- Simple: mod prime
- Good: FNV, MurmurHash
- Cryptographic: SHA, MD5 (for security)

---

### 7️⃣ Connections

Builds on: Arrays (Week 2), Big-O analysis (Week 1)

Enables: Caches, indexes, deduplication

---

### 8️⃣ Mathematics

**Birthday Paradox Applied:**
```
With m buckets and n items where λ = n/m:
Probability of no collision ≈ e^(-λ²/2)

λ = 0.5: 78% no collision
λ = 1.0: 61% no collision
λ = 2.0: 18% no collision

Keep λ < 1 for few collisions!
```

---

### 9️⃣ Design Intuition

**Use Hash Table For:**
- Fast lookups (O(1))
- Caching
- Deduplication
- Counting occurrences

**Avoid When:**
- Need sorted order
- Need range queries
- Memory very limited

---

### 🔟 Knowledge Check

1. Why is hash table lookup O(1)?
2. What happens with hash collisions?
3. Why does bad hash function break O(1)?
4. Explain chaining collision handling
5. When would you use open addressing instead?
6. What's load factor and why does it matter?
7. How does rehashing work?

### 1️⃣1️⃣ Hooks

**One-liner:** "Hash tables use hash function to map keys to indexes for O(1) lookup."

---

## PART 2: QUICK SUMMARY

**Hash Table:**
- Array of buckets
- Hash function maps key to index
- Chaining handles collisions

**Complexity:**
- Insert: O(1) average
- Lookup: O(1) average
- Worst case O(n) if all collide

**Key Insight:**
- Load factor matters
- Good hash function critical
- Rehashing when needed

---

## PART 3: QUESTIONS & ANSWERS

**Q1:** Why can hash table be O(n) worst case?
**A:** If hash function terrible (all hash to same bucket), becomes linked list.

**Q2:** Python dict implementation?
**A:** Open addressing with quadratic probing. Resizes when λ > 2/3.

**Q3:** Hash function for integers?
**A:** Simple: n % size. Good: Multiply-by-constant mod size.

**Q4:** Chaining vs open addressing?
**A:** Chaining: separate chains per bucket. Open: probe for next free slot.

**Q5:** Why rehash when λ > threshold?
**A:** Collisions increase, queries slow down. Rehashing redistributes keys.

**Q6:** Cryptographic vs regular hash?
**A:** Cryptographic: collision-resistant, slow. Regular: fast, may have collisions.

**Q7:** Size should be prime?
**A:** Yes! Prime size with modulo hash minimizes collisions (number theory).

---

## PART 4: README

**90-Minute Study:**
1. Why (15 min): Need for O(1) lookup
2. What (15 min): How hashing works
3. How (15 min): Chaining implementation
4. Visualization (15 min): See collisions, resolution
5. Analysis (10 min): Complexity, load factor

**Key Skill:** Understand hash collisions and solutions

---

**Status:** ✅ Day 3 Complete | **Next:** Day 4 - Hash Applications

