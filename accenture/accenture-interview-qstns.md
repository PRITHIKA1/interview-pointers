# Accenture On-Campus Placement — Complete Preparation Guide (2026)

> Compiled from the latest (2026 cycle) candidate-reported interview experiences, official pattern updates, and prep-portal data (PrepInsta, Unstop, Indeed, PlacementPreparation.io, Naukri). Confirm exact section counts/timings on your college's official test invite, since Accenture varies this slightly by campus and drive.

---

## 1. Overview of the Process

Accenture's campus hiring (2026 batch) runs in **3 broad stages**, each with sub-rounds:

| Stage | Round | Nature |
|---|---|---|
| 1 | Pre-Placement Talk (PPT) | Informational, non-elimination |
| 2 | **Online Assessment (NLT / MyAccess portal)** — 3 sub-rounds, ~175 minutes total | Elimination (sectional cut-offs) |
| 3 | **Technical Interview + HR Interview** (often combined into one panel) | Final selection |

Total questions across the online test: **~125 questions in 175 minutes.**

| Round | Assessment | No. of Questions | Duration |
|---|---|---|---|
| 1st | Behavioral / Psychometric Assessment | 54 | 20 min |
| 1st | Cognitive Assessment (Gamified) | 3 | 20 min |
| 2nd | Technical Assessment (MCQs) | 45 | 45 min |
| 2nd | Coding Assessment | 3 problems | 60 min |
| 3rd | Communication Assessment (AI-graded spoken English) | ~20–25 | 30 min |
| **Total** | | **~125** | **~175 min** |

**Key rules:**
- No negative marking.
- Each section has an **individual sectional cut-off** — you must clear every section, not just score well overall, to move ahead.
- Inter-sectional navigation is generally allowed within a section's time block.
- The **Communication Assessment (AI-graded spoken English)** has reportedly rejected technically strong candidates who skipped practicing it — don't ignore this round.

---

## 2. Round-by-Round Breakdown: What to Prepare

### Round 1A — Behavioral / Psychometric Assessment (54 Qs, 20 min)
Situational judgment / personality-style questions (agree–disagree, workplace scenarios).

**What to prepare:**
- Be consistent — the platform cross-checks for contradictory answers, so answer honestly rather than trying to "game" an ideal personality.
- Focus themes: teamwork, client orientation, adaptability, integrity, handling pressure.
- No right/wrong answers, but avoid extreme responses (always/never) — pick balanced, professional choices.

### Round 1B — Cognitive Assessment (Gamified, 3 Qs, 20 min)
Game-based puzzles replacing traditional quant/logical/verbal sections in the new pattern.

**What to prepare:**
- Practice game-based aptitude formats: pattern recognition, sequencing, spatial reasoning, quick decision-making games.
- Speed and consistency matter more than deep calculation — these are timed, intuitive games.
- Practice on PrepInsta's "Game Based Aptitude" or similar gamified-assessment practice sets.

### Round 2A — Technical Assessment (MCQs, 45 Qs, 45 min)
Covers three sub-topics:

| Topic | Focus Areas |
|---|---|
| **Fundamentals of Networking, Security & Cloud** | OSI/TCP-IP model, IP addressing, firewalls, encryption basics, cloud service models (IaaS/PaaS/SaaS), common cyber-attack types |
| **Common Applications & MS Office** | MS Excel formulas/shortcuts, MS Word, PowerPoint basics, general OS/computer fundamentals |
| **Pseudo Code** | Reading pseudo-code snippets and predicting output/logic (loops, conditionals, arrays, recursion) — this is the highest-weightage, highest-difficulty sub-section |

**Prep tips:**
- Pseudo-code carries the most weight and is rated "high difficulty" — practice reading unfamiliar pseudo-code syntax (not tied to one language) and tracing variable values by hand.
- Networking/Cloud/Security: revise basic definitions, don't go too deep — these are conceptual MCQs, not scenario-heavy.

### Round 2B — Coding Assessment (3 problems, 60 min) — Elimination Round
Languages allowed: **C, C++, Java, Python, JavaScript, HTML/CSS, .NET**

**What to prepare:**
- 2–3 problems, easy-to-moderate difficulty (arrays, strings, basic math/logic, sorting, searching, pattern printing).
- Practice on HackerRank / LeetCode (Easy tier) / PrepInsta's "Top 100 Codes."
- This round's score is **carried forward and considered again at the final interview stage**, so don't treat it as pass/fail only — a strong solution here helps your interview standing too.
- Focus on writing clean, compiling code over cleverness — partial test cases still earn partial credit.

**Common coding topics seen in recent drives:**
- Array manipulation (reverse, rotate, find duplicates)
- String manipulation (palindrome, anagram, reversal, frequency count)
- Number theory (prime check, factorial, Fibonacci, Armstrong numbers)
- Basic pattern printing
- Simple recursion problems

### Round 2C — Communication Assessment (AI-graded, ~20–25 Qs, 30 min)
Tests spoken/written English: read-aloud, sentence repeat, short spoken answers, sometimes short essay/typing.

**What to prepare:**
- Practice speaking clearly at a natural pace into a mic — clarity and grammar matter more than accent.
- Avoid long pauses, filler words ("umm," "like"), and don't rush.
- Practice a few "describe yourself," "describe your favorite place/hobby" one-minute spoken answers out loud beforehand.
- This is graded by AI and candidate reports show it has rejected otherwise-strong technical candidates — take it seriously, don't skip mock practice.

---

## 2A. ACTUAL QUESTIONS REPORTED — Online Assessment Rounds

> These are real, candidate-reported questions/patterns from recent Accenture drives (compiled from PrepInsta, ImpactMillions, and GeeksforGeeks question banks used for 2025–2026 batches). The exact numbers won't repeat verbatim every drive, but the **patterns repeat heavily** — practice these formats and you'll recognize the logic instantly on the real test.

### Pseudo-Code — Actual Question Patterns (with answers)

**Loops:**
```
Integer i, sum
Set sum = 0
for(i = 1 to 5)
  sum = sum + i
end for
```
Q: What is the value of `sum`? → **Answer: 15** (sum of 1 to 5)

**Recursion:**
```
Integer fun(Integer n)
  if (n <= 0) return 1
  return n * fun(n - 1)
```
Q: Output of `fun(2)`? → **Answer: 2** (computes factorial: 2 × fun(1) = 2 × 1 = 2)

**Bitwise Operators (a recurring high-frequency topic):**
- `Integer a = 5, b = 3; Print a & b` → **Answer: 1** (0101 AND 0011 = 0001)
- `Integer x = 8; x = x << 1; Print x` → **Answer: 16** (left shift doubles the value)
- `Integer x = 12; x = x >> 2; Print x` → **Answer: 3** (right shift by 2 = divide by 4)
- `Integer a = 9, b = 5; Print a ^ b` → **Answer: 12** (XOR)
- `Integer x = 7; x = ~x; Print x` → **Answer: -8** (bitwise NOT / two's complement)

**Arrays:**
```
Integer arr[3] = {2, 4, 6}
Print arr[1]
```
Q: Output? → **Answer: 4** (zero-indexed, so arr[1] is the 2nd element)

**Increment/Decrement:**
```
Integer x = 5, y
y = ++x
Print y
```
Q: Value of y? → **Answer: 6** (pre-increment happens before assignment)

**Number logic (frequently asked as "trace this and find output"):**
- Reverse a number: `while(num > 0) { digit = num%10; reversed = reversed*10 + digit; num = num/10 }` for num=1234 → **Answer: 4321**
- Sum of digits: same loop style, but `sum = sum + digit` for num=1234 → **Answer: 10**
- Factorial using a for-loop for n=5 → **Answer: 120**
- Prime check using a for-loop with `sqrt(num)` bound
- Fibonacci series generation (first 10 terms): **0 1 1 2 3 5 8 13 21 34**
- Bubble sort trace on a small array — asked to give the final sorted output
- Pattern printing (right triangle of `*`, inverted triangle) — asked to identify what the nested loop prints

**Stack-based questions (LIFO logic):**
```
Stack S
S.push(10)
S.push(20)
S.pop()
S.push(30)
S.size()
```
Q: Final size? → **Answer: 2** — practice tracing 4–5 push/pop/peek operations in sequence; this format repeats often.

**Prep tip:** Almost all pseudo-code questions fall into these 8 buckets: loops, recursion, arrays, bitwise ops, increment/decrement, conditionals, basic stack operations, and "trace and predict output." Master tracing variable values step-by-step on paper — that's the actual skill being tested.

---

### Coding Round — Actual Problems Asked (real problem statements, reported from recent on-campus & off-campus drives)

These are the **exact problem types** that have been reported repeatedly across Accenture drives — solve each one in your chosen language before the test:

1. **Rat Count House problem** — Given `r` rats, `unit` food needed per rat, and an array `arr` representing food in each house, find the minimum number of houses (from the start) whose combined food is enough to feed all rats. *(Tests: array traversal + running sum + early exit logic)*

2. **Binary String Operations** — A string of binary digits separated by A (AND), B (OR), C (XOR), e.g. `"1C0C1C1A0B1"`. Evaluate left to right, one operation at a time, and return the result. *(Tests: string parsing + bitwise logic)*

3. **Password Checker** — Return 1 if a string is a valid password: at least 4 characters, at least one digit, at least one capital letter, no space/slash, and must not start with a number. Else return 0. *(Tests: string validation logic)*

4. **Find Count within Difference** — Given an array, a number `num`, and a max difference `diff`, count how many array elements have `|arr[i] - num| <= diff`. *(Tests: array traversal + absolute difference)*

5. **Difference of Sums** — Given `n` and `m`, find the sum of all numbers from 1 to m NOT divisible by n, minus the sum of numbers that ARE divisible by n. *(Tests: loops + modulo)*

6. **Second Largest/Smallest from Even/Odd positions** — Given an array, find the second-largest element among even-indexed elements + second-smallest among odd-indexed elements, then return their sum. *(Tests: array indexing + sorting logic)*

7. **N-Base Notation Conversion** — Convert a decimal number to base-n notation (using digits 0–9, then A–Z for 10–35). *(Tests: number base conversion, division/modulo loop)*

8. **Move Hyphens to Front** — Given a string containing letters and hyphens, move all hyphens to the front while preserving the order of other characters. *(Tests: string manipulation, two-pointer technique)*

9. **Count Carries in Addition** — Given two numbers, count how many carry operations occur when adding them digit by digit (right to left). *(Tests: digit-by-digit arithmetic simulation)*

10. **Swap Two Characters Throughout String** — Replace every occurrence of `ch1` with `ch2` and vice versa in a given string. *(Tests: string traversal + character swapping)*

11. **Choice-Based Arithmetic Operation** — Given `a`, `b`, and a choice `c` (1=add, 2=subtract, 3=multiply, 4=divide), return the corresponding result. *(Tests: basic conditional logic — often a "warm-up" easy question)*

12. **Maximum Power-of-2 in Range** — Find the number between `a` and `b` with the highest exponent of 2 dividing it. *(Tests: loops + bit/factor counting)*

13. **Sum of Numbers Divisible by Both 3 and 5** — Between `m` and `n`, sum all numbers divisible by both. *(Tests: simple loop + modulo — common "easy" question)*

14. **Autobiographical Number Check** — A number where digit at position `i` equals the count of digit `i` in the number itself (e.g., "1210" is autobiographical). Return the count of distinct digits if valid, else 0. *(Tests: string/array frequency logic — a "hard" question)*

15. **Find Max Element and Its Index** — Standard array traversal to print the maximum value and its index. *(Very common "easy" warm-up question)*

16. **Palindrome numbers in a range** — Print all palindrome numbers between a lower and upper limit.

17. **Distance between three points** — Basic geometry/math: compute pairwise distances using the distance formula and sum them.

18. **Multiplication table + sum of multiples** — Print the first 10 multiples of a number and their sum.

**Pattern to notice:** Accenture reuses this exact pool of problems (or very close variants) across on-campus and off-campus drives — most are array/string manipulation, basic math/number theory, or simple simulation logic. None require advanced DSA (no trees/graphs/DP) — the focus is **clean, correct, compiling code**, not algorithmic cleverness.

**Scoring:** You need **2 complete outputs + 1 partial output minimum** to clear this round.

---

### Communication Assessment — What's Actually Asked
- Read-aloud sentences (checks pronunciation & fluency)
- Sentence repeat (listen and repeat exactly)
- Short spoken answers to prompts like "Describe your hometown," "Talk about a skill you're proud of," "Describe your favorite subject" (30–60 seconds each)
- Grammar/sentence-correction MCQs mixed in
- Sometimes a short typing/dictation task

---

## 3. Final Round — Technical + HR Interview

Accenture typically merges Technical and HR into **one panel interview** (sometimes two separate short interviews back-to-back) for campus freshers. Expect **20–30 minutes total.**

### A. Technical Interview — Topics to Prepare

| Topic | Sub-areas |
|---|---|
| **OOPs Concepts** | Encapsulation, Inheritance, Polymorphism, Abstraction; constructor vs destructor; virtual functions |
| **Data Structures & Algorithms** | Arrays, Linked Lists, Stacks, Queues, Trees, basic sorting/searching, time complexity basics |
| **DBMS / SQL** | Joins, normalization, keys (primary/foreign/candidate), subqueries, ACID properties, stored procedures |
| **Core Language (your chosen language)** | Java: JVM/JRE/JDK, exception handling; C/C++: memory allocation, pointers; Python: basic data structures |
| **Operating Systems basics** | Process vs thread, deadlock, memory management (light-touch, only if you mention OS in resume) |
| **Your Resume/Projects** | Be ready to explain every project/internship in detail — this is a very common deep-dive area |
| **Basic Networking** (if relevant) | OSI layers, IP addressing (carried over from the assessment round) |

### B. Full List — 30 Most Frequently Reported Technical Questions

*(Compiled from multiple recent candidate-report sources; not every question is asked to every candidate — the interviewer typically picks 5–8 based on your resume/language.)*

1. What are the similarities/differences between Java and C++?
2. Explain the memory allocation process in C.
3. What is recursion? Give an example.
4. What is a Collection Framework in Java?
5. Explain exception handling (try-catch-finally).
6. What is virtual inheritance in C++?
7. What is JDBC?
8. List Coffman's conditions that lead to deadlock.
9. What are short-term, long-term, and medium-term scheduling (OS)?
10. Write a program for the Fibonacci series.
11. What is a classifier in Python?
12. What are lambda expressions in Java?
13. What is the significance of `super` and `this` keywords in Java?
14. Explain the basic features/pillars of OOPs.
15. What is the length limit of an identifier?
16. Name the types of polymorphism in C++ (compile-time vs runtime).
17. What is database normalization? Name its forms.
18. What is the purpose of a classifier in Python? *(repeat variant of Q11)*
19. What is XML, and where is it used?
20. What are the different types of interfaces in Java?
21. What is encapsulation in Java?
22. What are the three types of loops in Java (for, while, do-while)?
23. What is a SortedMap in Java?
24. What is the difference between `sleep()` and `wait()` in Java?
25. Differentiate between a constructor and a destructor.
26. What is a Linked List class — how would you implement one?
27. What are the limitations of enumeration (enum) in Java?
28. Explain the difference between JRE, JDK, JVM, and JIT.
29. What is an overflow error?
30. Explain pointers and memory allocation in C (malloc/calloc/free).

**Plus, almost universally asked:**
- SQL: joins, subqueries, normalization, primary/foreign keys, `GROUP BY` vs `HAVING`
- DBMS: ACID properties, stored procedures, indexing
- A deep-dive into **your resume/final-year project** — expect 3–5 follow-up questions here regardless of your branch

### C. Sample Technical Q&A (Full answers for the most-repeated ones)

**Q1: What is Object-Oriented Programming? Explain its main features.**
> OOP is a programming paradigm based on the concept of "objects" containing data and methods. Its four pillars are:
> - **Encapsulation** – bundling data and methods together, restricting direct access to some components.
> - **Inheritance** – a class acquiring properties/behavior of another class.
> - **Polymorphism** – the same function/operator behaving differently based on context (overloading/overriding).
> - **Abstraction** – hiding implementation details and showing only essential features.

**Q2: Differentiate between a constructor and a destructor.**
> A constructor is a special method automatically invoked when an object is created; it initializes the object and has the same name as the class with no return type. A destructor is invoked automatically when an object goes out of scope/is destroyed, used to free resources; in C++ it's written as `~ClassName()`.

**Q3: Explain the difference between JDK, JRE, JVM, and JIT (for Java candidates).**
> - **JVM (Java Virtual Machine):** Executes Java bytecode; platform-dependent implementation that makes Java "write once, run anywhere."
> - **JRE (Java Runtime Environment):** JVM + libraries needed to *run* Java applications (no compiler).
> - **JDK (Java Development Kit):** JRE + development tools (compiler, debugger) needed to *build* Java applications.
> - **JIT (Just-In-Time compiler):** Part of the JVM that compiles bytecode to native machine code at runtime for faster execution.

**Q4: What is SQL, and why is it used?**
> SQL (Structured Query Language) is the standard language for creating, querying, updating, and managing relational databases. It's used for data definition (DDL), data manipulation (DML), and data control (DCL) across virtually all RDBMS products like MySQL, Oracle, and SQL Server.

**Q5: What are joins in SQL? Name the types.**
> A join combines rows from two or more tables based on a related column. Types: **INNER JOIN** (matching rows only), **LEFT JOIN** (all left table rows + matches), **RIGHT JOIN** (all right table rows + matches), **FULL OUTER JOIN** (all rows from both, matched where possible), and **SELF JOIN** (table joined with itself).

**Q6: What is recursion? Why is it useful?**
> Recursion is when a function calls itself to solve smaller instances of the same problem, with a base case to terminate it. It's useful because it can make code shorter and more readable for problems like tree traversal, factorial, or Fibonacci — though it trades off some memory/stack usage versus iterative solutions.

**Q7: Explain Virtual Inheritance in C++ (advanced/only if C++ is on resume).**
> Virtual inheritance ensures a derived class inherits only **one copy** of a base class's members even if it's reached through multiple inheritance paths. E.g., if B and C both inherit from A, and D inherits from both B and C, without virtual inheritance D gets two copies of A's members; with `virtual` inheritance it gets just one, avoiding the "diamond problem."

**Q8: Explain your final-year/major project in detail.**
> Be ready to explain: problem statement, your specific role, tech stack used, key challenges faced and how you solved them, and the outcome/impact. Interviewers often go 2–3 levels deep with follow-ups ("why did you choose X over Y," "what would you improve now"), so know your project inside-out — don't list technologies you can't explain.

**Q9: What is normalization in DBMS?**
> Normalization is the process of organizing database tables to reduce redundancy and improve data integrity, done through a series of forms (1NF, 2NF, 3NF, BCNF) — each removing a specific type of anomaly (e.g., repeating groups, partial/transitive dependency).

**Q10: What are Stored Procedures? Where are they stored?**
> A stored procedure is a precompiled collection of SQL statements saved in the database that can be executed as a single call. They're stored within the database itself (in the system catalog/metadata), improving performance (no repeated parsing) and reusability, and allowing centralized business logic.

**Q11: What is the difference between `sleep()` and `wait()` in Java?**
> `sleep()` pauses the current thread for a fixed time without releasing any lock it holds. `wait()` pauses the thread until another thread calls `notify()`/`notifyAll()`, and it *does* release the lock while waiting — used for inter-thread communication rather than a simple timed pause.

**Q12: List Coffman's conditions that lead to deadlock (OS).**
> Four conditions must hold simultaneously: **Mutual Exclusion** (resource held exclusively by one process), **Hold and Wait** (a process holds a resource while waiting for another), **No Preemption** (a resource can't be forcibly taken away), and **Circular Wait** (a closed chain of processes each waiting on the next).

**Q13: What are the limitations of enum in Java?**
> An enum can't extend another class (since it implicitly extends `java.lang.Enum`), its constants are fixed at compile time (can't be created dynamically), and each enum constant is a singleton, which limits flexibility for cases needing multiple mutable instances of similar objects.

**Q14: What is XML and where is it used?**
> XML (Extensible Markup Language) is a markup language for encoding documents in a format readable by both humans and machines. It's used to structure and exchange data across systems — e.g., configuration files, web service messages (SOAP), and data interchange between applications with different platforms/languages.

---

### D. HR Interview — Full List of Reported Questions + Sample Answers

Accenture's HR round is described consistently across sources as **conversational, not aggressive** — it evaluates fit, communication, and basic behavioral/situational responses.

**The 10 most frequently reported HR questions:**
1. What are the major businesses/divisions of Accenture?
2. What, according to you, are the core values of Accenture?
3. Why do you want to join us / why Accenture?
4. What are your career goals — where do you see yourself in 5 years?
5. How can you contribute to Accenture's continuous quest for excellence?
6. What are your strengths and weaknesses?
7. What are your long-term career goals?
8. What is your strategy for resolving conflicts with team members?
9. What work environment do you expect?
10. Have you faced any obstacles while working on a project, and how did you overcome them?

**Plus these near-universal ones:**
- Tell me about yourself.
- Are you willing to relocate / work rotational shifts?
- Do you have any questions for us?

**Q1: Tell me about yourself.**
> Keep it to 60–90 seconds: education → key strengths/skills → 1 standout project or achievement → why you're a good fit for the role. Practice this out loud — it's asked in nearly every interview experience.
>
> *Sample structure:* "Good morning, I'm [Name], a final-year B.Tech student in [branch] from [college]. I've built a strong foundation in [core skills], and led/worked on [project/achievement]. I was also [leadership role, e.g., class rep/club lead], which sharpened my communication and teamwork. I'm looking to start my career at a place like Accenture where I can apply my technical skills on real client projects while continuing to learn."

**Q2: Why do you want to join Accenture?**
> Mention Accenture's scale and diversity of work (multiple industries and technologies), the learning/upskilling culture, and how that aligns with your goal of building a strong, varied technical foundation early in your career. Avoid generic "it's a good company" answers — be specific.

**Q3: What are your strengths and weaknesses?**
> Pick a real strength relevant to the job (e.g., problem-solving, adaptability) with a one-line example. For weakness, pick something genuine but not disqualifying, and show you're actively working on it (e.g., "I used to hesitate presenting in large groups, so I started taking up presentation opportunities in college to improve").

**Q4: Are you comfortable working in rotational shifts / relocating?**
> Accenture serves global clients, so shift work and relocation are common. Answer honestly, but if you say yes, mean it — this is a genuine fit-check, not a formality.

**Q5: Describe a time you faced an obstacle in a project/team and how you handled it.**
> Use the **STAR method** (Situation, Task, Action, Result). Keep it specific and end with what you learned — interviewers value self-awareness over a "perfect" story.

**Q6: Where do you see yourself in 5 years?**
> Show ambition balanced with realism and loyalty to growing within the company — e.g., growing into a senior technical/consulting role, taking certifications, eventually leading a small team, ideally framed around growing *with* Accenture.

**Q7: Do you have any questions for us?**
> Always have 1–2 ready — e.g., about the training program, typical project allocation for freshers, or growth/certification opportunities. Never say "no."

---

## 4. Round-Wise Preparation Checklist

- [ ] **Cognitive/Gamified round:** Practice 3–4 gamified aptitude mock sets for speed and pattern recognition.
- [ ] **Technical MCQs:** Revise networking basics, MS Office shortcuts, and practice 30–40 pseudo-code tracing questions.
- [ ] **Coding round:** Solve 40–50 easy-level problems (arrays, strings, recursion, patterns) in your chosen language; ensure you can write bug-free, compiling code under time pressure.
- [ ] **Communication round:** Do 3–4 timed mock spoken-English recordings; listen back and fix pace/clarity/filler words.
- [ ] **Technical interview:** Revise OOPs, DBMS/SQL, your core language's fundamentals, and rehearse a 2-minute walkthrough of every project on your resume.
- [ ] **HR interview:** Prepare and rehearse (out loud) answers to: self-intro, why Accenture, strengths/weaknesses, one STAR-format behavioral story, and 2 questions to ask the interviewer.
- [ ] **General:** Carry resume copies, a valid photo ID, and dress in formal business attire; review Accenture's recent news/services (Consulting, Technology, Operations, Song) briefly so you can speak to "why Accenture" with substance.

---

## 5. Quick Reference: Recruitment Flow Diagram

```
Pre-Placement Talk
        │
        ▼
Online Assessment (NLT/MyAccess) — ~175 min total
  ├─ Behavioral/Psychometric (54 Qs, 20 min)
  ├─ Cognitive/Gamified (3 Qs, 20 min)
  ├─ Technical MCQs (45 Qs, 45 min)          ← sectional cut-off
  ├─ Coding (3 problems, 60 min)              ← elimination + score carried to interview
  └─ Communication Assessment (~20-25 Qs, 30 min)  ← AI-graded spoken English
        │
        ▼
Technical + HR Interview (combined panel, ~20-30 min)
        │
        ▼
        Offer
```

---

### Sources referenced
This guide synthesizes patterns and actual reported questions from: PrepInsta's Accenture Syllabus, Coding Questions & Pseudo-Code banks (2026), ImpactMillions' Accenture Pseudo-Code question archive, Indeed's "Top 40 Accenture Interview Questions" (2026), Unstop's Accenture Recruitment Process & Coding Questions articles, PlacementPreparation.io, GeeksforGeeks' Accenture Pseudocode Quiz, and recent (2026) Glassdoor Accenture interview experience snippets. Since Accenture doesn't officially publish exact section timings or a fixed question bank, **have your brother confirm the exact pattern on the official test invite email / campus placement cell notice closer to the drive date**, and treat the coding/pseudo-code questions here as high-probability *practice patterns* rather than a guaranteed leaked paper — Accenture rotates and remixes this pool across drives.