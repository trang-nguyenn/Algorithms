[630. Course Schedule III](https://leetcode.com/problems/course-schedule-iii/)

Similar to other priority queue problems, we need to know the optimum strategy of this problem before implementing the code.

The optimal strategy here is to choose all courses (#1)(sorted by their end time) provided that the time taken to finish such courses within end time (#2).
Constraints: (1) total time cannnot exceed the end time (need while loop to search)   
Optimal policy: always pop the courses with longest duration. $\Rightarrow$ use heap to store the duration

The priority queue will store the time to finish all courses that we are able to take. 


```python
courses.sort(key = lambda x: x[1])
total_time = 0
pq = []

for time, end in courses: #1
    total_time += time
    heapq.heappush(pq, -time)
    while 

