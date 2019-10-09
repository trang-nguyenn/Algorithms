# [1187-make-array-strictly-increasing](https://leetcode.com/problems/make-array-strictly-increasing/)

First thought: NP Hard as at every new node, we have 2 options: keep going with the current array or choose the new element from the arr2. If we go with this direction (by dfs, backtracking, bfs), time complexity is (2^N).   

To loop over this data structure, we only care about: The 2D dimensions of this data is `count` the number of time we need to change and `val` the last (and obviously largest) value of the modified array.    
     
 To compress this 2D, we notice that we only search for the array with `lowest number of changes`. This implies that we should do `argmax` on the `count` or `val`.
 
 ```python
 class Solution(object):
    def makeArrayIncreasing(self, arr1, arr2):
        """
        :type arr1: List[int]
        :type arr2: List[int]
        :rtype: int
        """
        arr2 = sorted(set(arr2))
        dp = {0:-float('inf')}
        for i, n in enumerate(arr1):
            new = {}
            for count, val in dp.items():
                if val<n: 
                    new[count] = min(n, new.get(count,float('inf')))
                idx = bisect.bisect_right(arr2,val)
                if idx !=  len(arr2):
                    new[count+1] = min(arr2[idx], new.get(count+1,float('inf')))
            dp = new.copy()
        return min(dp.keys()) if dp else -1
 ```
