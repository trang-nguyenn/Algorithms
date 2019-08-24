# [max-sum-of-rectangle-no-larger-than-k](https://leetcode.com/problems/max-sum-of-rectangle-no-larger-than-k/)

The looping technique of this problem is the same as the sum operator for contigous subarray.
**(I made a mistake on `left-1` in the indexing, where I use `left` and take a long time to debug)

```python
class Solution(object):
    def maxSumSubmatrix(self, matrix, k):
        """
        :type matrix: List[List[int]]
        :type k: int
        :rtype: int
        """
        Max = -float('inf')
        nrows, ncols = len(matrix), len(matrix[0])
        if nrows<ncols:
            matrix = [[matrix[r][c] for r in range(nrows)] for c in range(ncols)]
            nrows, ncols = ncols, nrows
            
        for r in range(nrows):
            for c in range(1,ncols):
                matrix[r][c] = matrix[r][c-1] + matrix[r][c]

            
        for left in range(ncols):
            for right in range(left, ncols):
                data, Sum = ..., 0
                for r in range(nrows):
                    Sum += matrix[r][right] - (matrix[r][left-1] if left>0 else 0)
                    
                    data ... Sum # Adding Sum to our data
        return Max
```

Initially, I use `set()` for data and search for all elements in data that is greater than `Sum-k`.   
In fact, while it works, this is data structure is quite inefficient to solve this problem.   

Very interesting in the way we use the `bisect insort` and bisect_left` to search to the new value in the array.

```python
class Solution(object):
    def maxSumSubmatrix(self, matrix, k):
        """
        :type matrix: List[List[int]]
        :type k: int
        :rtype: int
        """
        Max = -float('inf')

                data, Sum = [0], 0
                for r in range(nrows):
                    Sum += matrix[r][right] - (matrix[r][left-1] if left>0 else 0)
                    
                    idx = bisect.bisect_left(data, Sum-k)
                    if idx<len(data):
                        Max = max(Max, Sum-data[idx])
                        if Max == k: return k
                        
                    bisect.insort(data,Sum)
        return Max

```
