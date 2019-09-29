# Official bisect documents

https://github.com/python/cpython/blob/master/Lib/bisect.py#L15

# Seach the answer

When the function is monotonic, we can use binary search to find the answer.   
Plus or minus 1 is dependent on cases and is the difficult part of this search

```python
while left(+1)<right(-1):
    center = (left+right)//2
    if func(center)<val: left = center (+1)
    else: right = center (-1)
return left?right?
```


# bisect toolbox

A direct application of the binary search is bisect toolbox inside a list.

```python
left, right = 0, len(li)
```

The code for bisect.bisect_left(li, val)

```python
def bisect_left(li, val):
    left, right = 0, len(li)
    while left<right:
      center = (left+right)//2
      if li[center]>val:
      else
    return left,right?
```

The code for bisect.bisect_right(li, val)

```python
def bisect_left(li, val):
    left, right = 0, len(li)
    while left<right:
      center = (left+right)//2
      if li[center]>val:
      else
    return left,right?
```

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

# Problems that need Binary Search

The problems with `increasing` or `decreasing` properties are typically related to binary search.
If we need to find the index with certain values in a monotonic array, then binary search is a good candidate.

