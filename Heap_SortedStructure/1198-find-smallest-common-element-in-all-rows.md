# [1198-find-smallest-common-element-in-all-rows](https://leetcode.com/problems/find-smallest-common-element-in-all-rows/)

```python
class Solution(object):
    def smallestCommonElement(self, mat):
        """
        :type mat: List[List[int]]
        :rtype: int
        """
        for row in mat:
            row.append(float('inf'))
        
        data = sorted((mat[r][0],r,0) for r in range(len(mat)))
        
        while data[0][0] != data[-1][0]:
            _, r, c = data[0]
            data = data[1:]
            bisect.insort(data,(mat[r][c+1],r,c+1))
            
        return -1 if data[0][0] == float('inf') else data[0][0]
```
