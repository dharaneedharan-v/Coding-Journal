
### Minimum number of Coins

```python 
#User function Template for python3

class Solution:
    def minPartition(self, N):
        # code here
        Res = []
        Map = [1 ,2 , 5, 10, 20, 50, 100, 200, 500, 2000]
        for i in range(len(Map)-1 , -1 , -1 ):
            while  N >=Map[i]: #### NOT N == Map[i] == 0 :   we want tp check the if the Numbe Number is greater than the current element.. While isused insted of IF if there are more than the same element .
                Res.append(Map[i])
                N = N-Map[i]
        return Res
                
```