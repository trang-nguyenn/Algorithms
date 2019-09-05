Three Components of Trie() data structure:

The Trie() construction is pretty standard - the same attributes for nodes and the same looping techniques for addNode():   

**Node attribute**
```python
class Node:
    def __init__(self, isWord = False, string = None):
        self.child = {}
        self.isWord, self.string = isWord, string

class Trie:
    def __init__(self):
        self.child = {}
        self.isWord, self.string = False, None
```

**AddNode()**
```python
    def addNode(self,word):
        node = self
        for char in word:
            if char not in node.child: node.child[char] = Node()
            node = node.child[char]
        node.isWord, node.string = True, word
```

**Search new data**   
After Trie() is build, we need to throw in new data to search on this Trie() graph. The searching is similar to `addNode()`.
When seeing a new data, the way to search over the Trie() graph is also standard:
```python
        def search_root(word, root):
            node = root
            for char in word:
                if node.isWord:              return node.string
                elif char not in node.child: return word
                node = node.child[char]
            return word
```


# Dictionary as Trie()

After searching on this topic, all agree that build the Trie() graph with dictionary is much faster. We will talk about how to build above functionalities with simple dictionary.   

**Node Attribute**   
Simply adding a special key for the node. Let say `node\['string'] = word` serves 2 functions: check if there is a word at a given node, and return the value of the string.     
     
**AddNode()**     
Follow the standard code:
```python
        data = {}
        for w in words:
        ############ AddNode() ##############
            node = data  #start from the root
            for c in w:
                if c not in node: node[c] = {}
                node = node[c]
            node['string'] = w
```

**Search new data**     
Obviously, we need some kind of recursive here to travel over this graph. To be specific, it can be called `dfs`. We need to start from the `root` of the `Trie()` and move along the node until we can no longer travel and collect all we want to collect.   

```python
def dfs(node,idx):
    ...Termination Conditions...
    for key in node:
        dfs(node[key],new_idx)

```
