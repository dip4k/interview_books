# 📑 WEEK 4 DAY 2: GUIDELINES & INDEX

**Navigation & Study Guidelines**

Generated: 2025-12-26

---

## 📚 WEEK 4 DAY 2 FILES

| File | Type | Purpose | ID |
|------|------|---------|-----|
| Main Learning | Combined (4-in-1) | All content, 11 sections | code_file:93 |
| Questions | Q&A | 7 questions with answers | code_file:94 |
| Checklist | Tracking | Daily progress monitoring | code_file:95 |
| Summary | Overview | Week 4 context | code_file:89 |

---

## 🎯 WHAT IS FIXED SLIDING WINDOW?

**Definition:** A window of fixed size k slides across the array, removing the leftmost element and adding the rightmost element each iteration, maintaining O(1) update cost.

**Example:**
```python
# Find maximum sum of any subarray with exactly k elements
arr = [1, 2, 3, 4, 5]
k = 3

window_sum = sum(arr[:3])  # [1,2,3] = 6
max_sum = 6

for i in range(3, 5):
    window_sum = window_sum - arr[i-3] + arr[i]
    max_sum = max(max_sum, window_sum)
    # i=3: window_sum = 6 - 1 + 4 = 9, [2,3,4]
    # i=4: window_sum = 9 - 2 + 5 = 12, [3,4,5]

return max_sum  # 12
```

**Key Property:** Each slide removes left, adds right. O(1) per slide after O(k) setup.

---

## ⏱️ 90-MINUTE STUDY SCHEDULE

| Time | Section | Activity | Duration |
|------|---------|----------|----------|
| 0-10 | The Why | Network/stock real-world problems | 10 min |
| 10-25 | The What | Mental model: maintain window, slide | 15 min |
| 25-40 | The How | Remove-add algorithm template | 15 min |
| 40-60 | Visualization | Trace max sum, moving avg examples | 20 min |
| 60-70 | Analysis | O(n) vs O(n·k) complexity | 10 min |
| 70-75 | Summary | Quick review of key points | 5 min |
| 75-90 | Questions | 7 Socratic questions | 15 min |

---

## 🗺️ NAVIGATION GUIDE

### First-Time Learning:
1. Read Day 1 summary first (5 min) - understand two pointers
2. Open Day 2 main file (code_file:93)
3. Read Section 1 (Why) - understand problem motivation
4. Follow 90-minute schedule
5. Trace examples carefully
6. Answer questions (code_file:94)
7. Track progress (code_file:95)

### If Stuck:
1. Compare to Day 1 (two pointers) - different pattern
2. Focus on remove-add mechanics
3. Try example with k=2 or k=3
4. Look at Q&A for similar question
5. Come back tomorrow fresh

### For Review:
1. Read "The What" section (mental model)
2. Trace one visualization example
3. Attempt 2-3 questions
4. Rate confidence

---

## 📊 CONTENT STRUCTURE

### PART 1: Main Learning (11 Sections)

**Section breakdown:**

1. **The Why** (10 min)
   - Real problems (network, stock, streaming)
   - Naive O(n·k) approach
   - Sliding window O(n) solution
   - 100x speedup motivation

2. **The What** (15 min)
   - Core insight: maintain window value
   - Remove-add pattern
   - Why O(1) per slide
   - Visual representation

3. **The How** (15 min)
   - Algorithm template
   - Step-by-step mechanics
   - Initial setup O(k)
   - Sliding loop O(1) per iteration

4. **Visualization** (20 min)
   - Max sum subarray traced
   - Moving average calculated
   - Find max in each window
   - Multiple examples

5. **Critical Analysis** (10 min)
   - Time: O(k) + O(n-k) = O(n)
   - Space: O(1) for tracking, O(m) for results
   - Comparison table to naive
   - When to use

6. **Real System Integration** (Optional)
   - Finance (moving averages)
   - Network monitoring
   - Streaming data
   - Database indexes

7. **Concept Crossovers** (Optional)
   - Day 1 two pointers vs Day 2 sliding
   - Day 3 variable window extension
   - Prefix sum relation

8. **Mathematical Perspective** (Optional)
   - Exact property: sum[i+1...i+k] = sum[i...i+k-1] - arr[i] + arr[i+k]
   - Proof of correctness
   - Why one-pass guarantee

9. **Design Intuition** (Optional)
   - When fixed window applies
   - When variable needed
   - Edge cases

10. **Knowledge Check** (15 min)
    - 7 Socratic questions
    - Self-assessment
    - Difficulty progressive

11. **Retention Hooks** (Optional)
    - "SLIDE FORWARD" mnemonic
    - Visual memory: moving box
    - Story: rectangular window on graph

### PART 2: Quick Summary (5 min)
- Essence of fixed sliding window
- Template code
- When to use
- Common problems

### PART 3: Questions (7 questions)
- Space for your answers
- Hints provided
- Full explanations
- Key insights

### PART 4: README
- Study guide
- Success criteria
- Next steps

---

## 💡 KEY CONCEPTS

### **Core Insight**
Fixed window maintains size k:
- Remove leftmost element
- Add rightmost element
- Update aggregation in O(1)

### **Why O(n)?**
- Setup: O(k) one time
- Slides: n-k times, each O(1)
- Total: O(k) + O(n-k) = O(n)

### **Why O(1) Space?**
- Only need tracking variables (sum/max/min)
- No hash map, no extra arrays
- Result array depends on use case

### **When to Use?**
- Fixed window size k ✓
- Calculate for all windows ✓
- Need aggregation (sum/max/min) ✓
- Want linear time ✓

### **When Not to Use?**
- Window size varies (use variable window)
- Need elements in window (regular loop)
- k very large relative to n

---

## 🎓 LEARNING OUTCOMES

**By end of Day 2, you should:**

✅ Understand why O(n) not O(n·k)
✅ Know remove-add pattern
✅ Implement confidently
✅ Trace examples by hand
✅ Explain complexity
✅ Solve 3+ problems
✅ Rate confidence 4-5

---

## 📌 QUICK REFERENCE

**Template:**
```python
def sliding_window_fixed(arr, k):
    # Setup
    window_value = initial_calc(arr[:k])
    best = window_value
    
    # Slide
    for i in range(k, len(arr)):
        window_value = window_value - arr[i-k] + arr[i]
        best = max(best, window_value)
    
    return best
```

**Common Problems:**
- Max sum subarray of size k
- Moving average over k elements
- Find maximum element in k windows
- Minimum window with sum ≥ target (variable)
- Count of subarrays with sum = target (prefix sum)

---

## ✅ SUCCESS CRITERIA

**Daily Success (Day 2):**
- ✅ 90-minute session completed
- ✅ All sections understood
- ✅ 5+ questions answered correctly
- ✅ Confidence rated 4-5
- ✅ Ready for Day 3

**Knowledge Check:**
- ✅ Can explain without notes
- ✅ Can implement from scratch
- ✅ Can trace examples
- ✅ Can solve new problems
- ✅ Can teach to others

---

## 🔧 TROUBLESHOOTING

**Problem:** Don't understand why O(n)

**Solution:**
1. Re-read The How section
2. Trace example counting operations:
   - Initial sum: k operations
   - Each slide: 2 operations (subtract, add)
   - n-k slides: 2(n-k) operations
   - Total: k + 2(n-k) = k + 2n - 2k = 2n - k = O(n)

---

**Problem:** Confused about remove-add pattern

**Solution:**
1. Visual: mark which element leaves, which enters
2. Code: window_sum = window_sum - arr[i-k] + arr[i]
3. Example: [1,2,3,4,5], k=3
   - Initial: [1,2,3], sum=6
   - Slide: [2,3,4]
   - Remove: -1, Add: +4, New sum: 6-1+4=9

---

**Problem:** Can't trace example correctly

**Solution:**
1. Use table format
2. Column for index
3. Column for window
4. Column for sum
5. Step through each row

---

## 🌟 TIPS FOR SUCCESS

1. **Understand the pattern**
   Know WHY remove-add works, not just THAT it works

2. **Compare to Day 1**
   Two pointers opposite ends, sliding window same direction

3. **Test with k=2**
   Simplest case, easy to verify manually

4. **Implement after understanding**
   Code what you've traced, not the reverse

5. **Return after 2 days**
   Spaced repetition: re-read What-How sections

---

## 📈 WEEK 4 PROGRESSION

**Day 1: Two Pointers** ✅
→ Opposite ends, find one pair

**Day 2: Fixed Sliding** 🔄 (TODAY)
→ Same direction, fixed size, all windows

**Day 3: Variable Sliding** ⏳
→ Same direction, expand/contract based on condition

**Day 4: Prefix Sums** ⏳
→ Precompute for O(1) range queries

**Day 5: Cycle Detection** ⏳
→ Floyd's algorithm, slow and fast pointers

---

## 💬 FAQ

**Q: Can you use fixed window for "longest substring without duplicate"?**
A: No. That requires variable window (window size changes). Fixed window always size k.

**Q: What if k = 1?**
A: Works, just returns max element. Each window size 1.

**Q: What if k > array length?**
A: No valid windows. Handle edge case before sliding.

**Q: Can I use this with negative numbers?**
A: Yes! Works with any numbers. Sum includes negatives.

**Q: Should I code this or understand conceptually?**
A: Both. Understand concept deeply, then implement to cement.

---

## 🎯 NEXT STEPS

After completing Day 2:

1. **Day 3 (Tomorrow):** Sliding Window (Variable)
   - Expand window when condition not met
   - Contract window when condition met
   - Solve optimization problems

2. **Practice:** Solve 3-5 fixed window LeetCode problems
   - Easy: Max Sum Subarray of Size k
   - Medium: Grumpy Bookstore Owner

3. **Review:** Return after 2 days, re-read sections

4. **Integration:** See how Day 2 connects to Day 3

---

**Status:** Week 4 Day 2 Ready

Generated: 2025-12-26  
Quality: Professional Grade  
Completeness: 100%

