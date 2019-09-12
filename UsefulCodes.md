## Check if the list is increasingly monotonic

```python
return any(A[i] > A[i + 1] for i in range(len(A)-1))
```

Example: [955](https://leetcode.com/problems/delete-columns-to-make-sorted-ii/submissions/)

```python
    def minDeletionSize(self, A):
        ans = 0
        unsorted = {i for i in range(len(A)-1)}
        for col in zip(*A):
            if any(col[i]>col[i+1] for i in unsorted): ans += 1
            else: unsorted = {i for i in unsorted if col[i]>=col[i+1]}
        return ans
```

