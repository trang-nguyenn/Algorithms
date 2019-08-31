Some good codes on how to loop over the palindrome structure:

## Check the palindrome property of all substrings

Build the palindrome substrings table

```python
        isPal = {}
        for r in range(len(s)):
            for l in range(r,-1,-1):
                if l>r-2:   isPal[(l,r)] = True       #len()<2 is always palindrome
                else:       isPal[(l,r)] = (s[l] == s[r]) and isPal[(l+1,r-1)] #start,end + recursive
```
