# [max-sum-of-rectangle-no-larger-than-k](https://leetcode.com/problems/max-sum-of-rectangle-no-larger-than-k/)

The looping technique of this problem is the same as the sum operator for contigous subarray.   
**(I made a mistake on `left-1` in the indexing, where I use `left` and take a long time to debug)**

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

# Interesting Code with `kadane`


```python
class Solution(object):
    def maxSumSubmatrix(self, matrix, k):
        """
        :type matrix: List[List[int]]
        :type k: int
        :rtype: int
        """
        # O(MlogM) method is called only when quick check is passed,
        # which should only be used when max sum > k and try to use ceiling to find a sum <= k
        def bstSearch(sum_list, k):
            currSum = 0
            bst = BST()
            bst.insert(0)
            for sum in sum_list:
                currSum += sum
                prevSum = bst.ceiling(currSum - k)
                self.maxSum = max(self.maxSum, currSum - prevSum)
                bst.insert(currSum)

        # O(M) method is called for quick check the max sum of any sub arrays
        def kadane(sum_list, k):
            maxSum = -(1<<31)
            currSum = 0
            for sum in sum_list:
                currSum = max(sum, sum + currSum)
                maxSum = max(maxSum, currSum)
            if maxSum <= k:
                self.maxSum = max(self.maxSum, maxSum)
                return False
            else:
                return True

        M = len(matrix)
        if M == 0: return 0
        N = len(matrix[0])
        if N == 0: return 0

        self.maxSum = -(1<<31)
        for left in range(N):
            sum_list = [0]*M
            for right in range(left, N):
                for i in range(M):
                    sum_list[i] += matrix[i][right]

                # O(M) method kadane is called for quick check
                # False means the max sum in any sub array <= k, so unnecessary to do bstSearch,
                # which should only be used when max sum > k and try to use ceiling to find a sum <= k
                if kadane(sum_list, k):
                    bstSearch(sum_list, k)

                # early temination condition
                if self.maxSum == k:
                    return k

        return self.maxSum
    
class BST:
    def __init__(self):
        self.root = {}
    
    def insert(self, value):
        if self.root:
            self._insert(self.root, value)
        else:
            self.root = {"value": value}
            
    def _insert(self, cur_node, value):
        if value < cur_node["value"]:
            if "left" in cur_node:
                self._insert(cur_node["left"], value)
            else:
                cur_node["left"] = {"value": value}
        else:
            if "right" in cur_node:
                self._insert(cur_node["right"], value)
            else:
                cur_node["right"] = {"value": value}
                
    def ceiling(self, value):
        cur_node = self.root
        result = 1 << 31
        while cur_node:
            if cur_node["value"] < value:
                cur_node = cur_node.get("right", None)
            else:
                result = min(result, cur_node["value"])
                cur_node = cur_node.get("left", None)
        return result

```
