Certain problem has the property:    
```
func(s[left:right]) = prefix(s[right+1]) - prefix(s[left])
```
In this case, we can drastically reduce the computation time from $O(n^2)$ to O(n).   
I find awe on the creativity of people to think about different data structure to generate this prefix/suffix data.


## 1D cumSum for a list of numbers `nums`

```python
n = len(nums)
cumSum = [0] * (n+1)
for i in range(n):
      cumSum[i+1] = cumSum[i] + li[i]
```

## 2D cumSum for a grid of numbers `grid`

```python
nrow, ncol = len(grid), len(grid[0])
cumSum = [[0 for _ in range(ncol+1)] for _ in range(nrow+1)]

for r in range(nrow):
    for c in range(ncol):
        cumSum[r+1][c+1] = cumSum[r][c+1] + cumSum[r+1][c] - cumSum[r][c] + grid[r][c]


```
