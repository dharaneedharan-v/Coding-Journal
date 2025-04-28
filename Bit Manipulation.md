### [371. Sum of Two Integers](https://leetcode.com/problems/sum-of-two-integers/)

Using the Bitwise :

```python 
class Solution:

    def getSum(self, a: int, b: int) -> int:

        Mask = 0xFFFFFFFF # 8 F  32 bit  
        #This is due to negative value it will take it to the infinity

        # print(Mask)

        Max_int = 0x7FFFFFFF # 7 F 32 bit 

        # print(Max_int)

        while (b!= 0 ):

            a , b = (a ^ b) & Mask ,((a & b) << 1 )& Mask  

        return  a if a <= Max_int else ~(a^Mask)
```

Using the Libray  called Ctypes  : 

```python 

import ctypes
class Solution:
    def getSum(self, a: int, b: int) -> int:
        a = ctypes.c_int(a) # Wrap a in ctypes.c_int once at the start
        b = ctypes.c_int(b) # Wrap b in ctypes.c_int once at the start
        while(b.value!=0 ):
            # Perform bitwise operations directly without wrapping in ctypes.c_int
            a.value , b.value = (a.value ^ b.value ) , (a.value & b.value ) << 1 
        return a.value  
```