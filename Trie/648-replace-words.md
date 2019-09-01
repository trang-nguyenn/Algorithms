# [648-replace-words](https://leetcode.com/problems/replace-words/)

Typical example of using Trie() to fast search over the data.
   
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

## Code:

```python
class Node:
    def __init__(self, isWord = False, string = None):
        self.child = {}
        self.isWord, self.string = isWord, string

class Trie:
    def __init__(self):
        self.child = {}
        self.isWord, self.string = False, None
    
    def addNode(self,word):
        node = self
        for char in word:
            if char not in node.child: node.child[char] = Node()
            node = node.child[char]
        node.isWord, node.string = True, word

class Solution(object):
    def replaceWords(self, dict, sentence):
        """
        :type dict: List[str]
        :type sentence: str
        :rtype: str
        """
        root = Trie()
        for word in dict:
            root.addNode(word)
        
        def search_root(word, root):
            node = root
            for char in word:
                if node.isWord:              return node.string
                elif char not in node.child: return word
                node = node.child[char]
            return word
        
        data = sentence.split()
        ans = []
        for word in data:
            ans += [search_root(word, root)]
        
        return ' '.join(ans)
```

## Longer Solution

```python
class Solution(object):
    def replaceWords(self, dict, sentence):
        """
        :type dict: List[str]
        :type sentence: str
        :rtype: str
        """
        def search_word(string):
            for word in dict:
                if string.startswith(word): return word
            return string
        
        return ' '.join([search_word(string) for string in sentence.split()])
```
