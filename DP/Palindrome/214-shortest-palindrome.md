# (214-shortest-palindrome)[https://leetcode.com/problems/shortest-palindrome/]


So many interesting ideas from this question.

## python: stringa.startwith(stringb)

(startwith)[https://leetcode.com/problems/shortest-palindrome/discuss/60099/AC-in-288-ms-simple-brute-force]

```python
def shortestPalindrome(self, s):
    r = s[::-1]
    for i in range(len(s) + 1):
        if s.startswith(r[i:]):
            return r[:i] + s
```

```python
  s          dedcba
  r[0:]      abcded    Nope...
  r[1:]   (a)bcded     Nope...
  r[2:]  (ab)cded      Nope...
  r[3:] (abc)ded       Yes! Return abc + dedcba
```

## KMP algorithm

(explaination)[https://leetcode.com/problems/shortest-palindrome/discuss/60113/Clean-KMP-solution-with-super-detailed-explanation]   
(youtube)[https://www.youtube.com/watch?v=GTJr8OvyEVQ]   

```python
def shortestPalindrome(self, s):
    A=s+"*"+s[::-1]
    cont=[0]
    for i in range(1,len(A)):
        index=cont[i-1]
        while(index>0 and A[index]!=A[i]):
            index=cont[index-1]
        cont.append(index+(1 if A[index]==A[i] else 0))
    return s[cont[-1]:][::-1]+s

```
