# Accenture Interview — Latest Question Bank (2026 Batch)

> **Purpose:** This file is a pure question-bank — real, candidate-reported questions from recent Accenture on-campus drives (2024–2026), organized by round. Pair this with the process/strategy guide; use *this* file for actual drilling/practice. Sourced from GeeksforGeeks interview experiences, Naukri Code360 candidate reports, PrepInsta, Glassdoor (2026), Indeed, and ImpactMillions.
>
> **Note on this version:** All coding-round solutions have been converted from Python to **C++**.

---

## 0. A Real, Complete Interview Timeline (Sept 2024 batch, verified end-to-end)

A B.Tech candidate's full reported journey — useful to see how everything connects:

**Round 1 — Cognitive & Technical Assessment (90 min, 90 questions, 6 sections):**
English Ability, Abstract Reasoning, Critical Reasoning, Pseudo Code (Loops/Operators/Recursion), MS Office & Common Application, Computer Networking Security & Cloud (situation-based).

**Round 1B — Coding Assessment (45 min, 2 questions):**
1. *Rebound Height* — simulate a ball bouncing and losing height by a percentage each bounce; find height after N bounces or number of bounces till height < threshold.
2. *Count the highest decrement of temperature in an array (sub-array)* — given a temperature array, find the maximum drop between any two points in a contiguous subarray.

**Round 1C — Communication Assessment:**
- Read aloud a passage
- Listen to a narrative, repeat it back within a time limit
- Answer spoken questions
- "Just a Minute" (JAM) — speak on a topic for 60 seconds

**Round 2 — Technical + HR (25 min, combined, NOT purely technical):**
1. Introduce yourself.
2. What is your hobby?
3. Are you a pass-out graduate or in your final year?
4. Tell me about your final-year project.
5. How did you implement that system? *(this candidate had a Hybrid project)*
6. What technologies did you use?
7. What would you want to add/implement in your project in the future?
8. Which programming language did you use for your project?
9. Was it a solo or group project?
10. What was your specific role in the project?
11. When have you felt proudest in your life, and why?
12. When have you felt lowest in your life, and why?
13. **Situational:** If you're the team leader and one team member can't complete their task, what do you do?
14. **Situational:** If your project isn't completed on time, what do you do?
15. **Situational:** If there's a conflict between team members, how do you manage it?
16. **Situational:** If your project isn't complete and the deadline is near, what do you do?
17. Do you have any questions for me? *(always have 1–2 ready)*

**Key takeaways from this and similar real reports:**
- The final round is very often **combined Technical + HR**, and for many candidates it leans HR/behavioral-heavy with light or zero deep technical questioning.
- **Situational/managerial questions** ("what would you do if...") are extremely common — prepare 3–4 of these using a calm, structured answer (acknowledge issue → communicate → propose solution → escalate only if needed).
- Project deep-dive is close to guaranteed — know your project cold.

---

## 1. Pseudo-Code Round — Latest Question Patterns (with answers)

### Programming Fundamentals
```
Integer x
Set x = 5
x = x + 5
Print x
```
**Q: Output?** → **10**

### Loops
```
Integer i
for(i = 0 to 4)
  Print "Hello"
end for
```
**Q: How many times is "Hello" printed?** → **5 times** (i = 0,1,2,3,4)

```
Integer i, sum
Set sum = 0
for(i = 1 to 5)
  sum = sum + i
end for
```
**Q: Final value of sum?** → **15**

### Arrays
```
Integer arr[3] = {2, 4, 6}
Print arr[1]
```
**Q: Output?** → **4** (zero-indexed)

```
Integer arr[3] = {1, 2, 3}
arr[2] = arr[0] + arr[1]
```
**Q: Value of arr[2]?** → **3**

### Recursion
```
Integer fun(Integer n)
  if (n <= 0) return 1
  return n * fun(n - 1)
```
**Q: Output of fun(2)?** → **2** *(computes factorial: 2 × fun(1) = 2 × 1 = 2)*

```
Integer fun(Integer n)
  if (n == 0) return 1
  else return n + fun(n - 1)
```
**Q: What does this compute?** → **Sum of integers from n down to 1**

### Bitwise Operators — HIGH FREQUENCY, practice these thoroughly
| Snippet | Answer | Why |
|---|---|---|
| `a=5, b=3; Print a & b` | **1** | AND of 0101 & 0011 |
| `x=8; x = x << 1` | **16** | left shift doubles value |
| `x=12; x = x >> 2` | **3** | right shift ÷4 |
| `a=9, b=5; Print a ^ b` | **12** | XOR |
| `x=7; x = ~x` | **-8** | bitwise NOT (two's complement) |
| `a=4, b=7; Print a & ~b` | **0** | AND with complement |
| `x=15; x = x << 3` | **120** | left shift ×8 |
| `a=10, b=15; Print a \| ~b` | **-6** | OR with complement |
| `x=24; x = x >> 4` | **1** | right shift ÷16 |
| `x=-8; x = ~x` | **7** | NOT on negative (two's complement) |

### Increment / Decrement
```
Integer x = 5, y
y = ++x
Print y
```
**Q: Value of y?** → **6** (pre-increment happens before assignment)

### Conditional Statements
```
Integer a=10, b=20
if (a > b) Print "a is greater"
else Print "b is greater"
```
**Q: Output?** → **"b is greater"**

### Stack Operations (LIFO — asked as sequential trace-the-output)
```
Stack S
S.push(10)
S.push(20)
S.pop()
S.push(30)
S.size()
```
**Q: Final size?** → **2**

```
Stack S
S.push(60)
S.push(70)
S.pop()
S.pop()
S.push(80)
S.peek()
```
**Q: Output of peek()?** → **80**

### Classic "Trace and Predict" Programs (very frequently reused)
1. **Reverse a number:** `while(num>0){ digit=num%10; rev=rev*10+digit; num=num/10 }` for num=1234 → **4321**
2. **Sum of digits:** same loop, `sum += digit` for num=1234 → **10**
3. **Factorial (iterative):** for n=5 → **120**
4. **Prime check:** loop i=2 to sqrt(num), check num%i==0 → for num=13 → **true (prime)**
5. **Fibonacci first 10 terms:** → **0 1 1 2 3 5 8 13 21 34**
6. **Bubble sort trace:** given an unsorted array, predict the final sorted output
7. **Right-triangle star pattern** (nested for loop i=1 to n, j=1 to i, print `*`)
8. **Inverted triangle star pattern** (loop i=n down to 1)
9. **Array reversal via swap:** `for(i=0 to 4){ temp=arr[i]; arr[i]=arr[4-i]; arr[4-i]=temp }`

**Prep tip:** ~90% of pseudo-code questions fall into: loops, recursion, arrays, bitwise ops, increment/decrement, conditionals, or basic stack traces. Practice tracing variables step-by-step on paper — that IS the skill being tested.

---

## 2. Coding Round — Latest Actual Problems (verbatim problem statements)

**Rules reminder:** 2–3 questions, 45–60 minutes. Languages: C, C++, Java, Python, JavaScript, HTML/CSS, .NET. Need **2 complete + 1 partial output minimum** to clear.

### Recently reported exact problems (2024–2025 drives):

**1. Rebound Height**
> A ball is dropped from a height and rebounds to a certain percentage of its previous height each time it bounces. Given the initial height and rebound percentage, calculate the height after N bounces (or the number of bounces until the height drops below a given threshold).

```cpp
#include <bits/stdc++.h>
using namespace std;

double reboundHeight(double height, double percent, int bounces) {
    for (int i = 0; i < bounces; i++) {
        height = height * (percent / 100.0);
    }
    return height;
}

int main() {
    cout << reboundHeight(100, 50, 3) << endl; // -> 12.5
    return 0;
}
```

**2. Count the Highest Decrement of Temperature (Sub-array)**
> Given an array of daily temperatures, find the maximum decrease in temperature between any earlier day and a later day within a contiguous subarray (i.e., the biggest single "drop" you can find looking forward).

```cpp
#include <bits/stdc++.h>
using namespace std;

int maxTempDrop(vector<int>& arr) {
    int maxDrop = 0;
    int peak = arr[0];
    for (int i = 1; i < arr.size(); i++) {
        if (arr[i] > peak) {
            peak = arr[i];
        } else {
            maxDrop = max(maxDrop, peak - arr[i]);
        }
    }
    return maxDrop;
}

int main() {
    vector<int> arr = {30, 25, 35, 10, 40, 5};
    cout << maxTempDrop(arr) << endl; // O(n) peak-tracking approach
    return 0;
}
```

**3. Rat Count House**
> Given `r` rats, `unit` food needed per rat, and array `arr` of food available in each house, return the minimum number of houses (from the start) whose combined food is enough to feed all rats. Return -1 if array is null; return 0 if total food insufficient.

```cpp
#include <bits/stdc++.h>
using namespace std;

int ratCountHouse(int r, int unit, vector<int>* arr) {
    if (arr == nullptr) return -1;
    long long needed = (long long)r * unit;
    long long total = 0;
    for (int i = 0; i < arr->size(); i++) {
        total += (*arr)[i];
        if (total >= needed) return i + 1;
    }
    return 0;
}

int main() {
    vector<int> arr = {2, 8, 3, 5, 7, 4, 1, 2};
    cout << ratCountHouse(7, 2, &arr) << endl; // -> 4
    return 0;
}
```

**4. Binary String Operations**
> A string like `"1C0C1C1A0B1"` represents binary digits separated by operators: A=AND, B=OR, C=XOR. Evaluate strictly left to right and return the result.

```cpp
#include <bits/stdc++.h>
using namespace std;

int binaryStringOps(string s) {
    if (s.empty()) return -1;
    int result = s[0] - '0';
    int i = 1;
    while (i < s.size()) {
        char op = s[i];
        int val = s[i + 1] - '0';
        if (op == 'A') result = result & val;
        else if (op == 'B') result = result | val;
        else if (op == 'C') result = result ^ val;
        i += 2;
    }
    return result;
}

int main() {
    cout << binaryStringOps("1C0C1C1A0B1") << endl; // -> 1
    return 0;
}
```

**5. Password Checker**
> Return 1 if a string is a valid password: minimum 4 characters, at least one digit, at least one capital letter, no space or slash, and must not start with a number. Else return 0.

```cpp
#include <bits/stdc++.h>
using namespace std;

int checkPassword(string s) {
    if (s.size() < 4) return 0;
    if (isdigit(s[0])) return 0;
    if (s.find(' ') != string::npos || s.find('/') != string::npos) return 0;

    bool hasDigit = false, hasUpper = false;
    for (char c : s) {
        if (isdigit(c)) hasDigit = true;
        if (isupper(c)) hasUpper = true;
    }
    if (!hasDigit || !hasUpper) return 0;
    return 1;
}

int main() {
    cout << checkPassword("aA1_67") << endl;        // -> 1
    cout << checkPassword("a987 abC012") << endl;    // -> 0
    return 0;
}
```

**6. Find Count Within Difference**
> Given array `arr`, integer `num`, and `diff`, count elements where `|arr[i] - num| <= diff`.

```cpp
#include <bits/stdc++.h>
using namespace std;

int findCount(vector<int>& arr, int num, int diff) {
    int count = 0;
    for (int x : arr) {
        if (abs(x - num) <= diff) count++;
    }
    return count > 0 ? count : -1;
}

int main() {
    vector<int> arr = {12, 3, 14, 56, 77, 13};
    cout << findCount(arr, 13, 2) << endl; // -> 3
    return 0;
}
```

**7. Difference of Sums**
> Given `n` and `m`: find sum of all numbers 1 to m NOT divisible by n, minus sum of numbers that ARE divisible by n.

```cpp
#include <bits/stdc++.h>
using namespace std;

int differenceOfSum(int n, int m) {
    long long divSum = 0, notDivSum = 0;
    for (int i = 1; i <= m; i++) {
        if (i % n == 0) divSum += i;
        else notDivSum += i;
    }
    return notDivSum - divSum;
}

int main() {
    cout << differenceOfSum(4, 20) << endl; // -> 90
    return 0;
}
```

**8. Second Largest/Smallest at Even/Odd Positions**
> Given an array, find the sum of the second-largest element among even-indexed elements and the second-smallest among odd-indexed elements. (0th index treated as even.)

```cpp
#include <bits/stdc++.h>
using namespace std;

int largeSmallSum(vector<int>& arr) {
    if (arr.empty() || arr.size() <= 3) return 0;

    vector<int> evenVals, oddVals;
    for (int i = 0; i < arr.size(); i++) {
        if (i % 2 == 0) evenVals.push_back(arr[i]);
        else oddVals.push_back(arr[i]);
    }
    sort(evenVals.begin(), evenVals.end());
    sort(oddVals.begin(), oddVals.end());

    return evenVals[evenVals.size() - 2] + oddVals[1];
}

int main() {
    vector<int> arr = {3, 2, 1, 7, 5, 4};
    cout << largeSmallSum(arr) << endl; // -> 7
    return 0;
}
```

**9. N-Base Notation Conversion**
> Convert a decimal number to base-n notation using digits 0–9 then A–Z for values 10–35.

```cpp
#include <bits/stdc++.h>
using namespace std;

string decToNBase(int n, int num) {
    string digits = "0123456789ABCDEFGHIJKLMNOPQRSTUVWXYZ";
    if (num == 0) return "0";
    string result = "";
    while (num > 0) {
        result = digits[num % n] + result;
        num /= n;
    }
    return result;
}

int main() {
    cout << decToNBase(12, 718) << endl; // -> "4BA"
    return 0;
}
```

**10. Move Hyphens to Front**
> Given a string of letters and hyphens, move all hyphens to the front while preserving the relative order of the letters.

```cpp
#include <bits/stdc++.h>
using namespace std;

string moveHyphen(string s) {
    int hyphens = count(s.begin(), s.end(), '-');
    string letters = "";
    for (char c : s) {
        if (c != '-') letters += c;
    }
    return string(hyphens, '-') + letters;
}

int main() {
    cout << moveHyphen("Move-Hyphens-to-Front") << endl; // -> "--MoveHyphenstoFront"
    return 0;
}
```

**11. Count Carries in Addition**
> Given two numbers, count how many "carry" operations occur when adding them digit by digit from right to left.

```cpp
#include <bits/stdc++.h>
using namespace std;

int countCarries(int num1, int num2) {
    int carry = 0, count = 0;
    while (num1 > 0 || num2 > 0) {
        int d1 = num1 % 10;
        int d2 = num2 % 10;
        int total = d1 + d2 + carry;
        if (total >= 10) {
            carry = 1;
            count++;
        } else {
            carry = 0;
        }
        num1 /= 10;
        num2 /= 10;
    }
    return count;
}

int main() {
    cout << countCarries(451, 349) << endl; // -> 2
    return 0;
}
```

**12. Swap Two Characters Throughout a String**
> Replace every occurrence of ch1 with ch2 and vice versa in a lowercase string.

```cpp
#include <bits/stdc++.h>
using namespace std;

string replaceCharacter(string s, char ch1, char ch2) {
    if (ch1 == ch2) return s;
    if (s.find(ch1) == string::npos && s.find(ch2) == string::npos) return s;

    string result = s;
    for (char& c : result) {
        if (c == ch1) c = ch2;
        else if (c == ch2) c = ch1;
    }
    return result;
}

int main() {
    cout << replaceCharacter("apples", 'a', 'p') << endl; // -> "paales"
    return 0;
}
```

**13. Choice-Based Arithmetic**
> Given a, b, and choice c (1=add, 2=subtract, 3=multiply, 4=divide), return the result. *(Common easy warm-up question)*

```cpp
#include <bits/stdc++.h>
using namespace std;

int operationChoice(int c, int a, int b) {
    if (c == 1) return a + b;
    else if (c == 2) return a - b;
    else if (c == 3) return a * b;
    else if (c == 4) return a / b;
    return 0;
}

int main() {
    cout << operationChoice(2, 16, 20) << endl; // -> -4
    return 0;
}
```

**14. Maximum Power-of-2 in a Range**
> Find the number between a and b (inclusive) with the highest exponent of 2 dividing into it; if tied, return the smaller number.

```cpp
#include <bits/stdc++.h>
using namespace std;

int exponentOf2(int x) {
    int count = 0;
    while (x != 0 && x % 2 == 0) {
        x /= 2;
        count++;
    }
    return count;
}

int maxExponent(int a, int b) {
    int bestNum = a, bestExp = exponentOf2(a);
    for (int i = a + 1; i <= b; i++) {
        int e = exponentOf2(i);
        if (e > bestExp) {
            bestNum = i;
            bestExp = e;
        }
    }
    return bestNum;
}

int main() {
    cout << maxExponent(7, 12) << endl; // -> 8
    return 0;
}
```

**15. Sum of Numbers Divisible by Both 3 and 5**
> Between m and n inclusive, sum all numbers divisible by both 3 and 5.

```cpp
#include <bits/stdc++.h>
using namespace std;

int calculate(int m, int n) {
    int sum = 0;
    for (int i = m; i <= n; i++) {
        if (i % 3 == 0 && i % 5 == 0) sum += i;
    }
    return sum;
}

int main() {
    cout << calculate(12, 50) << endl; // -> 90
    return 0;
}
```

**16. Autobiographical Number**
> A number where the digit at position i equals the count of digit i in the number (e.g., "1210"). Return the count of distinct digits if valid, else 0. *(Reported as "hard" difficulty)*

```cpp
#include <bits/stdc++.h>
using namespace std;

int findAutoCount(string n) {
    if (n.empty()) return 0;

    bool isValid = true;
    for (int i = 0; i < n.size(); i++) {
        int expectedCount = n[i] - '0';
        int actualCount = count(n.begin(), n.end(), (char)('0' + i));
        if (actualCount != expectedCount) {
            isValid = false;
            break;
        }
    }

    if (isValid) {
        set<char> distinct(n.begin(), n.end());
        return distinct.size();
    }
    return 0;
}

int main() {
    cout << findAutoCount("1210") << endl; // -> 3
    return 0;
}
```

**17. Find Max Element and Its Index**
> Standard array traversal — print the maximum value and its index. *(Very common easy warm-up)*

```cpp
#include <bits/stdc++.h>
using namespace std;

void maxInArray(vector<int>& arr) {
    int maxVal = *max_element(arr.begin(), arr.end());
    int maxIdx = max_element(arr.begin(), arr.end()) - arr.begin();
    cout << maxVal << endl;
    cout << maxIdx << endl;
}

int main() {
    vector<int> arr = {23, 45, 82, 27, 66, 12, 78, 13, 71, 86};
    maxInArray(arr); // -> prints 86 then 9
    return 0;
}
```

**18. Palindrome Numbers in a Range**
> Print all palindrome numbers between a lower and upper limit.

```cpp
#include <bits/stdc++.h>
using namespace std;

bool isPalindrome(int num) {
    string s = to_string(num);
    string rev = s;
    reverse(rev.begin(), rev.end());
    return s == rev;
}

void printPalindromes(int low, int high) {
    for (int num = low; num <= high; num++) {
        if (isPalindrome(num)) cout << num << " ";
    }
    cout << endl;
}

int main() {
    printPalindromes(10, 80); // -> 11 22 33 44 55 66 77
    return 0;
}
```

**19. Distance Between Three Points**
> Compute pairwise distances between 3 given (x,y) points using the distance formula and sum them.

```cpp
#include <bits/stdc++.h>
using namespace std;

double sumOfDistances(double x1, double y1, double x2, double y2, double x3, double y3) {
    double d1 = sqrt(pow(x2 - x1, 2) + pow(y2 - y1, 2));
    double d2 = sqrt(pow(x3 - x2, 2) + pow(y3 - y2, 2));
    double d3 = sqrt(pow(x3 - x1, 2) + pow(y3 - y1, 2));
    return d1 + d2 + d3;
}

int main() {
    cout << sumOfDistances(1, 1, 2, 4, 3, 6) << endl; // -> sum of the three pairwise distances
    return 0;
}
```

**20. Multiplication Table + Sum of Multiples**
> Print the first 10 multiples of a given number and their sum.

```cpp
#include <bits/stdc++.h>
using namespace std;

void multiplicationTable(int n) {
    vector<int> multiples;
    int sum = 0;
    for (int i = 1; i <= 10; i++) {
        multiples.push_back(n * i);
        sum += n * i;
    }
    for (int i = 0; i < multiples.size(); i++) {
        cout << multiples[i];
        if (i != multiples.size() - 1) cout << ", ";
    }
    cout << endl << sum << endl;
}

int main() {
    multiplicationTable(5); // -> 5,10,...,50 and sum 275
    return 0;
}
```

### More recent pattern (Oct 2025 drive) — coding round expanded to 3 mixed-format questions:
Recent reports show Accenture testing a **3-question mixed format** in the coding round instead of pure DSA:
1. **A DSA question** (array/string logic, similar to above list)
2. **A SQL query-writing question** (e.g., joins, aggregation, filtering — write actual SQL against a given schema)
3. **A web-based question**: modify given HTML/CSS/JavaScript code to implement a specified webpage behavior/feature

**Takeaway:** If your brother is targeting a Tech/AASE role, he should **also practice basic SQL query writing and simple HTML/CSS/JS tweaks**, not just DSA — this format has been increasingly reported in recent (2025–2026) drives.

---

## 3. Technical MCQ Round — Sample Questions by Topic

### MS Office / Common Applications (sample style — 8-12 questions in this section)

**Q: Which key combination adjusts a row's height in a spreadsheet?**
> A: Right-click the row number → "Row Height," or drag the row border. (Some MCQ variants offer `Alt+H, O, H` as the Excel ribbon shortcut for Row Height.)

**Q: Which of these is NOT a valid MS Excel function — COUNTIF, VLOOKUP, SUMPRODUCT, FINDALL?**
> A: **FINDALL** is not a real Excel function (COUNTIF, VLOOKUP, and SUMPRODUCT are all valid).

**Q: What does "Change Case" do to selected text in MS Word?**
> A: Converts selected text between UPPERCASE, lowercase, Sentence case, Title Case, and tOGGLE cASE.

**Q: Which feature saves a document automatically after a set interval?**
> A: **AutoSave / AutoRecover.**

**Q: Starting with a certain MS Office version, "Photo Editor" was renamed to ___?**
> A: **Picture Manager.**

**Q: True/False — "You can translate right-to-left languages in MS Word."**
> A: **True** — MS Word's built-in Translator supports right-to-left languages (e.g., Arabic, Hebrew) as well as left-to-right ones.

**Q: In MS PowerPoint, what is used to control how one slide changes to the next?**
> A: **Slide Transitions** (found under the Transitions tab); animations control movement of objects *within* a slide.

**Q: In MS Outlook, what lets you automatically move/flag incoming emails based on set conditions?**
> A: **Rules** (Outlook Rules & Alerts).

### Networking, Security & Cloud (situation-based MCQs — 8-12 questions)

**Q: Which layer of the OSI model is responsible for routing and logical addressing?**
> A: **Layer 3 — Network Layer.** (Quick recap: 1-Physical, 2-Data Link, 3-Network, 4-Transport, 5-Session, 6-Presentation, 7-Application.)

**Q: In a cloud model where "the business pays directly for planning, people, hardware, software, and environment in the data center," which service model is this?**
> A: **IaaS (Infrastructure as a Service)** — the business manages more of the stack itself compared to PaaS/SaaS.

**Q: Which cloud model gives the LEAST control to the customer but requires the LEAST management overhead?**
> A: **SaaS (Software as a Service)** — e.g., Gmail, Office 365; the provider manages everything except usage/data.

**Q: What type of attack involves tricking a user into revealing confidential information by impersonating a trustworthy source?**
> A: **Phishing** (a form of social engineering).

**Q: What does a "metamorphic virus" do that a normal virus doesn't?**
> A: It rewrites its own code each time it infects a new file, changing its signature to evade antivirus detection — unlike a static virus, which keeps the same code.

**Q: During which phase of a WPA/WPA2 wireless connection can the encryption be most vulnerable to interception?**
> A: The **4-way handshake** (initial key exchange) — this is the phase attackers target (e.g., in the KRACK attack).

**Q: In an SSH command, what does the `-D` flag typically do?**
> A: Sets up **dynamic port forwarding** (creates a local SOCKS proxy through the SSH tunnel).

**Q: In an SSH command, what does the `-p` flag do?**
> A: Specifies **remote-to-local port forwarding** rules / or specifies which port to connect to, depending on context — used to allow remote hosts to connect through locally forwarded ports.

**Q: What is the primary function of antivirus software?**
> A: To detect, quarantine, and remove malicious software (viruses, worms, trojans) using signature-based and heuristic/behavioral detection.

**Q: What is a firewall primarily used for?**
> A: To monitor and control incoming/outgoing network traffic based on predefined security rules, acting as a barrier between trusted and untrusted networks.

**Prep tip:** These are conceptual, definition-level MCQs — not deep technical scenarios. A focused 3-4 hour revision of networking/cloud/security basics (OSI layers, cloud service models, common attack types) covers most of this section.

---

## 4. Technical Interview — Full Latest Question List

### The core repeating 30 (compiled from multiple 2025-2026 candidate reports):
1. What are the similarities/differences between Java and C++?
2. Explain the memory allocation process in C (malloc, calloc, free).
3. What is recursion? Give an example.
4. What is a Collection Framework in Java?
5. Explain exception handling (try-catch-finally) with an example.
6. What is virtual inheritance in C++?
7. What is JDBC?
8. List Coffman's conditions that lead to deadlock.
9. What are short-term, long-term, and medium-term scheduling (OS)?
10. Write/explain a program for the Fibonacci series.
11. What is a classifier in Python?
12. What are lambda expressions in Java?
13. What is the significance of `super` and `this` keywords in Java?
14. Explain the basic features/pillars of OOPs (encapsulation, inheritance, polymorphism, abstraction).
15. What is the identifier naming length limit in your language?
16. Name the types of polymorphism in C++ (compile-time vs runtime).
17. What is database normalization? Name its forms (1NF, 2NF, 3NF, BCNF).
18. What is the purpose of a classifier in Python? *(recurring variant)*
19. What is XML, and where is it used?
20. What are the different types of interfaces in Java?
21. What is encapsulation in Java (with example)?
22. What are the three types of loops in Java (for, while, do-while)?
23. What is a SortedMap in Java?
24. What is the difference between `sleep()` and `wait()` in Java?
25. Differentiate between a constructor and a destructor.
26. What is a Linked List class — how would you implement one?
27. What are the limitations of enum in Java?
28. Explain the difference between JRE, JDK, JVM, and JIT.
29. What is an overflow error?
30. Explain pointers and memory allocation in C.

### Plus, near-universally asked:
- SQL: joins (INNER/LEFT/RIGHT/FULL), subqueries, `GROUP BY` vs `HAVING`, primary vs foreign key
- DBMS: ACID properties, stored procedures, indexing, normalization
- A **deep-dive into your final-year/major project** — expect 3–6 follow-up questions regardless of branch (this is close to guaranteed based on multiple candidate reports)

### Full Model Answers for the Most-Repeated Ones

**Q: Explain the basic features of OOPs.**
> The four pillars are: **Encapsulation** (bundling data and methods, restricting direct access), **Inheritance** (a class acquiring properties of another), **Polymorphism** (same function behaving differently based on context — overloading/overriding), and **Abstraction** (hiding implementation, showing only essentials).

**Q: Differentiate between a constructor and a destructor.**
> A constructor is auto-invoked when an object is created, initializes it, shares the class name, and has no return type. A destructor is auto-invoked when an object is destroyed/goes out of scope, used to free resources; in C++ it's `~ClassName()`.

**Q: Explain JDK vs JRE vs JVM vs JIT.**
> **JVM** executes bytecode and enables "write once, run anywhere." **JRE** = JVM + libraries needed to *run* Java apps. **JDK** = JRE + development tools (compiler, debugger) to *build* apps. **JIT** compiles bytecode to native machine code at runtime for speed.

**Q: What is SQL and what are joins?**
> SQL is the standard language for managing relational databases (DDL/DML/DCL). Joins combine rows from multiple tables: **INNER JOIN** (matching rows only), **LEFT JOIN** (all left + matches), **RIGHT JOIN** (all right + matches), **FULL OUTER JOIN** (all rows, matched where possible), **SELF JOIN** (table joined with itself).

**Q: What is recursion, and what's a tradeoff?**
> A function calling itself to solve smaller instances of a problem, with a base case to terminate. It gives cleaner code for problems like tree traversal or factorial, but trades off extra stack memory/overhead versus an iterative approach.

**Q: What is virtual inheritance in C++?**
> Ensures a derived class inherits only ONE copy of a base class's members even through multiple inheritance paths (solves the "diamond problem"). If B and C both inherit from A, and D inherits from both, `virtual` inheritance ensures D gets a single copy of A's members.

**Q: What is the difference between `sleep()` and `wait()` in Java?**
> `sleep()` pauses a thread for a fixed duration WITHOUT releasing any held lock. `wait()` pauses until notified by another thread and DOES release the lock while waiting — used for inter-thread communication.

**Q: List Coffman's conditions for deadlock.**
> **Mutual Exclusion** (exclusive resource holding), **Hold and Wait** (holding one resource while waiting for another), **No Preemption** (can't forcibly take a resource), **Circular Wait** (a closed chain of processes waiting on each other).

**Q: What is database normalization?**
> The process of organizing tables to reduce redundancy and improve integrity, through progressive forms: 1NF (atomic values), 2NF (no partial dependency), 3NF (no transitive dependency), BCNF (stricter 3NF).

**Q: What are Stored Procedures?**
> Precompiled SQL statement collections stored in the database, callable as a single unit — improves performance (no repeated parsing) and centralizes business logic.

---

## 5. HR Interview — Full Latest Question List

### The 10 most frequently reported HR questions:
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

### Real situational/behavioral questions from a recent (2024) combined Tech+HR round:
11. Introduce yourself.
12. What is your hobby?
13. Are you a pass-out graduate or in final year?
14. When have you felt proudest in your life, and why?
15. When have you felt lowest in your life, and why?
16. **If you are the team leader and a team member can't complete their task, what do you do?**
17. **If your project isn't completed within time, what do you do?**
18. **If there's a conflict between team members, how do you manage it?**
19. **If your project isn't complete and the deadline is near, what do you do?**

### Other frequently asked:
20. Are you willing to relocate / work rotational shifts?
21. Do you have any questions for us? *(always have 1–2 ready)*
22. What certifications do you have? *(increasingly asked in 2026 reports — have your cloud/AI/data certs ready to discuss if you have any)*
23. Walk me through your resume/project in detail *(scenario-based follow-ups are common — expect the interviewer to probe "why," "how," and "what would you do differently")*

### Model Answers — Full Set

**Q1: What are the major businesses/divisions of Accenture?**
> Accenture organizes its work broadly into service lines such as **Strategy & Consulting, Technology, Operations, Song (marketing/customer experience), and Industry X** (engineering/manufacturing). You don't need exact detail — mention 2-3 by name to show you did basic research.

**Q2: What, according to you, are the core values of Accenture?**
> Accenture's stated core values include **Client Value Creation, One Global Network, Respect for the Individual, Best People, Integrity, and Stewardship.** Pick 2 that resonate and briefly say why (e.g., "Respect for the Individual stood out to me because it reflects the inclusive culture I want to work in").

**Q3: Why do you want to join us / why Accenture?**
> See "Why do you want to join Accenture?" model answer below.

**Q4: What are your career goals — where do you see yourself in 5 years?**
> See "Where do you see yourself in 5 years?" model answer below.

**Q5: How can you contribute to Accenture's continuous quest for excellence?**
> "By bringing a strong learning mindset — staying current with new technologies, applying what I learn directly to client problems, and consistently seeking feedback to improve my work. I also believe good collaboration and clear communication directly contribute to project quality and client satisfaction."

**Q6: What are your strengths and weaknesses?**
> See model answer below.

**Q7: What are your long-term career goals?**
> "Long-term, I want to grow from a strong individual contributor into someone who can lead technical teams and mentor others — ideally growing into a solution architect or technical lead role over the next several years, while continuing to build deep expertise in [your area of interest]."

**Q8: What is your strategy for resolving conflicts with team members?**
> "I'd first listen to understand the other person's perspective without getting defensive, then focus the conversation on the shared goal rather than who's right. If we can't agree, I'd suggest a quick check-in with a mentor or team lead rather than letting it drag on and affect the work."

**Q9: What work environment do you expect?**
> "I thrive in a collaborative environment that values open communication and continuous learning — where I can ask questions freely, get constructive feedback, and also have the space to work independently on problems."

**Q10: Have you faced any obstacles while working on a project, and how did you overcome them?**
> Use a real STAR-format example: Situation → Task → Action → Result. E.g., "During my final-year project, we hit a roadblock when [specific technical issue]. I broke the problem down, researched [specific approach], and after testing a couple of alternatives, we resolved it by [solution] — which taught me to debug systematically rather than guess."

**Q11: Introduce yourself.**
> See "Tell me about yourself" model answer below.

**Q12: What is your hobby?**
> Be genuine and specific — vague answers like "reading" without follow-up detail feel weak. E.g., "I enjoy competitive coding in my free time — it's helped sharpen my problem-solving speed, and I also play badminton regularly to stay active."

**Q13: Are you a pass-out graduate or in your final year?**
> A factual answer — just state your actual status clearly and confidently. If final year: "I'm currently in my final year, expecting to graduate in [month/year]."

**Q14: When have you felt proudest in your life, and why?**
> Pick a genuine, specific moment (academic, extracurricular, or personal) and briefly explain the "why" — interviewers want authenticity over a rehearsed "perfect" answer. E.g., "Winning [specific hackathon/event] felt proudest because it was the first time I saw an idea I built go from concept to a working demo under real time pressure."

**Q15: When have you felt lowest in your life, and why?**
> Be honest but keep it professional and forward-looking — briefly mention the setback, then pivot to what you learned or how you recovered. E.g., "Failing to clear a certain exam on my first attempt was tough, but it taught me to build a more disciplined study routine, and I cleared it on my second attempt."

**Q16 (Situational — team member blocked):** See model answer below.

**Q17 (Situational — project running late):**
> "I'd first assess exactly how far behind we are and why, then re-prioritize the remaining tasks to focus on what's most critical for the deadline. I'd communicate the risk to my lead/team early rather than late, and see if scope can be trimmed or a short extension negotiated — transparency early is better than a surprise at the deadline."

**Q18 (Situational — team conflict):** See model answer below.

**Q19 (Situational — project incomplete near deadline):**
> "I'd stay calm, quickly identify the minimum viable version of the project that can be delivered on time, and communicate proactively with whoever the deliverable is for about status and any risk — asking for a short extension if genuinely needed, backed by a clear plan for what's left."

**Q20: Are you willing to relocate / work rotational shifts?**
> Accenture serves global clients, so shift work and relocation are common. Answer honestly — if yes, say so plainly: "Yes, I'm open to relocating and working in rotational shifts as needed for the role."

**Q21: Do you have any questions for us?**
> Always have 1-2 ready, e.g.: "Could you tell me more about the training program for new hires?" or "What does a typical first project look like for someone in this role?" Never say "no."

**Q22: What certifications do you have?**
> If you have any (AWS/Azure/GCP fundamentals, coding platform certifications, etc.), name them briefly and mention what you learned. If you don't have any yet, it's fine to say so honestly and mention one you're currently working toward.

**Q23: Walk me through your resume/project in detail.**
> Structure it chronologically or by relevance: education → key skills → 1-2 major projects (problem, your role, tech stack, outcome) → any leadership/extracurricular highlight. Be ready for "why," "how," and "what would you do differently" follow-ups on whatever project you lead with.

**Q: Tell me about yourself.**
> Keep to 60–90 seconds: education → key strengths/skills → one standout project/achievement → why you're a fit.
> *Sample:* "Good morning, I'm [Name], a final-year B.Tech student in [branch] from [college]. I've built a strong foundation in [core skills], and led/worked on [project]. I was also [leadership role], which sharpened my communication and teamwork. I'm looking to start my career at a place like Accenture where I can apply my technical skills on real client projects while continuing to learn."

**Q: Why do you want to join Accenture?**
> Mention Accenture's scale and diversity of work across industries/technologies, its learning/upskilling culture, and how that aligns with building a strong early-career foundation. Be specific, not generic.

**Q: What are your strengths and weaknesses?**
> Pick a real strength relevant to the job with a one-line example. For weakness, pick something genuine but not disqualifying, and show active improvement (e.g., "I used to hesitate presenting in groups, so I started taking up presentation opportunities in college").

**Q: Situational — If a team member can't complete their task, what do you do?**
> "I'd first have a quick one-on-one to understand the blocker — is it a skill gap, unclear requirements, or a personal issue? Then I'd see if the task can be redistributed or if I can pair with them to unblock it, while keeping the rest of the team and any deadline stakeholders informed early rather than surprising them later."

**Q: Situational — If there's a conflict between team members, how do you manage it?**
> "I'd talk to each person separately first to understand both perspectives without taking sides, then bring them together for a calm, solution-focused conversation — keeping the discussion on the work/goal, not personal. If it's not resolved, I'd loop in a mentor/lead for guidance."

**Q: Where do you see yourself in 5 years?**
> Show ambition balanced with realism and loyalty — e.g., growing into a senior technical/consulting role, pursuing certifications, eventually leading a small team, ideally framed around growing *with* Accenture.

**Q: Do you have any questions for us?**
> Always have 1–2 ready — e.g., about the training program structure, typical project allocation for freshers, or growth/certification opportunities. Never say "no."

---

## 6. Quick-Fire Revision Checklist (night before the interview)

- [ ] Can explain all 4 OOPs pillars with one example each
- [ ] Can write/trace: factorial, Fibonacci, prime check, palindrome check, array reversal, bubble sort
- [ ] Comfortable tracing bitwise operations (AND, OR, XOR, NOT, shifts) by hand
- [ ] Can explain JDK/JRE/JVM/JIT (if Java) or pointers/memory allocation (if C/C++)
- [ ] Know SQL joins, normalization forms, and can write a basic query with WHERE/GROUP BY/JOIN
- [ ] Can explain your final-year project in under 2 minutes, and answer "why this tech stack," "what was hard," "what would you improve"
- [ ] Have 1 STAR-format story ready for: teamwork, conflict, missed deadline, leadership
- [ ] Have answers ready for the 4 "situational" questions (team member blocked, deadline slipping, conflict, project incomplete)
- [ ] Can explain "why Accenture" with something specific (not just "good brand")
- [ ] Have 2 questions ready to ask the interviewer at the end
- [ ] Basic networking/cloud MCQ revision done (OSI layers, IaaS/PaaS/SaaS, common attack types)
- [ ] Basic MS Office shortcut/feature revision done (Excel functions, Word features)

---

### Sources
Compiled from real, dated candidate reports and question banks: GeeksforGeeks "Accenture On-Campus Interview Experience for 2025 Pass-out Candidates" (Sept 2024 interview, published Jan 2025), Naukri Code360 candidate interview experiences ("Accenture On-Campus Oct 2025," "Accenture On-Campus Oct 2024"), PrepInsta's Coding Questions & Pseudo-Code banks (2026), ImpactMillions' Pseudo-Code archive, Indeed's "Top 40 Accenture Interview Questions" (2026), Prepdrive.in and Talent Battle's MS Office/Networking MCQ samples, and Glassdoor 2026 interview reviews.

**Note:** Accenture does not publish an official leaked question bank — these are patterns tracked across many real candidate reports. The exact wording won't repeat every drive, but the *underlying patterns and topic distribution* have stayed highly consistent across 2024, 2025, and 2026 batches, so this is high-value practice material.