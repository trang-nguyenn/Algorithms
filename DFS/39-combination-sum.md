# [39-combination-sum](https://leetcode.com/problems/combination-sum)

This is a typical DFS problem. Combination Sum and its variations demonstrates how the concept and code can be flexibly used and mofified to solve different problems.


```python
def dfs(var1, var2): # var1, var2 are variables to carry information needed to do the next dfs recursion
    if .... [some conditions]:
        ans.append(var1)
    else:
    next_moves = [...]
    for i, num in enumerate(next_moves):
        dfs(var1 + num, var2 + i) # modified var1,var2 for next search
```

## Code
```python
class Solution(object):
    def combinationSum(self, candidates, target):
        """
        :type candidates: List[int]
        :type target: int
        :rtype: List[List[int]]
        """
        candidates = sorted(candidates)
        if len(candidates) == 0: return [[]]
        ans = []
        
        def dfs(remain, temp, start = 0):
            if remain == 0:
                ans.append(temp)
            for i, num in enumerate(candidates[start:]):
                if num > remain: break
                dfs(remain-num, temp+[num], start + i)
        dfs(target, [])
        return ans
        

```
    
