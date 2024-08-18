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