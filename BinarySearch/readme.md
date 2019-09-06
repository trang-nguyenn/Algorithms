# bisect toolbox
Refer to the following link [Bisect](https://www.geeksforgeeks.org/bisect-algorithm-functions-in-python/)

# Seach the answer

When the function is monotonic, we can use binary search to find the answer.   
Plus or minus 1 is dependent on cases and is the difficult part of this search

```python
while left(+1)<right(-1):
  center = (left+right)//2
  if func(center)<val: left = center (+1)
  else: right = center (-1)
```
