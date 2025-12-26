# Week 4 Day 2: Sliding Window Technique - Dynamic Window Patterns

## 🗓 Metadata
**Topic:** Sliding Window Technique  
**Week:** Week 4  
**Day:** Day 2 of 5  
**Category:** Array/String Manipulation  
**Difficulty:** 🟡 Medium  
**Status:** 🔍 In Study  
**Last Reviewed:** —  
**Confidence Level (1–5):** —/5  

---

## 1️⃣ The Why — Engineering Motivation

### Real-World Problem

**Find the longest substring without repeating characters.**

```
String: "abcabcbb"
Answer: "abc" (length 3)

Why not longer?
- "abca" has 'a' repeated
- "abcab" has 'a' and 'b' repeated
- "abc" is longest unique substring
```

**Naive approach (O(n³)):**
```
for i in range(n):
    for j in range(i, n):
        substring = s[i:j+1]
        if all unique:
            update max length
```

**Problem:** Check all substrings = O(n²) pairs × O(n) uniqueness check = O(n³)

**Better approach (O(n)):**
```
Use sliding window with two pointers
left = 0
char_count = {}

for right in range(n):
    char = s[right]
    char_count[char] += 1
    
    while char_count[char] > 1:  # Duplicate found
        left_char = s[left]
        char_count[left_char] -= 1
        left += 1
    
    max_length = max(max_length, right - left + 1)
```

**This is sliding window!** Dynamic window expands and contracts based on conditions.

### Why This Matters

**Sliding window:**
1. **Optimizes substring/subarray problems from O(n²/n³) to O(n)**
2. **Extends two pointers** with dynamic resizing
3. **Works on unsorted data** (unlike two pointers)
4. **Fundamental pattern** for many real problems

---

## 2️⃣ The What — Mental Model & Intuition

### Core Analogy: Sliding Glass Window

**Imagine a glass window on a long wall.**

```
Wall (data): [a][b][c][a][b][c][b][b]

Glass window (window size varies):
Position 1: [a][b][c]
            ↑ left, ↑ right (window = 3)

"Does window contain any repeating characters?"
Answer: NO, unique letters

Move right edge:
Position 2:    [b][c][a]
               ↑         ↑ (window = 3)

"Does window contain repeating characters?"
Answer: NO

Move right edge:
Position 3:       [c][a][b]
                  ↑         ↑ (window = 3)

"Does window contain repeating characters?"
Answer: NO

Move right edge:
Position 4:          [a][b][c][b]
                     ↑            ↑ (window = 4)

"Does window contain repeating characters?"
Answer: YES ('b' appears twice)

Shrink from left:
Position 5:             [b][c][b]
                        ↑       ↑ (window = 3)

"Now unique?" Answer: NO

Shrink from left:
Position 6:                [c][b]
                           ↑     ↑ (window = 2)

"Now unique?" Answer: YES

Continue...
```

**Key insight:** Window expands when valid, shrinks when invalid.

### Mental Model: Elastic Band

```
Data:     [1, 2, 3, 4, 5, 6]
          
Expand when:   Condition satisfied ✓
Shrink when:   Condition violated ✗

Window moves across array exactly once:
- Left pointer moves right only
- Right pointer moves right only
- No backward movement

Result: O(n) time (each element touched ≤ 2 times)
```

### Why Window Slides (Not Nested Loops)

**Nested loops (O(n²)):**
```
for i in range(n):
    for j in range(i, n):
        process substring[i:j+1]
```

**Sliding window (O(n)):**
```
The key insight: 
When we expand window from [i,j] to [i, j+1],
we don't recalculate everything from scratch.

We just add element at j+1 to existing calculation!

Example (sum of subarrays):
[i, j] sum = 10
[i, j+1] sum = 10 + arr[j+1]  ← Incremental update!
```

This incremental approach avoids redundant work.

---

## 3️⃣ The How — Mechanical Walkthrough

### Sliding Window Template

```python
def sliding_window(arr, condition):
    left = 0
    result = 0
    window_data = {}  # or set, or counter
    
    for right in range(len(arr)):
        # Add right element to window
        window_data[arr[right]] += 1
        
        # Shrink window while condition violated
        while is_invalid(window_data):
            window_data[arr[left]] -= 1
            left += 1
        
        # Update result (window is now valid)
        result = max(result, right - left + 1)
    
    return result
```

### Example 1: Longest Substring Without Repeating

**Problem:** Find longest substring with all unique characters

```python
def longest_substring_without_repeating(s):
    char_count = {}
    left = 0
    max_length = 0
    
    for right in range(len(s)):
        # Add right character
        char = s[right]
        char_count[char] = char_count.get(char, 0) + 1
        
        # Shrink window if duplicate
        while char_count[char] > 1:
            left_char = s[left]
            char_count[left_char] -= 1
            left += 1
        
        # Update max length (window is unique)
        max_length = max(max_length, right - left + 1)
    
    return max_length

# Trace
s = "abcabcbb"
right=0, char='a': count={'a':1}, window="a", len=1
right=1, char='b': count={'a':1,'b':1}, window="ab", len=2
right=2, char='c': count={'a':1,'b':1,'c':1}, window="abc", len=3
right=3, char='a': count={'a':2,'b':1,'c':1}
  → Duplicate! Shrink:
  left=0, char='a': count={'a':1,'b':1,'c':1}, left=1
  window="bca", len=3
right=4, char='b': count={'a':1,'b':2,'c':1}
  → Duplicate! Shrink:
  left=1, char='b': count={'a':1,'b':1,'c':1}, left=2
  window="cab", len=3
right=5, char='c': count={'a':1,'b':1,'c':2}
  → Duplicate! Shrink:
  left=2, char='c': count={'a':1,'b':1,'c':1}, left=3
  window="abc", len=3
right=6, char='b': count={'a':1,'b':2,'c':1}
  → Duplicate! Shrink:
  left=3, char='a': count={'a':0,'b':2,'c':1}, left=4
  left=4, char='b': count={'a':0,'b':1,'c':1}, left=5
  window="cb", len=2
right=7, char='b': count={'a':0,'b':2,'c':1}
  → Duplicate! Shrink:
  left=5, char='c': count={'a':0,'b':2,'c':0}, left=6
  left=6, char='b': count={'a':0,'b':1,'c':0}, left=7
  window="b", len=1

Max length found: 3 ✓
```

### Example 2: Minimum Window Substring

**Problem:** Find smallest window in S containing all characters of T

```
S = "ADOBECODEBANC"
T = "ABC"
Output: "BANC"
```

```python
def min_window_substring(s, t):
    if not t or not s:
        return ""
    
    # Count characters needed
    dict_t = {}
    for char in t:
        dict_t[char] = dict_t.get(char, 0) + 1
    
    formed = 0  # How many unique chars in t have desired count in window
    required = len(dict_t)  # Number of unique characters in t
    
    window_counts = {}
    
    # Left and right pointers
    left = 0
    
    # Result: (window length, left, right)
    result = float("inf"), None, None
    
    for right in range(len(s)):
        # Add character from right
        char = s[right]
        window_counts[char] = window_counts.get(char, 0) + 1
        
        # Check if character count reaches required count
        if char in dict_t and window_counts[char] == dict_t[char]:
            formed += 1
        
        # Try to shrink window from left
        while left <= right and formed == required:
            char = s[left]
            
            # Save result if smaller
            if right - left + 1 < result[0]:
                result = (right - left + 1, left, right)
            
            # Remove left character
            window_counts[char] -= 1
            if char in dict_t and window_counts[char] < dict_t[char]:
                formed -= 1
            
            left += 1
    
    # Return substring or empty if not found
    return "" if result[0] == float("inf") else s[result[1]:result[2]+1]

# Trace abbreviated
S = "ADOBECODEBANC"
T = "ABC"

right expands to include all characters
left shrinks while window is valid
Result: "BANC"
```

### Example 3: Maximum Sum of Subarray of Size K

**Problem:** Find maximum sum of any contiguous subarray of size k

```python
def max_sum_subarray(arr, k):
    if k > len(arr):
        return None
    
    # Calculate sum of first window
    window_sum = sum(arr[:k])
    max_sum = window_sum
    
    # Slide window
    for right in range(k, len(arr)):
        # Remove leftmost element, add rightmost
        window_sum = window_sum - arr[right - k] + arr[right]
        max_sum = max(max_sum, window_sum)
    
    return max_sum

# Trace
arr = [2, 1, 5, 1, 3, 2]
k = 3

Window 1: [2, 1, 5] sum = 8
Window 2: [1, 5, 1] sum = 8 - 2 + 1 = 7
Window 3: [5, 1, 3] sum = 7 - 1 + 3 = 9
Window 4: [1, 3, 2] sum = 9 - 5 + 2 = 6

Max sum: 9 ✓
```

---

## 4️⃣ Visualization — Examples & Trace

### Visual Trace: Longest Substring Without Repeating

```
String: "dvdf"

Step 1:
[d v d f]
 L R
window = "dv"
count = {'d':1, 'v':1}
Unique ✓, len = 2

Step 2:
[d v d f]
 L   R
window = "dvd"
count = {'d':2, 'v':1}
Duplicate! Shrink from left

Step 3:
[d v d f]
   L R
window = "vd"
count = {'d':1, 'v':1}
Unique ✓, len = 2

Step 4:
[d v d f]
   L   R
window = "vdf"
count = {'d':1, 'v':1, 'f':1}
Unique ✓, len = 3 ← New max!

Answer: 3 (substring "vdf")
```

### Visual Trace: Minimum Window Substring

```
S = "ADOBECODEBANC"
T = "ABC"

Expand right to include A, B, C:
[A D O B E C...]
 L           R

Window has all characters

Shrink left to find minimum:
[... O B E C O D E B A N C]
         L       R

"BANC" found ✓ (size 4)

No smaller valid window exists
```

### Visual Trace: Maximum Sum Subarray (k=3)

```
Array: [2, 1, 5, 1, 3, 2]
k = 3

Window 1:
[2, 1, 5] 1, 3, 2
 -------
sum = 8

Slide right:
2, [1, 5, 1] 3, 2
    -------
sum = 8 - 2 + 1 = 7

Slide right:
2, 1, [5, 1, 3] 2
       -------
sum = 7 - 1 + 3 = 9 ← Max!

Slide right:
2, 1, 5, [1, 3, 2]
          -------
sum = 9 - 5 + 2 = 6

Maximum sum = 9
```

---

## 5️⃣ Critical Analysis — Performance & Robustness

### Time Complexity Analysis

**Sliding window:** O(n)

Why? Despite two pointers (left, right), each element touched at most twice:
```
Right pointer: moves from 0 to n-1 (n moves)
Left pointer: moves from 0 to n-1 once total (n moves)

Total work: 2n = O(n)
```

**Compared to nested loops O(n²):**
```
n = 1,000:     O(n²) = 1M operations
               O(n) = 2K operations
               500× speedup!

n = 10,000:    O(n²) = 100M operations
               O(n) = 20K operations
               5,000× speedup!
```

### Space Complexity

**Variable by approach:**

```
Basic sliding window: O(1) space
  Just left, right, result

With counter/hash: O(k) space where k = unique elements
  Worst case: O(n) if all unique

With hash table: O(alphabet size) = O(26) for lowercase English
```

### When Sliding Window Works

**Condition 1: Need to find optimal subarray/substring**
```
✓ Longest/shortest substring with property
✓ Maximum/minimum sum subarray
✓ Window with specific count of elements
```

**Condition 2: Can incrementally update**
```
✓ Adding element doesn't require full recalculation
✓ Removing element updates incrementally
✓ Examples: Sum, count, frequency
```

**Condition 3: Monotonic window validity**
```
When window is invalid, growing it further won't help
When window is valid, shrinking might find better

Example (unique characters):
"aab" is invalid (duplicate 'a')
"aabc" is still invalid (duplicate 'a')
Must shrink to fix

vs "aac" is invalid
"aac" might become valid, or might not
Must understand direction of fixing
```

### Edge Cases

**Edge Case 1: Empty string**
```
s = ""
left=0, right loop doesn't execute
max_length = 0 ✓
```

**Edge Case 2: All same characters**
```
s = "aaaa"
right=0: "a", len=1
right=1: "aa", char_count['a']=2 → shrink to "a", len=1
right=2: "aa" → shrink to "a", len=1
right=3: "aa" → shrink to "a", len=1
Answer: 1 ✓
```

**Edge Case 3: Window size larger than array**
```
arr = [1,2,3]
k = 5
Can't form window of size 5
Return None or 0
```

---

## 6️⃣ Real System Integration

### Where Sliding Window Appears

**Network packet processing:**
```
Stream of packets arriving
Process in windows of fixed size
Calculate statistics (average, max, min) per window
```

**Time-series analysis:**
```
Stock prices arriving in real-time
Calculate 50-day moving average
Window slides: remove oldest price, add newest

price = [100, 102, 98, 105, ...]
Window[0:50] average
Window[1:51] average = (average - price[0] + price[50]) / 50
```

**DNA pattern matching:**
```
Find substring in DNA sequence
Use sliding window to find patterns efficiently
```

**View count on YouTube:**
```
Track last 1M views (sliding window of time)
When new view arrives, remove view from 1M+ seconds ago
Calculate trend in current window
```

---

## 7️⃣ Concept Crossovers

### Builds On (Week 3)

**Sorting:** Pre-sorted data enables more sliding window optimizations

**Hash Tables:** Used internally in sliding window to track window contents

### Builds On (Week 4 Day 1)

**Two Pointers:** Sliding window extends with dynamic resizing

### Builds Toward (Week 4 Days 3-5)

**Prefix Sums:** Alternative approach to some sliding window problems

---

## 8️⃣ Mathematical & Theoretical Perspective

### Proof: Sliding Window Finds Optimal Solution

**Claim:** Sliding window finds optimal subarray/substring in O(n) time.

**Proof (longest substring without repeating):**

```
We want to prove that sliding window finds the longest substring
with all unique characters.

Key property: If [left, right] has a duplicate,
then any substring containing it also has that duplicate.

Proof that we don't miss the optimal:

Suppose optimal answer is [i, j] with length L

When our right pointer reaches j:
- All elements [0, j] have been considered
- Our left pointer is at some position ≤ i

Case 1: left < i
Then [left, j] contains [i, j] as a substring
If [i, j] is valid (no duplicates), then [left, j] is invalid
Unless left >= i... but left < i, so [left, j] has duplicates
before position i, or left has already passed position i.

Case 2: left = i  
Then [left, j] = [i, j]
If [i, j] is valid, our algorithm records length L

Case 3: left > i
This means our algorithm found duplicates in [i, j]
But [i, j] is supposed to be valid → Contradiction!

Therefore, our algorithm must encounter and record [i, j].
```

### Why Incremental Updates Work

**Key mathematical insight:**

```
For associative operations (sum, count, max with multiset),
we can update incrementally:

Remove leftmost element:
  new_value = old_value - leftmost_value

Add rightmost element:
  new_value = new_value + rightmost_value

Operations that work:
✓ Sum (sum -= arr[left], sum += arr[right])
✓ Product (product /= arr[left], product *= arr[right])
✓ Max count (for duplicates tracking)
✓ Frequency map

Operations that DON'T work:
✗ Max/Min in window (must recalculate)
✗ XOR with specific requirements
✗ Modulo operations (context-dependent)
```

---

## 9️⃣ Algorithmic Design Intuition

### Decision Framework

**When to use sliding window:**

```
Does problem ask for subarray/substring property?
  ├─ YES → Consider sliding window
  ├─ NO  → Try other approaches
  └─ Examples: longest, shortest, maximum, minimum

Can you incrementally update the metric?
  ├─ YES → Sliding window works ✓
  ├─ NO  → Might need segment tree or other structure
  └─ Examples: sum, count, frequency map

Is data ordered / ordered matters?
  ├─ YES → Sliding window natural
  ├─ NO  → Might still help with proper structure
  └─ For ordered: window preserves order

Can window expand and contract?
  ├─ YES → Flexible sliding window ✓
  ├─ NO  → Fixed-size window (simpler)
  └─ Most interesting problems: flexible size
```

### Pattern Recognition

**Pattern 1: Find longest/shortest with property**
```
Expand right for longest, shrink left when invalid
Longest substring without repeating
Shortest substring containing all characters
```

**Pattern 2: Fixed-size window computation**
```
Slide window of fixed size k
Update by: remove leftmost, add rightmost
Maximum sum subarray of size k
Average in sliding window
```

**Pattern 3: Two conditions**
```
Window valid when meets condition1 and not condition2
Expand when condition1 not met
Shrink when condition2 violated
At most K distinct elements
```

---

## 🔟 Knowledge Check — Socratic Reasoning

**Question 1: Why is sliding window O(n) and not O(n²)?**

Think: Each element processed how many times? Why don't we restart calculations?

**Question 2: When should you expand the window vs shrink it?**

Think: What conditions require expanding? What conditions require shrinking?

**Question 3: Why does sliding window need the window data to be "incrementally updatable"?**

Think: What happens if you can't incrementally update (like max/min)?

**Question 4: How is sliding window different from two pointers?**

Think: Can window size change? Does it always start from opposite ends?

**Question 5: Can you use sliding window on unsorted data?**

Think: Compare to two pointers requirement. What's the key difference?

---

## 1️⃣1️⃣ Retention Hook — Memory Anchors

### One-Line Essence

> **Sliding window: Dynamically expand/contract a window across array/string to find optimal subarray in O(n) time. Key: incremental updates allow constant-time changes.**

### Mnemonic: "WINDOW"

- **W**indow expands right
- **I**ncremental updates (not recalculating)
- **N**umber of elements: left to right
- **D**yamic size (expands and contracts)
- **O**ptimal subarray found
- **W**hen valid, record; when invalid, shrink

### Visual Anchor

```
Expanding (need more elements): Right moves right
Shrinking (condition violated): Left moves right

Both only move right! (never move left/backward)
This guarantees O(n) total movement
```

---

## 📚 Supplementary Data

### Sliding Window vs Other Approaches

| Approach | Time | Space | When |
|----------|------|-------|------|
| Nested loops | O(n²) | O(1) | Brute force baseline |
| Sliding window | O(n) | O(k) | Problems with monotonic validity |
| Segment tree | O(n log n) | O(n) | Range queries with updates |
| Hash table | O(n) | O(n) | Frequency/counting problems |

### Common Sliding Window Problems

**Type 1: Longest/Shortest with condition**
```
Longest substring without repeating
Longest substring with at most K distinct characters
Shortest substring containing all characters
Minimum window substring
```

**Type 2: Fixed-size window**
```
Maximum sum of subarray of size K
Sliding window maximum
Average of subarrays of size K
```

**Type 3: Two conditions**
```
At most K distinct elements
All elements appear at least M times
Contains target count of specific element
```

---

## 🔗 External References

1. **Interactive Visualizer:**
   - Algorithm Visualizer: https://algorithm-visualizer.org/

2. **LeetCode Problems:**
   - Longest Substring Without Repeating: https://leetcode.com/problems/longest-substring-without-repeating-characters/
   - Minimum Window Substring: https://leetcode.com/problems/minimum-window-substring/
   - Max Consecutive Ones III: https://leetcode.com/problems/max-consecutive-ones-iii/

3. **Related Concepts:**
   - Two Pointers (Week 4 Day 1)
   - Hash Tables (Week 3)
   - Frequency counting

---

## 📋 Summary

**Sliding Window Key Facts:**
✅ O(n) time, O(k) space (k = window elements)  
✅ Works on both sorted and unsorted data  
✅ Requires incrementally updatable metrics  
✅ Window expands and contracts dynamically  
✅ Every element processed at most twice  

**When to use:**
- Find optimal subarray/substring ✓
- Metric is incrementally updatable ✓
- Problem has monotonic validity property ✓
- Need O(n) solution ✓

**When NOT to use:**
- Metric not incrementally updatable (max/min) ✗
- Need all subarrays, not optimal one ✗
- Problem requires pre-sorting (use sort first) ✗

---

**Word Count:** ~3,000 words  
**Reading Time:** 85-95 minutes  
**Status:** ✅ Complete with all 11 sections + supplementary material

