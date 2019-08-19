# [45. Jump Game II](https://leetcode.com/problems/jump-game-ii/)

Priority Queue technique for this problem is a little bit overkill and not that efficient, but let's use it just for demo of technique:

Strategy: 
- Each time you reach and index, append all other smaller index and its max reach to the queue.
- Pop out the element with the maximum max reach and check whether it is >= last index

Priority Queue: store (max reach, index) of all elements that is reacheable from the initial position.

## Code
```
class Solution(object):
    def jump(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        if len(nums) == 1: return 0
        
        N, count, Max = len(nums), 0, 0
        pq = [(-nums[0], 0)] # -Max_index to reach from prev index
        nums = [(i, val) for i, val in enumerate(nums)][1:]
        
        while pq:
            count += 1
            temp, idx = heapq.heappop(pq)
            Max = max(-temp, Max) 
            if Max >= N-1:
                return count
            
            while nums and Max >= nums[0][0]:
                    i, val = nums.pop(0)
                    heapq.heappush(pq, (-(i+val), i))
        
```

## Note: 
There is a more optimal way to solve this problem based on [Jump Game I](https://leetcode.com/problems/jump-game/):

```
# Jump Game I
```
def canJump(nums):
  """
  :type nums: List[int]
  :rtype: bool
  """
      Max = 0
      for i, val in enumerate(nums):
          if i < Max: return False
          Max = max(i+val, Max)
      return Max >= len(nums)-1
```
```
# Jump Game II:
def jump(nums):
        last, curr, count = 0, 0, 0
        for i, val in enumerate(nums):
            if i < last: return -1
            elif i> last:
                last = curr
                count += 1
            curr = max(curr, i+val)
        return count
```

