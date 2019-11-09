# [32-longest-valid-parentheses](https://leetcode.com/problems/longest-valid-parentheses/)

There are a few solutions to this problem. 
1. The brute-force solution check if the substrings are valid and store the longest valid substring. This solution does not pass the test cases.
2. The second solution uses DP. More information about this solution can be found [here](https://leetcode.com/articles/longest-valid-parentheses/). However, the update rule is not easy to spot.
3. Stack solution 
4. Counter solution

### Stack
**Intuition**: the stack store the indices of invalid parentheses. The space between those invalid parentheses are the length of valid substrings of parentheses

```python
class Solution(object):
    def longestValidParentheses(self, s):
        """
        :type s: str
        :rtype: int
        """
        # idea: valid pair of parentheses will be pop out from the original stack. 
        # calculate the space between those parentheses will give the length of the longest valid parenthesis
        stack = []
        for i, c in enumerate(s):
            if c == '(': stack.append(i)
            else:
                if stack and s[stack[-1]] == '(': stack.pop()
                else: stack.append(i)
            # print(stack)
        stack = [-1] + stack + [len(s)]
        print(stack)
        return max([stack[i]-stack[i-1]-1 for i in range(1, len(stack))])
```

### Counter
**Intuition**: 
The string is valid only when (1) count of close/open parentheses are equal and (2) number of open parentheses are >= close parentheses at all times.

The count of open/close parentheses are half of the length of potential longest valid open/close parentheses pairs.

Thus:
- when count of open parenthesis = count of close parentheses, we update the longest valid string.
- when count of close parentheses > count of open parentheses, the substring is invalid, we update reset the count of open/close parentheses immediately.


```python
class Solution(object):
    def longestValidParentheses(self, s):
        """
        :type s: str
        :rtype: int
        """
        max_, o, c = 0,0,0 #max length, count of open/close parenthesis
        
        for char in s:
            if char == '(': o += 1
            else:
                c += 1
                if c > o:    c = o = 0
                elif c == o: max_ = max(max_, 2*o)
        
        o=c=0
        for char in reversed(s):
            if char == ')': o += 1
            else:
                c += 1
                if c > o:    c = o = 0
                elif c == o: max_ = max(max_, 2*o)
        
        return max_
```
