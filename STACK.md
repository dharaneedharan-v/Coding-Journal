
### [20. Valid Parentheses](https://leetcode.com/problems/valid-parentheses/)

APPROACH  :
 - **Push corresponding closing brackets** onto the stack when encountering an opening bracket (`(` → `)`, `{` → `}`, `[` → `]`).
- **Pop and check** when encountering a closing bracket:
    - If the stack is empty (no matching opening bracket), return `False`.
    - If the popped bracket does not match the current closing bracket, return `False`.
- **At the end**, return `True` **only if the stack is empty** (all brackets matched correctly).
```PYTHON 
class Solution:

    def isValid(self, s: str) -> bool:

        dd = []

        if len(s) == 1 :

            return False

        for i in s :

            if i == "(":

                dd.append(")")

            elif i == "{":

                dd.append("}")

            elif i == "[":

                dd.append("]")

            else :
				#Check the stack is empty or not 
                if not dd :

                    return False

                k = dd.pop()

                if k != i :

                    return False
#return True only the len of the stack is 0 
        return len(dd) == 0  # The core part of the code is here only if the stack is not empty means return False of the similar brackets alone there. =============IMPORTANT===================
```


### Monotonic Stack : 

### [402. Remove K Digits](https://leetcode.com/problems/remove-k-digits/)

```python 
class Solution:
    def removeKdigits(self, nums: str, k: int) -> str:
        stack = []
        for i in range(len(nums)) :
            while  stack and k > 0 and stack[-1] > nums[i]:
                stack.pop()
                k = k-1
            stack.append(nums[i])
        print(stack)
        if k > 0 :
            stack =  stack[:-k]
        return "".join(stack).lstrip("0") or "0"

```


