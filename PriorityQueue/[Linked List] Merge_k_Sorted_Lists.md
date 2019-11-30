# [merge-k-sorted-lists](https://leetcode.com/problems/merge-k-sorted-lists/)

Several things:
+ create a dummy and a curr, then flow the curr with the queue, and return dummy.next seems like the very good technique to return linked list
+ Priority Queue is a very common technique to work with the N-lists over a certain direction of optimiztion

```python
    dummy = ListNode(None)
    curr = dummy
    for _ in []:
      curr.next= node
      curr = curr.next
```

## Heapq toolbox
```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

class Solution(object):
    def mergeKLists(self, lists):
        """
        :type lists: List[ListNode]
        :rtype: ListNode
        """
        queue = [(node.val, node) for node in lists if node]
        heapq.heapify(queue)
        dummy = ListNode(None)
        curr = dummy
        while queue:
            _, node = heapq.heappop(queue)
            curr.next = node
            curr = node
            if node.next:
                heapq.heappush(queue, (node.next.val, node.next))
        return dummy.next
```

## Priority Queue toolbox
Credit: https://leetcode.com/problems/merge-k-sorted-lists/discuss/10511/10-line-python-solution-with-priority-queue
```python
from Queue import PriorityQueue
class Solution(object):
    def mergeKLists(self, lists):
        dummy = ListNode(None)
        curr = dummy
        q = PriorityQueue()
        for node in lists:
            if node: q.put((node.val,node))
        while q.qsize()>0:
            curr.next = q.get()[1]
            curr=curr.next
            if curr.next: q.put((curr.next.val, curr.next))
        return dummy.next
```
