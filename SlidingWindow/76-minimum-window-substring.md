# [76-minimum-window-substring](https://leetcode.com/problems/minimum-window-substring/)

My solution with the same idea but the implementation is quite long

```python
class Solution(object):
    def minWindow(self, s, t):
        """
        :type s: str
        :type t: str
        :rtype: str
        """
        from collections import Counter
        left, length = 0, float('inf')
        ref, cur = Counter(t), Counter()
        print(ref, cur)
        
        for right,char in enumerate(s):
            if char in ref:  cur[char] += 1
            while all(cur[c]>=ref[c] for c in ref):
                if right-left<length:
                    length = right-left
                    ans = s[left:right+1]
                if s[left] in ref: cur[s[left]] -= 1
                left += 1
            # print(left,right,cur)
        return ans if length != float('inf') else ''
```

Shorter time but with the same idea
```python
def minWindow(self, s, t):
    need, missing = collections.Counter(t), len(t)
    i = I = J = 0
    for j, c in enumerate(s, 1):
        missing -= need[c] > 0
        need[c] -= 1
        if not missing:
            while i < j and need[s[i]] < 0:
                need[s[i]] += 1
                i += 1
            if not J or j - i <= J - I:
                I, J = i, j
    return s[I:J]
```
