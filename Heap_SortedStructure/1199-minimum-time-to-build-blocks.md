# [1199-minimum-time-to-build-blocks](https://leetcode.com/problems/minimum-time-to-build-blocks/)
   
 Initially, I think about recursive, where we can reduce the dimension (list) into (2 smaller lists) and solve the problem by 2D dp, where the data is (start,end). The problems is the rules to update dp, I need another loop to scan over all possible seperations, which is ways too long (O(N^2)*O(N)=O(N^3)). 
      
 It turns out that this is a tree problem, where we grow the (binary) tree such that eventually all elements in the list are leaves. When we add in new input, we choose a branch to seperate, both add the new data and amend the cost of previous leaf. The data structure to carry on to the next element is `Heap`.
 
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
