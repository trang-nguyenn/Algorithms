# [1223-dice-roll-simulation](https://leetcode.com/problems/dice-roll-simulation/)

Obviously, we can DFS all the cases then adding the count if we have the valid string. Look at the problem, I understand that I need a kind of dp with "growing" number of keys to solve this seemingly NP-Hard problem.     

Initially, I did not see the `consecutive` condition, so I think about the key as a counter that counts all the elements in the list as `dimensionality reduction`. However, I can not find one.    

Then reading the hint of `dp(pos,times)` then I can figure out the solution.    

Probably, the differences between `dp` and `dfs` are:    
(1) the existance of the `dimensionality reduction` factor, here is from a list to the last element + its number of times it `consecutively` appears.     
(2) The `initial dp condition` and `initial dfs condition` is quite similar.   
(3) The `next_stages` rule in dfs is typically to select from a set of number, while the `next_stages` rules in `dp` is normally a mathematical equation. Finding the right `dimensionality reduction` and the right `equations` are the key for DP algorithms.     

Still quite complicated in the `initial dp condition`, and the `next stages dp update rules` with 2 cases: change the last indexes and add the same index.      

```python
class Solution(object):
    def dieSimulator(self, n, rollMax):
        """
        :type n: int
        :type rollMax: List[int]
        :rtype: int
        """
        mod = 10**9+7
        dp = {(dice,1): min(1,rollMax[dice]) for dice in range(6)}
        for k in range(1,n):
            new = collections.defaultdict(int)
            for dice in range(6):
                new[dice,1] = sum(count for (other, times), count in dp.items()
                                 if other != dice)%mod
            for (dice, times), count in dp.items():
                if times<rollMax[dice]:
                    new[dice,times+1] += count%mod
            dp = new
        return sum(dp.values())%mod
```
