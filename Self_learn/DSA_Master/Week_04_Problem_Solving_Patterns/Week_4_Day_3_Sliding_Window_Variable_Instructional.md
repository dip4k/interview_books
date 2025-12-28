# Week 4, Day 3: Sliding Window (Variable Size)

## 🗓 Metadata
**Week:** 4 | **Day:** 3 of 5 | **Topic:** Variable-Size Sliding Window  
**Category:** Problem-Solving Patterns | **Difficulty:** 🔴 Hard  
**Prerequisites:** Week 1-3, Day 2 (fixed sliding window)  
**Time:** 150-180 minutes | **Status:** 🔍 In Study

---

## 1️⃣ THE WHY — Engineering Motivation

### Real-World Problem
Finding optimal subarray where window size unknown (minimum window containing chars, longest substring without repeats). Fixed window won't work—need dynamic expansion/contraction based on constraint satisfaction.

### Design Problems Solved
- **Minimum window substring** (smallest substring containing all chars)
- **Longest substring without repeating characters**
- **Longest substring with exactly k distinct characters**
- **Smallest subarray with sum ≥ target**
- **Maximum sliding window** (with complexity variations)
- **Count anagrams** (window contains rearrangement)
- **Constrained path finding** (sliding along constraints)

### Real System Usage
- **Data compression (LZMA):** Dictionary window expands/contracts based on pattern matching needs
- **Video codec motion compensation:** Search window dynamically sized by motion magnitude
- **Network protocol buffer:** TCP window adapts based on congestion (window scaling)
- **Garbage collection:** Mark phase expands/contracts live object window
- **Database cursor:** Fetch window expands based on memory available
- **Spell checker:** Correction window expands to context boundaries
- **Machine learning:** Training window expands based on gradient stability

### Why Variable Sliding Window Matters
**Handles constraint-based problems where window size is unknown**, adapting dynamically. Extends two-pointer pattern to optimize across variable-sized windows.

---

## 2️⃣ THE WHAT — Mental Model & Intuition

### Core Analogy
Imagine **inflatable balloon** expanding/contracting in tunnel. Expand until you touch walls (constraint violated), then contract until valid again. Find smallest/largest valid balloon position.

### Key Invariants
1. **Valid Window Invariant:** Window always satisfies constraint (when expanded)
2. **Contraction Invariant:** Can shrink left without violating constraint
3. **Expansion Invariant:** Expand right until constraint breaks
4. **Optimality Invariant:** Track best valid window seen so far

### Visual Representation

```
Variable-Size Sliding Window (find min window with 'abc'):

String: "ADOBECODEBANC"
Target: "ABC"

[A                          Expand right looking for all chars
[A D O B E C          Constraint satisfied! Now contract left
  [ D O B E C         Can remove A, still valid
    [ O B E C         Can remove D, still valid
      [ B E C         Can remove O, still valid
        [ E C         Cannot remove B (missing from char set)
Minimal window: "BEC" (3 chars)

Continue expanding...
        [ E C O D E        Expand looking for full set again
[...and so on
```

---

## 3️⃣ THE HOW — Mechanical Walkthrough

### State Definition
- **window_chars:** Hash map of character counts in current window
- **required_chars:** Hash map of characters needed (target)
- **formed:** Count of unique characters in window matching required counts
- **left, right:** Window pointers

### Operation 1: Minimum Window Substring

```
Algorithm: Find smallest substring containing all target characters

Initialize:
  required = {}
  for each char in target:
    required[char]++
  
  window = {}
  formed = 0  // Unique chars in window with correct count
  required_count = len(required)
  
  left = 0
  result = (inf, -1, -1)  // (length, left, right)

For right = 0 to len(s) - 1:
  // Add character at right
  char = s[right]
  window[char]++
  
  // If this char's count matches required
  if char in required and window[char] == required[char]:
    formed++
  
  // Contract window from left while valid
  While left <= right and formed == required_count:
    // Update result if this window is smaller
    if right - left + 1 < result.length:
      result = (right - left + 1, left, right)
    
    // Remove left character
    char = s[left]
    window[char]--
    if char in required and window[char] < required[char]:
      formed--
    
    left++

return s[result.left:result.right+1]

Time: O(n) — each position visited at most twice
Space: O(m) — hash map for target characters
```

**Key Insight:** Expand until valid, contract until invalid, track minimum.

### Operation 2: Longest Substring Without Repeating Characters

```
Algorithm: Find longest substring with all unique characters

Initialize:
  char_index = {}  // Last seen index of each character
  max_length = 0
  left = 0

For right = 0 to len(s) - 1:
  char = s[right]
  
  // If char was seen and still in window
  if char in char_index and char_index[char] >= left:
    // Move left pointer past previous occurrence
    left = char_index[char] + 1
  
  // Update last seen index
  char_index[char] = right
  
  // Update max length
  max_length = max(max_length, right - left + 1)

return max_length

Time: O(n) — single pass
Space: O(min(n, charset)) — hash map size
```

**Key Insight:** When duplicate found, shrink left to exclude previous occurrence.

---

## 4️⃣ VISUALIZATION — Simulation & Examples

### Example 1: Minimum Window Substring

**Problem:** Find shortest substring of "ADOBECODEBANC" containing "ABC"

```
Target: "ABC" = {A:1, B:1, C:1}

right=0: "A" → window={A:1}, formed=1/3, not complete
right=1: "AD" → window={A:1,D:1}, formed=1/3
right=2: "ADO" → window={A:1,D:1,O:1}, formed=1/3
right=3: "ADOB" → window={A:1,D:1,O:1,B:1}, formed=2/3
right=4: "ADOBE" → window={A:1,D:1,O:1,B:1,E:1}, formed=2/3
right=5: "ADOBEC" → window={A:1,D:1,O:1,B:1,E:1,C:1}, formed=3/3 ✓ VALID!

Now contract left:
left=0: window="ADOBEC" (len=6), update result=6
left=1: window="DOBEC", remove A, formed=2/3 (invalid), stop

right=6: "DOBECD" → window={D:1,O:1,B:1,E:1,C:1,D:2}, formed=2/3
...continue expanding...
right=9: "DOBECODED" → window contains A,B,C (formed=3/3) ✓

Contract:
left moves to exclude extra D's until valid

Final: "BANC" is valid window, length=4
Answer: "BANC" (or "ADOBEC" if first found)
```

---

### Example 2: Longest Substring Without Repeating

**Problem:** Longest unique chars in "abcabcbb"

```
"abcabcbb"

right=0: "a" → unique, max=1
right=1: "ab" → unique, max=2
right=2: "abc" → unique, max=3
right=3: "abca" → 'a' at index 3, previous 'a' at index 0
         left = 0+1 = 1
         window = "bca" → max=3
right=4: "bcab" → 'b' at index 4, previous 'b' at index 1
         left = 1+1 = 2
         window = "cab" → max=3
right=5: "cabc" → 'c' at index 5, previous 'c' at index 2
         left = 2+1 = 3
         window = "abc" → max=3
right=6: "abcb" → 'b' at index 6, previous 'b' at index 4
         left = 4+1 = 5
         window = "cb" → max=3
right=7: "bcb" → 'b' at index 7, previous 'b' at index 6
         left = 6+1 = 7
         window = "b" → max=3

Answer: 3 (substring "abc")
```

---

## 5️⃣ CRITICAL ANALYSIS — Performance & Robustness

### Complexity Analysis

| Operation | Time | Space | Conditions |
|-----------|------|-------|-----------|
| **Min window substring** | O(n+m) | O(m) | Hash map of target size |
| **Longest unique** | O(n) | O(charset) | 26-256 chars |
| **With sorted required** | O(n log n) | O(1) | Preprocessing sorts |

### Edge Cases & Failure Modes

1. **No valid window:** Never satisfies constraint
   - ❌ **Risk:** Return invalid result
   - ✅ **Solution:** Return empty string or -1

2. **Entire string is window:** Window = input
   - ❌ **Risk:** Off-by-one in window size
   - ✅ **Solution:** Handle naturally (window expands to end)

3. **Multiple valid windows:** First, smallest, any?
   - ❌ **Risk:** Return wrong window
   - ✅ **Solution:** Specify which (usually smallest)

4. **Case sensitivity:** "a" vs "A"
   - ❌ **Risk:** Treat differently when shouldn't
   - ✅ **Solution:** Normalize upfront if needed

---

## 6️⃣ REAL SYSTEM INTEGRATION

### System 1: LZMA Compression Dictionary
Variable dictionary window adapts based on pattern matching:
```
Window starts small, expands until pattern matches found
When compression ratio plateaus, contract window
Dynamic sizing avoids unused memory in sparse data
```

### System 2: TCP Window Scaling (RFC 1323)
Network window adapts based on bandwidth-delay product:
```
Initial window: 64KB
If high latency detected, expand window
If congestion detected, contract window
Variable sizing optimizes throughput
```

### System 3: Video Codec Motion Search
Motion compensation window expands/contracts:
```
Search window starts small (+/-16 pixels)
If motion found at boundary, expand window
If no motion in window, contract it
Adapts to scene dynamics
```

### System 4-7: Database, ML, Spell Check, GC
Similar dynamic constraint satisfaction patterns

---

## 7️⃣ CONCEPT CROSSOVERS

### Builds On
- Day 2 (Fixed window): Pointers move forward pattern
- Two pointers: Convergent movement with constraint
- Hash tables: Character counting and constraint checking

### Built Upon By
- Week 11 DP: State space exploration with variable ranges
- Advanced patterns: Complex constraints requiring dynamic windows

---

## 8️⃣ MATHEMATICAL & THEORETICAL PERSPECTIVE

### Theorem: O(n) Time Minimum Window
**Claim:** Can find minimum window in O(n) time.

**Proof:**
- Right pointer: 0 to n-1, moves forward once per iteration = O(n)
- Left pointer: 0 to n-1, moves forward total (never backward) = O(n)
- Total pointer movements: 2n = O(n)
- Hash map operations: O(1) per update
- Total: O(n)

---

## 9️⃣ ALGORITHMIC DESIGN INTUITION

### When to Use Variable Sliding Window

✅ **Use when:**
- Window size unknown/variable based on constraint
- Constraint is on window contents (characters, sum, etc.)
- Need to find optimal window (min/max)

✅ **Examples:**
- Minimum window containing all characters
- Longest substring without repeating
- Smallest subarray with sum ≥ target

---

## 🔟 KNOWLEDGE CHECK — Socratic Reasoning

**Q1: How does variable sliding window ensure optimality?**
- Hint: Why contract left even after expanding to valid?
- Deep: What invariant about left ensures we don't miss optimal?

**Q2: Why can left pointer move only forward?**
- Hint: If we contract left, can we ever need to expand back to old position?
- Deep: How does monotonicity help here?

---

## 1️⃣1️⃣ RETENTION HOOK — Memory Anchors

**One-Liner:**
> **Variable sliding window adapts size based on constraint: expand right until valid, contract left until invalid, track best.**

**Mnemonic:** **ACCORDION** (expands and contracts) or **INFLATE/DEFLATE**

### 5 Cognitive Lenses

| **Computational** | Hash table maintains constraint state O(1) updates. Pointer movements O(n) total. |
| **Psychological** | Two-phase thinking: expand until valid, contract until invalid. Natural flow. |
| **Design Trade-off** | Variable window: handles more problems but complex logic. Fixed window: simpler but limited. |
| **AI/ML Analogy** | Binary search on window size: find smallest/largest valid configuration. |
| **Historical Context** | Formalized ~2010s in competitive programming as "two pointers with constraint." |

---

## Supplementary Outcomes

### Practice Problems (8+)

1. **Minimum Window Substring** (LeetCode 76)
   - Find shortest substring containing all chars
   - [Hard] 30 min

2. **Longest Substring Without Repeating Characters** (LeetCode 3)
   - Find longest with all unique chars
   - [Medium] 25 min

3. **Longest Substring with At Most Two Distinct Characters** (LeetCode 159)
   - Window with max 2 unique chars
   - [Medium] 25 min

4. **Minimum Size Subarray Sum** (LeetCode 209)
   - Shortest subarray with sum ≥ target
   - [Medium] 20 min

5. **Subarrays with Product Less Than K** (LeetCode 713)
   - Count subarrays with product < k
   - [Medium] 25 min

6. **Permutation in String** (LeetCode 567)
   - Check if permutation exists as substring
   - [Medium] 20 min

7. **Sliding Window Maximum** (variant with variable)
   - Max in dynamic-size windows
   - [Hard] 30 min

8. **Minimum Window Substring with Duplicates** (variant)
   - Allow duplicate chars in target
   - [Hard] 35 min

### Interview Q&A Highlights

**Q: Why can't fixed sliding window handle minimum window problem?**
A: Fixed window has predetermined size. Minimum window size varies based on which characters present. Need adaptive sizing.

**Q: How does hash map help with constraint checking?**
A: Counts occurrences of each character. Comparing counts tells us if constraint satisfied in O(1) time.

### Common Misconceptions

- ❌ **"Can always find minimum with fixed window"** → ✅ Only if you try all possible sizes (defeats purpose)
- ❌ **"Must track all characters individually"** → ✅ Hash map handles counting automatically

---

**Status:** ✅ Complete  
**Next:** Day 4 (Prefix Sums) uses different approach to optimize range queries

