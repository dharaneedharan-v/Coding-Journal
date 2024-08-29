
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