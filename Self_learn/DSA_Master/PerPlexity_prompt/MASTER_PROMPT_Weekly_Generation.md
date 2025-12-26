# 🚀 MASTER PROMPT FOR WEEKLY STUDY CURRICULUM GENERATION

**Version:** 2.0 Enhanced  
**Date Created:** December 26, 2025, 22:05 IST  
**Purpose:** Generate complete weekly curriculum packages (instructional + support + guidelines)  
**Status:** Production Ready  

---

## 📋 MASTER PROMPT - COMPLETE WORKFLOW

### Usage Instructions
Copy the relevant section below based on what you need to generate:
- **SECTION A:** Full Week Generation (all files at once)
- **SECTION B:** Day-by-Day Generation (individual instructional files)
- **SECTION C:** Support Files Generation (checklist, summary, roadmap, Q&A, index)
- **SECTION D:** Enhanced Guidelines Generation (master overview)

---

## 🎯 SECTION A: FULL WEEK GENERATION (All Files)

### Use This When: You want to generate ALL files for a complete week in one request

```
=== FULL WEEK GENERATION PROMPT ===

Generate complete Week [NUMBER] curriculum package with all deliverables:

WEEK OVERVIEW:
- Week Number: [NUMBER]
- Topic: [MAIN TOPIC]
- Subtopics: [LIST 3-5 SUBTOPICS]
- Difficulty: [EASY/MEDIUM/HARD]
- Time Investment: [HOURS]
- Prerequisites: [PREVIOUS WEEK or NONE]
- Bridge to: [NEXT WEEK]

PART 1: INSTRUCTIONAL CONTENT (Day-by-Day)

Generate [NUMBER] instructional files using 11-Section Framework:

For each file:
Format: Week_[NUMBER]_Day_[NUMBER]_[TOPIC].md
Length: 2,000-2,500 words
Time: 60-90 minutes reading

11 Mandatory Sections:
1. The Why — Engineering Motivation & Real-world context
2. The What — Mental Model & Intuition building
3. The How — Mechanical Walkthrough & implementation
4. Visualization — Traced Examples & step-by-step execution
5. Critical Analysis — Performance & Robustness comparison
6. Real System Integration — Production applications
7. Concept Crossovers — Connections to other techniques
8. Mathematical & Theoretical — Formal foundations
9. Algorithmic Design Intuition — Why design works this way
10. Knowledge Check — Socratic Reasoning questions
11. Retention Hook — Memory Anchors & mnemonics

Supplementary for each file:
- Complexity cheat sheets (time/space tables)
- 15-20 code examples
- 10-15 visualizations/traces
- External resource links
- Key insights summary

Day 1: [TOPIC 1]
Day 2: [TOPIC 2]
Day 3: [TOPIC 3]
Day 4: [TOPIC 4]
Day 5: [TOPIC 5 OR INTEGRATION]

Each file downloadable as .md artifact

---

PART 2: SUPPORT MATERIALS (5 Types)

Format: Week_[NUMBER]_[TYPE].md

A) CHECKLIST & PROGRESS TRACKING
- Daily progress tracker (all 11 sections per day)
- Confidence ratings (1-5 scale)
- Hands-on task completion checklist
- Learning objectives assessment
- Time spent tracking
- Key insights & questions
- Knowledge gaps section
- External resources tracked
- Success criteria verification
- Weekly summary section

B) SUMMARY & QUICK REFERENCE
- Executive summary (one-line essence per topic)
- Complexity comparison tables
- Decision matrices/trees
- Key insights & takeaways
- Common mistakes to avoid
- Problem-solving frameworks
- Interview quick answers
- Concept connections
- Trade-off analysis
- Mastery checklist

C) ROADMAP & TIME BUDGET
- Weekly overview & mission
- Phase-by-phase breakdown (5 phases)
- Time allocation per topic (hour-by-hour)
- Optimal reading path per day
- Cross-week integration points
- Recovery strategies (if behind)
- Study environment setup
- Success criteria
- Interview preparation timeline
- Progress metrics

D) Q&A PRACTICE QUESTIONS
- 10 questions per day × number of days
- Difficulty ratings (⭐ Easy to ⭐⭐⭐ Hard)
- Detailed answer explanations
- Socratic reasoning prompts
- Self-assessment section
- Learning recommendations based on answers
- Confidence tracking
- Topic-by-topic organization

E) COMPLETE INDEX & NAVIGATION
- Master navigation guide
- File structure overview
- Quick navigation by algorithm/problem type
- Daily learning path
- Complexity reference table
- Search index by concept
- Problem mapping table
- External references directory
- Success criteria checklist
- Interview prep mapping

Each file downloadable as .md artifact

---

PART 3: ENHANCED GUIDELINES (Master Overview)

Format: Week_[NUMBER]_Guidelines.md
Length: 3,000-4,000+ words
Structure: 12 comprehensive sections

12 Mandatory Sections:

1. DAILY BREAKDOWN & TIME ALLOCATION
   - Daily schedule with time allocations
   - Total learning vs practice hours
   - Daily progression logic with visualization

2. LEARNING OBJECTIVES
   - Knowledge targets (what to understand)
   - Practical skills (what to do)
   - Application abilities (where to use)
   - All with checkboxes

3. CORE CONCEPTS OVERVIEW
   - Main algorithms/techniques explanation
   - Prerequisites & requirements
   - Complexity analysis
   - When to use each concept

4. RECOMMENDED LEARNING PATH
   - Optimal order to study topics
   - Rationale for sequence
   - Building blocks approach
   - Daily schedule breakdown

5. COMMON MISTAKES TO AVOID
   - Mistake | Why Wrong | How to Fix | Impact
   - Per algorithm/technique
   - Real-world consequences
   - Prevention strategies

6. PRACTICE PROBLEMS GUIDE
   - Organized by difficulty (Easy/Medium/Hard)
   - Time estimates per problem
   - Source platforms with links
   - Problem recommendations
   - Total problem count

7. INTERVIEW PREPARATION
   - Common interview questions by level
   - How topics appear in interviews
   - Interview tips & strategies
   - Follow-up question handling
   - Trade-off discussion guidance

8. RESOURCES & REFERENCES
   - Online learning platforms (with links)
   - Visualization tools
   - Recommended books
   - Article references

9. ASSESSMENT & SUCCESS CRITERIA
   - Knowledge check (yes/no list)
   - Practical skills (can you do this)
   - Confidence targets (rating scales)
   - Mastery indicators

10. CONNECTION TO FUTURE WEEKS
    - How current week builds toward next
    - Prerequisites for Week N+1
    - Mastery importance
    - Application in advanced topics

11. FREQUENTLY ASKED QUESTIONS
    - Student questions with detailed answers
    - Common misconceptions
    - Troubleshooting guide
    - 15+ Q&A items

12. SCHEDULE & SUCCESS PATH
    - Recommended weekly schedule
    - Options (compressed/distributed)
    - Key milestones per day
    - Success progression visualization
    - Week completion checklist
    - Week 5 readiness criteria

Guidelines file downloadable as .md artifact

---

DELIVERABLES:

Total Files: [CALCULATE: 5 days + 5 support + 1 guidelines = 11 files]

All files generated as downloadable .md artifacts with:
✓ Markdown formatting
✓ Proper structure
✓ Consistent style
✓ Complete coverage
✓ No gaps
✓ Ready for immediate use

Generate and make available for download.
```

---

## 🎯 SECTION B: DAY-BY-DAY INSTRUCTIONAL FILE GENERATION

### Use This When: You want to generate individual day files one at a time

```
=== DAY-BY-DAY GENERATION PROMPT ===

Generate instructional content file:

FILE DETAILS:
- Week Number: [NUMBER]
- Day Number: [NUMBER]
- Topic: [SPECIFIC TOPIC NAME]
- Estimated Time: [60-90 minutes]
- Previous Day Topic: [PREVIOUS TOPIC or NONE]
- Next Day Topic: [NEXT TOPIC]

CONTENT REQUIREMENTS:

Format: Week_[NUMBER]_Day_[NUMBER]_[TOPIC].md
Word Count: 2,000-2,500 words
Target Length: 60-90 minute read

Use 11-Section Framework (MANDATORY):

SECTION 1️⃣: THE WHY — Engineering Motivation
- Why this algorithm/technique matters
- Real-world problems it solves
- Historical context
- Performance impact
- When companies/products use it
- Career relevance

SECTION 2️⃣: THE WHAT — Mental Model & Intuition
- High-level concept explanation
- Intuitive understanding
- Visual mental model
- Why it works (conceptually)
- Comparison to familiar concepts
- Key insight/core idea

SECTION 3️⃣: THE HOW — Mechanical Walkthrough
- Step-by-step implementation
- Algorithm pseudocode
- Code structure explanation
- Variable tracking
- Edge case handling
- Implementation details

SECTION 4️⃣: VISUALIZATION — Traced Examples
- 3-5 complete traced examples
- Step-by-step walkthrough
- Visual diagrams/ASCII art
- Input → Output progression
- Complexity calculation
- Edge cases shown

SECTION 5️⃣: CRITICAL ANALYSIS — Performance & Robustness
- Time complexity analysis (best/avg/worst)
- Space complexity analysis
- Trade-offs vs alternatives
- Robustness to input variations
- When algorithm fails
- Optimization opportunities

SECTION 6️⃣: REAL SYSTEM INTEGRATION
- Production use cases
- Real-world examples
- Industry applications
- Performance requirements
- Optimization techniques
- System design implications

SECTION 7️⃣: CONCEPT CROSSOVERS
- How this connects to previous weeks
- Related algorithms/techniques
- Synergies with other patterns
- Prerequisites from earlier
- Application with other methods
- Complementary approaches

SECTION 8️⃣: MATHEMATICAL & THEORETICAL
- Formal algorithm definition
- Mathematical proof (if applicable)
- Complexity proof
- Correctness verification
- Theoretical foundations
- Why complexity is proven

SECTION 9️⃣: ALGORITHMIC DESIGN INTUITION
- Design decision rationale
- Alternative approaches
- Why this approach chosen
- Trade-off analysis
- Extension possibilities
- Generalization to similar problems

SECTION 🔟: KNOWLEDGE CHECK — Socratic Reasoning
- 5-8 Socratic questions
- No simple answers
- Require deep thinking
- Progressive difficulty
- Check understanding
- Force verbalization

SECTION 1️⃣1️⃣: RETENTION HOOK — Memory Anchors
- Memorable phrase/analogy
- Visual memory aid
- Story or context
- Common mistake to avoid
- Quick reference phrase
- Interview talking point

SUPPLEMENTARY MATERIALS:

Include for each file:
- Complexity cheat sheet (table format)
- 15-20 code examples (different languages)
- 10-15 visualizations/diagrams
- 3-5 external resource links
- Key insights bullet points (3-5)
- Related problems list

QUALITY STANDARDS:
✓ All sections complete
✓ Code examples tested (logic verified)
✓ Visualizations clear
✓ No grammatical errors
✓ Consistent formatting
✓ Professional tone
✓ Accessible language
✓ Progressive difficulty

Generate and download as .md file (Week_[NUMBER]_Day_[NUMBER]_[TOPIC].md)
```

---

## 📊 SECTION C: SUPPORT FILES GENERATION

### Use This When: You want to generate support files (checklist, summary, roadmap, Q&A, index)

```
=== SUPPORT FILES GENERATION PROMPT ===

Generate support materials for Week [NUMBER]:

SUPPORT TYPE 1: CHECKLIST & PROGRESS TRACKING
File: Week_[NUMBER]_Checklist_Progress.md

Content:
□ Daily progress tracker (per day)
□ Reading progress (all 11 sections tracked)
□ Hands-on coding tasks
□ Confidence level ratings (1-5 scale)
□ Key insights captured
□ Questions/confusion documented
□ Time spent tracking
□ Learning objectives assessment (check marks)
□ Understanding levels by topic
□ Knowledge gaps section
□ External resources explored
□ Practice implementation tracking
□ Weekly summary
□ Success criteria checklist
□ Progress metrics
□ Notes & reflections

Formatting:
- Daily sections (one per day)
- Checkbox format for completion
- Rating scales for confidence
- Tables for organization
- Progress tracking sections
- Reflection prompts

---

SUPPORT TYPE 2: SUMMARY & QUICK REFERENCE
File: Week_[NUMBER]_Summary.md

Content:
□ Executive summary (2-3 lines per topic)
□ Complexity comparison tables
□ Algorithm/technique decision matrix
□ When to use each technique
□ Key insights & takeaways (bullet points)
□ Common mistakes overview
□ Problem-solving frameworks
□ Interview quick answers
□ Concept connection map
□ Space vs time trade-offs
□ Mastery checklist
□ Quick reference formulas/operations

Formatting:
- Concise explanations
- Tables for comparison
- Decision trees/matrices
- Quick lookup sections
- One-page cheat sheets
- Visual organization

---

SUPPORT TYPE 3: ROADMAP & TIME BUDGET
File: Week_[NUMBER]_Roadmap.md

Content:
□ Weekly overview & mission
□ Learning phases (5-phase breakdown)
□ Time allocation (hour-by-hour)
□ Daily reading path (optimal order)
□ Cross-week integration points
□ Recovery strategies (if behind schedule)
□ Study environment recommendations
□ Success criteria & checkpoints
□ Interview preparation schedule
□ Progress measurement points
□ Milestone tracking
□ Time buffer recommendations

Formatting:
- Phase-by-phase structure
- Time allocation tables
- Daily schedule format
- Recovery strategies
- Milestone checklists
- Progress metrics

---

SUPPORT TYPE 4: Q&A PRACTICE QUESTIONS
File: Week_[NUMBER]_QA_10_Questions_Per_Day.md

Content:
For each day (10 questions per day):
□ Question text
□ Difficulty rating (⭐ Easy to ⭐⭐⭐ Hard)
□ Detailed answer explanation
□ Why this matters (context)
□ Common mistakes in answering
□ Follow-up question
□ Related topic reference
□ Self-assessment guidance

Total: 10 questions × [NUMBER OF DAYS] = [TOTAL QUESTIONS]

Formatting:
- Questions numbered per day
- Difficulty indicators
- Answers in dedicated sections
- Self-assessment prompts
- Cross-references to main content
- Confidence tracking

---

SUPPORT TYPE 5: COMPLETE INDEX & NAVIGATION
File: Week_[NUMBER]_Complete_Index.md

Content:
□ File structure overview (list all files)
□ Quick navigation by algorithm/problem type
□ Daily learning path
□ Complexity reference table
□ Search index (searchable by concept)
□ Problem-type mapping
□ External resources directory
□ Success criteria checklist
□ Interview prep mapping
□ Milestone checklist
□ Quick lookup sections

Formatting:
- Master navigation guide
- File directory structure
- Algorithm/problem lookup table
- Complexity cheat sheet
- Cross-reference links
- Quick search index
- Topic mapping

---

GENERATION INSTRUCTIONS:

For each support file:
✓ Follow structure above exactly
✓ Use tables for organized data
✓ Include checkboxes where applicable
✓ Provide detailed content
✓ Maintain consistent formatting
✓ Include all required sections
✓ Add visual hierarchy
✓ Make downloadable as .md

Generate all 5 support files.
Download each as separate .md artifact.
```

---

## 📘 SECTION D: ENHANCED GUIDELINES GENERATION

### Use This When: You want to generate the master overview (12 sections)

```
=== ENHANCED GUIDELINES GENERATION PROMPT ===

Generate Enhanced Guidelines file for Week [NUMBER]:

FILE: Week_[NUMBER]_Guidelines.md
Length: 3,000-4,000+ words
Structure: 12 comprehensive sections (ALL MANDATORY)

WEEK OVERVIEW:
- Week Number: [NUMBER]
- Focus Topic: [MAIN TOPIC]
- Subtopics: [LIST SUBTOPICS]
- Difficulty: [EASY/MEDIUM/HARD]
- Time Investment: [HOURS]
- Prerequisites: [PREVIOUS WEEK]
- Bridge to: [NEXT WEEK]
- Interview Relevance: [HIGH/MEDIUM/LOW]

---

SECTION 1️⃣: DAILY BREAKDOWN & TIME ALLOCATION

Content:
- Daily schedule table (day, topic, time, outcomes)
- Total core learning time (minutes & hours)
- Total practice time (minutes & hours)
- Total week time
- Daily progression logic (visual flow)
- Time allocation rationale

Format:
| Day | Topic | Core Time | Practice | Outcomes |
Time calculations with clear breakdown

---

SECTION 2️⃣: LEARNING OBJECTIVES

Content:
- Knowledge targets (understanding goals)
- Practical skills (can do competencies)
- Application abilities (real-world usage)

Format:
Knowledge: [ ] Item 1, [ ] Item 2... (8+ items)
Skills: [ ] Item 1, [ ] Item 2... (8+ items)
Application: [ ] Item 1, [ ] Item 2... (7+ items)

---

SECTION 3️⃣: CORE CONCEPTS OVERVIEW

Content:
- Main algorithms/techniques explanation
- Prerequisites & requirements
- Mechanism (how it works)
- Complexity analysis
- When to use each
- Comparison tables

Format:
Code blocks with pseudo-code
Comparison tables
Requirement checklists
Use-case examples

---

SECTION 4️⃣: RECOMMENDED LEARNING PATH

Content:
- Optimal order to study topics
- Rationale for each ordering decision
- Building blocks approach
- Optimal daily schedule (minute breakdown)
- Visual progression diagram

Format:
Visual flow/tree structure
Daily schedule table
Minute-by-minute breakdown
Progression arrows/diagrams

---

SECTION 5️⃣: COMMON MISTAKES TO AVOID

Content:
- Mistake | Why It's Wrong | How to Fix | Impact
- Organized by algorithm/technique
- Real-world consequences
- Prevention strategies

Format:
Tables with 4 columns
3-7 mistakes per topic
Impact level indicators
Fix explanations

---

SECTION 6️⃣: PRACTICE PROBLEMS GUIDE

Content:
- Problems organized by difficulty
- Time estimates per problem
- Source platforms (LeetCode, GeeksforGeeks, etc.)
- Problem recommendations
- Total problem count per difficulty

Format:
Easy: [NUMBER] problems, [TIME] minutes each
Medium: [NUMBER] problems, [TIME] minutes each
Hard: [NUMBER] problems, [TIME] minutes each
Sources with links

---

SECTION 7️⃣: INTERVIEW PREPARATION

Content:
- Common interview questions by level
- How topics appear in interviews
- Interview tips & strategies
- Follow-up question handling
- Trade-off discussion guidance

Format:
Questions organized by difficulty
Tips in bullet format
Follow-up examples
Strategy explanations

---

SECTION 8️⃣: RESOURCES & REFERENCES

Content:
- Online learning platforms (with links)
- Visualization tools
- Recommended books
- Article/tutorial references
- Video recommendations

Format:
Categorized lists
Working links
Brief descriptions
Recommendations

---

SECTION 9️⃣: ASSESSMENT & SUCCESS CRITERIA

Content:
- Knowledge check (yes/no checklist)
- Practical skills assessment (can you do)
- Confidence targets (rating scales)
- Success checklist
- Mastery indicators

Format:
Checklist format
Rating scales (1-5)
Success criteria table
Confidence targets per skill

---

SECTION 🔟: CONNECTION TO FUTURE WEEKS

Content:
- How current week builds toward next
- Prerequisites for Week N+1
- Mastery importance rating
- Application in advanced topics
- Progression flow

Format:
Visual progression diagram
Prerequisite tables
Importance rankings
Connection explanations

---

SECTION 1️⃣1️⃣: FREQUENTLY ASKED QUESTIONS

Content:
- 15-20 common student questions
- Detailed answer explanations
- Why question matters
- Common misconceptions addressed
- Troubleshooting guidance

Format:
Q & A format
Organized by category
Clear explanations
Related topic cross-references

---

SECTION 1️⃣2️⃣: SCHEDULE & SUCCESS PATH

Content:
- Recommended weekly schedule options
- Key milestones per day
- Success path visualization
- Completion checklist
- Week N+1 readiness criteria

Format:
Multiple schedule options
Daily breakdown
Milestone visualization
Readiness checklist

---

QUALITY REQUIREMENTS:

For entire document:
✓ All 12 sections complete
✓ 3,000-4,000+ words total
✓ Professional formatting
✓ Clear hierarchy
✓ Consistent style
✓ All links working
✓ No gaps
✓ Markdown syntax correct
✓ Tables properly formatted
✓ Checkboxes functional
✓ Visually organized
✓ Easy to scan

Generate Enhanced Guidelines file.
Download as .md artifact (Week_[NUMBER]_Guidelines.md)
```

---

## 🎪 SECTION E: COMPLETE WORKFLOW SUMMARY

### Full Generation Workflow (Use This as Checklist)

```
STEP 1: GATHER INFORMATION
□ Finalize week number
□ Confirm main topics (5 topics for 5 days)
□ Identify difficulty level
□ Determine time investment
□ Confirm prerequisites
□ Identify next week connection

STEP 2: GENERATE INSTRUCTIONAL FILES (Day 1-5)
□ Day 1: Topic 1 (11-section framework, 2,000-2,500 words)
□ Day 2: Topic 2 (11-section framework, 2,000-2,500 words)
□ Day 3: Topic 3 (11-section framework, 2,000-2,500 words)
□ Day 4: Topic 4 (11-section framework, 2,000-2,500 words)
□ Day 5: Topic 5 (11-section framework, 2,000-2,500 words)

STEP 3: GENERATE SUPPORT FILES (5 Types)
□ Checklist & Progress Tracking
□ Summary & Quick Reference
□ Roadmap & Time Budget
□ Q&A Practice Questions (10 per day)
□ Complete Index & Navigation

STEP 4: GENERATE ENHANCED GUIDELINES
□ 12-section master overview
□ 3,000-4,000+ words
□ All sections complete
□ Comprehensive coverage

STEP 5: VERIFICATION
□ All files generated
□ All files downloadable
□ All sections complete
□ No gaps or missing content
□ Quality standards met

STEP 6: DELIVERY
□ List all files
□ Confirm artifact IDs
□ Provide download instructions
□ Ready for student/instructor use

Total: 5 instructional + 5 support + 1 guidelines = 11 Files
Time: ~5-6 hours learning, ~2-3 hours practice (varies by week)
Status: Ready for immediate use
```

---

## 🚀 QUICK REFERENCE: WHICH SECTION TO USE

### Quick Selection Guide

**Use SECTION A (Full Week)** when:
- You want all files at once
- You're generating a complete week
- You have all week information ready
- You want parallel generation

**Use SECTION B (Day-by-Day)** when:
- You're generating one day at a time
- You want to focus on a single topic
- You're doing sequential generation
- You want more control per day

**Use SECTION C (Support Files)** when:
- You already have instructional content
- You want to add support materials
- You're enhancing existing week
- You need specific support type

**Use SECTION D (Guidelines)** when:
- You want the master overview
- You're planning a week
- You're setting curriculum
- You need week summary

**Use SECTION E (Complete Workflow)** when:
- You're doing full generation
- You want a checklist to follow
- You're managing the complete process
- You need step-by-step guidance

---

## 💡 CUSTOMIZATION EXAMPLES

### Example 1: Week 5 (Greedy Algorithms)
```
Week Number: 5
Topics: 
  Day 1: Greedy Algorithm Fundamentals
  Day 2: Activity Selection & Interval Scheduling
  Day 3: Huffman Coding & Compression
  Day 4: Job Sequencing & Fractional Knapsack
  Day 5: Greedy Integration & Advanced Patterns

Use: SECTION A (Full Week Generation)
```

### Example 2: Just Day 3 Content
```
Week Number: [ANY]
Day Number: 3
Topic: [SPECIFIC TOPIC]

Use: SECTION B (Day-by-Day Generation)
```

### Example 3: Add Support to Existing Week
```
Week Number: [EXISTING WEEK]
Need: All 5 support files

Use: SECTION C (Support Files Generation)
```

### Example 4: Master Plan Overview
```
Week Number: 4
Need: Guidelines only

Use: SECTION D (Enhanced Guidelines)
```

---

## 📥 USAGE INSTRUCTIONS

### How to Use This Master Prompt

1. **Choose Your Section** (A, B, C, D, or E)
2. **Copy the Relevant Section**
3. **Replace Placeholders** with your values
4. **Paste into New Chat/Prompt**
5. **Execute Generation**
6. **Download Files** as they're created
7. **Verify Quality** against checklist
8. **Share with Students/Instructors**

### Template Variables to Replace

```
[NUMBER] → Week number (1, 2, 3, etc.)
[TOPIC] → Specific topic name
[MAIN TOPIC] → Week's main focus
[SUBTOPICS] → List of 3-5 subtopics
[HOURS] → Time investment (e.g., "8-10 hours")
[EASY/MEDIUM/HARD] → Difficulty level
[PREVIOUS WEEK] → Previous week name
[NEXT WEEK] → Next week name
[CALCULATE:] → Do math shown in brackets
[SPECIFIC INSTRUCTION] → Custom instruction
```

---

## ✅ QUALITY ASSURANCE CHECKLIST

For each generation request, verify:

**Instructional Files:**
- [ ] 11 sections present
- [ ] 2,000-2,500 words
- [ ] Code examples included (15-20)
- [ ] Visualizations included (10-15)
- [ ] Complexity analysis complete
- [ ] All sections have content
- [ ] Markdown formatted correctly
- [ ] Links included

**Support Files:**
- [ ] All 5 types generated
- [ ] Consistent formatting
- [ ] Complete content
- [ ] Checkboxes functional
- [ ] Tables properly formatted
- [ ] Clear organization
- [ ] All sections filled
- [ ] Ready to download

**Guidelines File:**
- [ ] All 12 sections present
- [ ] 3,000-4,000+ words
- [ ] Professional formatting
- [ ] All mandatory sections
- [ ] Complete coverage
- [ ] Clear structure
- [ ] Proper hierarchy
- [ ] Ready to download

**Overall Package:**
- [ ] All files generated
- [ ] Consistent quality
- [ ] No gaps or missing content
- [ ] All downloadable
- [ ] Professional presentation
- [ ] Ready for immediate use
- [ ] Exceeds expectations
- [ ] Production ready

---

## 📞 TROUBLESHOOTING

**If a file seems incomplete:**
- Check against the relevant section checklist
- Verify all mandatory items included
- Regenerate if missing sections
- Request specific section enhancement

**If formatting looks wrong:**
- Verify markdown syntax
- Check table formatting
- Confirm checkbox format
- Request reformatting if needed

**If content needs customization:**
- Identify specific customization needed
- Provide detailed instructions
- Request targeted enhancement
- Verify output matches needs

**If you need help:**
- Review the relevant section
- Check examples provided
- Refer to customization section
- Request clarification on instructions

---

## 🎓 BEST PRACTICES

1. **Always use SECTION A** for complete weeks (most efficient)
2. **Use SECTION B** only for individual days or when updating
3. **Complete all prompts** - don't skip sections
4. **Verify completeness** before downloading
5. **Review quality** against checklist
6. **Customize** only when truly needed
7. **Share examples** with students
8. **Track completion** with checklist files
9. **Update guidelines** as you go
10. **Iterate** based on feedback

---

## 📊 FILE COUNT SUMMARY

By using this master prompt:

**Full Week Generation (Section A):**
- 5 instructional files (Day 1-5)
- 5 support files
- 1 guidelines file
- **Total: 11 files per week**

**Estimated Word Count:**
- Instructional: ~12,500 words (5 × 2,500)
- Guidelines: ~3,500 words
- Support: ~15,000 words
- **Total: ~31,000 words per week**

**Estimated Time Investment:**
- Learning: 5-7 hours
- Practice: 2-3 hours
- **Total: 7-10 hours per week**

---

## 🚀 FINAL NOTES

This master prompt enables:
✅ Complete curriculum generation
✅ Consistent quality across weeks
✅ Professional-grade materials
✅ Student-ready content
✅ Instructor resources
✅ Interview preparation
✅ Full documentation
✅ Downloadable formats

Use sections as needed.
Customize for your context.
Generate with confidence.
Deliver with quality.

---

**Master Prompt Version:** 2.0 Enhanced  
**Status:** Production Ready ✅  
**Last Updated:** December 26, 2025, 22:05 IST  
**Ready to Use:** YES ✅

