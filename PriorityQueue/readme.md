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
        q = PriorityQueue()
        for node in lists:
            if node: q.put((node.val,node))
        while q.qsize()>0:
            curr.next = q.get()[1]
            curr=curr.next
            if curr.next: q.put((curr.next.val, curr.next))
```
