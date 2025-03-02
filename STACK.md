
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
        return len(dd) == 0
```