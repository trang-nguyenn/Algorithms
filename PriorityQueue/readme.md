# Priority Queue

Center around the concept of heap, where we always need to keep track of the smallest or largest element of a queue.     
Very famous applications include the Uniform Cost Search and Heuristic Search (A-star).     

## Python Modules

### heap
```python
    heapq.heapify(queue)
    heapq.heappop(li)
    val = heapq.heapppush(li, new_element)
    queue[0] # Smallest element
```

### Priority Queue
```python
from Queue import PriorityQueue
        q = PriorityQueue()
        for node in lists:
            if node: q.put((node.val,node))
        while q.qsize()>0:
            curr.next = q.get()[1]
            curr=curr.next
            if curr.next: q.put((curr.next.val, curr.next))
```

# Applications
 + Priority Queue is a very common technique to work with the `N-lists` over a certain direction of optimiztion
 + Priority Queue is a very common technique to work with the `search` where we can `quatify the cost` and use the Pri-Queue to select the next steps with lowest cost.
