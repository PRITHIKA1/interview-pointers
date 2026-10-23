# Virtusa Round 2: Coding Assessment — Java Crash-Prep Guide

**For:** BE/BTech CSE/IT campus placement  
**Role:** Regular / Associate Software Engineer  
**Language:** Java  
**Timing:** Tomorrow

> **Important:** Candidate reports are anecdotal, not official or guaranteed question papers. Confirm the round format and constraints from your campus invitation. Always follow the exact problem statement and input/output format provided in the assessment.

## 1. What to prioritize

1. **Graph BFS and shortest path:** grid traversal, queue, visited/distance arrays, unreachable destinations.
2. **Dynamic programming:** maximum alternating sum and string-construction operations.
3. **Recursion and arrays:** split a contiguous array when both parts have equal sums.
4. **Bit manipulation and strings:** XOR operations, binary-string generation, numerical strings.
5. **Written explanations:** algorithm idea, steps, correctness, complexity, and edge cases.

Recent 2026 candidate reports describe variations in the assessment. Some report a second coding stage with medium-to-hard problems involving BFS, DP, bit manipulation, recursion, arrays, and strings. Some reports mention separate written fields for explaining an approach. These reports should guide practice, not be treated as a prediction of the exact paper.

## 2. Reported pattern: Shortest path in a 2D grid

**Topics:** Graphs, BFS, queue

### Problem

You are given a grid where `0` represents an open cell and `1` represents a blocked cell. Find the minimum number of moves from the top-left cell to the bottom-right cell. You can move up, down, left, or right.

Return `-1` if the destination cannot be reached. Each move costs one, and the start cell has distance zero.

### Java solution

```java
import java.util.*;

class Solution {
    public int shortestPath(int[][] grid) {
        int rows = grid.length;
        if (rows == 0 || grid[0].length == 0) return -1;

        int cols = grid[0].length;

        if (grid[0][0] == 1 || grid[rows - 1][cols - 1] == 1) {
            return -1;
        }

        int[][] dist = new int[rows][cols];
        for (int[] row : dist) {
            Arrays.fill(row, -1);
        }

        int[] dr = {-1, 1, 0, 0};
        int[] dc = {0, 0, -1, 1};

        Queue<int[]> queue = new ArrayDeque<>();
        queue.offer(new int[]{0, 0});
        dist[0][0] = 0;

        while (!queue.isEmpty()) {
            int[] cur = queue.poll();
            int r = cur[0], c = cur[1];

            if (r == rows - 1 && c == cols - 1) {
                return dist[r][c];
            }

            for (int d = 0; d < 4; d++) {
                int nr = r + dr[d];
                int nc = c + dc[d];

                if (nr < 0 || nr >= rows || nc < 0 || nc >= cols) {
                    continue;
                }

                if (grid[nr][nc] == 1 || dist[nr][nc] != -1) {
                    continue;
                }

                dist[nr][nc] = dist[r][c] + 1;
                queue.offer(new int[]{nr, nc});
            }
        }

        return -1;
    }
}
```

### Explanation

1. Start from `(0, 0)` and add it to a queue.
2. Visit each valid, open, unvisited neighbor.
3. Set the neighbor's distance to the current distance plus one.
4. BFS visits cells in nondecreasing distance order, so the first visit to the destination gives the shortest path.
5. Return `-1` if the destination is never reached.

- **Time:** `O(R * C)`
- **Space:** `O(R * C)`

**Common mistakes:** not marking a cell visited when enqueuing it, moving through blocked cells, and forgetting blocked start/destination cases.

## 3. Reported pattern: Maximum alternating sum of an array

**Topics:** Dynamic programming, arrays

### Problem

Choose a subsequence of an array, preserving order, to maximize:

`a[i1] - a[i2] + a[i3] - a[i4] + ...`

You may skip elements. The solution below permits an empty subsequence, so the result is at least zero. If the actual statement requires a non-empty subsequence, adjust the initialization.

### Java solution

```java
class Solution {
    public long maxAlternatingSum(int[] nums) {
        long even = 0;
        long odd = Long.MIN_VALUE / 4;

        for (int x : nums) {
            long nextEven = Math.max(even, odd - x);
            long nextOdd = Math.max(odd, even + x);

            even = nextEven;
            odd = nextOdd;
        }

        return Math.max(even, odd);
    }
}
```

### Explanation

Maintain two states:

- `odd`: best alternating sum when the subsequence contains an odd number of elements.
- `even`: best alternating sum when it contains an even number of elements.

For each number `x`:

- Append `x` at a positive position: `even + x`.
- Append `x` at a negative position: `odd - x`.
- Or skip it and keep the previous best.

- **Time:** `O(n)`
- **Extra space:** `O(1)`

The exact alternating-sum definition can vary. Match the assessment's definition and whether an empty subsequence is allowed.

## 4. Reported pattern: Recursively split an array into equal-sum parts

**Topics:** Recursion, prefix sums, divide and conquer

### Problem

Repeatedly split a contiguous array segment into two contiguous parts only when both parts have equal sums. Each successful split counts as one operation; both resulting parts can be split again. Return the maximum possible number of splits.

Example: `[1, 1, 1, 1]` can be split into `[1, 1]` and `[1, 1]`, then each pair into single elements. Total splits: `3`.

### Java solution

```java
import java.util.*;

class Solution {
    private long[] prefix;
    private Map<Long, Integer> memo;

    public int maxSplits(int[] nums) {
        prefix = new long[nums.length + 1];

        for (int i = 0; i < nums.length; i++) {
            prefix[i + 1] = prefix[i] + nums[i];
        }

        memo = new HashMap<>();
        return dfs(0, nums.length - 1);
    }

    private int dfs(int left, int right) {
        if (left >= right) return 0;

        long key = (((long) left) << 32) | (right & 0xffffffffL);
        if (memo.containsKey(key)) return memo.get(key);

        long total = prefix[right + 1] - prefix[left];
        int best = 0;

        for (int mid = left; mid < right; mid++) {
            long leftSum = prefix[mid + 1] - prefix[left];
            long rightSum = total - leftSum;

            if (leftSum == rightSum) {
                int splits = 1
                        + dfs(left, mid)
                        + dfs(mid + 1, right);
                best = Math.max(best, splits);
            }
        }

        memo.put(key, best);
        return best;
    }
}
```

### Explanation

The prefix sum lets us calculate any range sum in `O(1)`:

`sum(left, right) = prefix[right + 1] - prefix[left]`

Try every split point. When the two parts have equal sums, count one split and recursively find the best splits on both sides. Memoization avoids solving the same segment repeatedly.

- **Worst-case time:** up to `O(n^3)`
- **Memo space:** `O(n^2)`

This implementation assumes every equal-sum split counts as one operation and both parts can be split recursively. Large constraints may require optimization.

## 5. Reported pattern: XOR operations on array prefixes and suffixes

**Topics:** Bit manipulation, arrays

Some reports describe operations that XOR either a prefix or suffix of an array. The exact operation payload is not clear from the report, so the following is a fully defined practice version—not a claim about the exact assessment question.

### Practice problem

Each query is `[type, k, mask]`:

- `[1, k, mask]`: XOR `mask` into the first `k` elements.
- `[2, k, mask]`: XOR `mask` into the last `k` elements.

Apply queries in order.

### Java solution

```java
class Solution {
    public int[] applyOperations(int[] arr, int[][] queries) {
        int n = arr.length;

        for (int[] q : queries) {
            int type = q[0];
            int k = q[1];
            int mask = q[2];

            if (k < 0 || k > n) {
                throw new IllegalArgumentException("Invalid k");
            }

            if (type == 1) {
                for (int i = 0; i < k; i++) {
                    arr[i] ^= mask;
                }
            } else if (type == 2) {
                for (int i = n - k; i < n; i++) {
                    arr[i] ^= mask;
                }
            }
        }

        return arr;
    }
}
```

- **Time:** `O(numberOfQueries * n)` in the worst case
- **Extra space:** `O(1)`, excluding input

Useful XOR properties:

- `x ^ x == 0`
- `x ^ 0 == x`
- XOR operations are associative and commutative.

Read the real statement carefully; do not assume it uses this exact query format.

## 6. Reported pattern: Minimum operations to type a string

**Topics:** Dynamic programming, string matching

### Practice problem

Given a target string `s`, you can:

- Type the next character for cost `1`.
- Copy a non-empty substring already present in the text constructed so far and append it, for cost `1`.

Return the minimum number of operations.

This is a simplified practice version of a reported string-construction problem. Confirm the precise copy rules in the actual statement.

### Java solution

```java
import java.util.*;

class Solution {
    public int minOperations(String s) {
        int n = s.length();
        int[] dp = new int[n + 1];
        Arrays.fill(dp, Integer.MAX_VALUE / 2);
        dp[0] = 0;

        for (int i = 0; i < n; i++) {
            dp[i + 1] = Math.min(dp[i + 1], dp[i] + 1);

            String built = s.substring(0, i);

            for (int len = 1; i + len <= n; len++) {
                String next = s.substring(i, i + len);

                if (built.contains(next)) {
                    dp[i + len] = Math.min(dp[i + len], dp[i] + 1);
                }
            }
        }

        return dp[n];
    }
}
```

### Explanation

`dp[i]` is the minimum cost to construct the first `i` characters. At each position, either type one character or append a substring that already appears in the constructed prefix.

- **Complexity:** This simple version can take up to `O(n^4)` time because of substring creation and searching.
- **Use:** Best for learning the recurrence and small inputs; optimize matching for large constraints.

The copied substring must already exist in the constructed prefix. It cannot be copied from a part of the target string that has not yet been constructed.

## 7. Binary-string generation with backtracking

**Topics:** Recursion, backtracking, bit manipulation

For `n = 2`, generate `00`, `01`, `10`, `11`.

### Java solution

```java
import java.util.*;

class Solution {
    public List<String> generateBinaryStrings(int n) {
        List<String> result = new ArrayList<>();
        generate(n, new StringBuilder(), result);
        return result;
    }

    private void generate(
            int n, StringBuilder current, List<String> result) {

        if (current.length() == n) {
            result.add(current.toString());
            return;
        }

        current.append('0');
        generate(n, current, result);
        current.deleteCharAt(current.length() - 1);

        current.append('1');
        generate(n, current, result);
        current.deleteCharAt(current.length() - 1);
    }
}
```

- **Time:** `O(n * 2^n)` to materialize all strings
- **Recursion depth:** `O(n)`, excluding output storage

If the problem adds a constraint—such as no consecutive ones or exactly `k` ones—check the condition during recursion and prune invalid branches.

## 8. Written approach questions

If the assessment provides text fields for explaining your approach, use this structure:

1. **Idea:** Name the algorithm and why it fits.
2. **Steps:** Explain initialization and the main loop, recursion, or DP transition.
3. **Correctness:** Explain why the algorithm finds the answer.
4. **Complexity:** State time and space complexity.
5. **Edge cases:** Mention boundaries, empty/minimum input, repeated values, and impossible cases as applicable.

### Example: BFS written explanation

> I use Breadth-First Search because every valid move has the same cost. I add the starting cell to a queue and explore its unvisited, non-blocked neighbors. I record each neighbor's distance as one more than the current cell's distance. Since BFS visits cells in nondecreasing distance order, the first visit to the destination gives the shortest path. If the destination is never visited, I return -1. Time and space complexity are both O(R × C).

Keep explanations clear and technically justified.

## 9. Focused mock assessment

**Suggested format:** 150 minutes, 5 questions. This mirrors a reported pattern and is not a verified official paper.

| Question | Time | Task |
|---|---:|---|
| 1 | 35 min | **Shortest path in a grid.** Find the minimum four-directional moves through open cells; return `-1` if impossible. Test a `1 × 1` grid, blocked endpoints, and an unreachable destination. |
| 2 | 30 min | **Maximum alternating sum.** Choose an order-preserving subsequence maximizing `first - second + third - ...`. State whether an empty subsequence is permitted. |
| 3 | 35 min | **Equal-sum recursive splits.** Split contiguous segments only when both parts have equal sums. Count the maximum number of successful splits. Example: `[1,1,1,1]` → `3`. |
| 4 | 25 min | **Written BFS explanation.** Explain data structures, traversal, correctness, time/space complexity, and unreachable destinations in 150–250 words. |
| 5 | 25 min | **Written recursion explanation.** Explain the recursion state, prefix sums, base case, best split, memoization, and worst-case complexity. |

### Test-taking strategy

- **First 5 minutes:** Read all three coding problems and choose the easiest one to start.
- **Next 100 minutes:** Solve the three coding problems. Get working code first; then test edge cases.
- **Next 40 minutes:** Write both approach explanations.
- **Final 5 minutes:** Check syntax, input/output format, integer overflow, and boundary conditions.

## 10. Last-night revision plan

### First 90 minutes — Learn and code

Implement BFS, alternating-sum DP, and recursive splitting from scratch. Do not only read the solutions.

### Next 60 minutes — Timed practice

Attempt the three coding questions without looking at the solutions. Test edge cases manually.

### Next 30 minutes — Written explanations

Practise explaining BFS, DP transitions, recursion, and complexity.

### Final 15 minutes — Java checklist

Review:

- `Queue` and `ArrayDeque`
- Arrays and `Arrays.fill`
- `StringBuilder`
- `HashMap`
- `long` for potentially large sums
- Sorting and basic string operations
- Off-by-one errors and boundary checks

If you have less time, prioritize **BFS, alternating-sum DP, recursion, and written explanations**.

## 11. Final exam checklist

- Read the exact problem statement and constraints.
- Match the required class name, method signature, and input/output format.
- Use `long` when sums may exceed the `int` range.
- Mark BFS nodes visited when enqueuing them.
- Check empty input, single-element input, blocked endpoints, and unreachable cases.
- For recursion, verify the base case and ensure each call makes progress.
- For DP, define the state and transition before coding.
- Compile and test a small example before submitting.
- Do not assume that a reported problem will appear unchanged in your assessment.

## Source notes

This guide is based on publicly reported candidate experiences and preparation material available in 2026. Candidate posts are anecdotal; question wording, constraints, and assessment format can differ by campus and hiring batch. Treat the examples above as practice problems, not official Virtusa questions.
