
### [69. Sqrt(x)](https://leetcode.com/problems/sqrtx/)

TC -> O(N)

```python 
class Solution:

    def mySqrt(self, x: int) -> int:

        ans = 0  

        if x == 1 :

            return 1

        for i in range(1,x):

            if i*i <= x:

                ans = i  

            else :

                break

        return ans
```

TIME COMPLEXITY : O( N LOG N )

```PYTHON 
class Solution:

    def mySqrt(self, x: int) -> int:

        ans = 0

        left =  1

        right = x  

        while (left <= right):

            mid = left + (right-left) // 2

            if mid * mid <= x :

                ans  = mid

                left =mid + 1

            else :

                right = mid -1

        return ans
```


###   Find Nth Root Of M

TC => O (LOG M)

```python

def NthRoot(n: int, m: int) -> int:

    root = m**(1/n)

    if round(root) **(n) ==m :

        return int(round(root)) 

    else :

        return -1
```



### [875. Koko Eating Bananas](https://leetcode.com/problems/koko-eating-bananas/)

```PYTHON 
class Solution:

    def minEatingSpeed(self, piles: List[int], h: int) -> int:

        left = 1  # Minimum possible eating speed

        right = max(piles)  # Maximum possible eating speed

        def ischeck(piles, mid):

            Sum = 0

            for i in piles:

                Sum += math.ceil(i / mid)  # Calculate hours required for each pile

            return Sum

  

        ans = -1

        while left <= right:

            mid = left + (right - left) // 2

            if ischeck(piles, mid) <= h:  # Check if current speed is valid

                ans = mid  # Store the current valid speed

                right = mid - 1  # Try smaller speeds

            else:

                left = mid + 1  # Try larger speeds

        return ans
       
```


### [1482. Minimum Number of Days to Make m Bouquets](https://leetcode.com/problems/minimum-number-of-days-to-make-m-bouquets/)

```PYTHON 

```

### BS on 2D Arrays: 

###  Row with Maximum 1's

```python 


def rowMaxOnes(mat, n, m):
    dd = [0]*n

    for i in range(n*m ):

        row = i//n 

        col = i % m 

        if mat[row][col] == 1 :

            dd[row]+=1 

    Max_1 = max(dd)

    if Max_1 ==  0 :

        return -1

    return dd.index(Max_1)
   ______________________________ OR ________________________________________


def rowMaxOnes(mat, n, m):

    Count_1 = 0

    Count_idx = -1

  

    for i in range((n)):

        dd = sum(mat[i])

        if dd > Count_1:

            Count_1 = dd

            Count_idx = i

    return Count_idx
```

O(N LOG M )

```python 
  
  

def lowerBound(arr, n, x):

    low = 0

    high = n - 1

    ans = n

  

    while low <= high:

        mid = (low + high) // 2

        # maybe an answer

        if arr[mid] >= x:

            ans = mid

            # look for smaller index on the left

            high = mid - 1

        else:

            low = mid + 1  # look on the right

    return ans

  

def rowWithMax1s(matrix, n, m):

    cnt_max = 0

    index = -1

  

    # traverse the rows:

    for i in range(n):

        # get the number of 1's:

        cnt_ones = m - lowerBound(matrix[i], m, 1)

        if cnt_ones > cnt_max:

            cnt_max = cnt_ones

            index = i

    return index
```

### [74. Search a 2D Matrix](https://leetcode.com/problems/search-a-2d-matrix/)


TC -> O(N^2)

```python 
class Solution:

    def searchMatrix(self, matrix: List[List[int]], target: int) -> bool:

        for i in range(len(matrix)):

            for j in range(len(matrix[0])):

                print(matrix[i][j])

                if matrix[i][j] == target:

                    return True

  

        return False
       
```


TC ->  O(N + logM) instead of O(N*logM)
```python 
class Solution:

    def searchMatrix(self, matrix: List[List[int]], target: int) -> bool:

        def binarySearch( mat,target):

            m = len(mat)

            left = 0

            right = m-1

            while (left <= right):

                mid = left + (right-left )// 2

                if mat[mid]== target:

                    return True

                elif mat[mid] < target :

                    left = mid+ 1

                else :

                    right = mid -1

            return False

        for i in range(len(matrix)):

            if matrix[i][0] <= target <=  matrix[i][len(matrix[0])-1]:

                return binarySearch(matrix[i],target)

        return False
```

*OPTIMAL APPROACH :* 
*TC -> O(log(NxM))*

*flatening the search into 1d dimention   logicaly (Imagine ) and acessing the index , from that index creating the 2d element.  

*If we convert the 2d into single means NM only not the optimal (log M N)*

```python 
class Solution:

    def searchMatrix(self, matrix: List[List[int]], target: int) -> bool:

        n = len(matrix)

        m = len(matrix[0])

        left = 0

        right = n*m -1

        while (left <= right):

            mid = left + (right-left )// 2

            l = mid//m

            r= mid %  m

            if matrix[l][r]== target:

                return True

            elif matrix[l][r] < target :

                left = mid+ 1

            else :

                right = mid -1

        return False
```