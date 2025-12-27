# Week 8, Day 1: Tries (Prefix Trees)

## 🗓 Metadata
**Week:** 8 | **Day:** 1 of 5 | **Topic:** Tries (Prefix Trees)  
**Category:** Specialized Data Structures | **Difficulty:** 🟡 Medium  
**Prerequisites:** Week 1-7, trees (Week 5), string basics  
**Time:** 90-120 minutes | **Status:** 🔍 In Study

---

## 1️⃣ THE WHY — Engineering Motivation

**Real-World Problem:**
Fast prefix-based string searching. Find all words matching prefix, autocomplete, spell checking. Trie allows O(m) search where m = string length (independent of dictionary size).

**Design Problems Solved:**
- Autocomplete (search suggestions)
- Spell checking (dictionary lookup)
- IP routing (longest prefix matching)
- Contact list filtering (prefix matching)
- Word search in board
- T9 predictive text
- Domain name matching

**Real System Usage:**
- **Google Search:** Autocomplete suggestions
- **Mobile Phones:** T9 text prediction
- **DNS/IP Routing:** Longest prefix match
- **IDE/Editors:** Code completion
- **Spell Checkers:** Dictionary lookup
- **Contact Lists:** Quick filtering
- **Database Indexes:** String prefix indexes

**Why Tries Matter:**
O(m) search time independent of dictionary size. Space-efficient prefix storage. Elegant for prefix-based problems. Natural for autocomplete and spell-check applications.

---

## 2️⃣ THE WHAT — Mental Model & Intuition

**Core Analogy:**
Think Trie like **directory structure** (folders as characters). Root is empty. Each node represents character. Path from root to node is prefix. Leaf nodes mark word endings.

```
Trie Example (words: cat, car, dog):
        root
       /    \
      c      d
      |      |
      a      o
     / \     |
    t   r    g
    
cat: root→c→a→t (leaf)
car: root→c→a→r (leaf)
dog: root→d→o→g (leaf)

Prefix "ca" reaches node, can traverse to both "cat" and "car"
```

**Key Invariants:**
1. **Root is empty:** Represents empty prefix
2. **Character per edge:** Each edge labeled with character
3. **Terminal marking:** Some nodes marked as word endings
4. **Prefix sharing:** Common prefixes share edges

**Visual Representation:**

```
Trie structure:
Each node has:
- children: map of character → child node
- isEndOfWord: boolean marking word endings

Example insertion: "cat"
root.children['c'] = new TrieNode()
node_c.children['a'] = new TrieNode()
node_a.children['t'] = new TrieNode()
node_t.isEndOfWord = true
```

---

## 3️⃣ THE HOW — Mechanical Walkthrough

**State:**
- `root`: root node of trie
- `children[c]`: child node for character c
- `isEndOfWord`: whether node marks word ending

**Operation 1: Insert String**
```
1. current = root
2. For each character c in string:
     if current.children[c] not exist:
       current.children[c] = new TrieNode()
     current = current.children[c]
3. current.isEndOfWord = true

Time: O(m) where m = length of string
Space: O(m) for new nodes
```

**Operation 2: Search String**
```
1. current = root
2. For each character c in string:
     if current.children[c] not exist:
       return false
     current = current.children[c]
3. return current.isEndOfWord

Time: O(m)
Space: O(1)
```

**Operation 3: Prefix Search**
```
1. current = root
2. For each character c in prefix:
     if current.children[c] not exist:
       return false (no words with prefix)
     current = current.children[c]
3. return true (prefix found, can traverse further)

Time: O(m)
```

**Operation 4: Get All Words with Prefix**
```
1. current = findPrefix(prefix)
2. if current not found: return []
3. dfs(current) to collect all words:
   - If isEndOfWord, add word to results
   - For each child, recursively collect

Time: O(n) where n = number of matching words
```

---

## 4️⃣ VISUALIZATION — Simulation & Examples

**Example 1: Insert and search in trie**

```
Insert: ["apple", "app", "apricot"]

Initial: root (empty)

After "apple":
root → a → p → p → l → e (end)

After "app":
root → a → p → p (end) → l → e (end)

After "apricot":
root → a → p (choice: p→p or r)
          → p → l → e (end)
          → r → i → c → o → t (end)

Trie structure:
        root
        |
        a
        |
        p
       / \
      p   r
      |   |
    (end) i
      |   |
      l   c
      |   |
      e   o
    (end) |
          t
        (end)

Search "apple": root→a→p→p→l→e (isEndOfWord=true) → FOUND
Search "app": root→a→p→p (isEndOfWord=true) → FOUND
Search "apr": root→a→p→r (isEndOfWord=false) → NOT FOUND
Prefix "ap": root→a→p (exists, can continue) → PREFIX EXISTS
```

**Example 2: Autocomplete with prefix**

```
Dictionary: ["cat", "car", "card", "care", "careful"]

User types: "car"
Find prefix "car": root→c→a→r (exists)

From node 'r', DFS to find all words:
- "car" (isEndOfWord=true)
- "card" (isEndOfWord=true)
- "care" (isEndOfWord=true)
- "careful" (isEndOfWord=true)

Suggestions: ["car", "card", "care", "careful"]
```

---

## 5️⃣ CRITICAL ANALYSIS — Performance & Robustness

| Operation | Time | Space | Notes |
|-----------|------|-------|-------|
| **Insert** | O(m) | O(m) | m = string length |
| **Search** | O(m) | O(1) | m = string length |
| **Prefix Search** | O(m) | O(1) | m = prefix length |
| **Get All Words** | O(n×m) | O(n×m) | n = matches, m = avg length |
| **Delete** | O(m) | O(1) | m = string length |

**Key Insight:** Time independent of dictionary size. Depends only on string/prefix length.

**Real Memory Behavior:**
- Space: O(ALPHABET_SIZE × n × m) where n = words, m = avg length
- English alphabet: 26 × ALPHABET_SIZE per node
- Sparse tries use hash maps instead of arrays

**Edge Cases & Failure Modes:**
- **Empty dictionary:** Root node only
- **Prefix not found:** Return immediately
- **Word is prefix of another:** Mark as end, continue tree
- **Delete non-existent:** No change
- **Case sensitivity:** Convert to lower/upper first

---

## 6️⃣ REAL SYSTEM INTEGRATION

**Google Search Autocomplete:**
- Trie of popular search terms
- User types, find matching prefix
- Suggest top results by frequency
- O(m) responsiveness regardless of dictionary size

**Mobile Phone T9:**
- Trie of dictionary words
- User enters digit sequence (2-9)
- Trie node maps digits to characters
- Predict word from partial input

**IDE Code Completion:**
- Trie of all available identifiers/functions
- User types prefix
- Suggest completions in real-time
- Fast feedback even with massive codebase

**DNS/IP Routing:**
- Trie of IP prefixes
- Longest prefix matching for routing
- O(m) lookup where m = IP address length
- Critical for network performance

**Spell Checker:**
- Trie of dictionary words
- Fast lookup for word validity
- Suggestions via edit distance on trie

---

## 7️⃣ CONCEPT CROSSOVERS

**Builds On:**
- Trees (Week 5)
- Hash maps (Week 2)
- DFS/BFS (Week 6)
- String manipulation

**Built Upon By:**
- **Ternary Search Trees:** Balanced prefix trees
- **Suffix Trees:** Trie of all suffixes
- **Trie with bit compression:** Space optimization
- **Radix Trees:** Compressed prefixes

**Used In Algorithms:**
- Autocomplete
- Spell checking
- IP routing
- Word search
- Prefix matching
- T9 prediction

---

## 8️⃣ MATHEMATICAL & THEORETICAL PERSPECTIVE

**Trie Space Complexity:**
For alphabet size σ and total length L (sum of all string lengths):
- Worst case: O(σ × L) when no sharing
- Best case: O(L) with maximum prefix sharing

**Search Time:**
Independent of dictionary size. Only depends on search string length m.
T(m) = O(m) × alphabet lookup = O(m) with hash map implementation.

**Comparison to Hash Map:**
- Hash Map: O(1) average, O(n) worst for search
- Trie: O(m) guaranteed for search, but prefix operations natural

---

## 9️⃣ ALGORITHMIC DESIGN INTUITION

**When to Use Tries:**

✅ **Use when:**
- Prefix-based operations needed
- Autocomplete/suggestions required
- Multiple searches in same dictionary
- Space-efficient prefix storage needed

✅ **Examples:**
- Autocomplete systems
- IP routing (longest prefix)
- Spell checking with suggestions
- T9 prediction

❌ **Don't use when:**
- Single searches only (hash map better)
- No prefix operations needed
- Very sparse dictionary
- Memory is critical constraint

---

## 🔟 KNOWLEDGE CHECK — Socratic Reasoning

**Q1:** Why is Trie search O(m) independent of dictionary size?

**Q2:** How does Trie share common prefixes?

**Q3:** Why use Trie over hash map for autocomplete?

**Q4:** How implement prefix search efficiently?

**Q5:** What's space complexity for n words of avg length m?

---

## 1️⃣1️⃣ RETENTION HOOK — Memory Anchors

**One-Liner:**
> **Trie: Prefix tree for fast string searching. O(m) search/insert, independent of dictionary size. Natural for autocomplete, spell-check, IP routing.**

**Mnemonic:** "T.R.I.E." → Tree, Retrieval, Insert, Efficient prefix

**Cognitive Lenses:**

| **Computational** | O(m) search independent of dictionary. Prefix operations natural. Trade space for speed. |
| **Psychological** | Intuitive: directory structure (folders as characters). Natural tree traversal. |
| **Design Trade-off** | Trie vs Hash Map: Trie better for prefixes, Hash Map better for single searches. |
| **AI/ML Analogy** | Similar to: prefix-matching in language models (autocomplete). |
| **Historical Context** | Trie (1959), still optimal for prefix-based problems. Foundation of many systems. |

---

## Supplementary Outcomes

**Practice Problems (8+):**
1. Implement Trie Insert, Search, StartsWith
2. Autocomplete System
3. Replace Words
4. Word Search II
5. Unique Email Addresses
6. Longest Word in Dictionary
7. Implement Magic Dictionary
8. Maximum XOR of Two Numbers in Array

**Interview Q&A Highlights:**
- Why Trie for autocomplete?
- Space vs time trade-offs?
- Prefix search algorithm?
- Delete implementation?
- When use vs hash map?

**Common Misconceptions:**
- ❌ "Trie slower than hash map" → ✅ Hash map O(1) search but O(m) for prefixes
- ❌ "Trie wastes space" → ✅ Space efficient with prefix sharing
- ❌ "Complex to implement" → ✅ Simple recursive structure
- ❌ "Only for English" → ✅ Works for any alphabet
- ❌ "Not practical for real systems" → ✅ Used in Google, DNS, phones

