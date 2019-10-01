# [1199-minimum-time-to-build-blocks](https://leetcode.com/problems/minimum-time-to-build-blocks/)

Both tree and priority queue data structure inside a problem. Tree is because we need to split out the data from a fixed node, and priority queue as we have optimum solution to build the tree.

```python
class Solution(object):
    def minBuildTime(self, blocks, split):
        """
        :type blocks: List[int]
        :type split: int
        :rtype: int
        """
        blocks.sort(key = lambda x: -x)
        tree = []
        for i,val in enumerate(blocks):
            if tree:
                cost, count = heapq.heappop(tree)
                heapq.heappush(tree,(cost+split, count+1))
            else:
                count = -1
            heapq.heappush(tree, (val+split*(count+1),count+1))
            # print(val,tree)
        return max(val for val,count in tree)

```
