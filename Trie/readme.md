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

** Search new data**
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
