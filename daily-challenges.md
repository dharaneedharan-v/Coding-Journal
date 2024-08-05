### [1508. Range Sum of Sorted Subarray Sums](https://leetcode.com/problems/range-sum-of-sorted-subarray-sums/)

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