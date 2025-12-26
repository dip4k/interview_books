# Week 1: Fundamentals & Array Basics - Guidelines

**Week Focus:** Foundation building with arrays, strings, and basic problem-solving  
**Total Time Investment:** 8-10 hours (learning + practice)  
**Difficulty Level:** 🟢 Easy  
**Prerequisites:** None (complete beginner-friendly)

---

## 📅 Daily Breakdown & Time Allocation

| Day | Topic | Time | Key Outcomes |
|-----|-------|------|--------------|
| **1** | Array Fundamentals | 90 min | Indexing, iteration, common operations |
| **2** | String Basics | 85 min | String manipulation, comparison, patterns |
| **3** | Basic Array Operations | 80 min | Insert, delete, search, modify |
| **4** | Basic String Operations | 75 min | Substring, split, merge, case handling |
| **5** | Integration & Practice | 70 min | Combine arrays and strings, solve problems |

**Total Core Learning:** ~400 minutes (6.7 hours)  
**Practice & Consolidation:** ~3 hours  

---

## 🎯 Week 1 Learning Objectives

### By Week End, You Should:

**Knowledge:**
- [ ] Understand array indexing (0-based)
- [ ] Know array iteration patterns
- [ ] Understand string immutability
- [ ] Know string methods and operations
- [ ] Understand time/space complexity (basic)

**Skills:**
- [ ] Access array elements by index
- [ ] Iterate through arrays (for, while)
- [ ] Manipulate strings (slice, concat, case)
- [ ] Write basic loops and conditions
- [ ] Handle array and string edge cases

**Application:**
- [ ] Solve simple array problems (searching, counting)
- [ ] Manipulate strings (reversal, palindrome check)
- [ ] Combine arrays and strings
- [ ] Write readable code with comments

---

## 📚 Core Concepts Overview

### Arrays
```
Declaration: arr = [1, 2, 3, 4, 5]
Indexing: arr[0] = 1, arr[-1] = 5 (Python)
Iteration: for i in range(len(arr)): use arr[i]
Time: Access O(1), Search O(n), Insert/Delete O(n)
Space: O(n) for array of size n
```

### Strings
```
Declaration: s = "hello"
Indexing: s[0] = 'h', s[-1] = 'o'
Iteration: for char in s: use char
Immutable: Can't modify, create new string
Time: Access O(1), Search O(n), Operations O(n)
Space: O(n) for string of length n
```

---

## 🔄 Recommended Learning Path

**Best Order to Study:**

1. **Day 1:** Array Fundamentals
   - Understand indexing, basic operations
   - Build mental model of arrays
   - Practice accessing elements

2. **Day 2:** String Basics
   - Learn string operations
   - Understand immutability
   - Practice string methods

3. **Day 3:** Array Operations Deep Dive
   - Insert, delete, search
   - Common patterns (sum, min/max, count)
   - Build practical skills

4. **Day 4:** String Operations Deep Dive
   - String manipulation patterns
   - Common transformations
   - Real-world string problems

5. **Day 5:** Integration
   - Combine arrays and strings
   - Solve mixed problems
   - Consolidate understanding

**Why This Order?**
- Arrays are more intuitive (start there)
- Strings build on array concepts
- Deep dive after basics solidified
- Integration requires both foundational

---

## ⚠️ Common Mistakes to Avoid

### Array-Related

| Mistake | Why It's Wrong | Fix |
|---------|----------------|-----|
| **Off-by-one errors** | Array indices 0 to n-1, not 1 to n | Use 0-based indexing consistently |
| **Forgetting boundaries** | Accessing arr[n] causes error | Always check: 0 ≤ index < len(arr) |
| **Modifying while iterating** | Can skip/double elements | Create new array or use safe iteration |
| **Confusing len(arr) with last index** | len([1,2,3]) = 3, but index is 2 | Remember: last_index = len(arr) - 1 |

### String-Related

| Mistake | Why It's Wrong | Fix |
|---------|----------------|-----|
| **Trying to modify strings** | Strings are immutable | Create new string (concatenate) |
| **Index out of bounds** | "hello"[5] doesn't exist | Check: index < len(string) |
| **Case sensitivity** | "A" ≠ "a" in comparison | Use .lower() or .upper() if needed |
| **Empty string handling** | Forgot edge case | Always check: if s or if len(s) > 0 |

---

## 🎓 Practice Problems Guide

### Array Problems

**Easy (Start Here):**
- Find maximum element in array
- Count occurrences of element
- Reverse an array
- Remove duplicates from sorted array
- Time: 15-20 min per problem

**Medium (After Easy Mastered):**
- Rotate array
- Merge sorted arrays
- Check if array is sorted
- Time: 20-30 min per problem

**Recommended Sources:**
- LeetCode: Easy Array problems
- HackerRank: Array Manipulation
- GeeksforGeeks: Array tutorials

### String Problems

**Easy:**
- Reverse a string
- Check if palindrome
- Convert case (upper/lower)
- Repeat string
- Time: 15-20 min per problem

**Medium:**
- Find longest substring without repeating
- Check if anagram
- String compression
- Time: 25-35 min per problem

---

## 💼 Interview Preparation

### How Week 1 Appears in Interviews

**Array Questions:**
- "Reverse an array in-place"
- "Find the maximum element"
- "Remove duplicates"
- "Rotate an array"

**String Questions:**
- "Check if string is palindrome"
- "Reverse a string"
- "Find longest substring without repeating characters"
- "Check if two strings are anagrams"

**Mixed Questions:**
- "Valid parentheses in string"
- "Two sum in array"

### Interview Tips
1. **Ask clarifications:** "Are there duplicates? Negative numbers?"
2. **State assumptions:** "I'll assume sorted array"
3. **Test edge cases:** Empty array, single element, duplicates
4. **Explain approach before coding:** "First I'll iterate..."
5. **Code cleanly:** Use descriptive variable names

---

## 🔗 Resources & References

### Online Platforms
- **LeetCode:** https://leetcode.com (Easy problems)
- **HackerRank:** https://www.hackerrank.com/domains/tutorials/10-days-of-javascript
- **GeeksforGeeks:** https://www.geeksforgeeks.org (Array/String tutorials)
- **Khan Academy:** https://www.khanacademy.org (CS basics)

### Visualization Tools
- **VisuAlgo:** https://www.cs.usfca.edu/~galles/visualization/ (Algorithm visualization)
- **Python Tutor:** https://pythontutor.com (Step-by-step code execution)

### Recommended Readings
- "Introduction to Algorithms" - CLRS (Chapter 1-2)
- "Cracking the Coding Interview" - McDowell (Chapter 1)

---

## ✅ Assessment & Success Criteria

### Knowledge Check
Answer "Yes" to these:
- [ ] I understand 0-based indexing
- [ ] I can iterate through arrays
- [ ] I understand string immutability
- [ ] I know basic string methods
- [ ] I can trace code by hand

### Practical Skills
Can you:
- [ ] Write a function to find max element
- [ ] Reverse a string manually
- [ ] Count occurrences in array
- [ ] Check if string is palindrome
- [ ] Handle empty array/string cases

### Confidence Targets
| Skill | Target |
|-------|--------|
| Array Indexing | 5/5 |
| Array Iteration | 5/5 |
| String Operations | 4/5 |
| Basic Problem-Solving | 3-4/5 |
| Overall Week 1 | 4/5 |

---

## 📊 Connection to Future Weeks

### Week 2: Foundation for Data Structures
```
Week 1 Arrays/Strings
    ↓
Week 2 Use arrays to implement: Stacks, Queues, HashMaps
    ↓
Understanding array access/operations essential
```

### Week 3: Foundation for Sorting
```
Week 1 Array basics
    ↓
Week 3 Sorting algorithms work on arrays
    ↓
Must be comfortable with iteration and swapping
```

### Week 4+: Advanced Techniques
```
Weeks 1-2 Fundamentals
    ↓
Week 4 Two Pointers, Sliding Window (on arrays/strings)
    ↓
All assume comfort with basic array/string operations
```

---

## ❓ Frequently Asked Questions

### Q1: Why start with arrays and not linked lists?
**A:** Arrays are more intuitive (direct indexing) and form basis for understanding data structures. Linked lists require understanding pointers (Week 2).

### Q2: Is string immutability important for interviews?
**A:** Yes! Affects approach. If immutable, create new string instead of modifying. Common follow-up: "How would you do this efficiently?"

### Q3: Why practice so many array problems?
**A:** Arrays are foundational. Mastering arrays makes Weeks 2-5 much easier. Pattern recognition develops through repetition.

### Q4: What if I find this too easy?
**A:** That's great! Move to Week 2 or try harder LeetCode problems (Medium level). Don't skip fundamentals though - understanding is critical.

### Q5: How much time should I spend on practice?
**A:** Rule of thumb: 30% learning, 70% practice. Minimum 2-3 hours practice per day.

---

## 🎯 Before Moving to Week 2

**Checklist:**
- [ ] Complete all 5 days of learning material
- [ ] Solve at least 5 easy array problems
- [ ] Solve at least 5 easy string problems
- [ ] Can trace code by hand confidently
- [ ] Feel comfortable with edge cases
- [ ] Confident: 4/5 or higher

**If not ready:**
- Review weak areas
- Solve 5+ more practice problems
- Don't rush to Week 2

---

## 📝 Week 1 Quick Summary

| Concept | Know It | Do It |
|---------|---------|-------|
| **Array indexing** | O(1) access | arr[i] = value |
| **Array iteration** | O(n) time | for i in range(len) |
| **String immutability** | Can't modify | Create new string |
| **String methods** | Many available | s.upper(), s.split() |
| **Time complexity** | O(n) typical | Linear scan arrays |

---

**Status:** Week 1 Ready for Study ✓  
**Expected Completion:** 1 week of consistent study  
**Success Rate:** 95%+ if you practice regularly  

