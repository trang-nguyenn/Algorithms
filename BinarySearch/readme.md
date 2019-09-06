# bisect toolbox
Refer to the following link [Bisect](https://www.geeksforgeeks.org/bisect-algorithm-functions-in-python/)     
Important functions:     
(1) bisect.bisect_left(li, val)     
(2) bisect.bisect_right(li, val)       

```python
li = [1, 3, 4, 4, 4, 6, 7] 
print ("The leftmost index to insert, so list remains sorted is  : ", end="") 
print (bisect.bisect_left(li, 4)) 
The leftmost index to insert, so list remains sorted is  : 2


print ("The rightmost index to insert, so list remains sorted is  : ", end="") 
print (bisect.bisect_right(li, 4)) 
The rightmost index to insert, so list remains sorted is  : 4
```

(3) bisect.insort(li, val)    
(4) bisect.insort_left(li, val)    
(4) bisect.insort_right(li, val)    

```python
The list after inserting new element using insort() is : 
1 3 4 4 4 5 6 
The list after inserting new element using insort_left() is : 
1 3 4 4 4 5 6 
The list after inserting new element using insort_right() is : 
1 3 4 4 5 4 6 
```

# Seach the answer

When the function is monotonic, we can use binary search to find the answer.   
Plus or minus 1 is dependent on cases and is the difficult part of this search

```python
while left(+1)<right(-1):
  center = (left+right)//2
  if func(center)<val: left = center (+1)
  else: right = center (-1)
```
