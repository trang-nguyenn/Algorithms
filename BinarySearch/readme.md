![image1](https://github.com/trang-nguyenn/Algorithms/blob/master/BinarySearch/BinarySearch.png)

# Official bisect documents

https://github.com/python/cpython/blob/master/Lib/bisect.py#L15

## Bisect_left

```python
def bisect_left(a, x, lo=0, hi=None):
    while lo < hi:
        mid = (lo+hi)//2
        if a[mid] < x: lo = mid+1
        else: hi = mid
    return lo
```

## Bisect_right

```python
def bisect_right(a, x, lo=0, hi=None):
    while lo < hi:
        mid = (lo+hi)//2
        if x < a[mid]: hi = mid
        else: lo = mid+1
    return lo
```

Not too sure if this is better
```python
while l <= r:
    k = (l + r) / 2
    cur_sum = func(k)
    if cur_sum <= threshold:
        max_square = max(max_square, k)
        l = k + 1
    else:
        r = k - 1
```

# Seach the answer

When the function is monotonic, we can use binary search to find the answer.   
Plus or minus 1 is dependent on cases and is the difficult part of this search

```python
# When mid does NOT have +1 then low side needs +1 to balance out the options
lo,hi = 0,N
while lo<hi:
    mid = (lo+hi)//2
    if isBalance(mid): hi = mid
    else:              lo = mid+1
return lo
```

```python
# When mid does have +1 then high side needs -1 to balance out the options
lo,hi = 0,N
while lo<hi:
    mid = (lo+hi+1)//2
    if isBalance(mid): lo = mid
    else:              hi = mid-1
return lo
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

# Bisect over 2D

If we want to binary search over a square, one of the good trick is we can choose the larger dimension (X or Y) to do our binary search.
