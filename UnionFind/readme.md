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
