# [46-permutations](https://leetcode.com/problems/permutations/)

Classic problem of permutations. With distinct number in nums:

```python
class Solution(object):
    def permute(self, nums):
        """
        :type nums: List[int]
        :rtype: List[List[int]]
        """
        n = len(nums)
        ans = []
        def dfs(li):
            if len(li) == n:
                ans.append(li)
            
            nxt = set(nums) - set(li)
            for num in nxt:
                dfs(li+[num])
        dfs([])
        return ans
        
```

Alternatively, using `itertools.permutations`

```python
class Solution(object):
    def permute(self, nums):
        from itertools import permutations
        return permutations(nums, len(nums))
```
