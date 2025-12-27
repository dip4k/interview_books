# Week 9, Day 2: String Matching - Rabin-Karp Algorithm

## 🗓 Metadata
**Week:** 9 | **Day:** 2 of 5 | **Topic:** Rabin-Karp Algorithm (Rolling Hash)  
**Category:** String Algorithms | **Difficulty:** 🟡 Medium  
**Prerequisites:** Week 1-8, hash functions, string matching basics  
**Time:** 90-120 minutes | **Status:** 🔍 In Study

---

## 1️⃣ THE WHY — Engineering Motivation

**Real-World Problem:**
Efficient pattern matching using hashing. Avoid character comparisons via hash equality. Multiple pattern matching efficiently. Rolling hash allows O(1) hash updates.

**Design Problems Solved:**
- Pattern matching (single and multiple)
- Substring search
- Multiple pattern detection
- Plagiarism detection (document similarity)
- DNA variant detection
- Duplicate substring detection
- 2D pattern matching (grid searches)
- Spam detection (pattern hashing)

**Real System Usage:**
- **Plagiarism Detection:** Hash documents, compare patterns
- **Spell Checkers:** Multiple word pattern matching
- **DNA Sequencing:** Find mutations (pattern variations)
- **Search Engines:** Document fingerprinting
- **Network Tools:** Intrusion detection patterns
- **Antivirus Software:** Malware signature matching
- **Compression:** Finding repeated substrings

**Why Rabin-Karp Matters:**
O(n+m) average case like KMP, but simpler to understand and implement. Rolling hash: elegant and practical. Extends easily to multiple patterns and 2D. More practical than KMP in many real systems.

---

## 2️⃣ THE WHAT — Mental Model & Intuition

**Core Analogy:**
Think Rabin-Karp like **pattern fingerprinting**. Hash pattern and text substrings. If hashes match, likely same substring (verify if needed). Rolling window hash updates efficiently.

```
Rolling Hash Concept:
Pattern: "ABC"
Text: "ABCDEF"

Hash("ABC") = h1
Hash("BCD") = h2 (don't recompute, use rolling hash)
  Remove 'A' contribution
  Add 'D' contribution
  O(1) update instead of O(m)

If Hash matches, string likely matches (with rare collisions)
```

**Key Invariants:**
1. **Hash Function:** Maps string to integer (multiple maps same string to same hash)
2. **Rolling Hash:** Update in O(1) by removing front, adding back
3. **Prime Modulo:** Reduce hash size, avoid overflow
4. **Collision Handling:** Verify actual match on hash collision

**Visual Representation:**

```
Pattern: "AB"
Text: "AABAB"
Base = 256, Prime = 101

Hash("AB") = (65*256 + 66) % 101 = 16706 % 101 = 66

Window 1: "AA" = (65*256 + 65) % 101 = 16705 % 101 = 65
Window 2: "AB" = (65*256 + 66) % 101 = 16706 % 101 = 66 ✓ Match
Window 3: "BA" = (66*256 + 65) % 101 = 16961 % 101 = 24
Window 4: "AB" = (65*256 + 66) % 101 = 16706 % 101 = 66 ✓ Match
```

---

## 3️⃣ THE HOW — Mechanical Walkthrough

**State:**
- `pattern`: string to search for
- `text`: string to search in
- `base`: alphabet size (256 for ASCII)
- `prime`: large prime for modulo
- `hash(pattern)`: hash of pattern
- `hash(window)`: rolling hash of current window

**Operation 1: Compute Pattern Hash & First Window Hash**
```
1. ComputeHash(string, base, prime):
     hash = 0
     for each char in string:
       hash = (hash * base + ord(char)) % prime
     return hash

2. ComputeFirstWindowHash(text, pattern_len, base, prime):
     return ComputeHash(text[0:pattern_len], base, prime)

Time: O(m) for pattern
Space: O(1)
```

**Operation 2: Rolling Hash Update**
```
1. RollingHash(prev_hash, old_char, new_char, base, prime, pattern_len):
     // Remove contribution of old character at position 0
     old_char_contrib = (ord(old_char) * pow(base, pattern_len-1, prime)) % prime
     
     // Remove old character
     hash = (prev_hash - old_char_contrib + prime) % prime
     
     // Shift left (multiply by base)
     hash = (hash * base) % prime
     
     // Add new character
     hash = (hash + ord(new_char)) % prime
     
     return hash

Time: O(1) per update (with fast modular exponentiation)
Space: O(1)
```

**Operation 3: Rabin-Karp Search**
```
1. RabinKarpSearch(text, pattern):
     if not pattern: return []
     
     base = 256
     prime = 101  // or large prime
     
     pattern_hash = ComputeHash(pattern, base, prime)
     window_hash = ComputeFirstWindowHash(text, len(pattern), base, prime)
     
     matches = []
     precompute = pow(base, len(pattern)-1, prime)
     
     for i in range(len(text) - len(pattern) + 1):
       if window_hash == pattern_hash:
         if text[i:i+len(pattern)] == pattern:  // Verify
           matches.append(i)
       
       if i < len(text) - len(pattern):
         window_hash = RollingHash(window_hash, text[i], 
                                   text[i+len(pattern)], 
                                   base, prime, len(pattern))
     
     return matches

Time: O(n+m) average, O(nm) worst (with verification)
Space: O(1)
```

---

## 4️⃣ VISUALIZATION — Simulation & Examples

**Example 1: Compute Rolling Hash**

```
Pattern: "AB"
Text: "AABAB"
Base = 256, Prime = 101

Hash function: (char_val * base + next_char) % prime

Initial hash for window "AA":
hash = 0
hash = (0 * 256 + 65) % 101 = 65
hash = (65 * 256 + 65) % 101 = 16705 % 101 = 65

Window "AB":
hash = 0
hash = (0 * 256 + 65) % 101 = 65
hash = (65 * 256 + 66) % 101 = 16706 % 101 = 66

Pattern hash: 66

Rolling from "AA" to "AB":
old_char_contrib = 65 * 256^(2-1) % 101 = 65 * 256 % 101
                 = 16640 % 101 = 40
hash = (65 - 40 + 101) % 101 = 126 % 101 = 25
hash = (25 * 256) % 101 = 6400 % 101 = 72
hash = (72 + 66) % 101 = 138 % 101 = 37

Hmm, let me recalculate more carefully:
Actually: old_char_contrib = 65 * (256^1) % 101
hash_without_old = (65 - old_contrib + 101) % 101
hash_shifted = (hash_without_old * 256) % 101
hash_new = (hash_shifted + 66) % 101

Let me use simpler math:
"AA" hash = (65 * 256 + 65) = 16705
Shift left by removing 65 from MSB, adding new char 66 at LSB
New hash should be computed as:
((16705 - 65 * 256) * 256 + 66) % 101
= ((16705 - 16640) * 256 + 66) % 101
= (65 * 256 + 66) % 101
= 16706 % 101 = 66 ✓
```

**Example 2: Rabin-Karp Search**

```
Text: "AABAB"
Pattern: "AB"
Pattern hash: 66

i=0: window="AA", hash=65, no match
     rolling: remove A (65), add B (66) → hash changes
i=1: window="AB", hash=66, hash matches! 
     verify: text[1:3]="AB" == pattern ✓ → match at position 1
     rolling: remove A, add A → new hash for "BA"
i=2: window="BA", hash != 66
     rolling: remove B, add B → hash for "AB"
i=3: window="AB", hash=66, hash matches!
     verify: text[3:5]="AB" == pattern ✓ → match at position 3

Matches: [1, 3]
```

---

## 5️⃣ CRITICAL ANALYSIS — Performance & Robustness

| Operation | Time | Space | Notes |
|-----------|------|-------|-------|
| **Compute Hash** | O(m) | O(1) | m = pattern length |
| **Rolling Update** | O(1) | O(1) | Per window |
| **Search** | O(n+m) avg | O(1) | n = text length |
| **Search Worst** | O(nm) | O(1) | All hash collisions |

**Key Insight:** Average case O(n+m) with good hash function. Worst case O(nm) but rare. Practical performance excellent.

**Hash Collision Handling:**
- Rare with good prime and base
- When hash matches, verify string equality
- False positives (hash collision): ~1/prime probability
- Single verification needed per match

**Real Memory Behavior:**
- Constant space (no LPS array unlike KMP)
- Rolling hash computes quickly (modular arithmetic)
- Verification only on hash matches (usually rare)

**Edge Cases & Failure Modes:**
- **Hash collision:** Rare but possible, always verify
- **Empty pattern:** Handle separately
- **Pattern longer than text:** No matches
- **Very large prime:** Causes overflow (use careful modular arithmetic)
- **Bad base choice:** More collisions possible
- **Pattern = text:** Match at position 0

---

## 6️⃣ REAL SYSTEM INTEGRATION

**Plagiarism Detection (MOSS, Turnitin):**
- Hash documents, compare patterns
- Rolling hash finds similar code fragments
- Practical and scalable approach

**DNA Variant Detection:**
- Find mutations in sequences
- Hash known patterns, find variants
- Faster than KMP for many patterns

**Search Engines (Document Fingerprinting):**
- Hash documents to detect duplicates
- Rabin-Karp fingerprints each document
- Quick similarity checks

**Spam/Malware Detection:**
- Hash known spam/malware patterns
- Rolling hash finds similar patterns
- Real-time detection systems

---

## 7️⃣ CONCEPT CROSSOVERS

**Builds On:**
- Hash functions (Week 2)
- String basics (Week 1)
- KMP algorithm (Day 1)

**Built Upon By:**
- **Multiple pattern matching:** Hash multiple patterns
- **2D pattern matching:** Rolling hash on 2D grids
- **Polynomial hashing:** Advanced rolling hash
- **Bloom filters:** Probabilistic data structures

**Used In Algorithms:**
- Pattern matching
- Plagiarism detection
- Document fingerprinting
- Bioinformatics
- Interview problems

---

## 8️⃣ MATHEMATICAL & THEORETICAL PERSPECTIVE

**Rolling Hash Formula:**
For window w = c₀c₁...c_{m-1}:
hash(w) = (c₀·b^(m-1) + c₁·b^(m-2) + ... + c_{m-1}) mod p

Remove c₀, add new character c_m:
new_hash = ((old_hash - c₀·b^(m-1)) · b + c_m) mod p

**Collision Probability:**
With prime p and random hash: P(collision) ≈ 1/p
With p = 10^9 + 7: collision probability ≈ 10^-9 (negligible)

**Time Complexity Proof:**
- Pattern hash: O(m)
- First window: O(m)
- Rolling updates: n-m updates, each O(1) → O(n)
- Verification: O(1) per match (rare), O(m) worst all matches
- Total: O(n+m) average, O(nm) worst

---

## 9️⃣ ALGORITHMIC DESIGN INTUITION

**When to Use Rabin-Karp:**

✅ **Use when:**
- Multiple patterns to search
- 2D pattern matching
- Plagiarism detection
- Simplicity preferred over KMP
- Hash function natural for problem

✅ **Examples:**
- Find multiple patterns
- 2D grid search
- Document fingerprinting
- Plagiarism detection

**When Use Alternatives:**

✅ **KMP:** Single pattern, guaranteed O(n+m)
✅ **Aho-Corasick:** Multiple patterns, optimal performance
✅ **Suffix structures:** Many patterns, complex queries
✅ **Simple search:** If sufficient

---

## 🔟 KNOWLEDGE CHECK — Socratic Reasoning

**Q1:** How does rolling hash update in O(1)?

**Q2:** Why is hash collision verification important?

**Q3:** Why O(n+m) average but O(nm) worst case?

**Q4:** How extend to multiple patterns?

**Q5:** When use Rabin-Karp over KMP?

---

## 1️⃣1️⃣ RETENTION HOOK — Memory Anchors

**One-Liner:**
> **Rabin-Karp: Hash-based pattern matching O(n+m) average. Rolling hash O(1) updates. Simple, elegant, extends to multiple patterns and 2D.**

**Mnemonic:** "R.K." → Rolling hash, Karp algorithm, Hash efficiently, Multiple patterns

**Cognitive Lenses:**

| **Computational** | O(n+m) average with rolling hash. O(1) per window. Simple probability theory. |
| **Psychological** | Intuitive: fingerprint strings, compare hashes, verify on match. |
| **Design Trade-off** | Simpler than KMP, more flexible than KMP, hash collision risk small. |
| **AI/ML Analogy** | Similar to: feature hashing in ML, signature-based detection. |
| **Historical Context** | Rabin-Karp (1987), still used in plagiarism detection, DNA analysis. |

---

## Supplementary Outcomes

**Practice Problems (8+):**
1. Implement Rabin-Karp
2. Find Substring Match (multiple patterns)
3. 2D Pattern Matching
4. Repeated DNA Sequences
5. Shortest Substring Containing All Characters (variant)
6. Plagiarism Detection (simplified)
7. Rabin-Karp with Multiple Patterns
8. Pattern Matching with Tolerance (approx match)

**Interview Q&A Highlights:**
- How compute rolling hash?
- Why verify on hash match?
- Time/space complexity?
- Multiple patterns handling?
- vs KMP comparison?

**Common Misconceptions:**
- ❌ "Hash collision breaks algorithm" → ✅ Rare, verification handles it
- ❌ "Rolling hash complex" → ✅ Simple modular arithmetic
- ❌ "Not practical" → ✅ Used in plagiarism detection, DNA analysis
- ❌ "Slower than KMP" → ✅ Often faster due to simplicity
- ❌ "Only for single pattern" → ✅ Extends naturally to multiple

