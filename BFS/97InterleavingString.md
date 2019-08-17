[97 Interleaving String](https://leetcode.com/problems/interleaving-string/)

Hard problem in LeetCode typically can be looped by either BFS/DFS or DP.
We can use BFS/DFS to search if the solution exists.
With DP we vectorize (vectorize here is pretty simple) and update the states when throwing in additional elements.

BFS/DFS use the operator to find the next valid elements, while DP use the operator to find the relationship of the previous to the new for the search (???)

## My DP solution

```python
class Solution(object):
    def isInterleave(self, s1, s2, s3):
        """
        :type s1: str
        :type s2: str
        :type s3: str
        :rtype: bool
        """
        if len(s1) + len(s2) != len(s3): return False        
        memo={}
        def isValid(i1,i2):
            if i1+i2==len(s3): memo[(i1,i2)] = True
            if (i1, i2) not in memo:
                c = s3[i1+i2]
                if   i1 == len(s1): memo[(i1,i2)] = s2[i2:] == s3[i1+i2:]
                elif i2 == len(s2): memo[(i1,i2)] = s1[i1:] == s3[i1+i2:]
                elif s1[i1] == c and s2[i2] != c: memo[(i1,i2)] = isValid(i1+1, i2)
                elif s1[i1] != c and s2[i2] == c: memo[(i1,i2)] = isValid(i1, i2+1)
                elif s1[i1] != c and s2[i2] != c: memo[(i1,i2)] = False
                else:        memo[(i1,i2)] = isValid(i1, i2+1) or isValid(i1+1, i2)
            return memo[(i1,i2)]
        return isValid(0,0)
```

## BFS Solution

```python
class Solution(object):
    def isInterleave(self, s1, s2, s3):
        """
        :type s1: str
        :type s2: str
        :type s3: str
        :rtype: bool
        """
        r, c, l= len(s1), len(s2), len(s3)
        if r+c != l:
            return False
        queue, visited = [(0, 0)], set((0, 0))
        while queue:
            x, y = queue.pop(0)
            if x+y == l:
                return True
            if x+1 <= r and s1[x] == s3[x+y] and (x+1, y) not in visited:
                queue.append((x+1, y)); visited.add((x+1, y))
            if y+1 <= c and s2[y] == s3[x+y] and (x, y+1) not in visited:
                queue.append((x, y+1)); visited.add((x, y+1))
        return False

```
