Some good codes on how to loop over the palindrome structure:

## Check the palindrome property of all substrings

Build the palindrome substrings table

```python
        isPal = {}
        for r in range(len(s)):
            for l in range(r+1,-1,-1):
                if l>=r:    isPal[(l,r)] = True
                else:       isPal[(l,r)] = (s[l] == s[r]) and isPal[(l+1,r-1)]
```
