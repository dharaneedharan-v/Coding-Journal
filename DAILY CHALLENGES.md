
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

Using the Recursion
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

Using Brute Force  : 

```python 
class Solution:

    def numberToWords(self, num: int) -> str:

        one_digit = {

            1: 'One',

            2: 'Two',

            3: 'Three',

            4: 'Four',

            5: 'Five',

            6: 'Six',

            7: 'Seven',

            8: 'Eight',

            9: 'Nine'

        }

  

        two_digit = {

            10: 'Ten',

            11: 'Eleven',

            12: 'Twelve',

            13: 'Thirteen',

            14: 'Fourteen',

            15: 'Fifteen',

            16: 'Sixteen',

            17: 'Seventeen',

            18: 'Eighteen',

            19: 'Nineteen'

        }

        tens = {

            2: 'Twenty',

            3: 'Thirty',

            4: 'Forty',

            5: 'Fifty',

            6: 'Sixty',

            7: 'Seventy',

            8: 'Eighty',

            9: 'Ninety'

        }

        def get_three_digit_num(num):

            if( not num ) : return ""

            if( not num// 100 ): return get_two_digit_num(num)

            return one_digit[ num // 100 ] + " Hundred" + ((" " + get_two_digit_num( num % 100 )) if( num % 100 ) else "")

        def get_two_digit_num( num ):

            if not num:

                return ''

            elif num < 10:

                return one_digit[ num ]

            elif num < 20:

                return two_digit[ num ]

                    # edge case 1

            return tens[ num//10 ] + ((" " + one_digit[ num % 10 ]) if( num % 10 ) else "")

        # edge case

        if(num == 0): return "Zero"

        billion = num // 1000000000

        million = (num - billion * 1000000000) // 1000000

        thousand = (num - billion * 1000000000 - million * 1000000) // 1000

        last_three = num - billion * 1000000000 - million * 1000000 - thousand * 1000

        result = ''

        if billion:        

            result = get_three_digit_num(billion) + ' Billion'

        if million:

            # space only when prev result is not None

            result += ' ' if result else ''    

            result += get_three_digit_num(million) + ' Million'

        if thousand:

            result += ' ' if result else ''

            result += get_three_digit_num(thousand) + ' Thousand'

        if last_three:

            result += ' ' if result else ''

            result += get_three_digit_num(last_three)

        return result
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


### [1593. Split a String Into the Max Number of Unique Substrings](https://leetcode.com/problems/split-a-string-into-the-max-number-of-unique-substrings/)

```python 
class Solution:

    def split(self, s: str, st: set) -> int:

        if not s:

            return len(st)  

  

        mx = len(st)

        for i in range(1, len(s) + 1):

            first = s[:i]  # Get the current prefix

            if first not in st:  # If the prefix is unique

                st.add(first)  # Insert it into the set

                mx = max(mx, self.split(s[i:], st))  # Recurse on the remaining string

                st.remove(first)  # Backtrack: remove the prefix from the set

  

        return mx  # Return the maximum number of unique substrings

  

    def maxUniqueSplit(self, s: str) -> int:

        st = set()  

        return self.split(s, st)
```


### [2583. Kth Largest Sum in a Binary Tree](https://leetcode.com/problems/kth-largest-sum-in-a-binary-tree/)


```python 
class Solution:

    def kthLargestLevelSum(self, root: TreeNode, k: int) -> int:
    
        queue, ans = deque([root]), []
        
        while len(queue) > 0:
        
            count = 0
            
            for _ in range(len(queue)):
            
                node = queue.popleft()
                if node.left : queue.append(node.left )

                if node.right: queue.append(node.right)
                
                count+= node.val
                
            ans.append(count)
            
        return sorted(ans)[-k] if k <= len(ans) else -1
```

### [2641. Cousins in Binary Tree II](https://leetcode.com/problems/cousins-in-binary-tree-ii/)

```python 

class Solution:

    def __init__(self):

        self.level_sums = [0] * 100000

  

    def replaceValueInTree(self, root):

        self._calculate_level_sum(root, 0)

        self.replace_value_in_tree_internal(root, 0, 0)

        return root

  

    def _calculate_level_sum(self, node, level):

        if node is None:

            return

        self.level_sums[level] += node.val

        self._calculate_level_sum(node.left, level + 1)

        self._calculate_level_sum(node.right, level + 1)

  

    def replace_value_in_tree_internal(self, node, sibling_sum, level):

        if node is None:

            return

        left_child_val = 0 if node.left is None else node.left.val

        right_child_val = 0 if node.right is None else node.right.val

  

        if level == 0 or level == 1:

            node.val = 0

        else:

            node.val = self.level_sums[level] - node.val - sibling_sum

        self.replace_value_in_tree_internal(

            node.left, right_child_val, level + 1

        )

        self.replace_value_in_tree_internal(

            node.right, left_child_val, level + 1

        )
```


### [951. Flip Equivalent Binary Trees](https://leetcode.com/problems/flip-equivalent-binary-trees/)

```python 

class Solution:

    def flipEquiv(self, root1, root2):

        def checker(node1, node2):

            if not node1 and not node2:

                return True

            if not node1 or not node2 or node1.val != node2.val:

                return False

            return ((checker(node1.left, node2.left) or checker(node1.left, node2.right)) and

                    (checker(node1.right, node2.right) or checker(node1.right, node2.left)))

        return checker(root1, root2)
```

### [1233. Remove Sub-Folders from the Filesystem](https://leetcode.com/problems/remove-sub-folders-from-the-filesystem/)

```python 

class Solution:

    def removeSubfolders(self, folder: List[str]) -> List[str]:

        folder.sort()
        # print(folder)

        res = []

        for i in folder:

            # Add folder to res only if it's not a subfolder of the last added folder
            if not res or not i.startswith(res[-1] + "/"):

                res.append(i)

        return res
```

### [2458. Height of Binary Tree After Subtree Removal Queries](https://leetcode.com/problems/height-of-binary-tree-after-subtree-removal-queries/)

```python 

class Solution:

    def treeQueries(

        self, root: Optional[TreeNode], queries: List[int]

    ) -> List[int]:

        result_map = {}

        height_cache = {}

  

        # Function to calculate the height of the tree

        def _height(node):

            if not node:

                return -1

  

            # Return cached height if already calculated

            if node in height_cache:

                return height_cache[node]

  

            h = 1 + max(_height(node.left), _height(node.right))

            height_cache[node] = h

            return h

        # DFS to precompute the maximum values after removing the subtree

        def _dfs(node, depth, max_val):

            if not node:

                return

  

            result_map[node.val] = max_val

  

            # Traverse left and right subtrees while updating max values

            _dfs(

                node.left,

                depth + 1,

                max(max_val, depth + 1 + _height(node.right)),

            )

            _dfs(

                node.right,

                depth + 1,

                max(max_val, depth + 1 + _height(node.left)),

            )

  

        # Run DFS to fill result_map with maximum heights after each query

        _dfs(root, 0, 0)

  

        # Build the result array based on the queries

        return [result_map[q] for q in queries]
```

### [2501. Longest Square Streak in an Array](https://leetcode.com/problems/longest-square-streak-in-an-array/)

```python 
class Solution:

    def longestSquareStreak(self, nums: List[int]) -> int:

        dd = {}

        res = -1

        dk = sorted(nums)

        for i in dk :

            sqrt = isqrt(i)

            # print(sqrt)

            if sqrt * sqrt == i and sqrt in dd :

                # print(sqrt)

                dd[i]  = dd[sqrt] +1

                res = max(dd[i],res )

            else :

                dd[i] = 1

        return res
```

### [2684. Maximum Number of Moves in a Grid](https://leetcode.com/problems/maximum-number-of-moves-in-a-grid/)

```python 
class Solution:

    def maxMoves(self, grid: List[List[int]]) -> int:

        m = len(grid)

        n = len(grid[0])

        res = 0

        dp = [0] * m

        for j in range(1, n):

            leftTop = 0

            found = False

            for i in range(m):

                cur = -1

                nxtLeftTop = dp[i]

                if i - 1 >= 0 and leftTop != -1 and grid[i][j] > grid[i-1][j-1]:

                    cur = max(cur, leftTop + 1)

                if dp[i] != -1 and grid[i][j] > grid[i][j-1]:

                    cur = max(cur, dp[i] + 1)

                if i + 1 < m and dp[i+1] != -1 and grid[i][j] > grid[i+1][j-1]:

                    cur = max(cur, dp[i+1] + 1)

                dp[i] = cur

                found = found or (dp[i] != -1)

                leftTop = nxtLeftTop

            if not found:

                break

            res = j

        return res
```

### [2490. Circular Sentence](https://leetcode.com/problems/circular-sentence/)

```python 

class Solution:

    def isCircularSentence(self, sentence: str) -> bool:

        sent = sentence.split()

        print(sent)

        for i in range(len(sent)):

            if sent[i-1][-1] != sent[i][0]:

                return False

        return True
```

### [1957. Delete Characters to Make Fancy String](https://leetcode.com/problems/delete-characters-to-make-fancy-string/)

```python 

class Solution:

    def makeFancyString(self, s: str) -> str:

        res = []

        for i in s:

            if len(res) >= 2 and res[-1] == i and res[-2] == i :

                continue

            res.append(i)

        # print (res)

        return "".join(res)
```


### [3163. String Compression III](https://leetcode.com/problems/string-compression-iii/)

```python 
class Solution:

    def compressedString(self, word: str) -> str:

        start = word[0]

        res = ''

        count = 1

        for i in range(1,len(word)):

            if word[i] == start and count < 9 :

                count = count +1

            else :

                res =res+str(count)+ start

                start = word[i]

                count = 1

        res = res + str(count) + start

        print(res)

        return res
        
```

### [2914. Minimum Number of Changes to Make Binary String Beautiful](https://leetcode.com/problems/minimum-number-of-changes-to-make-binary-string-beautiful/)

```python 
class Solution:

    def minChanges(self, s: str) -> int:

        count = 0

        for i in range(1,len(s),2):

            if s[i-1] != s[i]:

                count = count + 1

        return count
```

### [3011. Find if Array Can Be Sorted](https://leetcode.com/problems/find-if-array-can-be-sorted/)

```python 
class Solution:

    def canSortArray(self, nums):

        n = len(nums)

        values = nums.copy()

        for i in range(n):

            for j in range(n - i - 1):

                if values[j] <= values[j + 1]:

                    # No swap needed

                    continue

                else:

                    if bin(values[j]).count("1") == bin(values[j + 1]).count(

                        "1"

                    ):

                        values[j], values[j + 1] = values[j + 1], values[j]

                    else:

                        return False

        return True
```


### [2275. Largest Combination With Bitwise AND Greater Than Zero](https://leetcode.com/problems/largest-combination-with-bitwise-and-greater-than-zero/)

```python 

class Solution:

    def largestCombination(self, candidates):

        max_count = 0  

        for i in range(24):

            count = 0  

            for num in candidates:

                if (num & (1 << i)) != 0:  

                    count += 1

            max_count = max(max_count, count)  

        return max_count
```

### [1829. Maximum XOR for Each Query](https://leetcode.com/problems/maximum-xor-for-each-query/)


```python 
class Solution:

    def getMaximumXor(self, a: List[int], q: int) -> List[int]:

        return [2**q-1^x for x in accumulate(a,xor)][::-1]
```


### [2601. Prime Subtraction Operation](https://leetcode.com/problems/prime-subtraction-operation/)

```python 
class Solution:

    def isprime(self, n):

        for i in range(2, isqrt(n) + 1):

            if n % i == 0:

                return False

        return True

  

    def primeSubOperation(self, nums):

        maxElement = max(nums)

        previous_prime = [0] * (maxElement + 1)

        for i in range(2, maxElement + 1):

            if self.isprime(i):

                previous_prime[i] = i

            else:

                previous_prime[i] = previous_prime[i - 1]

  

        for i in range(len(nums)):

            if i == 0:

                bound = nums[0]

            else:

                bound = nums[i] - nums[i - 1]

            if bound <= 0:

                return False

            largest_prime = previous_prime[bound - 1]

            nums[i] -= largest_prime

  

        return True
```

### [2070. Most Beautiful Item for Each Query](https://leetcode.com/problems/most-beautiful-item-for-each-query/)

```python 


class Solution:

    def maximumBeauty(self, A, queries):

        A = sorted(A + [[0, 0]])

        print(A)

        for i in range(len(A) - 1):

            A[i + 1][1] = max(A[i][1], A[i + 1][1])

        return [A[bisect.bisect(A, [q + 1]) - 1][1] for q in queries]
```


### [2563. Count the Number of Fair Pairs](https://leetcode.com/problems/count-the-number-of-fair-pairs/)

```python 
class Solution:

    def countFairPairs(self, nums: List[int], lower: int, upper: int) -> int:

        f = lambda x: sum(bisect_right(nums, x - num, hi=i) for i, num in enumerate(nums))

        nums.sort()

        return f(upper) - f(lower - 1)
```

### [2064. Minimized Maximum of Products Distributed to Any Store](https://leetcode.com/problems/minimized-maximum-of-products-distributed-to-any-store/)

```python 
class Solution:

    def minimizedMaximum(self, n: int, quantities: List[int]) -> int:

        l, r = 1, max(quantities)

        while l < r:

            tally, m = 0, (l+r)//2

            for k in quantities:

                tally+= (k-1)//m+1

            if tally <= n:  r = m

            else: l = m+1

        return r
```

### [1574. Shortest Subarray to be Removed to Make Array Sorted](https://leetcode.com/problems/shortest-subarray-to-be-removed-to-make-array-sorted/)

```python 

class Solution:

    def findLengthOfShortestSubarray(self, arr: List[int]) -> int:

        n = len(arr)

        i, j = 0, n-1

  

        while i < n-1 and arr[i+1] >= arr[i]: i+= 1

        if i == n-1: return 0

        while j > 0   and arr[j-1] <= arr[j]: j-= 1

  

        pref, suff, p, s = arr[:i+1], arr[j:], i+1, n-j

        ans = min(n-p,n-s)

        for i, num in enumerate(pref):

            j = bisect_left(suff, num)

            ans = min(ans,n-s-i+j-1)

  

        return ans
```


### [3254. Find the Power of K-Size Subarrays I](https://leetcode.com/problems/find-the-power-of-k-size-subarrays-i/)


```python 
class Solution:

    def resultsArray(self, nums: List[int], k: int) -> List[int]:

        res = []

        l = 0

        consec_cnt = 1

        for r in range(len(nums)):

            if r > 0 and nums[r - 1] + 1 == nums[r]:

                consec_cnt += 1

  

            if r - l + 1 > k:

                if nums[l] + 1 == nums[l + 1]:

                    consec_cnt -= 1

                l += 1

  

            if r - l + 1 == k:

                res.append(nums[r] if consec_cnt == k else -1)

        return res
```

### [862. Shortest Subarray with Sum at Least K](https://leetcode.com/problems/shortest-subarray-with-sum-at-least-k/)

```python 
class Solution:

        def shortestSubarray(self, A, K):

            d = collections.deque([[0, 0]])

            res, cur = float('inf'), 0

            for i, a in enumerate(A):

                cur += a

                while d and cur - d[0][1] >= K:

                    res = min(res, i + 1 - d.popleft()[0])

                while d and cur <= d[-1][1]:

                    d.pop()

                d.append([i + 1, cur])

            return res if res < float('inf') else -1
```

#### [1652. Defuse the Bomb](https://leetcode.com/problems/defuse-the-bomb/)

```python 
class Solution:

    def decrypt(self, code: List[int], k: int) -> List[int]:

        if k==0: return [0 for i in code]

        temp = code

        code = code*2

        for i in range(len(temp)):

            if k>0:

                temp[i] = sum(code[i+1:i+k+1])

            else:

                temp[i] = sum(code[i+len(temp)+k:i+len(temp)])

        return temp
```

### [2461. Maximum Sum of Distinct Subarrays With Length K](https://leetcode.com/problems/maximum-sum-of-distinct-subarrays-with-length-k/)

```python 

class Solution:

    def maximumSubarraySum(self, nums: List[int], k: int) -> int:

        n: int = len(nums)

        if n == 1:

            return nums[0]

        if k == 1:

            return max(nums)

        if n == k:

            return sum(nums) if len(set(nums)) == n else 0

  

        left, right = 0, 1

        result, t = 0, nums[0]

  

        visited = {nums[0]}

  

        while right < n:

            while nums[right] in visited:

                t -= nums[left]

                visited.remove(nums[left])

                left += 1

            t += nums[right]

            visited.add(nums[right])

  

            if right - left + 1 == k:

                result = max(result, t)

                t -= nums[left]

                visited.remove(nums[left])

                left += 1

            right += 1

  

        return result
```


### [2516. Take K of Each Character From Left and Right](https://leetcode.com/problems/take-k-of-each-character-from-left-and-right/)

```python 
class Solution:

    def takeCharacters(self, s: str, k: int) -> int:

  

        ctr, left, rght = [0, 0, 0], 0, 0

        n = len(s)

        s = list(map(lambda x: ord(x) - 97, s))

        for ch in s: ctr[ch]+= 1

        if min(ctr) < k: return -1

  

        for rght in range(n):

            ctr[s[rght]] -= 1

            if min(ctr) < k:

                ctr[s[left]]+= 1

                left+= 1  

        return n - rght + left - 1
```


### [2257. Count Unguarded Cells in the Grid](https://leetcode.com/problems/count-unguarded-cells-in-the-grid/)


```python 
class Solution:

    def countUnguarded(self, m: int, n: int, guards: List[List[int]], walls: List[List[int]]) -> int:

        def display(mat):

            for row in mat:

                print(row)

            print('-----------------')

        def countUnguard(mat):

            count=0

            for row in mat:

                for element in row:

                    if element==" ":

                        count+=1

            return count

        grid=[[" "]*n for _ in range(m)]

        #display(grid)

        for r,c in walls:

            grid[r][c]="W"

        #display(grid)

        for r,c in guards:

            grid[r][c]="G"

        #display(grid)

        for i in range(m):

            for j in range(n):

                if grid[i][j]=="G":

                    #RIGHT

                    for k in range(j+1,n):

                        if grid[i][k]=="W" or grid[i][k]=="G":

                            break

                        else:

                            grid[i][k]="B"

                    #LEFT

                    for k in range(j-1,-1,-1):

                        if grid[i][k]=="W" or grid[i][k]=="G":

                            break

                        else:

                            grid[i][k]="B"

                    #DOWN

                    for k in range(i+1,m):

                        if (grid[k][j]=="W" or grid[k][j]=="G"):

                            break

                        else:

                            grid[k][j]="B"

                    #UP

                    for k in range(i-1,-1,-1):

                        if grid[k][j]=="W" or grid[k][j]=="G":

                            break

                        else:

                            grid[k][j]="B"

        #display(grid)

        count=countUnguard(grid)

        return count
```

### [1072. Flip Columns For Maximum Number of Equal Rows](https://leetcode.com/problems/flip-columns-for-maximum-number-of-equal-rows/)

```python 
class Solution:

    def maxEqualRowsAfterFlips(self, matrix: List[List[int]]) -> int:

        return max(Counter(tuple(r if r[0] else (1 - i for i in r)) for r in matrix).values())
```


### [1861. Rotating the Box](https://leetcode.com/problems/rotating-the-box/)

```python 
class Solution:

    def rotateTheBox(self, box: List[List[str]]) -> List[List[str]]:

        m, n = len(box), len(box[0])

        for r in range(m):

            target = n - 1

            for c in range(n - 1, -1, -1):

                if box[r][c] == '*':

                    target = c - 1

                elif box[r][c] == '#':

                    if target != c:

                        box[r][target] = box[r][c]

                        box[r][c] = '.'

                    target -= 1

  

        return [[box[r][c] for r in range(m - 1, -1, -1)] for c in range(n)]
```

### [3243. Shortest Distance After Road Addition Queries I](https://leetcode.com/problems/shortest-distance-after-road-addition-queries-i/)

```python 
class Solution:
    def shortestDistanceAfterQueries(self, n, queries):
        adj = [[i+1] for i in range(n-1)] + [[]]
        d, ans = list(range(n)), []
        for beg, end in queries:
            adj[beg].append(end)
            
            if d[beg] + 1 < d[end]:
                queue = deque([end])
                d[end] = d[beg] + 1
                
                while queue:
                    v = queue.popleft()
                    
                    for next_node in adj[v]:
                        if d[v] + 1 < d[next_node]:
                            d[next_node] = d[v] + 1
                            queue.append(next_node)
            
            ans.append(d[-1])
        
        return ans

```

### [1346. Check If N and Its Double Exist](https://leetcode.com/problems/check-if-n-and-its-double-exist/) 

```python 
O(N^2):

class Solution:

    def checkIfExist(self, arr: List[int]) -> bool:

        for i in range(len(arr)):

            for j in range (len(arr)):

                if i != j and arr[i] == 2*arr[j]:

                    return True

        return False


O(N): 

class Solution:

    def checkIfExist(self, arr: List[int]) -> bool:

        dd = set ()

        for i in arr :

            if i*2 in dd or i/2 in dd:

                return True

            dd.add(i)

        return False
```


### [1455. Check If a Word Occurs As a Prefix of Any Word in a Sentence](https://leetcode.com/problems/check-if-a-word-occurs-as-a-prefix-of-any-word-in-a-sentence/)

```python 
class Solution:

    def isPrefixOfWord(self, sentence: str, searchWord: str) -> int:

        dd  = sentence.split()

        # print(dd)

        for index, word in enumerate(dd,start = 1):

            # print(index,word)

            if word.startswith(searchWord):

                return index

        return -1
```


### [2825. Make String a Subsequence Using Cyclic Increments](https://leetcode.com/problems/make-string-a-subsequence-using-cyclic-increments/)

```python 
class Solution:

    def canMakeSubsequence(self, s: str, t: str) -> bool:

        i = 0

        for c in s:

            i += i<len(t) and (ord(t[i])-ord(c))%26<=1

  

        return i == len(t)
```

### [3264. Final Array State After K Multiplication Operations I](https://leetcode.com/problems/final-array-state-after-k-multiplication-operations-i/)

```python 
class Solution:

    def getFinalState(self, nums: List[int], k: int, multiplier: int) -> List[int]:

        for _ in range(k):

            idx = nums.index(min(nums))

            nums[idx] *= multiplier

            # print(nums)

        return nums
```

### [1475. Final Prices With a Special Discount in a Shop](https://leetcode.com/problems/final-prices-with-a-special-discount-in-a-shop/)

```python 
class Solution:

    def finalPrices(self, prices: List[int]) -> List[int]:

        for i in range(len(prices)):

            for j in range(i+1 , len(prices)):

                if (prices[i]>= prices[j]):

                    prices[i] = prices[i] - prices[j]

                    break

        return prices
```


### [2270. Number of Ways to Split Array](https://leetcode.com/problems/number-of-ways-to-split-array/)

```python 

class Solution:

    def waysToSplitArray(self, nums: List[int]) -> int:

        count = 0

        dd = sum(nums)

        leftSum = 0

        rightSum = dd

        for i in range(len(nums)-1):

            leftSum +=nums[i]

            rightSum -=nums[i]

            if leftSum >= rightSum :

                count +=1

        return count
```



### [1930. Unique Length-3 Palindromic Subsequences](https://leetcode.com/problems/unique-length-3-palindromic-subsequences/)

```python 
class Solution:

    def countPalindromicSubsequence(self, s: str) -> int:

        ans = 0

        dd = set(s)

        for idx in dd :

            i, j = s.index(idx), s.rindex(idx)

            dk = set()

            for k in range(i+1 , j):

                dk.add(s[k])

            ans = ans+len(dk)

        return ans
```


### [1408. String Matching in an Array](https://leetcode.com/problems/string-matching-in-an-array/)

```python 
class Solution:

    def stringMatching(self, words: List[str]) -> List[str]:

        ans = set()

        for x in words:

            for y in words:

                if x != y and x in y:

                    ans.add(x)

        return list(ans)
```



### [2965. Find Missing and Repeated Values](https://leetcode.com/problems/find-missing-and-repeated-values/)


```python 
class Solution:

    def findMissingAndRepeatedValues(self, grid: List[List[int]]) -> List[int]:

        dd={}

        row  = len(grid)

        col = len(grid[0])

        Total = [i for i in range(1,row* col+1) ]

        for i in range(len(grid)):

            for j in range(len(grid[0])):

                dk = (grid[i][j])

                if dk not in dd:

                    dd[dk] = 1

                else :

                    dd[dk] +=1

        print(dd)

        res = []

        for idx , val in dd.items():

            if val >= 2 :

                res.append(idx)

        print(res)

        idx = set(dd.keys())

        print(idx)

  

        for i in (Total):

            if  i  not in idx :

                res.append(i)

        print(res)

        return res
```

### [1780. Check if Number is a Sum of Powers of Three](https://leetcode.com/problems/check-if-number-is-a-sum-of-powers-of-three/)

```python 

class Solution:

    def checkPowersOfThree(self, n: int) -> bool:

        for i in range(14, -1, -1):

            Pow = 3**i

            if n - Pow >= 0:

                n -= Pow

                if n == 0:

                    return True

        return False
```


### [3375. Minimum Operations to Make Array Values Equal to K](https://leetcode.com/problems/minimum-operations-to-make-array-values-equal-to-k/)


```python 
class Solution:

    def minOperations(self, nums: List[int], k: int) -> int:

        dd  = {}

        for i in range(len(nums)):

            if nums[i] < k :

                return -1

            elif nums[i] > k :

                if nums[i] not in dd :

                    dd[nums[i]] = 1

                else :

                    dd[nums[i]] += 1

        return len(dd)
```


### [1534. Count Good Triplets](https://leetcode.com/problems/count-good-triplets/)


```python 
class Solution:

    def countGoodTriplets(self, arr: List[int], a: int, b: int, c: int) -> int:

        Len = len(arr)

        count = 0

        for  i in range((Len)-2):

            for  j in range(i+1, Len-1):

                for k in range(j+1 , Len):

                    if (

                        abs(arr[i]-arr[j]) <= a and

                        abs(arr[j]-arr[k])<= b and

                        abs(arr[k]-arr[i]) <= c

                    ):count = count + 1

        return count
```

### [1922. Count Good Numbers](https://leetcode.com/problems/count-good-numbers/)

```python 
class Solution:

    MOD = 10**9+ 7

    def Exponetial (self, x:int , n:int )->int:

        res  =  1

        while (n > 0 ):

            if n & 1 :

                res = res * x % self.MOD

            x   =  x* x % self.MOD

            # n = n // 2

            n = n >> 1

        return res % self.MOD

    def countGoodNumbers(self, n: int) -> int:

        return (self.Exponetial(4,n//2) * self.Exponetial(5,n-n//2 ) )%  self.MOD
```



### [2176. Count Equal and Divisible Pairs in an Array](https://leetcode.com/problems/count-equal-and-divisible-pairs-in-an-array/)


```python 

class Solution:

    def countPairs(self, nums: List[int], k: int) -> int:

        count = 0

        for i in range(len(nums)):

            for j in range(len(nums)):

                if i == j :

                    break

                if nums[i] == nums[j]:

                    if i*j  % k == 0 :

                        count += 1

        return count
```

### [2824. Count Pairs Whose Sum is Less than Target](https://leetcode.com/problems/count-pairs-whose-sum-is-less-than-target/)


Brute Force : 
```python 
class Solution:

    def countPairs(self, nums: List[int], target: int) -> int:

        count = 0

        for i in range(len(nums)):

            for j in range(i+1, len(nums)):

                if nums[i] + nums[j] < target :

                    count = count + 1

                    print(i,j)

        # print(count)

        return count
```


### [2563. Count the Number of Fair Pairs](https://leetcode.com/problems/count-the-number-of-fair-pairs/)

Brute Force : 

```python 
class Solution:

    def countFairPairs(self, nums: List[int], lower: int, upper: int) -> int:

        count = 0

        for i in range(len(nums)):

            for j in range(i+1, len(nums)):

                if lower <= nums[i] + nums[j] <= upper:

                    # print(i,j)

                    count += 1

        return count
```



### [781. Rabbits in Forest](https://leetcode.com/problems/rabbits-in-forest/)


```python 
class Solution:

    def numRabbits(self, ans: List[int]) -> int:

        dd = {}

        for i in range(len(ans)):

            if ans[i] not in dd :

                dd[ans[i]] = 1

            else :

                dd[ans[i]] += 1

        res  = 0

        for idx , val in dd.items():

            res = res+ (idx+ 1 ) * ceil(val/(idx+1 ))

        print(res)

        return res
```

-----------------digit Sum --------------------
### [1399. Count Largest Group](https://leetcode.com/problems/count-largest-group/)

```python 
class Solution:

    def countLargestGroup(self, n: int) -> int:

        def isdigitSum(N):

            Sum = 0

            if N <9 :

                return N

            else :

                while (N > 0):

                    Mod = N % 10

                    Sum = Sum + Mod

                    N = N //10

            return Sum

        dd  = {}

        for i in range(1,n+1):

            DS = isdigitSum(i)

            if DS not in  dd :

                dd[DS] =1

            else :

                dd[DS] += 1

        Max = max(dd.values())

        count = 0

        for idx , val in dd.items():

            if val == Max :

                count = count+1

        return count
        
```


### [2544. Alternating Digit Sum](https://leetcode.com/problems/alternating-digit-sum/)


```python 
class Solution:
    def alternateDigitSum(self, n: int) -> int:
        String = str(n)
        Sum = 0 
        for i in range(0,len(String)-1,2):
            dk = (int(String[i])-int(String[i+1]))
            Sum += dk 
        return Sum  if len(String)  & 1 == 0  else  Sum + int(String[-1]) 


```

### [258. Add Digits](https://leetcode.com/problems/add-digits/)

```python 
class Solution:

    def addDigits(self, num: int) -> int:

        def isdigitSum (N :int) -> int :

            Sum = 0

            while N > 0 :

                Mod = N % 10

                Sum += Mod

                N = N//10

            return Sum

        # String = str(num)

        if num == 0 :

            return 0

        if num <= 9 :

            return num

        while (num > 9):

            # print(isdigitSum(num))

            num  =  isdigitSum(num)

        return num
```


### [3174. Clear Digits](https://leetcode.com/problems/clear-digits/)


```python 
class Solution:
    def clearDigits(self, s: str) -> str:
        stack = []
        for i in range(len(s)):
            if s[i].isdigit():
                if stack :
                    stack.pop()
            else :
                stack.append(s[i])
        return "".join(stack)

```


### [2799. Count Complete Subarrays in an Array](https://leetcode.com/problems/count-complete-subarrays-in-an-array/)


Brute Force : 


```python 
class Solution:
    def countCompleteSubarrays(self, nums: List[int]) -> int:
        dist = len(set(nums))
        # print(dist)
        res = []
        count = 0 
        for i in range(len(nums)):
            for j in range(i+1 , len(nums)+1):
                dk = (len(set(nums[i:j])))
                if dk == dist :
                    count  += 1
        # print(count)
        return count 
```


Optimized From N^3   to N ^2 : 

```python 
class Solution:
    def countCompleteSubarrays(self, nums: List[int]) -> int:
        dist = len(set(nums))
        # print(dist)
        count = 0 
        for i in range(len(nums)):
            Final  = set()
            for j in range(i , len(nums)):
                # dk = (len(set(nums[i:j]))) # instead of buliding the Every time Check from the set 
                Final.add(nums[j])
                if len(Final) == dist :
                    count  += len(nums)-j 
                    break
        # print(count)
        return count 
```

### [3392. Count Subarrays of Length Three With a Condition](https://leetcode.com/problems/count-subarrays-of-length-three-with-a-condition/)

Fixed Sliding Window Problem
Brute Force : 

```python 
class Solution:
    def countSubarrays(self, nums: List[int]) -> int:
        count  = 0 
        for i in range(len(nums)):
            for j in range(i+1, len(nums)+1):
                dk = (nums[i:j])
                if len(dk ) == 3 :
                    First = dk[0]
                    Last = dk[-1]
                    Second = dk[1]
                    if Last + First == Second / 2 :
                        List.append(dk)
                        count = count +1 
        return count 
        


```


Optimized 

```python 
class Solution:
    def countSubarrays(self, nums: List[int]) -> int:
        k = 3 
        n = len(nums)
        count = 0 
        for i in range(n-k+1 ):
            First = nums[i]
            Second = nums[i+1]
            Third = nums[i+2]
            if First + Third == Second / 2 :
                count += 1 
        return count 
```


### [2302. Count Subarrays With Score Less Than K](https://leetcode.com/problems/count-subarrays-with-score-less-than-k/)


Brute Force Solution :  TLE 

TC -> O(N^2) 

```python 
class Solution:
    def countSubarrays(self, nums: List[int], k: int) -> int:
        count = 0 
        for  i in range(len(nums)):
            ctn = 0
            Sum = 0 
            for j in range(i+1, len(nums)+1):
                Sum = Sum + nums[j-1]
                ctn +=  1
                if ctn*Sum  < k :
                    count += 1 
        return count 

```


### [2962. Count Subarrays Where Max Element Appears at Least K Times](https://leetcode.com/problems/count-subarrays-where-max-element-appears-at-least-k-times/)
Brute Force :  Time Limit Exceeded
TC -> O(N^2)
```python 
class Solution:
    def countSubarrays(self, nums: List[int], k: int):
        count = 0 
        Max = max(nums)
        for i in range(len(nums)):
            for j in range(i+1, len(nums)+1):
                Sub = (nums[i:j])
                Count = Sub.count(Max)
                if Count >= k :
                    count += 1
        return count 
```


### [3396. Minimum Number of Operations to Make Elements in Array Distinct](https://leetcode.com/problems/minimum-number-of-operations-to-make-elements-in-array-distinct/)

```python 
class Solution:
    def minimumOperations(self, nums: List[int]) -> int:
        count = 0
        while len(nums) != len(set(nums)):
            count += 1
            nums = nums[3:]  # remove first 3 elements
        return count
```


### [1295. Find Numbers with Even Number of Digits](https://leetcode.com/problems/find-numbers-with-even-number-of-digits/)

```python 
class Solution:
    def findNumbers(self, nums: List[int]) -> int:
        count = 0 
        for i in range(len(nums)):
            dk = (len(str(nums[i])))
            if dk  & 1 == 0 :
                count += 1
        return count 
```


### [2843. Count Symmetric Integers](https://leetcode.com/problems/count-symmetric-integers/)


```python 

class Solution:
    def countSymmetricIntegers(self, low: int, high: int) -> int:
        count = 0 
        def check (N:int)-> bool :
            Str = str(N)
            Len = len(Str)
            if Len % 2 == 1  :
                return 0 
            Half = Len// 2
            SumFirst = sum([int(i) for i in Str[:Half]])
            SumLast= sum ([ int(i) for i in  Str[Half:]])
            # print(SumFirst, SumLast)
            if SumFirst == SumLast : return 1
            return 0 
        # dd = []
        for i in range(low , high+1):
            if check(i) == 1 :
                # dd.append(i)
                count += 1
        # print(dd)
        return count 


```

### [1920. Build Array from Permutation](https://leetcode.com/problems/build-array-from-permutation/)

```python 
class Solution:
    def buildArray(self, nums: List[int]) -> List[int]:
        dd = []
        for i in range(len(nums)):
            dd.append(nums[nums[i]])
        return dd 
```

### [2094. Finding 3-Digit Even Numbers](https://leetcode.com/problems/finding-3-digit-even-numbers/)

```python 
class Solution:
    def findEvenNumbers(self, digits: List[int]) -> List[int]:
        Sample = list(set(permutations(digits, 3)))
        String = " ".join(["".join(map(str, i)) for i in Sample])
        String = String.split() # String to Number ["124", "126"] => [124, 126] 
        res = [i for i in String if int(i) % 2 == 0]
        K = sorted(res, key=lambda x: int(x))
        KP = [i for i in K if i[0] != '0']
        res = [] 
        for i in KP :
            if i not in res : res.append(int(i))
        return res 
```


###  [1550. Three Consecutive Odds](https://leetcode.com/problems/three-consecutive-odds/)

```python 
class Solution:
    def threeConsecutiveOdds(self, arr: List[int]) -> bool:
        for i in range(len(arr)-2):
            if( arr[i] & 1 == 1 and arr[i+1] & 1 == 1 and arr[i+2] &1  == 1) :return True
        return False 

```


### [3335. Total Characters in String After Transformations I](https://leetcode.com/problems/total-characters-in-string-after-transformations-i/)

Optimized : DP 

```python
class Solution:
    def lengthAfterTransformations(self, s: str, t: int) -> int:
        MOD = 1000000007
        cnt = [0] * 26
        
        for char in s:
            cnt[ord(char) - ord('a')] += 1

        for _ in range(t):
            tmp = [0] * 26
            for i in range(26):
                if i == 25:
                    tmp[0] = (tmp[0] + cnt[i]) % MOD
                    tmp[1] = (tmp[1] + cnt[i]) % MOD
                else:
                    tmp[i + 1] = (tmp[i + 1] + cnt[i]) % MOD
            cnt = tmp

        return sum(cnt) % MOD
```

TLE : 

```python 
class Solution:
    def lengthAfterTransformations(self, s: str, t: int) -> int:
        def check (dk : str)-> str:
            res = ""
            for i in range(len(dk)):
                if dk[i] == "z":
                    res += 'ab'
                else :
                    res = res+str(chr(ord(dk[i])+1))
            return res
        Res = s 
        for i in range(t):
            Res = (check(Res))
        return len(Res) % 1000007

```


### [1346. Check If N and Its Double Exist](https://leetcode.com/problems/check-if-n-and-its-double-exist/)


```python 
class Solution:
    def checkIfExist(self, arr: List[int]) -> bool:
        for i in range(len(arr)):
            for j in range(len(arr)):
                if i != j and (arr[i])== (2*arr[j]):
                    print(arr[i], 2*arr[j])
                    return True
        return False 
```


### [3024. Type of Triangle](https://leetcode.com/problems/type-of-triangle/) 


IMPORTANT : 

### Triangle Rule Reminder:

Before classifying as **equilateral**, **isosceles**, or **scalene**, you **must first check** whether the three sides **can form a valid triangle**.

```python

a + b > c
b + c > a
a + c > b

```

```python 
class Solution:
    def triangleType(self, nums: List[int]) -> str:
        nums.sort()
        if nums[1] + nums[0] < nums[2]:
            return "none"
        if nums[1] == nums[2] == nums[0] :
            return "equilateral"
        if nums[1] == nums[2] :
            return  "isosceles"
        else : return "scalene"
```


### [2894. Divisible and Non-divisible Sums Difference](https://leetcode.com/problems/divisible-and-non-divisible-sums-difference/)

```python 
class Solution:
    def differenceOfSums(self, n: int, m: int) -> int:
        rem = Zero = 0 
        for i in range(1,n+1):
            if i % m == 0 :
                Zero += i 
            else :
                rem += i 
        return rem- Zero 
```

### [2942. Find Words Containing Character](https://leetcode.com/problems/find-words-containing-character/)

```python 
class Solution:
    def findWordsContaining(self, words: List[str], x: str) -> List[int]:
         return [  i for i in range(len(words)) if x in words[i]]
```


### [440. K-th Smallest in Lexicographical Order](https://leetcode.com/problems/k-th-smallest-in-lexicographical-order/)

TLE == > Memory Limit Exceeded ....

```python 
class Solution:
    def findKthNumber(self, n: int, k: int) -> int:
        X = [ str(i)  for i in range(1,n+1) ]
        # print(X)
        dk = sorted(X , reverse = False)
        # print(dk)
        return int(dk[k-1])
```


### [3442. Maximum Difference Between Even and Odd Frequency I](https://leetcode.com/problems/maximum-difference-between-even-and-odd-frequency-i/)


```python 
class Solution:
    def maxDifference(self, s: str) -> int:
        Map = {}
        for i in range(len(s)):
            if s[i] not in Map:
                Map[s[i]] = 1
            else:
                Map[s[i]] += 1

        # print(Map)

        Eval = [val for idx, val in Map.items() if val & 1 == 0]
        Oval = [val for idx, val in Map.items() if val & 1 == 1]

        if not Eval or not Oval:
            return 0  # No valid comparison possible

        MinEval = min(Eval)
        MaxOval = max(Oval)

        # print(MinEval, MaxOval)
        # print(Eval, Oval)

        return MaxOval - MinEval

```


### [3423. Maximum Difference Between Adjacent Elements in a Circular Array](https://leetcode.com/problems/maximum-difference-between-adjacent-elements-in-a-circular-array/)


```python 
class Solution:
    def maxAdjacentDistance(self, nums: List[int]) -> int:
        Max = 0 
        Len= len(nums)
        for i in range(len(nums)):
            Max = max(Max , abs(nums[i] - nums[(i+1)%Len]))
        print(Max)
        return Max 

```