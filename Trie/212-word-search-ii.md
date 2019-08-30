# [212-word-search-ii](https://leetcode.com/problems/word-search-ii/)

Trie() problem where we need to build a graph from the given data structure.    
Sound like from the connecting edges, we need to build a dictionary that map from one edges to its nearby nodes.   

For visualization, please visit: [Wiki](https://en.wikipedia.org/wiki/Trie)    

We dont know yet how should we build the Trie(), just we need the function addNode() inside this class
We also want to dfs all the element of the board

```python
class Solution(object):
    def findWords(self, grid, words):
        """
        :type board: List[List[str]]
        :type words: List[str]
        :rtype: List[str]
        """
        data = Trie()
        for word in words:
            data.addNode(word)
            
        ans = []
        nrow, ncol = len(grid), len(grid[0])
        for r in range(nrow):
            for c in range(ncol):
                dfs(r,c)
        return ans
```
