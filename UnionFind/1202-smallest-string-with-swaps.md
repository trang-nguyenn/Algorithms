# [1202-smallest-string-with-swaps](https://leetcode.com/problems/smallest-string-with-swaps/)

Tricky union find implementation, as if we did not update the parent of the node right after we find_root, it will be TLE as it takes lots of time to recompute again.

```python
class Solution(object):
    def smallestStringWithSwaps(self, s, pairs):
        """
        :type s: str
        :type pairs: List[List[int]]
        :rtype: str
        """
        N = len(s)
        parent = [i for i in range(N)]
        
        def find(i):
            memo = set([i])
            while parent[i] != i:
                i = parent[i]; memo.add(i)
            for node in memo: parent[node] = i
            return i
        
        def union(i1,i2):
            parent[find(i1)] = find(i2)
        
        for i1,i2 in pairs:
            union(i1,i2)
        
        # print(parent)
        data = collections.defaultdict(list)
        for i,val in enumerate(parent):
            data[find(val)].append(i)
            
        ans = list(s)
        for indexes in data.values():
            indexes.sort()
            string = sorted(s[i] for i in indexes)
            for i,c in zip(indexes,string):
                ans[i] = c
        return ''.join(ans)
```

Anyway, I think dfs/bfs to find the union is still the cleanest technique

```python
        graph = collections.defaultdict(set)
        for i1,i2 in pairs:
            graph[i1].add(i2); graph[i2].add(i1)
        
        ans = list(s)
        visited = set()
        for i1 in range(len(s)):
            if i1 not in visited:
                index, queue = set([i1]), set([i1])
                while queue:
                    queue = {nxt for idx in queue
                           for nxt in graph[idx] if nxt not in index}
                    index |= queue
                visited |= index
                index = sorted(index)
                string = sorted(s[i] for i in index)
                for i,c in zip(index, string):
                    ans[i] = c
        return ''.join(ans) 
```
