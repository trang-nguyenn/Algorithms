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

We know that when we move to a new location of the box, we move to a new Trie() node, `implying that this data (location of the Trie() node) is varying with our looping`. Since no other variable in the dfs loop can represent this location, we need `an additional variable` inside the dfs loop. It also becomes clearer on the termination condition and how to construct the Trie() attributes when we throw in this `node` variable.   

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

Ok, well, I made several mistakes:    
(1) I need to start the dfs with the value of the grid at that location, and the starting node is root.child\[val] rather than node.    
     
(2) I made this mistake twice. Even if I see the Trie() that has a word, I should continue the loop. After the initialial `if`, I should  keep going with no `else`   
   
(3) Please make myself clearer on the code for Trie() data. Well, need to think of a better Trie() node for cleaner looping...      
     
     
### What is Trie()

(1) A graph, where we can move from one node to other nodes with some keys. It must have a dictionary inside.    
     
(2) Trie is the root of the graph, we no need to have any attribute to this root. This root only needs trie.child to point to the next Nodes of interest. We can store any attribute to the Node() by creating a new class... Some elevation of mindset here... I think about dp with various variables rather than a new class... Well, need to learn more on how ppl program Trie()...      

```python
class Node:
    def __init__(self, isWord = False, string = None):
        self.child = {}
        self.isWord, self.string = isWord, string
    
class Trie:
    def __init__(self):
        self.child = {}
```
   
**The data structure for Trie() - root and Node() - children complete here with the right dimensions of atributes. Next is to really store the data to this structure.**       
   
(3) We know that we have to build the function trie.addNode(word) to input a new word to this data structure.    
     
`When a new word come in, should we create new Node() for the graph? Should we change the attribute of certain nodes? Generally, the looping over this graph to store new word is similar to DFS (Sound like a YES for me)?`   
   
The addition of this new data can be creative... See palindrome pairs examples... See how we should balance out the programming on different paths to produce a good code.     

```python
    def addNode(self,word):
        # How can we store the data of this word? Equals to 2 questions?
        # Word len() == N must visited N nodes
        # Where should we create a new node? - Fixed strategy of moving along word
        # Word is a list of char, each char is the key of the edges in this graph
        
        # fixed flows:
        node = self
        for s in word:
            if s not in node.child: node.child[s] = Trie()
            node = node.child[s]
            # Update atribute if needed
        # Update attribut if needed

        # Where should we update the attributes of a given node?
```

Again, all these codes is to support the main Trie() code:

```python
        data = Trie()
        for word in words:
            data.addNode(word)
```
