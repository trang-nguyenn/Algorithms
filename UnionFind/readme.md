Very easy code to remember:
https://leetcode.com/problems/redundant-connection/discuss/108002/Unicode-Find-(5-short-lines)


```python
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

```


```python
class UnionFind:
    def __init__(self):
        self.A={}
    
    def find(self,a):
        if a not in self.A: self.A[a]=a
        while self.A[a] != a:
            u=self.A[self.A[a]]
            self.A[a]=u
            a=u
        return a
    
    def merge(self,a,b):
        a=self.find(a)
        b=self.find(b)
        self.A[b] = self.A[a]
```

Union-Find with graph approach:
Intuition: Iterate through each element of the graph to find the group of connected slements (union)


```python
def UnionFind(graph)
'''
input: a graph of type dictionary
output: a dictionary of key:val = node: itsGroup
'''


    visited = set()
    union = {}
    for e in graph:
        if e not in visited:
            # find group
            group = set()
            stack = [e]

            while stack:
                node = stack.pop()
                visited.add(node)    
                group.add(node)
                stack += [new for new in graph[node] if new not in visited]
            for node in group:
                union[node] = union
    return union     
            
```
