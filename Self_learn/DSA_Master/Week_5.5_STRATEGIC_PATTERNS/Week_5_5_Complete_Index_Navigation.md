# Week 5.5: Complete Index & Navigation

**Week:** 5.5 | **Topic:** Optimization Techniques | **Files:** 11 total

---

## 📑 FILE STRUCTURE

```
Week 5.5 Complete Package (11 files)
│
├─ Instructional Files (5 files)
│  ├─ Week_5_5_Day_1_Difference_Array.md [67]
│  ├─ Week_5_5_Day_2_In_Place_Replacement.md [68]
│  ├─ Week_5_5_Day_3_Deque_Sliding_Window.md [69]
│  ├─ Week_5_5_Day_4_Advanced_Combinations.md [70]
│  └─ Week_5_5_Day_5_Integration_Mastery.md [71]
│
├─ Support Files (5 files)
│  ├─ Week_5_5_Checklist_Progress.md [72]
│  ├─ Week_5_5_Summary_Quick_Reference.md [73]
│  ├─ Week_5_5_Roadmap_Time_Budget.md [74]
│  ├─ Week_5_5_QA_Practice_Questions.md [75]
│  └─ Week_5_5_Complete_Index_Navigation.md [76]
│
└─ Guidelines File (1 file)
   └─ Week_5_5_Guidelines.md [to be generated]
```

---

## 🔍 QUICK NAVIGATION BY TOPIC

### Difference Array [67]
**Primary:** Week_5_5_Day_1_Difference_Array.md  
**Quick Ref:** [73] Summary → Difference Array section  
**Practice:** [75] Q&A Day 1  
**Checklist:** [72] Day 1  
**Why:** Range updates O(1) instead of O(k)

### In-Place Replacement [68]
**Primary:** Week_5_5_Day_2_In_Place_Replacement.md  
**Quick Ref:** [73] Summary → In-Place section  
**Practice:** [75] Q&A Day 2  
**Checklist:** [72] Day 2  
**Why:** O(1) space instead of O(n)

### Deque Sliding Window [69]
**Primary:** Week_5_5_Day_3_Deque_Sliding_Window.md  
**Quick Ref:** [73] Summary → Deque section  
**Practice:** [75] Q&A Day 3  
**Checklist:** [72] Day 3  
**Why:** O(n) instead of O(n log n)

### Advanced Combinations [70]
**Primary:** Week_5_5_Day_4_Advanced_Combinations.md  
**Quick Ref:** [73] Summary → Combinations section  
**Practice:** [75] Q&A Day 4  
**Checklist:** [72] Day 4  
**Why:** Real problems combine techniques

### Integration & Mastery [71]
**Primary:** Week_5_5_Day_5_Integration_Mastery.md  
**Quick Ref:** [73] Summary → Pattern Recognition  
**Practice:** [75] Q&A Day 5  
**Checklist:** [72] Day 5  
**Why:** Pattern recognition skill

---

## 📊 DECISION MATRIX (When to Use)

| Situation | Technique | File | Complexity |
|-----------|-----------|------|-----------|
| Range updates | Difference Array | [67] | O(m+n) |
| Space constraint | In-Place | [68] | O(n), O(1) space |
| Window max/min | Deque | [69] | O(n) |
| Multiple ops | Combinations | [70] | Varies |
| Pattern unsure? | Pattern Matrix | [71] | Reference |

---

## 🎓 LEARNING PATH

### Path 1: Linear Progression (Days 1-5)
```
Day 1: Difference Array [67]
   ↓
Day 2: In-Place [68]
   ↓
Day 3: Deque [69]
   ↓
Day 4: Combinations [70]
   ↓
Day 5: Integration [71]
   ↓
Master [73]
```

### Path 2: Technique-First Deep Dive
```
Choose one technique from [67], [68], [69]
→ Read full article
→ Practice Q&A from [75]
→ Solve 3-5 problems
→ Move to next technique
```

### Path 3: Interview Prep
```
Use [73] Summary (5 min)
→ Identify technique needed
→ Review [67], [68], or [69]
→ Code template from [73]
→ Solve problem in [75]
```

---

## 📚 BY LEARNING OBJECTIVE

### "I want to understand..."

**...range updates efficiently**
→ [67] Sections 1-2 + [73] Difference Array

**...space optimization**
→ [68] Sections 1-2 + [73] In-Place

**...sliding window optimization**
→ [69] Sections 1-2 + [73] Deque

**...combining techniques**
→ [70] Sections 1-2 + [71] Pattern Recognition

**...when to use each**
→ [71] Decision Matrix + [73] Technique Tree

---

## 🧮 COMPLEXITY COMPARISON

**Quick Reference:** [73] Complexity Comparison Table

| Problem | Naive | Optimized | Technique |
|---------|-------|-----------|-----------|
| m range updates | O(m×k) | O(m+n) | Difference Array |
| n removals | O(n) space | O(1) space | In-Place |
| k window queries | O(n×k) | O(n) | Deque |

---

## ✅ DAILY CHECKLIST LOCATIONS

- **Day 1 Progress:** [72] Day 1 section
- **Day 2 Progress:** [72] Day 2 section
- **Day 3 Progress:** [72] Day 3 section
- **Day 4 Progress:** [72] Day 4 section
- **Day 5 Progress:** [72] Day 5 section
- **Overall Progress:** [72] Summary section

---

## 📝 PRACTICE PROBLEM TRACKER

| Day | Easy | Medium | Hard | Total |
|-----|------|--------|------|-------|
| **1** | 2-3 | 1-2 | 0-1 | 3-6 |
| **2** | 2-3 | 1-2 | 0-1 | 3-6 |
| **3** | 2-3 | 1-2 | 0-1 | 3-6 |
| **4** | 1 | 2 | 1 | 4 |
| **5** | Review | Review | Mix | 15+ total |

**Find problems:** [75] Q&A sections

---

## 🔄 BEFORE WEEK 6, CHECKLIST

From [71]:
- [ ] Understand all 4 techniques
- [ ] Confidence 4/5 on Days 1-3
- [ ] Solved 15+ problems
- [ ] Can recognize which technique(s)
- [ ] Can code from scratch in 5 minutes

**Status:** _____ (Not Ready / Ready / Exceeded)

---

## 💾 QUICK REFERENCE GUIDES

**Code Templates:** [73] Code Templates section

```python
# Difference Array
diff = [0] * (n + 1)
for left, right, val in updates:
    diff[left] += val
    diff[right + 1] -= val
current = 0
result = []
for i in range(n):
    current += diff[i]
    result.append(current)
```

```python
# In-Place Removal
j = 0
for i in range(len(arr)):
    if should_keep(arr[i]):
        arr[j] = arr[i]
        j += 1
return j
```

```python
# Deque Sliding Window Max
dq = deque()
for i in range(len(arr)):
    if dq and dq[0] < i - k + 1:
        dq.popleft()
    while dq and arr[dq[-1]] < arr[i]:
        dq.pop()
    dq.append(i)
    if i >= k - 1:
        result.append(arr[dq[0]])
```

---

## 🆘 TROUBLESHOOTING

**Confused about technique?**
→ [73] Decision Tree

**Can't remember implementation?**
→ [73] Code Templates

**Stuck on problem?**
→ [75] Q&A with answers

**Need time plan?**
→ [74] Roadmap

**Want to track progress?**
→ [72] Checklist

---

## 📖 FILES TO DOWNLOAD (In Order)

1. [71] Week_5_5_Day_5_Integration_Mastery.md ← Start (overview)
2. [67] Week_5_5_Day_1_Difference_Array.md
3. [68] Week_5_5_Day_2_In_Place_Replacement.md
4. [69] Week_5_5_Day_3_Deque_Sliding_Window.md
5. [70] Week_5_5_Day_4_Advanced_Combinations.md
6. [72] Week_5_5_Checklist_Progress.md
7. [73] Week_5_5_Summary_Quick_Reference.md
8. [74] Week_5_5_Roadmap_Time_Budget.md
9. [75] Week_5_5_QA_Practice_Questions.md
10. [76] Week_5_5_Complete_Index_Navigation.md (this file)

---

## 🎯 SUCCESS PATH

```
Week 5 (Trees): Foundation
    ↓
Week 5.5 (Optimization): Application
    ↓
Week 6 (Graphs): Generalization

Week 5.5 bridges foundation + application → advanced algorithms
```

---

**Index Version:** 1.0 Week 5.5 Complete  
**Purpose:** Easy cross-referencing  
**Use:** Find exactly what you need when you need it

Use this index to navigate Week 5.5 efficiently! 📍

