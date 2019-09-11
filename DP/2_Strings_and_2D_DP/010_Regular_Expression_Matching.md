# [10. Regular Expression Matching](https://leetcode.com/problems/regular-expression-matching/)

Well, 2D table search where we need to find our way from the begining of the table to the other end (Sound familiar huh). The really difficult part of this problem is to correctly understand the meaning of a node in this 2D table:     
(1) True if the text `from that loc outward` and the pattern `from that loc outward` matches. NOT the two symbols at the loc matches.   
(2) The connection rules from one grid to the other, where the `*` rules makes it really hard (I remember the problem of * for the parenthesis then). Does look backward easier than look forward? (No, forward is easier in this problem).   

```python
class Solution(object):
    def isMatch(self, S, P):
        """
        :type s: str
        :type p: str
        :rtype: bool
        """
        queue = [(0,0)]
        visited = set()
        while queue:
            i1, i2 = queue.pop()
            visited.add((i1,i2))
            if (i1,i2) == (len(S),len(P)): return True
            
            valid = i1<len(S) and i2<len(P) and P[i2] in {S[i1],'.'}
            if valid and (i1+1,i2+1) not in visited:
                queue.append((i1+1,i2+1))
            
            if i2+1<len(P) and P[i2+1] =='*':
                if valid and (i1+1,i2) not in visited:
                    queue.append((i1+1,i2))
                if (i1,i2+2) not in visited:
                    queue.append((i1,i2+2))
        return False
```


Typically, we have two 1D array/string/list, and we need to calculate some information out of these two data. 2D DP table is generally a good choice, as we can typically reduce the dimensions of the 1D data.   

Also, we often pad the first element of the string with 'NULL' for the initial starting point.

Well, the DP update rule of this exercise is well advanced compared to my programming logical level at the moment. Might be one day when I do more exercises with similar logic, I can figure out this logic faster.

Code is credited to [DP](https://leetcode.com/problems/regular-expression-matching/discuss/5723/My-DP-approach-in-Python-with-comments-and-unittest)

```python
class Solution(object):
    def isMatch(self, s, p):
        # The DP table and the string s and p use the same indexes i and j, but
        # table[i][j] means the match status between p[:i] and s[:j], i.e.
        # table[0][0] means the match status of two empty strings, and
        # table[1][1] means the match status of p[0] and s[0]. Therefore, when
        # refering to the i-th and the j-th characters of p and s for updating
        # table[i][j], we use p[i - 1] and s[j - 1].

        # Initialize the table with False. The first row is satisfied.
        table = [[False] * (len(s) + 1) for _ in range(len(p) + 1)]

        # Update the corner case of matching two empty strings.
        table[0][0] = True

        # Update the corner case of when s is an empty string but p is not.
        # Since each '*' can eliminate the charter before it, the table is
        # vertically updated by the one before previous. [test_symbol_0]
        for i in range(2, len(p) + 1):
            table[i][0] = table[i - 2][0] and p[i - 1] == '*'

        for i in range(1, len(p) + 1):
            for j in range(1, len(s) + 1):
                if p[i - 1] != "*":
                    # Update the table by referring the diagonal element.
                    table[i][j] = table[i - 1][j - 1] and \
                                  (p[i - 1] == s[j - 1] or p[i - 1] == '.')
                else:
                    # Eliminations (referring to the vertical element)
                    # Either refer to the one before previous or the previous.
                    # I.e. * eliminate the previous or count the previous.
                    # [test_symbol_1]
                    table[i][j] = table[i - 2][j] or table[i - 1][j]

                    # Propagations (referring to the horizontal element)
                    # If p's previous one is equal to the current s, with
                    # helps of *, the status can be propagated from the left.
                    # [test_symbol_2]
                    if p[i - 2] == s[j - 1] or p[i - 2] == '.':
                        table[i][j] |= table[i][j - 1]

        return table[-1][-1]

```
