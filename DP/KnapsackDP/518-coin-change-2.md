# [518. Coin Change 2](https://leetcode.com/problems/coin-change-2/)

This is a typical knapsack problem with `options` are the types of coins available for picking. 

For a typical knapsack problem, we will need a 2D dp table, with x-axis ranging (0, target) and y-axis ranging from (0, len(options)). 
With this structure, we will figure out the necessary update rule to solve a specific problem.

![Update Rule](https://github.com/trang-nguyenn/Algorithms/blob/master/DP/KnapsackDP/images/Annotation%202019-09-01%20092927.jpg)

The update rule is:

```
if col-coinValue >= 0: 
    dp[i+1][col] = dp[i][col] + dp[i+1][col-coinValue] 
else: 
    dp[i+1][col] = dp[i][col]
```

## Code
```python
class Solution(object):
    def change(self, amount, coins):
        """
        :type amount: int
        :type coins: List[int]
        :rtype: int
        """
        dp = [[1 if i ==0 else 0 for i in range(amount+1)] for _ in range(len(coins)+1)]
        
        for i, c in enumerate(coins):
            for col in range(1, amount+1):
                dp[i+1][col] = dp[i][col] + dp[i+1][col-c] if col >= c else dp[i][col]
        
        return dp[-1][-1]
        
```
