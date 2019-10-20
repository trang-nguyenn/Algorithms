![Image](https://github.com/trang-nguyenn/Algorithms/blob/master/SlidingWindow/SlidingWindow.png)

# Skeleton

Data is the input data structure.    
WindowData is the structure we use to check if the window is still valid.    

To check the maximum valid window:
```python
left = 0
for right in range(len(data)):
    WindowData.__add__(data[right])
    if WindowData.__valid__() == False:
        WindowData.__remove__(data[left])
        left += 1
return right-left+1
```

If we want to remember what is the correct window at all points, e.g, dp\[], then we need to change `if` to `while`:

```python

left = 0
for right in range(len(data)):
    WindowData.__add__(data[right])
    while WindowData.__valid__() == False:  # change if to while
        WindowData.__remove__(data[left])
        left += 1
    dp[right] = func(left,right)  # remember all the updates
return max(dp)  # return what we need to return
```

# [1004](https://leetcode.com/problems/max-consecutive-ones-iii/)
```
WindowData: count number of 0 inside the windown
WindowData.__add__()     : +1 if data[right] == 0 else 0
WindowData.__remove__()  : -1 if data[left] == 0 else 0
WindowData.__valid__()   : count<=K 
```

# [424](https://leetcode.com/problems/longest-repeating-character-replacement/submissions/)

```
WindowData: Counter()
WindowData.__add__()     : data[right] += 1
WindowData.__remove__()  : data[left]  -= 1
WindowData.__valid__()   : quite complex function here = right-left+1 - max(Counter().values)
```
