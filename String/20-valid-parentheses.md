# [20-valid-parentheses](https://leetcode.com/problems/valid-parentheses)

#### Intuition:
* it is good to have an open parenthesis at anytime
* when you get a close parenthesis, it must follow the same type of open parenthesis
* the string is valid if and only if all close parentheses are accompanied by the same type of open parenthesis and there is no open parenthesis which do not have its close parenthesis.

## Code

```python
class Solution(object):
    def isValid(self, s):
        """
        :type s: str
        :rtype: bool
        """
        stack = []
        
        for c in s:
            if c in ('(', '[', '{'):
                stack.append(c)
            else:
                if not stack: return False
                else: 
                    temp = stack.pop()
                    if temp == '(' and c != ')': return False
                    if temp == '[' and c != ']': return False
                    if temp == '{' and c != '}': return False
                
        return True if not stack else False
```
