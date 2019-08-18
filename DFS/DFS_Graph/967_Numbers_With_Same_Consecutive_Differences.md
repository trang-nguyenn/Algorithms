[967. Numbers With Same Consecutive Differences](https://leetcode.com/problems/numbers-with-same-consecutive-differences/)

Similar to the search of permutation, we can use `DFS` or `Set Interation`

## DFS

```python
class Solution(object):
    def numsSameConsecDiff(self, N, K):
        """
        :type N: int
        :type K: int
        :rtype: List[int]
        """
        if N == 1: return list(range(0,10))
        self.ans = []
        def dfs(S):
            if len(S) == N: self.ans.append(int(S))
            else:
                if not S: next_search = range(1,10)
                else    : next_search = [n for n in set([int(S[-1])-K,int(S[-1])+K]) if -1<n<10]
                for n in next_search:
                    dfs(S+str(n))
        dfs('')
        return self.ans
```

## Set Iterative
[Reference](https://leetcode.com/problems/numbers-with-same-consecutive-differences/discuss/211183/JavaC%2B%2BPython-Iterative-Solution)

```python
    def numsSameConsecDiff(self, N, K):
        cur = range(10)
        for i in range(N - 1):
            cur = {x * 10 + y for x in cur for y in [x % 10 + K, x % 10 - K] if x and 0 <= y < 10}
        return list(cur)
```
