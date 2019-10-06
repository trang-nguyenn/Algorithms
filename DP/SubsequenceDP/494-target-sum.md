# [494-target-sum](https://leetcode.com/problems/target-sum/)

```python
class Solution(object):
    def findTargetSumWays(self, nums, S):
        """
        :type nums: List[int]
        :type S: int
        :rtype: int
        """
        from collections import defaultdict
        dp = defaultdict(int)
        dp[0] = 1
        for n in nums:
            new = defaultdict(int)
            for s in dp:
                new[s+n] += dp[s]
                new[s-n] += dp[s]
            dp = new
        return dp[S]
```
