# 📘 WEEK 4 DAY 3: SLIDING WINDOW (VARIABLE) - Complete Learning Package

**Week 4, Day 3: Problem-Solving Pattern - Sliding Window with Variable Size**

Generated: 2025-12-26 | Duration: 90 minutes | Difficulty: 🔴 Hard | Target: 4-5/5

---

## PART 1: MAIN CONTENT (11 Sections)

### 1️⃣ The Why: Engineering Motivation

**Problem:** Find the longest substring with all unique characters.

Real-world:
- **Password validation:** Find longest valid segment without repeated chars
- **Data compression:** Find longest non-repeating sequence
- **Load balancing:** Find longest balanced window in packet data
- **DNA analysis:** Find longest substring without repeated nucleotides
- **Cache optimization:** Longest useful memory window

**Naive approach:** Check all substrings O(n³)
```python
max_length = 0
for i in range(n):
    for j in range(i+1, n+1):
        if all_unique(arr[i:j]):
            max_length = max(max_length, j - i)
return max_length
```

**Sliding window approach:** Expand/contract O(n)
```python
left = 0
char_set = set()
max_length = 0

for right in range(n):
    while arr[right] in char_set:
        char_set.remove(arr[left])
        left += 1
    char_set.add(arr[right])
    max_length = max(max_length, right - left + 1)

return max_length
```

**Performance difference:** 1000 items: 1B ops vs 1K ops (1M times faster!)

---

### 2️⃣ The What: Mental Model

**Core Insight:** Expand window while condition valid, contract when invalid. Maintain two pointers moving same direction.

**Key Difference from Fixed:**
- Fixed: Window size k is constant
- Variable: Window size changes based on condition

**Why this works:**
- Expand right to include more elements
- Contract left when condition violated
- Both pointers move only right (never left again)
- Each element processed at most twice

**Visual:**
```
String: "abcabcbb", Find longest substring without duplicate

Initial:
[a] b c a b c b b
 ↑
left=0, right=0
set={a}, length=1

Expand:
[a b] c a b c b b
 ↑ ↑
left=0, right=1
set={a,b}, length=2

Expand:
[a b c] a b c b b
 ↑   ↑
left=0, right=2
set={a,b,c}, length=3

Duplicate 'a' at index 3! Contract:
a [b c a] b c b b
   ↑ ↑
left=1, right=3
set={b,c,a}, length=3

Continue expanding...
```

**Key Property:** Two pointers move same direction, never backtrack. Each element visited ≤2 times.

---

### 3️⃣ The How: Mechanics

**Algorithm Template:**
```python
def sliding_window_variable(arr, condition):
    left = 0
    state = {}  # Track window state
    result = 0
    
    for right in range(len(arr)):
        # Expand: add element at right
        state[arr[right]] = state.get(arr[right], 0) + 1
        
        # Contract: while condition violated
        while not condition(state):
            state[arr[left]] -= 1
            if state[arr[left]] == 0:
                del state[arr[left]]
            left += 1
        
        # Calculate: update result
        result = max(result, right - left + 1)
    
    return result
```

**Step-by-step for longest unique substring:**
1. Initialize left=0, empty set
2. For each right position:
   a. Add arr[right] to set
   b. If duplicate found:
      - Remove arr[left] from set
      - Increment left
      - Repeat until valid
   c. Update max length
3. Return max length

**Why O(n)?**
- Right pointer: moves n times (0 to n-1)
- Left pointer: moves at most n times total
- Each element: added and removed at most once
- Total: O(n) not O(n²)

---

### 4️⃣ Visualization: Examples

**Example 1: Longest Substring Without Repeating Characters**
```
Input: "abcabcbb"

Step 1: right=0, arr[0]='a'
  Window: [a]
  set={a}, left=0, length=1

Step 2: right=1, arr[1]='b'
  Window: [ab]
  set={a,b}, left=0, length=2

Step 3: right=2, arr[2]='c'
  Window: [abc]
  set={a,b,c}, left=0, length=3

Step 4: right=3, arr[3]='a' (duplicate!)
  Window: [abc a] → contract
  Remove arr[0]='a': [bc a]
  set={b,c,a}, left=1, length=3

Step 5: right=4, arr[4]='b' (duplicate!)
  Window: [bc ab] → contract
  Remove arr[1]='b': [c ab]
  set={c,a,b}, left=2, length=3

... continue until end

Result: 3 (window "abc" or "cab")
```

**Example 2: Minimum Window Substring**
```
String: "ADOBECODEBANC"
Target: "ABC"

Find smallest substring containing all chars from target.
Window expands until all chars present.
Window contracts to minimum while keeping all chars.
Result: "BANC" (length 4)
```

**Example 3: Longest Substring with At Most k Distinct**
```
String: "eceba", k=2

[e]           set={e}, max=1
[e c]         set={e,c}, max=2
[e c e]       set={e,c}, max=3
[e c e b]     (3 distinct, need contract)
[c e b]       set={c,e,b}, max=3
[c e b a]     (4 distinct, contract)
[e b a]       set={e,b,a}, max=3

Result: 3 ("ecb" or "eba")
```

---

### 5️⃣ Critical Analysis

**Time Complexity:**
- Right pointer: n iterations
- Left pointer: moves at most n times total
- While loop total iterations: n (amortized)
- Per iteration: O(1)
- Total: O(n)

**Space Complexity:**
- Hash map/set: O(min(n, alphabet_size))
- For strings: O(26) for lowercase English
- For general: O(n) worst case

**Comparison to Fixed Window:**

| Aspect | Fixed | Variable |
|--------|-------|----------|
| Window size | Constant k | Changes |
| Pointer movement | Both move right | Both move right |
| Contract condition | Never | When violated |
| Complexity | O(n) | O(n) |
| Space | O(1) tracking | O(alphabet) |
| Difficulty | Medium | Hard |

**Key Insight:** Variable window harder conceptually but same time complexity as fixed.

---

### 6️⃣ Real System Integration

**Text Processing:**
- Auto-complete: longest valid prefix without repeating
- Spell checking: longest meaningful substring

**Network Protocols:**
- Sliding window in TCP (flow control)
- Find valid packet sequences

**Database Queries:**
- Find optimal window for aggregations
- Range-based partitioning

**Compression Algorithms:**
- Find longest non-repeating sequences
- Optimal chunking strategies

---

### 7️⃣ Concept Crossovers

**Builds On:**
- Week 1: Big-O analysis
- Week 2: Hash maps/sets
- Week 3: String processing
- Week 4 Day 1-2: Pointer movement patterns

**Enables:**
- Week 4 Day 4: Prefix sums with variable windows
- Week 5: Tree window problems
- Week 11: DP with sliding windows
- Week 12: Advanced window problems

**Related Techniques:**
- Two pointers (Day 1): opposite ends
- Fixed window (Day 2): constant size
- Variable window (Day 3): expand/contract

---

### 8️⃣ Mathematical Perspective

**Key Property:**
For variable window, left and right pointers each move at most n steps total.

```
left + right movements ≤ 2n = O(n)
```

**Why never backtrack?**
If arr[right] added doesn't satisfy condition and we contract,
when right moves forward, arr[left] will never satisfy condition
at its new position better than at old position.

**Proof Sketch:**
Suppose condition violated at (left, right).
We contract to (left', right) where left' > left.
Window [left', right] is subset of [left, right].
If [left, right] violated, subset [left', right] still violates.
Keep contracting until satisfied.
right then moves forward to right+1.
No need to return left to previous position.

---

### 9️⃣ Algorithmic Design Intuition

**When to Use Variable Sliding Window:**
1. Find substring/subarray with property
2. Window size not fixed (varies)
3. Condition can be checked incrementally
4. Want O(n) time

**When NOT to Use:**
- Window size is fixed (use fixed window)
- Condition non-monotonic (needs random access)
- Two-pointer approach better (Day 1)

**Problem Patterns:**
- Longest/shortest substring/subarray
- Contains k distinct characters
- Sum equals/exceeds target
- Valid/invalid Windows based on condition

---

### 🔟 Knowledge Check

1. Why doesn't left pointer move backward?
2. Trace longest unique substring on "dvdf"
3. How would you modify for "at most k distinct characters"?
4. Compare to two pointers (Day 1) - when use which?
5. Why O(n) and not O(n²)?
6. How to find minimum length instead of maximum?
7. What if you need both length AND substring itself?

---

### 1️⃣1️⃣ Retention Hooks

**One-liner:** "Variable sliding window expands right to explore, contracts left when condition violated, both move right only, giving O(n) complexity."

**Mnemonic - "EXPAND-CONTRACT":**
- **E**xpand: right pointer forward to include elements
- **X**tract: remove condition violations
- **P**rune: contract left until valid
- **A**chieve: track optimal result
- **N**ever: left pointer never goes backward
- **D**irection: both pointers move right only

**C**ontest: expand while condition good
- **O**nly: both pointers move right
- **N**eed: hash map to track state
- **T**wo: track left and right positions
- **R**ight: both move same direction
- **A**void: left doesn't go back
- **C**alculate: update result each iteration
- **T**ime: O(n) because pointers tracked

**Visual Memory:**
```
Think: "Elastic window that stretches and shrinks"
┌─────────────────────────────────────┐
1  2  3  4  5  6  7  8  9
[1][2]       ← initially small
[1][2][3][4] ← expands
[2][3][4]    ← contracts left
      [3][4][5][6] ← expands again
```

**Story:** "Imagine a rubber band on a rope. Right end moves forward to include new segments. Left end moves forward only when condition fails. Band never shrinks backward."

---

## PART 2: QUICK SUMMARY

**Variable Sliding Window Essence:**

Right pointer expands to include elements. Left pointer contracts when condition violated. Both move right only, giving O(n) total complexity.

**When to Use:**
- Variable window size ✓
- Find optimal substring/subarray ✓
- Condition checkable incrementally ✓
- Want O(n) time ✓

**Template:**
```python
def sliding_window_variable(arr, valid_condition):
    left = 0
    state = {}
    best = 0
    
    for right in range(len(arr)):
        # Expand: add element at right
        state[arr[right]] = state.get(arr[right], 0) + 1
        
        # Contract: while condition violated
        while not valid_condition(state):
            state[arr[left]] -= 1
            left += 1
        
        # Calculate: update best
        best = max(best, right - left + 1)
    
    return best
```

**Real Problems:**
- Longest substring without repeating
- Minimum window substring
- At most k distinct characters
- Longest subarray with sum = target
- Subarrays with product < k

---

## PART 3: SOCRATIC QUESTIONS & ANSWERS

**Q1:** Why can't left pointer move backward in variable window?

**A:** Because we never return to a previously checked state. If we contract left to position i, elements before i were determined insufficient. If right moves forward, no benefit to checking left=i-1 again (we'd reject for same reason).

---

**Q2:** Trace longest unique substring on "dvdf"

**A:**
```
d:     set={d}, left=0, right=0, length=1
dv:    set={d,v}, left=0, right=1, length=2
dvd:   conflict! contract
v d:   set={v,d}, left=1, right=2, length=2
vdf:   set={v,d,f}, left=1, right=3, length=3

Result: 3 (substring "vdf")
```

---

**Q3:** How to modify for "at most k distinct characters"?

**A:**
```python
def max_k_distinct(s, k):
    left = 0
    char_count = {}
    max_len = 0
    
    for right in range(len(s)):
        char_count[s[right]] = char_count.get(s[right], 0) + 1
        
        # Contract while more than k distinct
        while len(char_count) > k:
            char_count[s[left]] -= 1
            if char_count[s[left]] == 0:
                del char_count[s[left]]
            left += 1
        
        max_len = max(max_len, right - left + 1)
    
    return max_len
```

---

**Q4:** Compare variable window to two pointers (Day 1). When use which?

**A:**
- Two pointers: find one pair in sorted array
- Variable window: find longest/shortest substring with property

Different problems, both O(n). Two pointers requires sorting; variable doesn't.

---

**Q5:** Why is time O(n) not O(n²)?

**A:** Each pointer moves at most n steps. Right moves n steps. Left moves at most n steps. Total: 2n = O(n). NOT n steps of n work.

---

**Q6:** How to find MINIMUM length instead of maximum?

**A:**
```python
def min_window(s, t):
    # Similar but track minimum
    min_len = float('inf')
    # ... expand-contract logic ...
    min_len = min(min_len, right - left + 1)
    return min_len
```

---

**Q7:** What if you need both length AND the substring itself?

**A:**
```python
def longest_unique_substring(s):
    left = 0
    char_set = set()
    max_len = 0
    max_start = 0
    
    for right in range(len(s)):
        while s[right] in char_set:
            char_set.remove(s[left])
            left += 1
        char_set.add(s[right])
        
        if right - left + 1 > max_len:
            max_len = right - left + 1
            max_start = left
    
    return s[max_start:max_start+max_len]
```

---

## PART 4: README

**90-Minute Study Guide:**
1. The Why (10 min): Understand expansion/contraction
2. The What (15 min): Mental model of variable window
3. The How (15 min): Expand-contract algorithm
4. Visualization (20 min): Trace longest unique example
5. Quick Summary (5 min): Review key points
6. Questions (15 min): Test understanding

**Key Skill:** Recognize when window size varies, implement efficiently

**Practice:** Longest unique substring, minimum window, k distinct characters

**Difficulty:** Hardest pattern so far. Takes time to master but core technique.

**Connection:** Day 1 (two pointers), Day 2 (fixed window) → Day 3 (variable). Each builds intuition for next.

---

**Status:** ✅ Day 3 Complete | **Next:** Day 4 - Prefix Sums

