# Week 4.5: Q&A - 30 Socratic Questions with Detailed Answers

**10 Questions per Day × 3 Days = 30 Total Questions**

---

## 📅 DAY 1: BINARY SEARCH (10 Questions)

### Q1.1: Why can't you use binary search on unsorted arrays?

**Difficulty:** ⭐ Easy

**Answer:**
Binary search assumes: left half has smaller values, right half has larger values. On unsorted arrays, this assumption breaks. Example: [5,1,9,3,7], middle is 9. Going left/right doesn't guarantee direction. Need sorted data for directional confidence.

---

### Q1.2: Why is binary search O(log n) and not O(n)?

**Difficulty:** ⭐ Easy

**Answer:**
Each iteration eliminates half of remaining elements. Starting with n elements:
- After 1 iteration: n/2 elements
- After 2 iterations: n/4 elements
- After k iterations: n/2^k elements

To reach 1 element: n/2^k = 1, so k = log₂(n). Total iterations: O(log n).

---

### Q1.3: Trace binary search on [1,3,5,7,9,11], target=7

**Difficulty:** ⭐ Medium

**Answer:**
```
left=0, right=5, mid=2: arr[2]=5, 5 < 7, left=3
left=3, right=5, mid=4: arr[4]=9, 9 > 7, right=3
left=3, right=3, mid=3: arr[3]=7, 7 == 7 → FOUND! ✓
```

---

### Q1.4: What's the advantage of binary search vs hash table?

**Difficulty:** ⭐⭐ Medium

**Answer:**
Hash table: O(1) average, O(n) space. Better for exact match.
Binary search: O(log n) time, O(1) space. Better when:
- Space is critical
- Data already sorted
- Need first/last/nearest element
- Answer space searching

---

### Q1.5: How do you find first occurrence with duplicates?

**Difficulty:** ⭐⭐ Medium

**Answer:**
When you find target, don't return immediately. Instead, continue searching left:
```
if arr[mid] == target:
    result = mid  # Remember position
    right = mid - 1  # Keep searching left
```

Eventually will land on first occurrence.

---

### Q1.6: What's "answer space searching"?

**Difficulty:** ⭐⭐ Medium

**Answer:**
Instead of searching array elements, search range of possible answers.

Example: "Minimum eating speed for Koko to finish h hours"
```
Don't search banana piles
Search eating speeds [1 to max(piles)]
For each speed, check if valid (takes ≤ h hours)
Binary search finds minimum valid speed
```

---

### Q1.7: Why mid = (left + right) // 2 instead of / 2.0?

**Difficulty:** ⭐⭐ Medium

**Answer:**
Integer division avoids floating point. Also avoids overflow: (left + right) can overflow. Better: mid = left + (right - left) // 2.

---

### Q1.8: Can you binary search linked lists?

**Difficulty:** ⭐⭐ Medium

**Answer:**
Technically no. Binary search needs O(1) random access. Linked lists have O(n) access. Cost of finding mid = O(n), making binary search O(n log n) total. Use linear search instead.

---

### Q1.9: How to search in rotated sorted array?

**Difficulty:** ⭐⭐ Hard

**Answer:**
One half is always sorted. Find which half, check if target is in that sorted half, search accordingly.

```
if arr[left] <= arr[mid]:  # Left sorted
    if arr[left] <= target < arr[mid]:
        right = mid - 1  # Target in left
    else:
        left = mid + 1   # Target in right
```

---

### Q1.10: Why need left <= right condition vs left < right?

**Difficulty:** ⭐⭐ Medium

**Answer:**
left < right would exit when left==right (single element). Need one more check on that element.
left <= right continues to check when single element remains.

```
Difference:
left < right: [1,2,3] searching for 1
  Mid=2(value 2), go left. left=0, right=0. Exit! Never checked 1.
  
left <= right: 
  Mid=2(value 2), go left. left=0, right=0. Check again! Found 1 ✓
```

---

## 📅 DAY 2: BIT MANIPULATION (10 Questions)

### Q2.1: Why does n & (n-1) remove rightmost set bit?

**Difficulty:** ⭐ Easy

**Answer:**
When you subtract 1:
- All bits right of rightmost 1 flip (0→1)
- The rightmost 1 becomes 0

AND operation keeps only matching 1s, so rightmost 1 disappears.

```
n = 1100
n-1 = 1011
AND = 1000 (rightmost 1 gone) ✓
```

---

### Q2.2: What's the difference between AND and OR?

**Difficulty:** ⭐ Easy

**Answer:**
AND: Both must be 1 to produce 1
OR: At least one must be 1 to produce 1

```
1001 & 0110 = 0000
1001 | 0110 = 1111
```

---

### Q2.3: Why is XOR useful for duplicates?

**Difficulty:** ⭐ Easy

**Answer:**
XOR has special property: a ^ a = 0, a ^ 0 = a

So duplicates cancel! If array has all duplicates except one:
```
a ^ b ^ a ^ c ^ b = (a ^ a) ^ (b ^ b) ^ c = 0 ^ 0 ^ c = c ✓
```

---

### Q2.4: How to check if bit k is set in number n?

**Difficulty:** ⭐ Medium

**Answer:**
```
(n & (1 << k)) != 0
```

Create mask with 1 at position k, AND with n. If result non-zero, bit was set.

---

### Q2.5: How to set bit k in number n?

**Difficulty:** ⭐ Medium

**Answer:**
```
n | (1 << k)
```

OR with mask of 1 at position k. OR always sets to 1 (doesn't affect other bits).

---

### Q2.6: How to clear (set to 0) bit k in number n?

**Difficulty:** ⭐⭐ Medium

**Answer:**
```
n & ~(1 << k)
```

Create mask with 1 at position k, flip it (~), AND with n. Clears only bit k.

---

### Q2.7: How to count number of set bits (1s)?

**Difficulty:** ⭐⭐ Medium

**Answer:**
Approach 1: Check last bit, right shift
```
count = 0
while n:
    count += n & 1
    n >>= 1
```

Approach 2: Brian Kernighan - n & (n-1) removes one bit each time
```
count = 0
while n:
    n &= n - 1
    count += 1
```

---

### Q2.8: What does 1 << k represent?

**Difficulty:** ⭐ Easy

**Answer:**
2^k (2 to the power k). Shift 1 left by k positions = multiply by 2^k.

```
1 << 0 = 1 = 2^0
1 << 1 = 2 = 2^1
1 << 2 = 4 = 2^2
1 << 3 = 8 = 2^3
```

---

### Q2.9: How to check if number is power of 2?

**Difficulty:** ⭐⭐ Medium

**Answer:**
```
n > 0 && (n & (n-1)) == 0
```

Power of 2 has exactly one bit set. n & (n-1) removes that bit, result = 0.

---

### Q2.10: What about negative numbers in bit operations?

**Difficulty:** ⭐⭐⭐ Hard

**Answer:**
Languages handle differently:
- Python: Unlimited bits, automatically handles
- Java/C++: Two's complement, sign extension possible

Example: -1 in 32-bit is all 1s (11111111...)
Right shift might extend sign bit.

Use >>> (unsigned right shift) to avoid issues.

---

## 📅 DAY 3: INTEGRATION (10 Questions)

### Q3.1: When would you combine binary search with sliding window?

**Difficulty:** ⭐⭐ Medium

**Answer:**
Rarely. Sliding window finds candidates, but binary search doesn't naturally optimize its bounds.

Exception: If you can binary search window size (fixed window problems).

---

### Q3.2: How do binary search and two pointers relate?

**Difficulty:** ⭐⭐ Medium

**Answer:**
Both work on sorted data and find elements O(log n) or O(n).
- Binary search: Divide in half each iteration
- Two pointers: Converge from ends

Different strategies, complementary uses.

---

### Q3.3: Why combine binary search with prefix sums?

**Difficulty:** ⭐⭐ Medium

**Answer:**
Binary search on prefix array values! Example:
```
Find smallest prefix sum ≥ target
Binary search on prefix array

Or: Find subarray with sum ≤ k
Binary search positions in prefix
```

---

### Q3.4: When would bit manipulation matter in larger algorithm?

**Difficulty:** ⭐⭐ Medium

**Answer:**
Space-critical or performance-critical sections:

```
Instead of 8 booleans (8 bytes):
Use 1 byte with 8 bits (1 byte)

In large dataset: 8× space savings
In tight loop: O(1) permission checks
```

---

### Q3.5: How to decide when to combine techniques?

**Difficulty:** ⭐⭐ Hard

**Answer:**
1. Can single technique solve it? Yes → Use it, keep simple
2. Single technique insufficient? Yes → Consider combining
3. Do techniques synergize? Yes → Combine!
4. Total complexity acceptable? Yes → Use combination
5. Code maintainability OK? Yes → Finalize

---

### Q3.6: What makes "answer space searching" work?

**Difficulty:** ⭐⭐ Medium

**Answer:**
Answer space must be:
1. Sorted/ordered (to binary search)
2. Monotonic in validity (larger answer usually valid if smaller is)

Example: Eating speed
- If speed 4 works, speed 5+ work too (monotonic)
- Binary search finds minimum valid speed

---

### Q3.7: How would you solve "kth smallest in rotated array" using Week 4.5?

**Difficulty:** ⭐⭐⭐ Hard

**Answer:**
1. Binary search finds rotation point
2. Adjust k by rotation offset
3. Return element at adjusted position

Combines binary search (find pivot) with array indexing (map to correct position).

---

### Q3.8: Can you always use integration when techniques work separately?

**Difficulty:** ⭐⭐ Medium

**Answer:**
No. Integration helps when:
- Techniques complement each other
- Overall complexity improves
- Code clarity maintained

Combining wrong techniques can hurt. Example: Sliding window + two pointers don't naturally combine.

---

### Q3.9: What's the relationship between problem constraints and technique choice?

**Difficulty:** ⭐⭐⭐ Hard

**Answer:**
Constraints guide technique:
- Sorted data? → Binary search possible
- Need O(log n)? → Binary search
- Space critical? → Bit manipulation, two pointers (O(1))
- Multiple queries? → Prefix sums (preprocess once)
- Subarray property? → Sliding window
- Multiple targets? → Advanced two pointers

---

### Q3.10: How to practice integration effectively?

**Difficulty:** ⭐ Easy

**Answer:**
1. **Problem first:** Read problem, identify constraints
2. **Technique brainstorm:** List applicable techniques
3. **Evaluate:** Which best? Any synergies?
4. **Implement:** Code, trace, test
5. **Reflect:** Why this approach? What else could work?

Repeat until pattern recognition is automatic.

---

## 📋 Self-Assessment

**After answering all 30 questions:**

- [ ] Confidence 1-2/5: Review relevant sections deeply
- [ ] Confidence 3/5: Understand concepts, gaps remain
- [ ] Confidence 4/5: Good understanding, ready to practice
- [ ] Confidence 5/5: Mastered all topics ✓ Ready for Week 5!

---

**Total Questions:** 30  
**Estimated Time:** 2-3 hours to work through  
**Success Criteria:** Confident answers to 80%+ of questions  

**Ready for Week 5?** Check confidence levels above!

