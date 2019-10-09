When we throw in new data to an 1D array, we need to check on all the possible subsequences ending with this new data.   
   
This section summaries all special forms of the data structure that remembers all the previous subsequences.

# First thought

NP hard problem where we expect the exponential time complexity. (2\^N), every step we expand our search in the multiplication ways.   
Same as the bfs problem, where we "append" the new elements to all previous elements.

# Min/Max Condition

Normally we dp over the new array element.
`dp` as a dictionary with `keys` and `values` to represent 2 dimensions of the problems.    
(What if we need additional informations to make it 3D?)   
With the min/max condition, we can use max/min operation to "lumped" the keys of the search, or compress the 2D dimensions in the `dp.keys()` direction.     
