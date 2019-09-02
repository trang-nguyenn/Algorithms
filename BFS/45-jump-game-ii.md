# [45-jump-game-ii](https://leetcode.com/problems/jump-game-ii/)

Not too hard, but the fact that we compress the queue with nodes to its `start` to `end` drastically save the computation time.   
   
It is worth mentioning that I have tried multiple ways and I have searched over the solutions in the discussion, only this solution declares variables in the way that I feel smooth and clean. Others, including mine, always need some dummy cases for len(nums)<2 .... In addition, I like the `start` and `end` variables, which makes the logic very clear for me to imagine.

```python
class Solution(object):
    def jump(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        start = end = step = 0
        while end < len(nums)-1:
            start, end = end+1, max([i+nums[i] for i in range(start, end+1)])
            step += 1
        return step
```
