This is probaly the most interesting data structure among all the basics for coding interview.    
The looping and indexing techniques over this data structure have full of `twist` and `turn`.     

The fundamental is still the `graph_out` (a node to a set of nexts), `graph_in`, (a node to a set of previous).    
`number_out`, `number_in` can be a slight dimensionality reduction for the length of the `graph_out` and `graph_in`.     

Sometimes we see `queue` and `stack` to loop over this graph, and we stop the looping when we are out of elements in the `queue` or `stack`. We are still looking for the next elements from the neighbors in `graph_out` and `graph_in`. But if we want to work out graph problems, there is `something extra` ... What is this `something extra`?

## Queue (or you might think about its duality BFS) and the detecting loop problem

Something extra here is the update rule of the `number_out`. We need to do an extra step of deleting the "visited" connection over our looping before we can add the neighbor to the queue. Check out the code below. 

```python
        queue = [i for i in num_out if num_out[i]==0]
        while queue:
            node = queue.pop(0)
            for prev in incoming[node]:
                num_out[prev] -= 1
                if num_out[prev] == 0: queue.append(prev)
```

Think deeper on this technique? What is bfs here? What are the layers of the bfs? What nodes have the same "bfs depth"?   
The "depth" here is the number of "directed outflows". We need a trick to reveal this data.

## Stack (or you might think about its duality DFS) for Topological Sorting

When we do sorting, we need a "value", such as 2<3, but what can be the "value" here in graph?     
There is always extra flavors in the graph structure, something similar but not quite.    
We are talking about the order of flows. Prev must come before node, and node must come before its nexts.

`"white-gray-black" DFS` should be in the textbook for all the teaching of dfs. 

[source](https://www.geeksforgeeks.org/python-program-for-topological-sorting/)

The things in extra is the "marked" color of the node, which is equivalent to signal that the node is "out of the graph consideration". When we search for this neibourgh, we can assume that we don't see this neibourgh.   
When all the neibourghs of a node is marked "visited", the node is equivalent to have no neibourgh, and we understand that the node is a leaf.

```python 
from collections import defaultdict 

class Graph: 
    def __init__(self,vertices): 
        self.graph = defaultdict(list) #dictionary containing adjacency List 
        self.V = vertices #No. of vertices 
  
    def addEdge(self,u,v): 
        self.graph[u].append(v) 
  
    def dfs(self,v,visited,stack): 
        visited[v] = True
        for i in self.graph[v]: 
            if visited[i] == False: 
                self.dfs(i,visited,stack) 
        stack.insert(0,v) 
  
    def topologicalSort(self): 
        visited = [False]*self.V 
        stack =[] 
        for i in range(self.V): 
            if visited[i] == False:  
                self.dfs(i,visited,stack) 
        return stack
```

```python
        WHITE,BLACK = 0, 1
        color = collections.defaultdict(int)
        stack = []
        def dfs(node):
            if color[node] == WHITE:
                for nei in outcoming[node]:
                    if color[nei] != BLACK:
                        dfs(nei)
                color[node] = BLACK
                stack.append(node)
        
        for node in range(numCourses):
            dfs(node)
        return stack
```
```python
        white, gray, black = 0,1,2
        color = collections.defaultdict(int)
        stack = []
        def dfs(node):
            if color[node] != white:
                return color[node] == black
            
            color[node] = gray
            for nei in outgoing[node]:
                if color[nei]== gray or dfs(nei) == False:
                    return False
            color[node] = black
            stack.append(node)
            return True
        
        for node in vertices:
            if dfs(node) == False: return ""
```

## Critical Connections (stack or queue? search deep or search nearby first?) 

https://leetcode.com/problems/critical-connections-in-a-network/

```python
class Solution(object):
    def criticalConnections(self, n, connections):
        """
        :type n: int
        :type connections: List[List[int]]
        :rtype: List[List[int]]
        """
        graph = {}
        for n1, n2 in connections:
            graph.setdefault(n1,set()).add(n2)
            graph.setdefault(n2,set()).add(n1)    
            
        number, score = [None]*n, [None]*n
        self.count = 0
        
        def dfs(node, root):
            number[node],score[node] = self.count, self.count
            self.count += 1
            
            for nxt in graph[node]:
                if number[nxt] == None:  dfs(nxt, node)
            score[node] = min(score[nxt] for nxt in graph[node]|set([node]) if nxt!=root)
           
        dfs(0, None)
        return [[n1, n2] for n1, n2 in connections if score[n1]>number[n2] or score[n2]>number[n1]]
```

## Print all topological sort

We use `dfs` and reduce `in_degree` together for this printing
```python
out_flow = {a: set() for a in Actions}
indegree = {a: 0 for a in Actions}
for first, second in Sequence:
    out_flow[first].add(second)
    indegree[second] += 1
    
ans = []
def dfs(S):
    if len(S) == 4:
        ans.append(S)
        return
    queue = [a for a in sorted(Actions) if indegree[a]==0 and a not in S]
    for a in queue:
        for nxt in out_flow[a]: indegree[nxt] -= 1
        dfs(S+[a])
        for nxt in out_flow[a]: indegree[nxt] += 1
```

## Graph tranversal with dp 

[Jump Game Problem](https://leetcode.com/problems/jump-game-v/)     
DP relationship between nodes of the graph: `dp[node] = max(dp[node], 1 + max(dp[child] for child in graph[node]))`

```python
        dp = [1]*len(arr)
        visited = set()
        
        def dfs(node):
            visited.add(node)
            for nei in graph[node]:
                if nei not in visited:
                    dfs(nei)
                dp[node] = max(dp[node], 1+dp[nei])
        
        for node in range(len(arr)):  
            if node not in visited:  
                dfs(node)  

        return max(dp)  
```
