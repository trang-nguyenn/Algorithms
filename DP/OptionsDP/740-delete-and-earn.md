# [740-delete-and-earn](https://leetcode.com/problems/delete-and-earn/)

I was initially confused when I first this problem, however, it was similar to [House Robber II](https://leetcode.com/problems/house-robber-ii/), for which at every number, one need to decide whether to delete or not to delete this number.

Follow the same strategy, where the update rule is `dp[i+2] = max(dp[i]+ val, dp[i+1]), we can solve this problem.`


## Code

```python
class Solution(object):
    def deleteAndEarn(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        if not nums: return 0
        
        counter = {num:0 for num in range(max(nums))}
        for num in nums:
            counter[num] = counter.get(num,0) +1
        numVal = [key* val for key, val in counter.items()]
        
        dp = [0]* (len(numVal)+2)
        for i in range(len(numVal)):
            dp[i+2] = max(dp[i] + numVal[i], dp[i+1])
        
        return dp[-1]
        
```
