# [Word_Ladder](https://leetcode.com/problems/word-ladder/)

First, we need to form the graph by checking if one word is "connected" to the other.
Second, BFS to find the shortest path.

I heard that we can double-sided BFS to boost the searching time?

```python
class Solution(object):
    def ladderLength(self, beginWord, endWord, wordList):
        """
        :type beginWord: str
        :type endWord: str
        :type wordList: List[str]
        :rtype: int
        """
        if endWord not in wordList: return 0
        
        start, end = set([beginWord]), set([endWord])
        wordList = set(wordList)
        length = 1
        while start:
            if start&end:
                return length
            length += 1
            wordList -= start
            start = wordList & {word[:i] + chr(char_idx) + word[i+1:]
                                for word in start 
                                for i in range(len(word)) 
                                for char_idx in range(ord('a'),ord('z')+1)}
            if len(start)>len(end):
                start, end = end, start
        return 0
```

# [word-ladder-ii](https://leetcode.com/problems/word-ladder-ii/)

```python
class Solution(object):
    def findLadders(self, beginWord, endWord, wordList):
        """
        :type beginWord: str
        :type endWord: str
        :type wordList: List[str]
        :rtype: List[List[str]]
        """
        if endWord not in wordList: return []
        
        remaining = set(wordList)
        front_path, back_path = [(beginWord,[beginWord])], [(endWord,[endWord])]
        visited_front, visited_back = set([beginWord]), set([endWord])
      
        
        while front_path:
            # print('------------------')
            # print(front_path, back_path, remaining)
            
            remaining -= visited_front
            front_path = [ (new_word, path + [new_word])
                    for word, path in front_path
                    for ii in range(len(word))
                    for new_word in [word[:ii] + chr(idx) + word[ii+1:] for idx in range(ord('a'), ord('z')+1)]
                    if new_word in remaining]
            
            # print(front_path, back_path,remaining)
            visited_front = {word for word, _ in front_path}
            visited_back  = {word for word, _ in back_path}
            join =  visited_front & visited_back
            if join:
                return [path1 + path2[:-1][::-1] if path1[0] == beginWord else path2 + path1[:-1][::-1]
                        for word1, path1 in front_path if word1 in join
                        for word2, path2 in back_path if word2 == word1]
            
            if len(front_path)> len(back_path):
                front_path   , back_path    = back_path, front_path
                visited_front, visited_back = visited_back, visited_front
        
        return []
```
