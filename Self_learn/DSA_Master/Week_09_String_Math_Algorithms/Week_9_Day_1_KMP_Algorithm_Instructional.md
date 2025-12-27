# Week 9, Day 1: String Matching - KMP Algorithm

## 🗓 Metadata
**Week:** 9 | **Day:** 1 of 5 | **Topic:** KMP Algorithm (Knuth-Morris-Pratt)  
**Category:** String Algorithms | **Difficulty:** 🟡 Medium  
**Prerequisites:** Week 1-8, string basics, pattern matching concepts  
**Time:** 90-120 minutes | **Status:** 🔍 In Study

---

## 1️⃣ THE WHY — Engineering Motivation

**Real-World Problem:**
Find all occurrences of pattern in text efficiently. Naive approach: O(nm) per position check. KMP: O(n+m) single pass. Elegant use of failure function to skip redundant comparisons.

**Design Problems Solved:**
- Pattern matching (all occurrences)
- Substring search
- Text processing
- DNA sequence matching
- Log file analysis
- Network packet inspection
- Plagiarism detection variants
- Autocomplete filtering

**Real System Usage:**
- **Text Editors:** Find & replace (Ctrl+F in VS Code)
- **Search Engines:** Pattern matching in documents
- **DNA Analysis:** Sequence matching in bioinformatics
- **Log Processing:** Find patterns in log files
- **Network Tools:** Packet inspection (grep-like)
- **File Systems:** Pattern matching in file search
- **Compilers:** Lexical analysis, pattern matching

**Why KMP Matters:**
O(n+m) optimal for single pattern matching. Elegant algorithm demonstrating preprocessing. More intuitive than suffix structures for single pattern. Fundamental for interview preparation.

---

## 2️⃣ THE WHAT — Mental Model & Intuition

**Core Analogy:**
Think KMP like **learning from failure**. When mismatch occurs, don't restart from beginning. Use "failure function" (LPS array) to know how far back to go. Smart backtracking.

```
Naive approach (mismatch at position 3):
Pattern: "ABABD"
Text: "ABABCABABD"
Mismatch at D vs C
Restart comparison from position 2 in text (inefficient)

KMP approach (mismatch at position 3):
Pattern: "ABABD"
Text: "ABABCABABD"
Mismatch at D vs C
LPS[2] = 2 (means "ABA" matches start)
Skip to position 2 in pattern (efficient)
```

**Key Invariants:**
1. **LPS Array:** LPS[i] = longest proper prefix which is also suffix of pattern[0..i]
2. **Proper Prefix/Suffix:** No whole string, only proper parts
3. **Deterministic:** LPS completely determines pattern structure
4. **No Backtracking:** Text pointer never resets

**Visual Representation:**

```
Pattern: "ABABAC"
LPS array:
Index:  0 1 2 3 4 5
Pattern: A B A B A C
LPS:    0 0 1 2 3 0

LPS[0] = 0 (single char, no proper prefix/suffix)
LPS[1] = 0 (AB has no prefix=suffix)
LPS[2] = 1 (ABA: prefix "A" = suffix "A")
LPS[3] = 2 (ABAB: prefix "AB" = suffix "AB")
LPS[4] = 3 (ABABA: prefix "ABA" = suffix "ABA")
LPS[5] = 0 (ABABAC: no proper prefix=suffix)
```

---

## 3️⃣ THE HOW — Mechanical Walkthrough

**State:**
- `pattern`: string to search for
- `text`: string to search in
- `LPS[i]`: longest proper prefix which is also suffix of pattern[0..i]
- `j`: pattern index, `i`: text index

**Operation 1: Compute LPS Array**
```
1. ComputeLPS(pattern):
     lps = [0] * len(pattern)
     len = 0  // length of previous longest prefix suffix
     i = 1
     
     while i < len(pattern):
       if pattern[i] == pattern[len]:
         len += 1
         lps[i] = len
         i += 1
       else:
         if len != 0:
           len = lps[len - 1]  // Use previous LPS value
         else:
           lps[i] = 0
           i += 1
     return lps

Time: O(m) where m = pattern length
Space: O(m)
```

**Operation 2: KMP Search**
```
1. KMPSearch(text, pattern):
     if not pattern: return []
     lps = ComputeLPS(pattern)
     matches = []
     
     i = 0  // text index
     j = 0  // pattern index
     
     while i < len(text):
       if pattern[j] == text[i]:
         i += 1
         j += 1
       
       if j == len(pattern):
         matches.append(i - j)  // Found match
         j = lps[j - 1]  // Continue searching
       elif i < len(text) and pattern[j] != text[i]:
         if j != 0:
           j = lps[j - 1]  // Skip unnecessary comparisons
         else:
           i += 1
     
     return matches

Time: O(n) where n = text length
Space: O(1) for search (O(m) for LPS)
```

---

## 4️⃣ VISUALIZATION — Simulation & Examples

**Example 1: Build LPS Array**

```
Pattern: "ABABAC"

Step 1: i=1, len=0
  pattern[1]='B' != pattern[0]='A'
  lps[1] = 0

Step 2: i=2, len=0
  pattern[2]='A' == pattern[0]='A'
  len = 1, lps[2] = 1

Step 3: i=3, len=1
  pattern[3]='B' == pattern[1]='B'
  len = 2, lps[3] = 2

Step 4: i=4, len=2
  pattern[4]='A' == pattern[2]='A'
  len = 3, lps[4] = 3

Step 5: i=5, len=3
  pattern[5]='C' != pattern[3]='B'
  len = lps[3-1] = lps[2] = 1
  pattern[5]='C' != pattern[1]='B'
  len = lps[1-1] = lps[0] = 0
  pattern[5]='C' != pattern[0]='A'
  lps[5] = 0

Final LPS: [0, 0, 1, 2, 3, 0]
```

**Example 2: KMP Search**

```
Text: "ABABDABABAC"
Pattern: "ABABAC"
LPS: [0, 0, 1, 2, 3, 0]

Positions: 0 1 2 3 4 5 6 7 8 9 10
Text:      A B A B D A B A B A C
Pattern:   A B A B A C

i=0, j=0: A==A, i++, j++ (i=1, j=1)
i=1, j=1: B==B, i++, j++ (i=2, j=2)
i=2, j=2: A==A, i++, j++ (i=3, j=3)
i=3, j=3: B==B, i++, j++ (i=4, j=4)
i=4, j=4: D!=A, j=lps[3]=2
i=4, j=2: D!=A, j=lps[1]=0
i=4, j=0: D!=A, i++

i=5, j=0: A==A, i++, j++ (i=6, j=1)
i=6, j=1: B==B, i++, j++ (i=7, j=2)
i=7, j=2: A==A, i++, j++ (i=8, j=3)
i=8, j=3: B==B, i++, j++ (i=9, j=4)
i=9, j=4: A==A, i++, j++ (i=10, j=5)
i=10, j=5: C==C, i++, j++ (i=11, j=6)

j==6 (pattern length), match found at position 11-6=5
j = lps[5] = 0

i=11 >= len(text), done

Matches at position: 5
```

---

## 5️⃣ CRITICAL ANALYSIS — Performance & Robustness

| Operation | Time | Space | Notes |
|-----------|------|-------|-------|
| **Build LPS** | O(m) | O(m) | m = pattern length |
| **Search** | O(n) | O(1) | n = text length |
| **Total** | O(n+m) | O(m) | One-time preprocessing |

**Key Insight:** O(n+m) optimal for single pattern. No algorithm can do better (must read entire text).

**Real Memory Behavior:**
- LPS array: small (pattern length)
- Single pass through text: excellent cache locality
- No backtracking on text pointer: sequential access

**Edge Cases & Failure Modes:**
- **Empty pattern:** Handle separately
- **Pattern longer than text:** No matches
- **Pattern = text:** Match at position 0
- **Repeated pattern:** "AAA" finding "AA" multiple times
- **All same characters:** LPS array is [0,1,2,3,...]
- **Disjoint pattern:** LPS array all 0s

---

## 6️⃣ REAL SYSTEM INTEGRATION

**Text Editors (VS Code, Sublime):**
- Find & Replace feature
- User types pattern
- KMP finds all occurrences
- O(n+m) fast response for large documents

**Log Processing Tools (grep):**
- Search through massive logs
- KMP ensures O(n+m) performance
- Works for complex patterns in pipelines

**DNA Sequence Analysis:**
- Find motifs in sequences
- Pattern = gene sequence
- Text = chromosome
- Critical for bioinformatics

**Network Intrusion Detection:**
- Scan packets for malicious patterns
- KMP for fast pattern matching
- Real-time performance requirement

---

## 7️⃣ CONCEPT CROSSOVERS

**Builds On:**
- Basic string operations (Week 1)
- Hash functions (Week 2)
- Arrays (Week 1)

**Built Upon By:**
- **Rabin-Karp:** Rolling hash variant (Day 2)
- **Aho-Corasick:** Multiple patterns (advanced)
- **Boyer-Moore:** Faster for large alphabets
- **Suffix structures:** Alternative for multiple patterns

**Used In Algorithms:**
- Text processing
- Pattern matching
- Substring search
- Interview problems (hard)

---

## 8️⃣ MATHEMATICAL & THEORETICAL PERSPECTIVE

**Time Complexity Proof:**
- LPS computation: each element processed once = O(m)
- Search: text pointer i increases monotonically from 0 to n, never decreases = O(n)
- Total: O(n+m) proven

**Correctness via Invariant:**
Invariant: j characters matched in pattern, i characters read in text.
- If next match: j++, i++
- If mismatch: skip using LPS to known good state
- Invariant maintained throughout

**LPS Array Property:**
LPS[i] < i for all i (proper prefix/suffix strictly smaller than string).
This ensures progress: when mismatch, we skip forward.

---

## 9️⃣ ALGORITHMIC DESIGN INTUITION

**When to Use KMP:**

✅ **Use when:**
- Single pattern matching needed
- Speed critical (O(n+m) required)
- Interview or competitive programming
- Pattern length moderate

✅ **Examples:**
- Text editor find
- Substring search
- Pattern matching
- Log analysis

**When Use Alternatives:**

✅ **Rabin-Karp:** Multiple patterns, hash flexibility
✅ **Suffix structures:** All patterns once, many queries
✅ **Aho-Corasick:** Multiple patterns optimally
✅ **Simple strstr():** If sufficient for constraints

---

## 🔟 KNOWLEDGE CHECK — Socratic Reasoning

**Q1:** Why does LPS array prevent redundant comparisons?

**Q2:** What does LPS[i] represent exactly?

**Q3:** Why is the algorithm O(n+m) and not O(nm)?

**Q4:** How handle multiple matches?

**Q5:** What happens with overlapping patterns?

---

## 1️⃣1️⃣ RETENTION HOOK — Memory Anchors

**One-Liner:**
> **KMP Algorithm: O(n+m) pattern matching via LPS failure function. Learn from mismatch, skip efficiently. Elegant preprocessing-based approach. Interview favorite.**

**Mnemonic:** "K.M.P." → Knuth-Morris-Pratt, Know failure, Match efficiently, Process once

**Cognitive Lenses:**

| **Computational** | O(n+m) optimal. Single pass text. LPS array drives efficiency. |
| **Psychological** | Intuitive: learn from failures, use knowledge to skip forward. |
| **Design Trade-off** | KMP O(n+m) vs naive O(nm). Worth LPS preprocessing. |
| **AI/ML Analogy** | Similar to: dynamic programming state machine transitions. |
| **Historical Context** | KMP (1977), revolutionary for pattern matching. Still taught/used. |

---

## Supplementary Outcomes

**Practice Problems (8+):**
1. Implement KMP
2. Find First Occurrence of Pattern
3. Count Occurrences of Pattern
4. Find the Index of First Occurrence (LeetCode)
5. Repeated Substring Pattern
6. Shortest Palindrome (KMP variant)
7. KMP with Multiple Patterns
8. Pattern Matching with Overlaps

**Interview Q&A Highlights:**
- How compute LPS array?
- Why O(n+m) complexity?
- Handle overlapping patterns?
- When use KMP vs other approaches?
- Implement from scratch?

**Common Misconceptions:**
- ❌ "LPS array just prefix/suffix count" → ✅ Longest proper prefix which IS suffix (specific matching property)
- ❌ "Complex to implement" → ✅ ~15 lines of code, becomes routine
- ❌ "Rarely used in practice" → ✅ Text editors, log tools, DNA analysis use it
- ❌ "Always use built-in string search" → ✅ Understanding KMP valuable for interviews and optimization
- ❌ "Only one pattern solution" → ✅ KMP just one technique; Rabin-Karp, Aho-Corasick alternatives

