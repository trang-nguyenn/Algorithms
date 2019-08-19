# [Target Sum](https://leetcode.com/problems/target-sum/)

Interesting `knapsack`.
When we throw in a new data, we have several directions to process this new information. The dp must be able to correctly update the value in all directions. It also implies that we need the same amount of variables as the number of directions to loop over the raw input data.

The skeleton for knapsack looping is as follows:

```python
        dp = defaultdict(int)  # key:val
        for n in nums:
            temp_dp = defaultdict(int)
            for key, val in dp.items():
                temp_dp[... n1...] = ...
                temp_dp[... n2...] = ...
            dp = temp_dp
        return dp[xx]
```

The solution for the problem is as:

```python
from collections import defaultdict
class Solution(object):
    def findTargetSumWays(self, nums, S):
        """
        :type nums: List[int]
        :type S: int
        :rtype: int
        """
        dp = defaultdict(int)  # Sum: count number of Sum
        dp[0] = 0
        for n in nums:
            temp_dp = defaultdict(int)
            for Sum, count in dp.items():
                temp_dp[Sum+n] += count if count != 0 else 1
                temp_dp[Sum-n] += count if count != 0 else 1
            dp = temp_dp
            #print(dp)
        return dp[S]
```

## Comments

`knapsack` gives us a sense that we have a 2D table looping, one dimension is the 1D input data, and other dimension is the possible knapsack options (here is -1, 1). We can loop horizonally first (all data first) or we can loop vertically (all knapsack option first, then gradually throw in data). In this example, we loop vertically.
(but why?) (does it work if we choose to loop horizonally?)
