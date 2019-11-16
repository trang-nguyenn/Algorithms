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
