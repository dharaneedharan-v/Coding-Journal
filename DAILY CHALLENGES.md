
## [1508. Range Sum of Sorted Subarray Sums](https://leetcode.com/problems/range-sum-of-sorted-subarray-sums/)

```python

class Solution:
    def rangeSum(self, nums: List[int], n: int, left: int, right: int) -> int:
        dd = len(nums)
        mod = 10**9+7
        result = []
        for i in range(len(nums)):
            for j in range(i,dd):
                dk = sum(nums[i:j+1])
                result.append(dk)
        kk = sorted(result)
        d = sum(kk[left-1:right])
        return d%mod

```

###  [2053. Kth Distinct String in an Array](https://leetcode.com/problems/kth-distinct-string-in-an-array/)
```python

class Solution:

    def kthDistinct(self, arr: List[str], k: int) -> str:

        counter = Counter(arr)

        print (counter)

        for v in arr:

            if counter[v] == 1:

                k -= 1

                if k == 0:

                    return v

        return ''
```
### [3016. Minimum Number of Pushes to Type Word II](https://leetcode.com/problems/minimum-number-of-pushes-to-type-word-ii/)
USING THE COUNTER:

```python

 class Solution:

    def minimumPushes(self, word: str) -> int:
        frequency = Counter(word)
        # Step 2: Sort characters by frequency in descending order
        sorted_frequencies = sorted(frequency.values(), reverse=True)

        # Step 3: Calculate the minimum number of pushes

        dk = 0

        for i, freq in enumerate(sorted_frequencies):

            dk += (i // 8 + 1) * freq

        return dk
```
USING THE DICTIONARY :

```python
class Solution:

    def minimumPushes(self, word: str) -> int:

        dd = {}

        for i in word:

            if i in dd:

                dd[i] += 1

            else:

                dd[i] = 1

        # Step 2: Sort characters by frequency in descending order

        # Convert dictionary values to a list and sort it in descending order

        dd_sort = sorted(dd.values(), reverse=True)

        # Step 3: Calculate the minimum number of pushes

        dk = 0

        for i, freq in enumerate(dd_sort):

            # Calculate the key number (1-based) by (i // 8 + 1)

            dk += (i // 8 + 1) * freq

        print(dk)

        return dk
```
### [273. Integer to English Words](https://leetcode.com/problems/integer-to-english-words/)

```python

class Solution:

    # Dictionary to store words for numbers

    number_to_words_map = {

        1000000000: "Billion", 1000000: "Million", 1000: "Thousand",

        100: "Hundred", 90: "Ninety", 80: "Eighty", 70: "Seventy",

        60: "Sixty", 50: "Fifty", 40: "Forty", 30: "Thirty",

        20: "Twenty", 19: "Nineteen", 18: "Eighteen", 17: "Seventeen",

        16: "Sixteen", 15: "Fifteen", 14: "Fourteen", 13: "Thirteen",

        12: "Twelve", 11: "Eleven", 10: "Ten", 9: "Nine", 8: "Eight",

        7: "Seven", 6: "Six", 5: "Five", 4: "Four", 3: "Three",

        2: "Two", 1: "One"

    }

    def numberToWords(self, num: int) -> str:

        if num == 0:

            return "Zero"

        for value, word in self.number_to_words_map.items():

            # Check if the number is greater than or equal to the current unit

            if num >= value:

                # Convert the quotient to words if the current unit is 100 or greater

                prefix = (self.numberToWords(num // value) + " ") if num >= 100 else ""

                # Get the word for the current unit

                unit = word

                # Convert the remainder to words if it's not zero

                suffix = "" if num % value == 0 else " " + self.numberToWords(num % value)

                return prefix + unit + suffix

        return ""

```

### [885. Spiral Matrix III](https://leetcode.com/problems/spiral-matrix-iii/)
```python
class Solution:

    def spiralMatrixIII(self, rows: int, cols: int, rStart: int, cStart: int) -> List[List[int]]:

        direct = [[0, 1], [1, 0], [0, -1], [-1, 0]]

        res = []

        step = 0

        while len(res) < rows * cols:

            drow, dcol = direct[step % 4]

            step += 1

            for _ in range((step + 1) // 2):

                if 0 <= rStart < rows and 0 <= cStart < cols:

                    res.append([rStart, cStart])

                rStart += drow

                cStart += dcol

        return res

```

### [840. Magic Squares In Grid](https://leetcode.com/problems/magic-squares-in-grid/)

```python

class Solution:

    def numMagicSquaresInside(self, grid: List[List[int]]) -> int:

        def isMagic(i, j):

            once=[False]*10

            rowSum=[0]*3

            colSum= [0]*3

  

            for a in range(i-1, i+2):

                for b in range(j-1, j+2):

                    x= grid[a][b]

                    if x < 1 or x > 9: return False

                    rowSum[a-i+1] += x

                    colSum[b-j+1] += x

                    if once[x]:

                        return False  # it's not unique

                    once[x]=True

  

            for b in once[1:]:

                if not b: return False

  

            for sum in rowSum:

                if sum!=15: return False

            for sum in colSum:

                if sum!=15: return False

            return grid[i-1][j-1]+grid[i+1][j+1]==10 and grid[i+1][j-1]+grid[i-1][j+1]==10

        r, c = len(grid), len(grid[0])

        if r < 3 or c < 3:

            return 0

  

        cnt=0

        for i in range(1, r-1):

            for j in range(1, c-1):

                if grid[i][j] == 5 and isMagic(i, j):

                    cnt+=1

        return cnt
```

### [860. Lemonade Change](https://leetcode.com/problems/lemonade-change/)

```python 
class Solution:

    def lemonadeChange(self, bills: List[int]) -> bool:

        ten , five , twenty = 0,0,0

        for i in bills :

            if i == 5 :

                five += 1

            elif i == 10:

                if five == 0:

                    return 0

                else:

                    ten +=1

                    five -=1

            elif i == 20:

                if ten > 0 and five > 0:

                    ten -= 1

                    five -= 1

                elif five >= 3:

                    five -= 3

                else:

                    return False

        return True
```



### [624. Maximum Distance in Arrays](https://leetcode.com/problems/maximum-distance-in-arrays/)
```python 

  
Code

Testcase

Testcase

Test Result

[624. Maximum Distance in Arrays](https://leetcode.com/problems/maximum-distance-in-arrays/)
```
  

### [264. Ugly Number II](https://leetcode.com/problems/ugly-number-ii/)
```python 

class Solution:

    def nthUglyNumber(self, n: int) -> int:

        ugly_numbers_set = set()

        ugly_numbers_set.add(1)

        current_ugly = 1

        for i in range(n):

            current_ugly = min(ugly_numbers_set)

            ugly_numbers_set.remove(current_ugly)

            ugly_numbers_set.add(current_ugly * 2)

            ugly_numbers_set.add(current_ugly * 3)

            ugly_numbers_set.add(current_ugly * 5)

        return current_ugly
```
### [650. 2 Keys Keyboard](https://leetcode.com/problems/2-keys-keyboard/)

```python

class Solution:

    def minSteps(self, n: int) -> int:

        ans = 0

        d = 2

        while n > 1:

            while n % d == 0:

                ans += d

                n //= d

            d += 1

        return ans 
```


### [1140. Stone Game II](https://leetcode.com/problems/stone-game-ii/)



```python 
class Solution:

    @staticmethod

    def _suffix_sum(piles: List[int]) -> List[int]:

        suffix_sum = [0]

  

        for pile in reversed(piles):

            suffix_sum.append(suffix_sum[-1] + pile)

  

        suffix_sum.reverse()

  

        return suffix_sum
```

### [664. Strange Printer](https://leetcode.com/problems/strange-printer/)

```python 

class Solution:

    def strangePrinter(self, s: str) -> int:

        n = len(s)

        dp = [[0] * n for _ in range(n)]

        for i in range(n - 1, -1, -1):  

            dp[i][i] = 1  

            for j in range(i + 1, n):

                dp[i][j] = dp[i][j - 1] + 1  

                for k in range(i, j):

                    if s[k] == s[j]:

                        dp[i][j] = min(dp[i][j], dp[i][k] + (dp[k + 1][j - 1] if k + 1 <= j - 1 else 0))

        return dp[0][n-1]
```

### [476. Number Complement](https://leetcode.com/problems/number-complement/)

```python 

class Solution:

    def findComplement(self, num: int) -> int:

        a  = bin(num)[2:]

        dd = ''.join(['0' if i == '1' else '1' for i in a])

        dk = int(dd,2)

        return (dk)
```

### [592. Fraction Addition and Subtraction](https://leetcode.com/problems/fraction-addition-and-subtraction/)
```python 

class Solution:

    def fractionAddition(self, expression):

        ints = map(int, re.findall('[+-]?\d+', expression))

        A, B = 0, 1

        for a in ints:

            b = next(ints)

            A = A * b + a * B

            B *= b

            g = math.gcd(A, B)

            A //= g

            B //= g

        return '%d/%d' % (A, B)
```
### [564. Find the Closest Palindrome](https://leetcode.com/problems/find-the-closest-palindrome/)

```python 

class Solution:

    def nearestPalindromic(self, n: str) -> str:

        l = len(n)

        p, n = int(n[:(l+1)//2]), int(n)

        candidates = {

            10**(l-1) - 1,  # Largest palindrome with one less digit

            10**l + 1       # Smallest palindrome with one more digit

        }

        for q in (-1, 0, 1):

            t = str(p + q)

            palindrome = int(t + t[-1-l%2::-1])  # Mirror the first half to create a palindrome

            candidates.add(palindrome)

        candidates.discard(n)

        return str(min(candidates, key=lambda v: (abs(v - n), v)))
```
### [145. Binary Tree Postorder Traversal](https://leetcode.com/problems/binary-tree-postorder-traversal/)

```python
class Solution:

    def postorderTraversal(self, r: Optional[TreeNode]) -> List[int]:return (f:=lambda n:n and f(n.left)+f(n.right)+[n.val] or [])(r)
```

### [590. N-ary Tree Postorder Traversal](https://leetcode.com/problems/n-ary-tree-postorder-traversal/)

```python 
class Solution:

    def postorder(self, r: 'Node') -> List[int]:

        return (f:=lambda n,q=[]:n and [*map(f,n.children),q.append(n.val)] and q)(r)
```

### [1514. Path with Maximum Probability](https://leetcode.com/problems/path-with-maximum-probability/)
```python 
class Solution:

    def maxProbability(self, n: int, edges: List[List[int]], succProb: List[float], start: int, end: int) -> float:

  

        g, dq = defaultdict(list), deque([start])

        for i, (a, b) in enumerate(edges):

            g[a].append([b, i])

            g[b].append([a, i])

        p = [0.0] * n    

        p[start] = 1.0

        while dq:

            cur = dq.popleft()

            for neighbor, i in g[cur]:

                if p[cur] * succProb[i] > p[neighbor]:

                    p[neighbor] = p[cur] * succProb[i]

                    dq.append(neighbor)

        return p[end]
```

### [1905. Count Sub Islands](https://leetcode.com/problems/count-sub-islands/)
```python 


class Solution:

    def countSubIslands(self, grid1: List[List[int]], grid2: List[List[int]]) -> int:

        m=len(grid1)

        n=len(grid1[0])

        def dfs(i,j):

            if i<0 or i>=m or j<0 or j>=n or grid2[i][j]==0:

                return

            grid2[i][j]=0

            dfs(i+1,j)

            dfs(i,j+1)

            dfs(i,j-1)

            dfs(i-1,j)

        # removing all the non-common sub-islands

        for i in range(m):

            for j in range(n):

                if grid2[i][j]==1 and grid1[i][j]==0:

                    dfs(i,j)

        c=0

        # counting sub-islands

        for i in range(m):

            for j in range(n):

                if grid2[i][j]==1:

                    dfs(i,j)

                    c+=1

        return c
```

### [947. Most Stones Removed with Same Row or Column](https://leetcode.com/problems/most-stones-removed-with-same-row-or-column/)


 ```python

class Solution:
    def removeStones(self, points):
        uf = {}
        def find(x):
            if x != uf.setdefault(x, x):
                uf[x] = find(uf[x])
            return uf[x]
        for i, j in points:
            uf[find(i)] = find(~j)
        return len(points) - len({find(x) for x in uf})
```


###  [2699. Modify Graph Edge Weights](https://leetcode.com/problems/modify-graph-edge-weights/)
```python 

import heapq

  

class Solution:

    def modifiedGraphEdges(self, n, edges, source, destination, target):

        adjs = [{} for _ in range(n)]

  

        for edge in edges:

            adjs[edge[0]][edge[1]] = edge[2]

            adjs[edge[1]][edge[0]] = edge[2]

  

        distTo = [float('inf')] * n

        distTo[source] = 0

  

        pq = [(0, source)]

        heapq.heapify(pq)

  

        self.dijkstra(adjs, distTo, pq)

  

        if distTo[destination] == target:

            return self.fill(edges)

        elif distTo[destination] < target:

            return []

  

        for edge in edges:

            if edge[2] == -1:

                edge[2] = 1

                adjs[edge[0]][edge[1]] = 1

                adjs[edge[1]][edge[0]] = 1

  

                pq = [(distTo[edge[0]], edge[0]), (distTo[edge[1]], edge[1])]

  

                self.dijkstra(adjs, distTo, pq)

  

                if distTo[destination] == target:

                    return self.fill(edges)

                elif distTo[destination] < target:

                    edge[2] += target - distTo[destination]

                    adjs[edge[0]][edge[1]] = edge[2]

                    adjs[edge[1]][edge[0]] = edge[2]

                    return self.fill(edges)

  

        return []

  

    def fill(self, edges):

        for edge in edges:

            if edge[2] == -1:

                edge[2] = int(2e9)

        return edges

  

    def dijkstra(self, adjs, distTo, pq):

        while pq:

            curr_dist, curr = heapq.heappop(pq)

  

            for next_node, weight in adjs[curr].items():

                if weight > 0:

                    if distTo[next_node] - weight > distTo[curr]:

                        distTo[next_node] = distTo[curr] + weight

                        heapq.heappush(pq, (distTo[next_node], next_node))
```

### [1514. Path with Maximum Probability](https://leetcode.com/problems/path-with-maximum-probability/)
```python 
class Solution:

    def maxProbability(self, n: int, edges: List[List[int]], succProb: List[float], start: int, end: int) -> float:

  

        g, dq = defaultdict(list), deque([start])

        for i, (a, b) in enumerate(edges):

            g[a].append([b, i])

            g[b].append([a, i])

        p = [0.0] * n    

        p[start] = 1.0

        while dq:

            cur = dq.popleft()

            for neighbor, i in g[cur]:

                if p[cur] * succProb[i] > p[neighbor]:

                    p[neighbor] = p[cur] * succProb[i]

                    dq.append(neighbor)

        return p[end]
```

### [2022. Convert 1D Array Into 2D Array](https://leetcode.com/problems/convert-1d-array-into-2d-array/)

```python


class Solution:

    def construct2DArray(self, original: List[int], m: int, n: int) -> List[List[int]]:

        if m*n != len(original):return []

        res = [[0] * n for _ in range(m)]

        for i in range(len(original)):

            r,c  = divmod(i,n)

            res[r][c] = original[i]

        return (res)
```

### [1894. Find the Student that Will Replace the Chalk](https://leetcode.com/problems/find-the-student-that-will-replace-the-chalk/)


```python
class Solution:
    def chalkReplacer(self, chalk, k):
        n = len(chalk)
        total_chalk = sum(chalk)
        k %= total_chalk
        
        for i in range(n):
            if k < chalk[i]:
                return i
            k -= chalk[i]
        
        return 0
```

### [1945. Sum of Digits of String After Convert](https://leetcode.com/problems/sum-of-digits-of-string-after-convert/)
```python
class Solution:
def getLucky(self, s: str, k: int) -> int:

            q = ''.join(str(ord(c)-96) for c in s)

            for _ in range(k):

                q = sum(map(int,str(q)))

            return q
```

###  [874. Walking Robot Simulation](https://leetcode.com/problems/walking-robot-simulation/)

```python
class Solution:

    def robotSim(self, commands: List[int], obstacles: List[List[int]]) -> int:

        obstacles = set(map(tuple, obstacles))

        direction = [(0, 1), (1, 0), (0, -1), (-1, 0)]

        x = y = di = 0

        ans = 0

        for cmd in commands:

            if cmd == -2:

                di = (di - 1) % 4

            elif cmd == -1:

                di = (di + 1) % 4

            else:

                for k in range(cmd):

                    if (x + direction[di][0], y + direction[di][1]) not in obstacles:

                        x += direction[di][0]

                        y += direction[di][1]

                        ans = max(ans, x * x + y * y)

        return ans

```


### [3217. Delete Nodes From Linked List Present in Array](https://leetcode.com/problems/delete-nodes-from-linked-list-present-in-array/)
```python 
class Solution:

    def modifiedList(self, a: List[int], h: Optional[ListNode]) -> Optional[ListNode]:

        def f(node, a={*a}):

            if node:

                if node.val in a:

                    return f(node.next)

                return ListNode(node.val, f(node.next))

        return f(h)
```

### [2028. Find Missing Observations](https://leetcode.com/problems/find-missing-observations/)
```python 
class Solution:

    def missingRolls(self, rolls: List[int], mean: int, n: int) -> List[int]:

        sum_rolls = sum(rolls)

        # Find the remaining sum.

        remaining_sum = mean * (n + len(rolls)) - sum_rolls

        # Check if sum is valid or not.

        if remaining_sum > 6 * n or remaining_sum < n:

            return []

        distribute_mean = remaining_sum // n

        mod = remaining_sum % n

        # Distribute the remaining mod elements in n_elements list.

        n_elements = [distribute_mean] * n

        for i in range(mod):

            n_elements[i] += 1

        return n_elements
```

### [2326. Spiral Matrix IV](https://leetcode.com/problems/spiral-matrix-iv/)
```python 


class Solution:

    def spiralMatrix(self, m: int, n: int, head: "ListNode") -> List[List[int]]:

        # Store the east, south, west, north movements in a matrix.

        i = 0

        j = 0

        cur_d = 0

        movement = [[0, 1], [1, 0], [0, -1], [-1, 0]]

        res = [[-1 for _ in range(n)] for _ in range(m)]

  

        while head is not None:

            res[i][j] = head.val

            newi = i + movement[cur_d][0]

            newj = j + movement[cur_d][1]

  

            # If we bump into an edge or an already filled cell, change the

            # direction.

            if (

                min(newi, newj) < 0

                or newi >= m

                or newj >= n

                or res[newi][newj] != -1

            ):

                cur_d = (cur_d + 1) % 4

            i += movement[cur_d][0]

            j += movement[cur_d][1]

  

            head = head.next

  

        return res
```
### [1367. Linked List in Binary Tree](https://leetcode.com/problems/linked-list-in-binary-tree/)

```python 

class Solution:

        def isSubPath(self, head, root):

            def dfs(head, root):

                if not head: return True

                if not root: return False

                return root.val == head.val and (dfs(head.next, root.left) or dfs(head.next, root.right))

            if not head: return True

            if not root: return False

            return dfs(head, root) or self.isSubPath(head, root.left) or self.isSubPath(head, root.right)
            
```

### [2807. Insert Greatest Common Divisors in Linked List](https://leetcode.com/problems/insert-greatest-common-divisors-in-linked-list/)

```python 
# Definition for singly-linked list.

# class ListNode:

#     def __init__(self, val=0, next=None):

#         self.val = val

#         self.next = next

class Solution:

    def insertGreatestCommonDivisors(self, head: Optional[ListNode]) -> Optional[ListNode]:

        node_dha = head

        while node_dha.next != None:

            node_dha.next , node_dha = ListNode(gcd(node_dha.val,node_dha.next.val),node_dha.next),node_dha.next

        return head

        # print(head)

            # print(node_dha)
```

### [2220. Minimum Bit Flips to Convert Number](https://leetcode.com/problems/minimum-bit-flips-to-convert-number/)

```python 

class Solution:

    def minBitFlips(self, start: int, goal: int) -> int:

        count = 0

        while start or goal :

            if start&1 != goal&1 :

                count = count +1

            start = start>>1

            goal = goal>>1

        return (count)
```

### [1684. Count the Number of Consistent Strings](https://leetcode.com/problems/count-the-number-of-consistent-strings/)
```python 
class Solution:

    def countConsistentStrings(self, allowed: str, words: List[str]) -> int:

        allowed = set(allowed)

        count = 0

        for i in words :

            flag = 1

            for char in i :

                if char not in allowed :

                    flag = 0

                    break

            if flag == 1:

                count = count +1

        return count

#USING THE SUPPER SET


class Solution:

    def countConsistentStrings(self, allowed: str, words: List[str]) -> int:

        return sum(map({*allowed}.issuperset,words))
```

### [179. Largest Number](https://leetcode.com/problems/largest-number/)
```python 
class Solution:

    def largestNumber(self, nums: List[int]) -> str:

        array = list(map(str, nums))

        array.sort(key=lambda x: x*10, reverse=True)

        print (array)

        if array[0] == "0":

            return "0"

        largest = ''.join(array)

        return largest
```

### [241. Different Ways to Add Parentheses](https://leetcode.com/problems/different-ways-to-add-parentheses/)

```python 

class Solution:

    def diffWaysToCompute(self, expression: str) -> List[int]:

        res = []

        # ans = []

        for i in range(len(expression)):

            oper = expression[i]

            if oper == "+" or oper == "-" or oper == "*":

                sub_str1 = expression[0 : i]

                sub_str2 = expression[i + 1 : ]

                s1 = self.diffWaysToCompute(sub_str1)

                s2 = self.diffWaysToCompute(sub_str2)

                for i in s1:

                    for j in s2:

                        if oper == "*":

                            res.append(int(i) * int(j))

                        if oper == "+":

                            res.append(int(i) + int(j))

                        if oper == "-":

                            res.append(int(i) - int(j))

        if len(res) == 0:

            res.append(int(expression))

        # print(res)

        return res
```

### [214. Shortest Palindrome](https://leetcode.com/problems/shortest-palindrome/)

```python 
class Solution:

    def shortestPalindrome(self, s: str) -> str:

        length = len(s)

        reverse = s[::-1]

        for i in range(length):

            if s[:length-i] == reverse[i:]:

                return reverse[:i]+s

        return ""
```

### [386. Lexicographical Numbers](https://leetcode.com/problems/lexicographical-numbers/)
```python 
def lexicalOrder(self, n: int) -> List[int]:
    lexicographical_numbers = []
    current_number = 1

    # Generate numbers from 1 to n
    for _ in range(n):
        lexicographical_numbers.append(current_number)

        # If multiplying the current number by 10 is within the limit, do it
        if current_number * 10 <= n:
            current_number *= 10
        else:
            # Adjust the current number by moving up one digit
            while current_number % 10 == 9 or current_number >= n:
                current_number //= 10  # Remove the last digit
            current_number += 1  # Increment the number

    return lexicographical_numbers

# 2nd approach:

class Solution:

    def lexicalOrder(self, n: int) -> List[int]:

        l = [str(x) for x in range ( 1, n+1)]

        l.sort()

        l2 = [int(x) for x in l]

        return l2
```

### [440. K-th Smallest in Lexicographical Order](https://leetcode.com/problems/k-th-smallest-in-lexicographical-order/)

```python 

class Solution:

    def findKthNumber(self, n: int, k: int) -> int:

        cur = 1

        k -= 1

        while k > 0:

            steps = self.countSteps(cur, n)

            if steps <= k:

                cur += 1

                k -= steps

            else:

                cur *= 10

                k -= 1

        return cur

    def countSteps(self, p: int, n: int) -> int:

        steps = 0

        f, l = p, p

        while f <= n:

            steps += min(n + 1, l + 1) - f

            f *= 10

            l = l * 10 + 9

        return steps
```

### [2707. Extra Characters in a String](https://leetcode.com/problems/extra-characters-in-a-string/)

```python 
class Solution:
    def minExtraChar(self, s: str, dictionary: List[str]) -> int:
        n, dictionary_set = len(s), set(dictionary)
        @cache
        def dp(start):
            if start == n:
                return 0
            # To count this character as a left over character 
            # move to index 'start + 1'
            ans = dp(start + 1) + 1
            for end in range(start, n):
                curr = s[start: end + 1]
                if curr in dictionary_set:
                    ans = min(ans, dp(end + 1))
            return ans
            
        return dp(0)
```

### [3043. Find the Length of the Longest Common Prefix](https://leetcode.com/problems/find-the-length-of-the-longest-common-prefix/)

```python 
class Solution:

    def longestCommonPrefix(self, a: List[int], b: List[int]) -> int:

        return max(map(len,(f:=lambda e:{str(v)[:i] for v in e for i in range(9)})(a)&f(b)))


```

### [2416. Sum of Prefix Scores of Strings](https://leetcode.com/problems/sum-of-prefix-scores-of-strings/)

```python
class TrieNode:
    def __init__(self):
        self.children = {} 
        self.counts = 0
    
    def insert(self, word):
        curr = self
        for c in word:
            if c not in curr.children:
                curr.children[c] = TrieNode()
            curr = curr.children[c]
            curr.counts += 1
    
    def search(self, word):
        res = 0
        curr = self
        for c in word:
            curr = curr.children[c]
            res += curr.counts
        return res

class Solution:
    def sumPrefixScores(self, words: List[str]) -> List[int]:
        root = TrieNode()
        for word in words:
            root.insert(word) 
        
        res = []
        for word in words:
            res.append(root.search(word)) 
        
        return res
```

```python
class Solution:

    def sumPrefixScores(self, words: List[str]) -> List[int]:

        prefix_map: Dict[str, int] = dict()

        for word in words:

            prefix = ""

            for char in word:

                prefix += char

                freq = 1 if prefix not in prefix_map else prefix_map[prefix]+1

                prefix_map[prefix] = freq

        answer: List[int] = [0 for _ in range(len(words))]

        for i in range(0, len(words)):

            prefix = ""

            freq = 0

            for char in words[i]:

                prefix += char

                freq += prefix_map[prefix]

            answer[i] = freq

        return answer
```

### [729. My Calendar I](https://leetcode.com/problems/my-calendar-i/)

```python 

class MyCalendar:

  

    def __init__(self):

        self.calendar = []

  

    def book(self, start: int, end: int) -> bool:

        right = len(self.calendar)

        if right == 0:

            self.calendar.append((start, end))

            return True

  

        left = 0

        while left < right:

            mid = int(left + (right - left)/2)

            if self.calendar[mid][1] <= start:

                left = mid + 1

            else:

                right = mid

  

        if left == len(self.calendar):

            self.calendar.append((start, end))

            return True

        if self.calendar[left][0] >= end:

            self.calendar.insert(left, (start, end))

            return True

        return False
```

### [731. My Calendar II](https://leetcode.com/problems/my-calendar-ii/)

```python 
from sortedcontainers import SortedList
class MyCalendarTwo:

    def __init__(self):

        self.calendar = SortedList()

    def book(self, start, end):

        self.calendar.add((start,1))

        self.calendar.add((end,-1))
        total = 0

        for i,j in self.calendar:

            total += j

            if total == 3:

                self.calendar.remove((start,1))

                self.calendar.remove((end,-1))

                return False
        return True
```

### [641. Design Circular Deque](https://leetcode.com/problems/design-circular-deque/)

```python

class MyCircularDeque:

    def __init__(self, k: int):

        self.v = [-1] * k  # Initialize deque with -1

        self.front = 0

        self.back = 0

        self.size = 0  # Keeps track of the current number of elements

        self.capacity = k

  

    def insertFront(self, value: int) -> bool:

        if self.isFull():

            return False

  

        # Way - 01

        if self.front == 0:

            self.front = self.capacity - 1  # Wrap around to the end

        else:

            self.front -= 1  # Simply decrement front

  

        # Way - 02 (Alternative method commented out)

        # self.front = (self.front - 1 + self.capacity) % self.capacity

  

        self.v[self.front] = value

        self.size += 1

        return True

  

    def insertLast(self, value: int) -> bool:

        if self.isFull():

            return False

  

        self.v[self.back] = value

  

        # Way - 01

        if self.back == self.capacity - 1:

            self.back = 0  # Wrap around to the beginning

        else:

            self.back += 1  # Simply increment back

  

        # Way - 02 (Alternative method commented out)

        # self.back = (self.back + 1) % self.capacity

  

        self.size += 1

        return True

  

    def deleteFront(self) -> bool:

        if self.isEmpty():

            return False

  

        self.v[self.front] = -1

  

        # Way - 01

        if self.front == self.capacity - 1:

            self.front = 0  # Wrap around to the beginning

        else:

            self.front += 1  # Simply increment front

  

        # Way - 02 (Alternative method commented out)

        # self.front = (self.front + 1) % self.capacity

  

        self.size -= 1

        return True

  

    def deleteLast(self) -> bool:

        if self.isEmpty():

            return False

  

        if self.back == 0:

            self.back = self.capacity - 1  # Wrap around to the end

        else:

            self.back -= 1  # Simply decrement back

  

        self.v[self.back] = -1

        self.size -= 1

        return True

  

    def getFront(self) -> int:

        if self.isEmpty():

            return -1

        return self.v[self.front]

  

    def getRear(self) -> int:

        if self.isEmpty():

            return -1

        if self.back == 0:

            return self.v[self.capacity - 1]  # Wrap around to the last valid element

        else:

            return self.v[self.back - 1]  # Get the last element

  

    def isEmpty(self) -> bool:

        return self.size == 0

  

    def isFull(self) -> bool:

        return self.size == self.capacity
```

### [432. All O`one Data Structure](https://leetcode.com/problems/all-oone-data-structure/)

```python 
class AllOne:

    def __init__(self):

        self.myDict = {}

  

    def inc(self, key: str) -> None:

        if key in self.myDict:

            self.myDict[key] += 1

        else:

            self.myDict[key] = 1

  

    def dec(self, key: str) -> None:

        if key in self.myDict:

            if self.myDict[key] > 1:

                self.myDict[key] -= 1

            else:

                self.myDict.pop(key)

  

    def getMaxKey(self) -> str:

        if not self.myDict:

            return ""

        maxVal = max(self.myDict.values())

        for key in self.myDict.keys():

            if self.myDict[key] == maxVal:

                return key

  

    def getMinKey(self) -> str:

        if not self.myDict:

            return ""

        minVal = min(self.myDict.values())

        for key in self.myDict.keys():

            if self.myDict[key] == minVal:

                return key
```

### [1381. Design a Stack With Increment Operation](https://leetcode.com/problems/design-a-stack-with-increment-operation/)

```python 
class CustomStack:

    def __init__(self, maxSize: int):

        self.stack = [0] * maxSize

        self.top = -1

  

    def push(self, x: int) -> None:

        if self.top < len(self.stack) - 1:

            self.top += 1

            self.stack[self.top] = x

  

    def pop(self) -> int:

        if self.top != -1:

            value = self.stack[self.top]

            self.top -= 1

            return value

        return -1

  

    def increment(self, k: int, val: int) -> None:

        for i in range(min(k, self.top + 1)):

            self.stack[i] += val
```

###  [1497. Check If Array Pairs Are Divisible by k](https://leetcode.com/problems/check-if-array-pairs-are-divisible-by-k/)

```python 

	class Solution:

    def canArrange(self, a: List[int], k: int) -> bool:

        a = sorted(v%k for v in a)

        j = a.count(0)

        if j%2:

            return False

        return all((p+q)%k==0 for p,q in zip(a[j:], a[::-1]))

```
### [1331. Rank Transform of an Array](https://leetcode.com/problems/rank-transform-of-an-array/)

```python

class Solution:

    def arrayRankTransform(self, arr: List[int]) -> List[int]:

        dd= sorted(set(arr))        

        dk = {rank:ind+1 for ind , rank in enumerate (dd)}

        print (dk)

        dm = [dk[i] for i in arr]

        print(dm)

        return dm
```

### [1590. Make Sum Divisible by P](https://leetcode.com/problems/make-sum-divisible-by-p/)

```python 
class Solution:
    def minSubarray(self, nums: List[int], p: int) -> int:

        if sum(nums)%p==0:

            return 0

        target = sum(nums) % p

        dic,n = {0:-1},len(nums)

        cur,ret = 0,n

        for i,num in enumerate(nums):

            cur = (cur+num)%p

            if dic.get((cur-target)%p) is not None:

                ret = min(ret,i-dic.get((cur-target)%p))

            dic[cur] = i

        return ret if ret < n else -1
```

### [2491. Divide Players Into Teams of Equal Skill](https://leetcode.com/problems/divide-players-into-teams-of-equal-skill/)

```python 
class Solution:

    def dividePlayers(self, skill: List[int]) -> int:

        skill.sort()

        total_skill = skill[0] + skill[-1]  #  sum for each pair

        chemistry_sum = 0

        # Step 2: Pair players using two pointers
        for i in range(len(skill) // 2):
            # Check if the sum of current pair matches the required total_skill
            
            if skill[i] + skill[-i - 1] != total_skill:
                return -1  
                
            chemistry_sum += skill[i] * skill[-i - 1]
            
        return chemistry_sum  
```

### [567. Permutation in String](https://leetcode.com/problems/permutation-in-string/)

```python 
class Solution:

    def checkInclusion(self, s1: str, s2: str) -> bool:

        sorted_s1 = sorted(s1)

        len_s1 = len(s1)

        for i in range(len(s2) - len_s1 + 1):  # Ensure the loop doesn't go out of bounds

            substring = s2[i:i + len_s1]

            if sorted(substring) == sorted_s1:  

                return True

  

        return False
```

### [1813. Sentence Similarity III](https://leetcode.com/problems/sentence-similarity-iii/)

```python  
class Solution:

    def areSentencesSimilar(self, s1: str, s2: str) -> bool:

        sentence1 = deque(s1.split())

        sentence2 = deque(s2.split())

        while sentence1 and sentence2 and sentence1[0] == sentence2[0]:

            sentence1.popleft()

            sentence2.popleft()

        while sentence1 and sentence2 and sentence1[-1] == sentence2[-1]:

            sentence1.pop()

            sentence2.pop()

        return not sentence1 or not sentence2
```

### [2696. Minimum String Length After Removing Substrings](https://leetcode.com/problems/minimum-string-length-after-removing-substrings/)

```python 
class Solution:

    def minLength(self, s: str) -> int:

        while len(s):

            org = s

            if "AB" in s :

                s = s.replace("AB","")

            elif "CD" in  s :

                s = s.replace("CD", "")

            if org == s :

                break

        return len(s)
```

### [1963. Minimum Number of Swaps to Make the String Balanced](https://leetcode.com/problems/minimum-number-of-swaps-to-make-the-string-balanced/)

```python 
class Solution:

    def minSwaps(self, s: str) -> int:

        size = 0

        for i in range(len(s)) :

            if s[i] == "[":

                size = size+1

            elif s[i] == "]":

                if size > 0 :

  

                    size = size-1

  

        # print(size)

        return (size +1 )//2
```

### [921. Minimum Add to Make Parentheses Valid](https://leetcode.com/problems/minimum-add-to-make-parentheses-valid/)

```python 
class Solution:

    def minAddToMakeValid(self, s: str) -> int:

        count  = 0

        close  = 0

        for i in s :

            if i == '(':

                count = count +1

            else :

                if count > 0 :

                    count = count -1

                else :

                    close = close +1

        return count + close
```

### [962. Maximum Width Ramp](https://leetcode.com/problems/maximum-width-ramp/?envType=daily-question&envId=2024-10-10)

```python 

class Solution:

    def maxWidthRamp(self, nums):

        n = len(nums)

        indices_stack = []

        for i in range(n):

            if not indices_stack or nums[indices_stack[-1]] > nums[i]:

                indices_stack.append(i)

        max_width = 0

        for j in range(n - 1, -1, -1):

            while indices_stack and nums[indices_stack[-1]] <= nums[j]:

                max_width = max(max_width, j - indices_stack[-1])

                indices_stack.pop()

  

        return max_width
```


### [1942. The Number of the Smallest Unoccupied Chair](https://leetcode.com/problems/the-number-of-the-smallest-unoccupied-chair/)

```python
class Solution:

    def smallestChair(self, times: List[List[int]], targetFriend: int) -> int:

        target_time = times[targetFriend]

        times.sort()

        n = len(times)

        chair_time = [0] * n

        for time in times:

            for i in range(n):

                if chair_time[i] <= time[0]:

                    chair_time[i] = time[1]

                    if time == target_time:

                        return i

                    break

        return 0
```

### [2406. Divide Intervals Into Minimum Number of Groups](https://leetcode.com/problems/divide-intervals-into-minimum-number-of-groups/)

```python
 class Solution:

    def minGroups(self, intervals: List[List[int]]) -> int:

        pq = []

        for left, right in sorted(intervals):

            if pq and pq[0] < left:

                heappop(pq)

            heappush(pq, right)

        return len(pq)
```

### [632. Smallest Range Covering Elements from K Lists](https://leetcode.com/problems/smallest-range-covering-elements-from-k-lists/)

```python 

class Solution:

    def smallestRange(self, nums: List[List[int]]) -> List[int]:

        merged = []

        for i in range(len(nums)):

            for num in nums[i]:

                merged.append((num, i))

        merged.sort()

        freq = defaultdict(int)

        left, count = 0, 0

        range_start, range_end = 0, float("inf")

  

        for right in range(len(merged)):

            freq[merged[right][1]] += 1

            if freq[merged[right][1]] == 1:

                count += 1

            while count == len(nums):

                cur_range = merged[right][0] - merged[left][0]

                if cur_range < range_end - range_start:

                    range_start = merged[left][0]

                    range_end = merged[right][0]

  

                freq[merged[left][1]] -= 1

                if freq[merged[left][1]] == 0:

                    count -= 1

                left += 1

  

        return [range_start, range_end]
```

### [2530. Maximal Score After Applying K Operations](https://leetcode.com/problems/maximal-score-after-applying-k-operations/)

```python 
class Solution:

    def maxKelements(self, nums: List[int], k: int) -> int:

        heapify(pq:=[-x for x in nums])

        score=0

        for i in range(k):

            x=-heappop(pq)

            score+=x

            if x==1:

                score+=k-1-i

                break

            heappush(pq, -((x+2)//3))

        return score
```


### [2938. Separate Black and White Balls](https://leetcode.com/problems/separate-black-and-white-balls/)

```python 

class Solution:

    def minimumSteps(self, s: str) -> int:

        swap = 0

        count = 0

        for i in s :

            if i == '0':

                swap = swap + count

            else :

                count = count +1

        return swap
```

### [1405. Longest Happy String](https://leetcode.com/problems/longest-happy-string/)

```python 

class Solution:

    def longestDiverseString(self, a: int, b: int, c: int) -> str:

        char_counts = [['a', a], ['b', b], ['c', c]]

        result = []

  

        while True:

            char_counts.sort(key=lambda x: -x[1])

            added = False

  

            for i in range(3):

                char, count = char_counts[i]

                if count <= 0:

                    continue

                if len(result) >= 2 and result[-1] == result[-2] == char:

                    continue

                result.append(char)

                char_counts[i][1] -= 1

                added = True

                break

            if not added:

                break

        return ''.join(result)
```

### [670. Maximum Swap](https://leetcode.com/problems/maximum-swap/)

```python 

class Solution:
    def maximumSwap(self, num: int) -> int:
        number = list(str(num))
        sorted_number = sorted(number, reverse=True)
        
        for i in range(len(number)):
            if sorted_number[i] > number[i]:
                pos = ''.join(number).rfind(sorted_number[i])
                number[i], number[pos] = number[pos], number[i]
                return int(''.join(number))
        
        return num

```

### [2044. Count Number of Maximum Bitwise-OR Subsets](https://leetcode.com/problems/count-number-of-maximum-bitwise-or-subsets/)

```python 
class Solution:

    def countMaxOrSubsets(self, nums: List[int]) -> int:

        max_or = 0

        prev = Counter()

        prev[0] = 1

        for elem in nums:

            max_or |= elem

  

            current = Counter()

            for prev_or, cnt in prev.items():

                current[prev_or | elem] += cnt

            prev.update(current)

        return prev[max_or]
```

### [1545. Find Kth Bit in Nth Binary String](https://leetcode.com/problems/find-kth-bit-in-nth-binary-string/)

```python 

class Solution:

    def findKthBit(self, n: int, k: int) -> str:

        s = "0"

        for i in range(n-1):

            s  = s+"1" + s[::-1].replace("0","a").replace("1","0").replace("a","1")

        return (s[k-1])
```

### [1106. Parsing A Boolean Expression](https://leetcode.com/problems/parsing-a-boolean-expression/)

```python 

class Solution:

    def parseBoolExpr(self, S, t=True, f=False):

        return eval(S.replace('!', 'not |').replace('&(', 'all([').replace('|(', 'any([').replace(')', '])'))
       
```