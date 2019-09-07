# [493-reverse-pairs](https://leetcode.com/problems/reverse-pairs/)

Almost TLE but it works

```python
class Solution(object):
    def reversePairs(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        li, ans = [], 0
        for n in nums:
            valid_idx = bisect.bisect(li,2*n)
            ans += len(li)-valid_idx
            
            idx = bisect.bisect(li,n)
            li.insert(idx,n)
            
            # print(li, ans)
        return ans
```
