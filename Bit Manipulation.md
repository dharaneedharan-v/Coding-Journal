
# Hint : 

### ***For the division :*** 
### Expressions:

- `2 % 1` → Modulo operation (remainder after division)
    
- `2 & 1` → Bitwise AND operation
    

---

### Result:

- `2 % 1` → `0` (because 2 divided by 1 leaves remainder 0)
    
- `2 & 1` → `0` (binary: `10 & 01 = 00`)

In most CPUs:

- Bitwise `&` → takes **1 cycle**
    
- Modulo `%` → takes **multiple cycles** (division is more complex than AND)



# left Shift : Pow( 2 , 3 ) = 8 
## 👉 What does `2 << 3` mean in Python?

It’s a **bitwise left shift**:

> Shift the number `2` left by `3` bits.




Using the left Shift :    HINT : Left Shift is used as pow of 2 , Right shift is used for the division.... 

```python 
power_of_2 = 1 << 3

print(power_of_2) 1 means 2 


```

Example : 

| Expression | Meaning  | Result |
| ---------- | -------- | ------ |
| `1 << 3`   | `1 * 2³` | 8      |
| `2 << 3`   | `2 * 2³` | 16     |
| `5 << 2`   | `5 * 2²` | 20     |
| `4 << 1`   | `4 * 2¹` | 8      |
# Right Shift :  Integer Division 

## 👉 What does `x >> n` mean?

> It means: **Shift the bits of `x` to the right by `n` positions**  
> In math: It's like doing **integer division** by `2ⁿ`

```python 
16 >> 3 == 16 // (2 ** 3) == 16 // 8 == 2
```


Example :

| Expression | Meaning   | Result |
| ---------- | --------- | ------ |
| `8 >> 1`   | `8 // 2`  | 4      |
| `16 >> 2`  | `16 // 4` | 4      |
| `32 >> 3`  | `32 // 8` | 4      |
| `5 >> 1`   | `5 // 2`  | 2      |
# ***Power of 2 :*** 

*🔧 Bitwise Condition:*

```python 
n > 0 and (n & (n - 1)) == 0


```


### *📘 Explanation:*

#### *Example 1:*

```python 
n = 8      # binary: 1000
n - 1 = 7  # binary: 0111

8 & 7 = 0  → so, it's a power of 2 ✅

```

*Example 2:*

```python 
n = 10     # binary: 1010
n - 1 = 9  # binary: 1001

10 & 9 = 1000 → not 0 → not a power of 2 ❌

```

*Why the n > 0 :* 

*The expression `(n & (n - 1)) == 0` only makes sense for **positive numbers**.*

*If `n <= 0`:*

- *`0` is **not** a power of 2.*
    
- ***Negative numbers** have different binary representations (two's complement) and may falsely pass the test.*
### *Summary (for quick recall):*

- *✅ Power of 2 → only one `1` bit → `n & (n - 1) == 0`*

```python 
   1000    ← 8
&  0111    ← 7
=  0000

```

*Since the result is `0`, it means **only one `1` was present** → it's a power of 2 ✅*

- *❌ If more than one bit is set → result ≠ 0*
    
- *🕒 Time: O(1), 📦 Space: O(1)*


# **k-th bit** of a number is set ( is `1`)

### Example: Checking the 3rd bit of `n = 10` (binary: `1010`)

#### Step 1: Write the binary of `n`

The binary representation of `10` is:

```yaml
n = 10 → binary: 1010

```


#### Step 2: Identify the bit positions

The positions of the bits are counted **from right to left**, starting at 0:

```yaml
Binary: 1 0 1 0
Position: 3 2 1 0

```

So, the **3rd bit** (from the right) is the `1` in the **position 3** (it is set to 1).

#### Step 3: Create a **mask** for the k-th bit

You want to check the **3rd bit** (counting from `0`), so the mask will be created by shifting `1` to the 3rd position:


```yaml 
1 << 3  → 1000 (binary)  → This is 8 (decimal).

```


#### Step 4: Apply **bitwise AND** with `n`

Now, use the bitwise AND operator (`&`) between `n = 10` (which is `1010` in binary) and the mask `1000` (which is `8` in decimal):


```yaml
n = 10 → binary: 1010
mask = 1 << 3 = 8 → binary: 1000

10 & 8 → 1010 & 1000 = 1000 (binary) → which is 8 (non-zero)


```



#### Step 5: Interpretation

- The result is **non-zero** (it's `1000`), which means the 3rd bit is set (`1`).
    

### Conclusion:

- The **3rd bit** of `n = 10` is **set to 1** (because `1000` is non-zero).
    
- So, the check will return **True** if we check `k = 3`


### Example: Checking the 3rd bit of `n = 6` (binary: `0110`)

#### Step 1: Write the binary representation of `n`

The binary representation of `n = 6` is:

```ini
n = 6 → binary: 0110

```

#### Step 2: Identify the bit positions

The positions of the bits are counted **from right to left**, starting at position 0:

```makefile 
Binary: 0 1 1 0
Position: 3 2 1 0

```

So, the **3rd bit** (from the right) is the `0` in the **position 3** (it is not set).

#### Step 3: Create a **mask** for the k-th bit

You want to check the **3rd bit** (counting from `0`), so the mask will be created by shifting `1` to the 3rd position:

```python 
1 << 3  → 1000 (binary)  → This is 8 (decimal).

```

#### Step 4: Apply **bitwise AND** with `n`

Now, use the bitwise AND operator (`&`) between `n = 6` (which is `0110` in binary) and the mask `1000` (which is `8` in decimal):

```python 
n = 6 → binary: 0110
mask = 1 << 3 = 8 → binary: 1000

6 & 8 → 0110 & 1000 = 0000 (binary) → which is 0

```
### Final Answer:

- **n = 6** (binary: `0110`)
    
- **k = 3** (checking the 3rd bit)
    
- Since the result of `6 & (1 << 3)` is `0`, the **3rd bit is not set**.


## 🎯 Quick Rule:

```python 
(n & (1 << k)) != 0  → True (bit is set)
(n & (1 << k)) == 0  → False (bit is not set)

```

### ✅ How to toggle the k-th bit:

### ✅ **Logic**:

To **toggle** (flip) the k-th bit of a number:

1. **Create a mask** that has only the k-th bit set to `1`.
    
2. Use the **bitwise XOR** (`^`) operation to **toggle** the bit:
    
    - If the k-th bit is `0`, it becomes `1`.
        
    - If the k-th bit is `1`, it becomes `0`.
        

The XOR operation works like this:

- `0 ^ 1 = 1` (flips `0` to `1`)
    
- `1 ^ 1 = 0` (flips `1` to `0`)
    

---

### ✅ **Core Part**:

1. **Create a mask**: `1 << k`
    
    - This shifts `1` to the k-th position, making a mask with only the k-th bit set.
        
2. **Apply XOR**: `n ^ (1 << k)`
    
    - XOR the number `n` with the mask. This will flip the k-th bit.

```python 
def toggle_kth_bit(n, k):
    return n ^ (1 << k)

```

**Example 1**: Toggle the 2nd bit of `n = 10` (binary: `1010`)
#### Step 1: Write the binary form of `n`

ini

CopyEdit

```python 
n = 10 → binary: 1010
```


#### Step 2: Create a mask to toggle the 2nd bit

- The 2nd bit corresponds to position `2`, so create the mask:

```python 
1 << 2 → binary: 0100
```
    

#### Step 3: Apply XOR to toggle the 2nd bit

- XOR the mask `0100` with `n = 1010`:
```python 
1010
^ 0100
--------
1110  → This is 14 in decimal

```
#### Step 4: Result

The **2nd bit** of `10` is toggled from `1` to `0`, resulting in `14`.

### 🎯 **Summary**:

- **Logic**:
    
    - Create a mask: `1 << k`
        
    - Toggle with XOR: `n ^ (1 << k)`
        
- **Time Complexity**: O(1)
    
- **Space Complexity**: O(1)

# How to **set** the k-th bit of a number: 

### ✅ **Goal**:

Set the **k-th bit to 1**, **no matter what it was before** (even if it was already 1).
### ✅ **Core Logic**:

Use **bitwise OR** (`|`) with a mask that has only the **k-th bit set**.

- Why?
    
    - `0 | 1 = 1` → sets bit to 1
        
    - `1 | 1 = 1` → keeps bit 1
        
    - So, OR always **forces** the k-th bit to be 1.
### 🧠 Steps:

1. Create a mask with only the k-th bit set:

```python 
mask = 1 << k

```
    
2. Use bitwise OR to set the bit:

```python 
n | mask
```

###  Python Code:

```python 
def set_kth_bit(n, k):
    return n | (1 << k)
```

### Example: Set the 1st bit of `n = 10` (binary `1010`)

#### Step 1: Binary of 10
```python 
n = 10 → binary: 1010

```
#### Step 2: Create a mask for 1st bit

```python 
1 << 1 = 0010 (binary) → 2 in decimal

```

#### Step 3: OR operation

```python 
  1010  (n = 10)
| 0010  (mask = 2)
-------
  1010  → result = 10

```

#### ✅ Result:

The 1st bit is already set → value remains 10.
### 🎯 Summary:

|Operation|Purpose|Bitwise Formula|
|---|---|---|
|Set|Force to `1`|`n|

- **Always sets** the k-th bit to 1
    
- **Time Complexity**: O(1)

# How to **unset** (clear) the k-th bit of a number
### ✅ **Goal**:

Force the **k-th bit to 0**, no matter what it was before.

---

### ✅ **Core Logic**:

Use **bitwise AND** with a mask that has **all 1s except the k-th bit as 0**.

---

### 🧠 Steps:

1. Create a mask with the k-th bit as `0` and all other bits as `1`:
    
```python 
mask = ~(1 << k)

```
    
    - `1 << k`: sets only the k-th bit to `1`
        
    - `~`: inverts the bits — now the k-th bit is `0`, others are `1`
        
2. Use bitwise AND to clear the bit:

```python 
n & mask
```

---

###  Python Code:

```python 
def clear_kth_bit(n, k):
    return n & ~(1 << k)

```

---

### 🔍 Example 1: Clear the 1st bit of `n = 10` (binary `1010`)

#### Step 1: Binary of 10

```python 
n = 10 → binary: 1010

```

#### Step 2: Create a mask

```python 
1 << 1 = 0010
~(0010) = 1101

```

#### Step 3: AND operation

```python 
  1010
& 1101
-------
  1000 → result = 8

```

  

#### ✅ Result:

The 1st bit is cleared → result is 8.

---

### 🔍 Example 2: Clear the 2nd bit of `n = 15` (binary `1111`)

```python 
1 << 2 = 0100
~0100 = 1011

1111
& 1011
-------
1011 → result = 11

```

---

### 🎯 Summary:

|Operation|Purpose|Bitwise Formula|
|---|---|---|
|Clear|Force bit to `0`|`n & ~(1 << k)`|

- **Time Complexity**: O(1)

## 🔢 Multiply or Divide by 2ᵏ Using Bitwise

### ✅ **Multiplication by 2ᵏ**

#### 🧠 Logic:

To multiply a number `n` by 2ᵏ, **left shift** it by `k` bits:

### 🧮 Formula:
```python 
n << k   # Multiplies n by 2^k

```

#### 🧪 Example:

```python 
n = 3
k = 4
result = 3 << 4  # 3 * 2^4 = 3 * 16 = 48

```

---

### ✅ **Division by 2ᵏ**

#### 🧠 Logic:

To divide a number `n` by 2ᵏ, **right shift** it by `k` bits:

### 🧮 Formula:

```python 
n >> k   # Divides n by 2^k (floor division)
```

#### 🧪 Example:

```python 
n = 48
k = 4
result = 48 >> 4  # 48 // 16 = 3

```

✅ `48 >> 4` = `3`

---

### ⚠️ Works only with integers

- Python's `>>` and `<<` work only on integers.
    
- For floating-point math, use `*` and `/`.
    

---

### 🔍 Bonus: With Negative Numbers

- **Multiplication (`<<`)**: Still works fine.
    
- **Division (`>>`)**: Performs **floor division**, i.e., rounds **toward negative infinity**.
    

```python 
-5 >> 1 → -3   ✅ (-5 // 2)
```

---
## ⚠️ Bitwise with **Floating Points**

### ❌ Not Allowed!

Bitwise operations only work with **integers** in Python.  
Trying something like:

```python 
3.5 << 1
```

### ✅ Workaround:

If you really need to apply bitwise on floating numbers, **convert** to int first — but be cautious:

```python 
int(3.5) << 1  → (3 << 1) = 6
```
### 🧾 Final Summary:

|Operation|Bitwise Expression|Result|
|---|---|---|
|Multiply by 2ᵏ|`n << k`|`n * (2^k)`|
|Divide by 2ᵏ|`n >> k`|`n // (2^k)`|

| Case                   | Works with Bitwise? | Notes                     |
| ---------------------- | ------------------- | ------------------------- |
| Positive Integers      | ✅ Yes               | Fully supported           |
| Negative Integers      | ✅ Yes               | Uses two’s complement     |
| Floating Point Numbers | ❌ No                | Must convert to int first |
|                        |                     |                           |

# **`x % (2^k)`** using **bitwise operators**
## ✅ Core Logic

To compute `x % (2^k)`, just **mask the lowest `k` bits** of `x` using **bitwise AND**:

### 🧮 Formula:

```python
x % (2 ** k) == x & ((1 << k) - 1)

```
---

## 📌 Why It Works

- `(1 << k)` creates a number with only the **k+1-th bit** set.
    
- Subtracting 1 gives a number where the **lowest k bits are all 1**.
    
- ANDing with `x` gives only the lowest `k` bits of `x` — which is `x % (2^k)`.
    

---

## 🧪 Example:

Let’s compute `77 % 8` using bitwise.

### Step 1: Convert to binary

- `77` → `1001101`
    
- `8` = `2^3` → So, `k = 3`
    

### Step 2: Compute using bitwise

```python 
x = 77
k = 3
mask = (1 << 3) - 1 = 8 - 1 = 7 → binary: 0111

result = 77 & 7
        = 1001101 & 0000111
        = 0000101 → 5

```

✅ `77 % 8 = 5`

---

## ✅  Code:

```python 
def mod_power_of_two(x, k):
    return x & ((1 << k) - 1)
```

---

## 🎯 Summary

| Expression  | Bitwise Formula      | Meaning                |
| ----------- | -------------------- | ---------------------- |
| `x % (2^k)` | `x & ((1 << k) - 1)` | Get remainder with 2^k |


# How to **swap two numbers without using a temp variable**

## ✅ Logic using XOR

XOR has a key property:

> `a ^ b ^ b = a`  
> `a ^ a = 0`  
> `a ^ 0 = a`

So you can swap two values like this:

### 🧮 Swap Steps:

```python 
a = a ^ b
b = a ^ b  # becomes original a
a = a ^ b  # becomes original b

```
---

## 🧪 Python Code:

```python 
def swap(a, b):
    a = a ^ b
    b = a ^ b
    a = a ^ b
    return a, b

```
### 🔍 Example:

```python 
a = 5
b = 7

# After swap
a, b = swap(5, 7)
print(a, b)  # Output: 7 5

```
✅ It swaps `a` and `b` **without** a third variable.

---

## ⚠️ Notes:

- Only works with **integers**
    
- May behave unexpectedly if `a` and `b` refer to the **same memory location** (like in C/C++)
    
- In Python, **tuple unpacking** is preferred:
    
```python 
a, b = b, a  # cleaner and more readable
```

---

### 🎯 Summary:

|Method|Code|Temp Variable?|
|---|---|---|
|XOR Swap|`a ^= b; b ^= a; a ^= b`|❌ No|
|Pythonic|`a, b = b, a`|❌ No|

### How to **count set bits** (1s) in an integer **efficiently**

## ✅ Goal:

Count how many bits are set to `1` in the **binary representation** of a number.

---

## ✅ Efficient Method: **Brian Kernighan’s Algorithm**

### 🧠 Logic:

Each time you do `n & (n - 1)`, it **removes the rightmost set bit**.

Repeat this until `n` becomes `0`.

---

### 🔧 Formula:

```python 
while n > 0:
    n = n & (n - 1)
    count += 1

```

---

### 🧪 Python Code:

```python
def count_set_bits(n):
    count = 0
    while n:
        n = n & (n - 1)
        count += 1
    return count

```

---

### 🔍 Example:

Let’s count set bits in `n = 13` (binary `1101`):

1. `1101` → rightmost `1` removed → `1100`
    
2. `1100` → rightmost `1` removed → `1000`
    
3. `1000` → rightmost `1` removed → `0000`
    

✅ `3` set bits.

---

## 🕒 Time Complexity:

- **O(k)** where `k` is the number of set bits (very efficient!)
    
- Better than looping over all 32 or 64 bits.
    

---

### 🆚 Other Methods:

|Method|Time Complexity|Notes|
|---|---|---|
|`bin(n).count('1')`|O(n) string ops|Pythonic, less efficient|
|Brian Kernighan’s Algo|O(k)|Efficient and interview-worthy ✅|

---

### 🎯 Summary:

|Task|Bitwise Trick|
|---|---|
|Count set bits|`n = n & (n - 1)` repeatedly|


==========================================================
### *[371. Sum of Two Integers](https://leetcode.com/problems/sum-of-two-integers/)*

*Using the Bitwise :*

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

*Using the Libray  called Ctypes  :* 

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



### *[29. Divide Two Integers](https://leetcode.com/problems/divide-two-integers/)*


 *Core logic is Subtract the  dividend = dividend - divisor*  

*If the value is greater , we go for the concept of doubling the  divisor..* 

*Need to handle the Negative Values also , only the positive value only go to the  loop . If not* 
*infinite loop .*

*Sign is important for this ...* 

*Use the XOR or Not operator ...*

```python 
class Solution:
    def divide(self, dividend: int, divisor: int) -> int:
        Neg  = (dividend < 0 ) != (divisor < 0 ) 
        count = 0 
        if divisor ==  0 or dividend == 0 :return count 
        dividend = abs(dividend)
        divisor = abs(divisor)

        while (dividend >= divisor):
            Temp  = divisor 
            Mul = 1
            while (Temp + Temp <= dividend):
                Temp   = Temp + Temp 
                Mul = Mul + Mul 
            
            dividend = dividend - Temp 
            count = count + Mul 
        if Neg :
            count = - count # _- Negative Sign count 
            return count 
		# clamping the Value to avoid the Overflow  
        return min(max(count,-2**31), 2 ** 31 -1 )

        
```

### [231. Power of Two](https://leetcode.com/problems/power-of-two/)


```python 
class Solution:
    def isPowerOfTwo(self, n: int) -> bool:
        def power (N :int)-> bool:
            return (n > 0 )and ( n & ( n -1 )) == 0 
        return power(n)
```


```python 
class Solution:
    def isPowerOfTwo(self, n: int) -> bool:
        for i in range(31):
            ans = 2** i 
            if ans ==  n :
                return True 
        return False         
```

### [191. Number of 1 Bits](https://leetcode.com/problems/number-of-1-bits/)


```python 
class Solution:
    def hammingWeight(self, n: int) -> int:
        count = 0 
        while (n > 0 ):
            n  = n & (n-1)
            count += 1
        return count 
```


### [338. Counting Bits](https://leetcode.com/problems/counting-bits/)

Followed the Number of bit counting 

```python 
class Solution:
    def countBits(self, n: int) -> List[int]:
        def Numer(N:int):
            count =  0 
            while (N>0):
                N = N & (N-1)
                count += 1 
            return count 
        res = []
        for  i in range(n+1):
            res.append(Numer(i))
        return res

```


### [190. Reverse Bits](https://leetcode.com/problems/reverse-bits/)

```python 
class Solution:
    def reverseBits(self, n: int) -> int:
        Bin = bin(n)[2:].zfill(32)
        String = Bin[::-1]
        return int((String),2)

```

Using the Bit Manipulation :

```python 
class Solution:
    def reverseBits(self, n: int) -> int:
        res = 0 
        temp =  0 
        for  i in range(32):
            Lsb = n & 1  # Last bit is a 0 or 1 finding
            temp =  Lsb << (31-i) 
            res = temp | res 
            n = n >> 1 
        return res 
```

### Set the rightmost unset bit

```python 
class Solution:
	def setBit(self, n):
        return n | (n+1)
        
```


### [2220. Minimum Bit Flips to Convert Number](https://leetcode.com/problems/minimum-bit-flips-to-convert-number/)

XOR of the start and goal , 
Count the set bit alone. 
```python 
class Solution:
    def minBitFlips(self, start: int, goal: int) -> int:
        Ans = start  ^ goal 
        count = 0 
        while Ans > 0 :
            Ans = Ans & (Ans-1)
            count += 1 
        return count 

```

### [78. Subsets](https://leetcode.com/problems/subsets/)


Normal For Loop :  Not Efficient : 

```python 
class Solution:
    def subsets(self, nums: List[int]) -> List[List[int]]:
        res = [[]]
        for i in nums :
            temp = []
            for j in res :
                temp.append((j+[i]))
            # res.append(temp) # use the extend 
            res = res + temp 
        return res 



```

Using the Bit Manipulation : 

```python 
class Solution:
    def subsets(self, nums: List[int]) -> List[List[int]]:
        res = []
        for i in range(2**len(nums)) : ## (1 << len(nums)
            Subset = []
            for j in range(len(nums)):
                if i & (1 << j ):
                    Subset.append(nums[j])
            res.append(Subset)
        return res 
```


### [260. Single Number III](https://leetcode.com/problems/single-number-iii/)

MySolution  : 

```python 
class Solution:
    def singleNumber(self, nums: List[int]) -> List[int]:
        dd = {}
        for i in range(len(nums)):
            if nums[i] not in dd :
                dd[nums[i]] = 1 
            else : dd[nums[i]] += 1
        res = []
        for idx , val in dd.items():
            if val == 1 :
                res.append(idx)
        return res 

```

Another Approach : 

```python
class Solution:
    def singleNumber(self, nums: List[int]) -> List[int]:
        res = []
        for i in range(len(nums)):
            if nums[i] not in res :
                res.append(nums[i])
            else :
                res.remove(nums[i])
        # print(res)
        return res 
```

Optimized And In Bit Manipulation : 

HINT : 
### 🧠 **Memory Trick: "XOR, Mask, Split, Solve"**

Break it down into this **4-step mantra**:

1. **XOR everything**:  
    All duplicates cancel out — you’re left with `a ^ b` (two unique numbers).
    
2. **Mask the difference**:  
    Use `Xor & -Xor` to isolate **one differing bit** between `a` and `b`.
    
3. **Split by the bit**:  
    Group the numbers by whether that bit is **0 or 1**.
    
4. **Solve by XOR in each group**:  
    XOR within each group — all duplicates cancel again — only unique number remains in each.
    

```python 
class Solution:
    def singleNumber(self, nums: List[int]) -> List[int]:
        Xor = 0 
        for i in range(len(nums)):
            Xor = Xor ^ nums[i]
        # print(Xor)
        Mask = Xor & -Xor
        # print(Mask)
        Ans = 0 
        group1 = []
        group2 = []
        for i in range(len(nums)):
            if Mask & nums[i] == 0:group1.append(nums[i])
            else :group2.append(nums[i])
        # print(group1, group2)
        X = 0 
        Final = []
        for i in range(len(group1)):
            X = X ^ group1[i]
        Final.append(X)
        Y = 0 
        for i in range(len(group2)):
            Y = Y ^ group2[i]
        Final.append(Y)
        return Final
```

 OR 
 
```python 
class Solution:
    def singleNumber(self, nums: List[int]) -> List[int]:
        # Finding XOR of the two elements that appear only once
        xor = 0
        for num in nums:
            xor ^= num
        # Finding the rightmost set bit
        mask = xor & -xor
        num1 = 0
        for num in nums:
            if mask & num == 0:
                num1 ^= num
        return [num1, xor^num1]
```
### [136. Single Number](https://leetcode.com/problems/single-number/)


Using the Bit Manipulation :  

```python 
class Solution:
    def singleNumber(self, nums: List[int]) -> int:
        Ans = 0 
        for u in range(len(nums)):
            Ans = Ans ^ nums[u]
            print(Ans)
        return Ans 
```

### [137. Single Number II](https://leetcode.com/problems/single-number-ii/)

Using the Sorting : 

```python 
class Solution:
    def singleNumber(self, nums: List[int]) -> int:
        nums.sort()
        if len(nums) == 1 :return nums[0]
        if nums[0] != nums[1]:return nums[0]
        if nums[-1] != nums[-2] :return nums[-1]
        for i in range(1,len(nums), 3):
            if nums[i] != nums[i-1]:
                return nums[i-1]
```

Using the Bit Manipulation : 

```python 
class Solution:
    def singleNumber(self, nums):
        ones, twos = 0, 0

        for num in nums:
            # Update ones and twos
            ones = (ones ^ num) & ~twos
            twos = (twos ^ num) & ~ones

        return ones  # The single number remains in "ones"
```


### [50. Pow(x, n)](https://leetcode.com/problems/powx-n/)

Brute Force : 
TLE : 

```python 
class Solution:
    def myPow(self, x: float, n: int) -> float:
        Ans= 1
        for   i in range(abs(n)):
            Ans = Ans * x
        print(Ans)
        return 1/Ans if n < 0 else float(Ans)
```

Optimal : 

HINT :  Multiply the Base and reduce the base  

Important : Not work for the Odd numbers Need to be handled Using the If condition 

```python 
res = 1
n = 13 → odd → res *= x (res = 2)
x = 2 → 4, n = 6

n = 6 → even → skip res
x = 4 → 16, n = 3

n = 3 → odd → res *= x (res = 2 * 16 = 32)
x = 16 → 256, n = 1

n = 1 → odd → res *= x (res = 32 * 256 = 8192)

```

```python 
class Solution:
    def myPow(self, x: float, n: int) -> float:
        res = 1
        if n < 0 :
            n = -n
            x = 1/x 
        while n > 0 :
            if n % 2 == 1 : ### For the Odd Numbers
                res = res *  x 
            x = x * x 
            n  = n // 2
        print(res)
        return  res 
```