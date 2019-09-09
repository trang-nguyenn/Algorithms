# (1187-make-array-strictly-increasing) [https://leetcode.com/problems/make-array-strictly-increasing/]

Several techniques are as follows:
## Naivee Search (TLE)

```python
class Solution(object):
    def makeArrayIncreasing(self, arr1, arr2):
        """
        :type arr1: List[int]
        :type arr2: List[int]
        :rtype: int
        """
        arr2 = sorted(set(arr2))
        queue = [(0, -float('inf'))]
        depth = 0
        while queue and depth<len(arr1):
            
            queue1 = [(count,arr1[depth]) for count,prev in queue if prev<arr1[depth]]
            queue2 = [(count+1, arr2[i2]) for count, prev in queue 
                      for i2 in [bisect.bisect_right(arr2,prev)] if i2<len(arr2)]
            queue = set(queue1+queue2)
            depth +=1
        
        if depth == len(arr1) and queue:
            queue = list(queue)
            queue.sort(key = lambda x: x[0])
            return queue[0][0]
        return -1
```

# Improved Search

```python
class Solution(object):
    def makeArrayIncreasing(self, arr1, arr2):
        """
        :type arr1: List[int]
        :type arr2: List[int]
        :rtype: int
        """
        arr2 = sorted(set(arr2))
        queue = {0: -float('inf')}
        depth = 0
        while queue and depth<len(arr1):
            
            queue1 = {(count,arr1[depth]) for count,prev in queue.items() if prev<arr1[depth]}
            queue2 = {(count+1, arr2[i2]) for count,prev in queue.items() 
                      for i2 in [bisect.bisect_right(arr2,prev)] if i2<len(arr2)}
            
            queue = collections.defaultdict(lambda: float('inf'))
            for count, val in queue1|queue2:
                queue[count] = min(queue[count],val)
            
            depth +=1
        
        if depth == len(arr1) and queue:
            return min(queue.keys())
        return -1
```

Writing in dp form
```python
        bfs = {0: -float('inf')}
        for n1 in arr1:
            now = {}
            for count, prev in bfs.items():
                if prev<n1: 
                    now[count] = min(now.get(count,float('inf')),n1)
                i2 = bisect.bisect_right(arr2,prev)
                if i2<len(arr2):
                    now[count+1] = min(now.get(count+1, float('inf')),arr2[i2])
            bfs = now
        return min(bfs.keys()) if bfs else -1
```

# DFS with visited and decision making
When we evaluate the optimum solution at a given node, we can save the computation time. Calculate from the leaf of the tree first, then gradually move up, making a decistion of what path to go by the `min operator`.

```python
        memo = {}
        def dfs(i1, prev):
            if i1 == len(arr1):  return 0  #Evalute the leaf
            if (i1,prev) not in memo:
                option1 = dfs(i1+1, arr1[i1]) if arr1[i1]>prev else float('inf')
                i2 = bisect.bisect_right(arr2,prev)
                option2 = 1+ dfs(i1+1, arr2[i2]) if i2<len(arr2) else float('inf')
                memo[(i1,prev)] = min(option1, option2)  # visited and decision making
            return memo[(i1,prev)]
        ans = dfs(0, -float('inf'))
        return ans if ans != float('inf') else -1
```
