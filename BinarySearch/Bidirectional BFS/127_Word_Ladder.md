# [127 Word Ladder](https://leetcode.com/problems/word-ladder/)


Sometime, the next search can be very extensive: We cover a large range of cases to find out what can be the next move.

**The lesson here is NOT afraid of writing 3 for loops to search for the next possible nodes of the graph.**

Interesting and useful examples of **bidirectional BFS*** to find the shortest connected graph.   
Note that we must have **visited** for graph search, and in this algorithm, the visited is by directly substracting the remaining value of the dictionary of words.   

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
        remainingWord = set(wordList)
        length = 1
        while start:
            if start&end:
                return length
            length += 1
            remainingWord -= start  # similar to update visited
            start = remainingWord & {word[:i] + chr(char_idx) + word[i+1:]
                                    for word in start 
                                    for i in range(len(word)) 
                                    for char_idx in range(ord('a'),ord('z')+1)}
                                    
            # Simple but very effective code to drastically save the searching time with bidirectional BFS
            if len(start)>len(end):
                start, end = end, start
        return 0

```

Well, I like the code with `3 for loops`. Need to be Strong enough to do an extensive search at that moment.

This *bold* search reminds me on the other problems:   
(Concatenated Words)[https://github.com/trang-nguyenn/Algorithms/blob/master/DFS/472\.\%20Concatenated\%20Words.md]



# (126 Word Ladder)[https://leetcode.com/problems/word-ladder/]

Slightly more complicated when we need to return the path.   
The `for loop` I write for the front_path and return reminds me on how people write **GMAT sentences** and pack 4-5 layers of small sentences into a full sentence.

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

            remaining -= visited_front
            front_path = [ (new_word, path + [new_word])
                    for word, path in front_path
                    for ii in range(len(word))
                    for new_word in [word[:ii] + chr(idx) + word[ii+1:] for idx in range(ord('a'), ord('z')+1)]
                    if new_word in remaining]
            
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
