# 📑 WEEK 4.5: GUIDELINES & INDEX

**Navigation & Study Guidelines - Critical Patterns Bridge**

Generated: 2025-12-26

---

## 📚 WEEK 4.5 FILES OVERVIEW

| File | Type | Purpose | Duration | ID |
|------|------|---------|----------|-----|
| Day 1 Learning | Combined (4-in-1) | Hash Map/Set, 11 sections | 90 min | code_file:109 |
| Day 2 Learning | Combined (4-in-1) | Monotonic Stack, 11 sections | 90 min | code_file:110 |
| Day 3 Learning | Combined (4-in-1) | Merge Operations, 11 sections | 90 min | code_file:111 |
| Day 4 Learning | Combined (4-in-1) | Partition & Kadane's, 11 sections | 90 min | code_file:112 |
| Guidelines | Navigation | This file + study structure | — | code_file:113 |
| Questions | Q&A | 7 questions × 4 days = 28 Q&A | — | code_file:114 |
| Checklist | Tracking | Daily progress + week review | — | code_file:115 |

---

## 🎯 WHAT IS WEEK 4.5?

**The Critical Bridge Between Week 4 and Week 5**

Week 4 taught you **pointer movement patterns** (2-pointer, sliding windows, prefix sums, cycle detection).

Week 4.5 teaches you **data structure operations & algorithmic patterns** that are **essential prerequisites** for Week 5.

**Without Week 4.5:** You solve 40-50% of interview problems  
**With Week 4.5:** You solve 70-80% of interview problems  
**With 4 + 4.5 + 5:** You solve 85-90% of interview problems

---

## ⏱️ 90-MINUTE STUDY SCHEDULE (Per Day)

| Time | Section | Activity | Duration |
|------|---------|----------|----------|
| 0-10 | The Why | Real-world motivation | 10 min |
| 10-25 | The What | Mental model & concept | 15 min |
| 25-40 | The How | Implementation mechanics | 15 min |
| 40-60 | Visualization | Trace examples carefully | 20 min |
| 60-70 | Analysis | Complexity & comparison | 10 min |
| 70-75 | Summary | Key insights | 5 min |
| 75-90 | Questions | Socratic questions | 15 min |

---

## 🗺️ NAVIGATION GUIDE

### **First Time Learning (All 4 Days)**

**Day 1: Saturday - Hash Map/Set**
1. Read guidelines (5 min) - context
2. Open code_file:109
3. Follow 90-minute schedule
4. Trace examples (critical!)
5. Answer 7 questions
6. Light review before sleep

**Day 2: Sunday - Monotonic Stack**
1. Quick review Day 1 (5 min)
2. Open code_file:110
3. Understand "monotonic" concept
4. Trace next greater example multiple times
5. Answer 7 questions
6. Connect to Week 4 patterns

**Day 3: Monday - Merge Operations**
1. Quick review Days 1-2 (5 min)
2. Open code_file:111
3. Focus on two-pointer merge
4. Trace multiple examples
5. Answer 7 questions
6. Appreciate O(n) optimization

**Day 4: Tuesday - Partition & Kadane's**
1. Quick review Days 1-3 (10 min)
2. Open code_file:112
3. Learn partition first (easier)
4. Then Kadane's algorithm
5. Answer 7 questions
6. Complete Week 4.5 checklist

### **If Stuck on Specific Pattern**

**Hash Map Problem:**
- Review Q1-Q7 in code_file:114
- Focus on space-time tradeoff
- Understand hash function concept

**Monotonic Stack Problem:**
- Review visualization section
- Trace [2, 1, 2, 4, 3] by hand
- Understand why O(n) amortized

**Merge Problem:**
- Review two-pointer concept from Week 4
- Trace simple example [1, 3, 5] + [2, 4, 6]
- Understand how sorted property helps

**Partition/Kadane Problem:**
- Partition: review two-pointer mechanics
- Kadane's: understand extend vs restart decision

### **For Quick Review (After Learning)**

1. Read "The What" section (5 min) - mental model
2. Trace one example (3 min)
3. Attempt 2-3 questions (5 min)
4. Rate confidence (1 min)

---

## 🎯 4 PATTERNS AT A GLANCE

### **Pattern 1: Hash Map / Hash Set** (Day 1)

**One-liner:** Trade space for time to achieve O(1) lookup.

**Key Operations:**
- Add: O(1) average
- Remove: O(1) average
- Lookup: O(1) average
- Iterate: O(n)

**When to Use:**
- ✅ Fast membership testing
- ✅ Frequency counting
- ✅ Duplicate detection
- ✅ Anagrams, grouping

**When NOT to Use:**
- ❌ Need sorted order (use TreeMap)
- ❌ Range queries (use arrays)
- ❌ Very limited space

**Usage in Interviews:** **70% of problems!**

---

### **Pattern 2: Monotonic Stack** (Day 2)

**One-liner:** Maintain monotonic order while finding next greater/smaller.

**Key Property:**
- Stack in increasing or decreasing order
- New element pops smaller elements
- Popped element found its answer
- O(n) amortized (each element pushed/popped once)

**When to Use:**
- ✅ Next/previous greater element
- ✅ Trapping rain water
- ✅ Largest rectangle histogram
- ✅ Daily temperatures

**When NOT to Use:**
- ❌ Need sorted result (use sort)
- ❌ Random access (not applicable)

**Usage in Interviews:** **20-30% of stack problems!**

---

### **Pattern 3: Merge Operations** (Day 3)

**One-liner:** Combine sorted structures using two pointers in O(n) time.

**Key Advantage:**
- O(n+m) vs O((n+m) log(n+m)) for sort
- Leverages pre-sorted property
- Two pointers from starts

**When to Use:**
- ✅ Both arrays sorted
- ✅ Merge without re-sorting
- ✅ Merge K lists (extension)
- ✅ Interval merging

**When NOT to Use:**
- ❌ Arrays not sorted
- ❌ Need in-place with no extra space

**Usage in Interviews:** **30% of array/list problems!**

---

### **Pattern 4: Partition & Kadane's** (Day 4)

**Partition One-liner:** Segregate elements in-place using two pointers.

**Kadane One-liner:** Dynamic decision: extend sum or restart fresh.

**When to Use Partition:**
- ✅ Move zeros to end
- ✅ Dutch National Flag (0s, 1s, 2s)
- ✅ Segregate elements by condition
- ✅ Quicksort partitioning

**When to Use Kadane's:**
- ✅ Maximum subarray sum
- ✅ Maximum product subarray
- ✅ Circular array max
- ✅ Maximum streak

**Usage in Interviews:** **15% + 10% respectively!**

---

## 💡 KEY CONCEPTS

### **Hash Maps (Frequency Pattern)**
```python
freq = {}
for num in arr:
    freq[num] = freq.get(num, 0) + 1
```

### **Monotonic Stack (Next Greater Pattern)**
```python
stack = []
for i in range(len(arr)):
    while stack and arr[stack[-1]] < arr[i]:
        idx = stack.pop()
        result[idx] = arr[i]
    stack.append(i)
```

### **Merge (Two Pointer Pattern)**
```python
result = []
i = j = 0
while i < len(arr1) and j < len(arr2):
    if arr1[i] <= arr2[j]:
        result.append(arr1[i])
        i += 1
    else:
        result.append(arr2[j])
        j += 1
result.extend(arr1[i:] + arr2[j:])
```

### **Kadane's (Dynamic Programming Pattern)**
```python
current_max = global_max = arr[0]
for i in range(1, len(arr)):
    current_max = max(arr[i], current_max + arr[i])
    global_max = max(global_max, current_max)
```

---

## ✅ SUCCESS CRITERIA

### **Daily Success Criteria**

**Each Day:**
- ✅ 90-minute session completed
- ✅ All 11 sections understood
- ✅ Examples traced by hand
- ✅ 7 questions answered
- ✅ Confidence 4-5/5

### **Week 4.5 Overall Success**

- ✅ 4 patterns mastered
- ✅ 360 minutes invested
- ✅ 28 questions answered
- ✅ 70-80% interview problems coverable
- ✅ **Ready for Week 5!**

---

## 🔧 TROUBLESHOOTING

### **Issue: Don't understand hash O(1) advantage**

**Solution:**
Think of it as "direct access". Hash function maps value to location directly. No searching needed. Same as array index access [0], [1], etc.

---

### **Issue: Confused by monotonic stack**

**Solution:**
Trace simple example [2, 1, 2, 4, 3] step-by-step on paper. Write out stack contents at each step. See that popped elements always < current.

---

### **Issue: Can't trace merge**

**Solution:**
Use two columns side-by-side. Left = array1, Right = array2. Compare top elements, move smaller to result. Continue until one empty.

---

### **Issue: Don't understand extend vs restart (Kadane)**

**Solution:**
At position i, ask: "Is the previous sum helpful?" If current value > previous sum + value, start fresh. Otherwise extend.

---

## 🌟 TIPS FOR SUCCESS

1. **Trace Examples Carefully**
   - Don't skip this step
   - Write out intermediate states
   - See pattern emerge

2. **Connect to Week 4**
   - Hash: extends two-pointer lookups
   - Stack: complements other patterns
   - Merge: similar to two-pointer merge
   - Partition: two-pointer manipulation

3. **Do Practice Problems**
   - 5-7 problems per pattern
   - Reinforces learning
   - Builds confidence
   - Interview-ready practice

4. **Sleep Between Days**
   - Memory consolidation happens during sleep
   - Don't cram all 4 days together
   - Space over 4-5 days ideal

5. **Teach Someone Else**
   - Explain pattern in your own words
   - Find gaps in understanding
   - Deepen learning significantly

---

## 📈 LEARNING PROGRESSION

**Before Week 4.5:**
- Understand pointer patterns
- Know sliding windows
- Familiar with prefix sums
- Ready for data structures

**After Day 1:**
- Understand O(1) hashing
- Can use hash maps effectively
- Foundation for everything

**After Day 2:**
- Can solve next greater problems
- Understand monotonic concept
- Unlock medium/hard problems

**After Day 3:**
- Can merge sorted structures
- Understand merge sort basis
- Efficient combination strategy

**After Day 4:**
- Can partition arrays
- Can find max subarray
- Complete fundamental foundation

**Before Week 5:**
- Ready for advanced patterns
- 70-80% interview coverage
- Confident fundamental knowledge

---

## 🎓 CONNECTIONS TO OTHER TOPICS

### **Hash Maps → Week 5+**
- Multi-map problems
- Group anagrams
- Frequency-based algorithms
- LRU cache

### **Monotonic Stack → Week 5+**
- Trapping rain water (hard)
- Largest rectangle histogram (hard)
- Daily temperatures (easy)
- Next greater element variations

### **Merge Operations → Week 5+**
- Merge K sorted lists (hard)
- Merge intervals (medium)
- Merge sort implementation
- External sorting

### **Partition & Kadane's → Week 5+**
- Quicksort implementation
- Advanced DP problems
- Stock trading variants
- Maximum profit patterns

---

## 📋 QUICK REFERENCE

**Hash Map Complexity:**
- Add: O(1) avg, O(n) worst
- Delete: O(1) avg, O(n) worst
- Lookup: O(1) avg, O(n) worst
- Space: O(n)

**Monotonic Stack Complexity:**
- Build: O(n)
- Each element pushed/popped once
- Total: O(n) amortized
- Space: O(n)

**Merge Complexity:**
- Time: O(n+m)
- Space: O(n+m) for result, O(1) in-place
- No re-sorting needed

**Partition Complexity:**
- Time: O(n) single pass
- Space: O(1) in-place
- Swap to segregate

**Kadane's Complexity:**
- Time: O(n) single pass
- Space: O(1) only variables
- 1000x faster than O(n²) naive

---

## 🎯 WEEK 4.5 VS OTHER WEEKS

| Aspect | Week 4 | Week 4.5 | Week 5 |
|--------|--------|----------|--------|
| Focus | Pointers | Data Structures | Advanced |
| Difficulty | 🟡 Medium | 🟡 Medium | 🟠 Hard |
| Patterns | 5 | 4 | 5+ |
| Interview % | 40-50% | +30% | +15% |
| Total Coverage | 40-50% | 70-80% | 85-90% |

---

## 💬 FAQ

**Q: Should I do all 4 days consecutively?**

A: Ideal: Spread over 4-5 days. Day/Day+1 allows sleep consolidation. Cramming reduces retention.

**Q: Can I skip any pattern?**

A: NO! All 4 are essential:
- Hash: 70% of problems
- Stack: Unique pattern class
- Merge: Fundamental algorithm
- Partition/Kadane: Array + DP

**Q: How much practice needed?**

A: Minimum 5-7 problems per pattern. More if time allows. Interview readiness requires hands-on.

**Q: What if I don't understand a pattern?**

A: Revisit that day's learning file. Review Q&A. Trace more examples. Sleep on it. Return next day.

**Q: Is Week 4.5 necessary for Week 5?**

A: YES. Week 5 builds on these patterns. Without them, Week 5 content won't connect properly.

---

## 🏁 WEEK 4.5 COMPLETION

**When done with all 4 days:**
1. Review checklist (mark everything complete)
2. Reflect on learning (what was easiest/hardest?)
3. Practice 1 problem per pattern
4. Sleep well (memory consolidation)
5. Ready for Week 5!

---

**Status:** Week 4.5 Guide Ready | Study Structure Complete

