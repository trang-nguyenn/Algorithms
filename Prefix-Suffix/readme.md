Certain problem has the property:    
```
f(s[left:right]) = prefix(s[right+1]) - prefix(s[left])
```
In this case, we can drastically reduce the computation time from $O(n^2)$ to O(n).   
I find awe on the creativity of people to think about different data structure to generate this prefix/suffix data.
