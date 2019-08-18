[number-of-squareful-arrays](https://leetcode.com/problems/number-of-squareful-arrays/)

Interesting example of dfs over a graph.   
(1) I need to build the graph by myself to connect from a number to other numbers if their sum is a square
(2) DFS over the graph for non-overlap permutation that one element is "square" connected to its next.

## My code 
(It is long and it doesnot look nice but it works (>60%))

```python
class Solution(object):
    def numSquarefulPerms(self, A):
        """
        :type A: List[int]
        :rtype: int
        """
        from collections import defaultdict, Counter
        counter, data, N = Counter(A), set(A), len(A)
        graph = defaultdict(set)
        for a1 in counter:
            for a2 in counter:
                if int((a1+a2)**0.5)**2 == a1+a2:
                    if a1!=a2 or (a1 == a2 and counter[a1]>1):
                        graph[a1].add(a2); graph[a2].add(a1)
        self.count = 0
        def dfs(S):
            if len(S) == N: self.count += 1
            else:
                if len(S) == 0: next_search = data
                else:  next_search = {n for n in graph[S[-1]] if S.count(n)<counter[n]}
                for n in next_search:
                    dfs(S+[n])
        dfs([])
        return self.count
```

Btw, I like that fact that I started to use `defaultdict` and `Counter`


