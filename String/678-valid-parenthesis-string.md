# [678-valid-parenthesis-string](https://leetcode.com/problems/valid-parenthesis-string/)

##### Intuition: while looping through the string s,
* if char == '(', it must be accompanied by a maximum of +=1 close parenthesis (cmax) and minimum of +=1 close parenthesis (cmin)
(cmax, cmin = max/min # close parenthesis required) 
* if char == ')', the counter cmax will be -=1 , cmin will be reduced by 1 until it reaches 0 (cmin cannot get negative, since making any more `(` after that is still invalid)
* if char == '*', the counter cmax will be +=1 (the * is used as `(`), cmin will be reduced by 1 until it reaches 0 (the * is used as `)`)

* At anytime, if cmax < 0, the string is invalid as it maximum number of possible open parenthesis is less than maximum number of close parenthesis
* The string is valid only when final cmin == 0 (no more close parenthesis needed).

## Code

```python
class Solution(object):
    def checkValidString(self, s):
        """
        :type s: str
        :rtype: bool
        """
        rmax, rmin = 0, 0 
        for c in s:
            if c == '(':
                rmax += 1
                rmin += 1
            if c== ')':
                rmax -= 1
                rmin = max(rmin -1, 0)
            if c == '*':
                rmax += 1 # alterisk used as '('
                rmin = max(rmin -1, 0) # alterisk used as ')'
            if rmax <0: return False
        
        return rmin == 0
```
