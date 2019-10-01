# [301-remove-invalid-parentheses](https://leetcode.com/problems/remove-invalid-parentheses/)

I believe this is not the shortest way to implement the function, but it works, and I love the way the next_moves is written down.   
Somehow too long at the first time I see it, but it works.

```python
class Solution(object):
    def removeInvalidParentheses(self, s):
        """
        :type s: str
        :rtype: List[str]
        """
        def isValid(a):
            count = 0
            for c in a:
                if c == '(': count += 1
                elif c == ')': count -= 1
                if count<0: return False
            return count == 0
        
        possibles = {s}
        while possibles:
            valid = {p for p in possibles if isValid(p)}
            if valid:
                return valid
            possibles = {p[:i] + p[i+1:] for p in possibles for i in range(len(p))}

```
