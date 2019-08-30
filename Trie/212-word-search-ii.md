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

Although we have not defined the Trie() and its attribute, we know we need to dfs with this skeleton:

```python
        def dfs(S,x,y, visited):
            if ...
            
            next_search = [(x+dx,y+dy, grid[x+dx,y+dy]) for dx,dy in nxt
                          if 0<=x+dx<nrow and 0<=y+dy<ncol 
                           and (x+dx,y+dy) not in visited]
            
            for x, y, val in next_search:
                if ...:
                    dfs(S+[val], x,y, visited|{(x,y)})
```

We know that when we learn the new value of the box, we move to the new Trie() node, implying that this data is varying with our looping. So we need an additional variable inside the dfs. It also becomes clear on the termination condition and the Trie() class when we throw in this `node` variable.   

```python
        def dfs(S,x,y, visited, node):
            if node.isWord:  ans.append(node.string)
            else:
                next_search = [(x+dx,y+dy, grid[x+dx,y+dy]) for dx,dy in nxt
                              if 0<=x+dx<nrow and 0<=y+dy<ncol 
                               and (x+dx,y+dy) not in visited]

                for x, y, val in next_search:
                    if val in node:
                        dfs(S+[val], x,y, visited|{(x,y)}, node[val])
```
