# [minimum-moves-to-move-a-box-to-their-target-location](https://leetcode.com/problems/minimum-moves-to-move-a-box-to-their-target-location/)

Simple thinking is to use bfs to search for both player to nearby box, and search from box to the target.

```python
To be written
```

## A-star
A-star search solution - quite a smart way to search over the problem.
Heuristic (an under-estimate of the remaining moves required) is the Manhattan distance between box and target.
A state consist of box and person locations together.     

Repeatedly pop the state with the lowest heuristic + previous moves off the heap.     
Attempt to move the person in all 4 directions.    
If any direction moves the person to the box, check if the box can move to the nex position in the grid.     


https://leetcode.com/problems/minimum-moves-to-move-a-box-to-their-target-location/discuss/431061/A-star-search
