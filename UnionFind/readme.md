Very easy code to remember:
https://leetcode.com/problems/redundant-connection/discuss/108002/Unicode-Find-(5-short-lines)

Union-Find is like traversal over a tree.     

Need a center data structure to store the parent of a given node.
(updating this is our main purpose of runing the union-find code)
+ Normal: a dictionary: parent = {node:node for node in all_nodes}
+ Slightly more advanced: a list: index-node, list\[index\] = parent: `li = [i for i in range(all_nodes)]`

At the end of this union-find, we want to know the parents of all nodes.    
Main function:
+ find_root: like recursive


```python
parent = [i for i in range(N)]
        
        def find(i):
            path = set([i])
            while parent[i] != i:
                i = parent[i]; path.add(i)
            for node in path: parent[node] = i
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
