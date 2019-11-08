# [802-find-eventual-safe-states](https://leetcode.com/problems/find-eventual-safe-states/)


When we check a node, we first mark it as 1 in our check array. 1 indicates that it's a potentially unsafe node. Once we detect a cycle (if a node is already marked as 1 in our check array which means it's met twice in one single DFS), we leave all nodes in DFS path as 1 since they are all linked to a cycle and return False.

But if DFS finished and no cycle detected, then this node is safe and we marked it as 2, indicating it's clean. Later when we DFS on other nodes and meet a chide node marked with 2, we just pass checking that child node since we have already verified it.

```python
def eventualSafeNodes(graph):
	check = collections.Counter()
	def dfs(node):
		if check[node]: return check[node] == 2
		check[node] = 1
		for nei in graph[node]:
			if check[nei] == 1 or (not check[nei] and not dfs(nei)): return False
		check[node] = 2
		return True
	return list(filter(dfs, range(len(graph))))
```

```python
class Solution(object):
    def eventualSafeNodes(self, graph):
        WHITE, GRAY, BLACK = 0, 1, 2
        color = collections.defaultdict(int)

        def dfs(node):
            if color[node] != white:
                return color[node] == BLACK

            color[node] = GRAY
            for nei in graph[node]:
                if color[nei] == BLACK:
                    continue
                if color[nei] == GRAY or not dfs(nei):
                    return False
            color[node] = BLACK
            return True

        return filter(dfs, range(len(graph)))
```
