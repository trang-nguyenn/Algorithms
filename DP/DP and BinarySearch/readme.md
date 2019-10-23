Typically, all the problems can be seen as an NP-Hard problem if we can define `next_steps` for the dfs.     

Then the condition of `max` or `min` comes in, and we can substaintially reduce the search to `O(N)` or `O(N^2)`, as we can deterministically choose one out of many options that are available at a given "depth".     

Seen in this direction, the `dp` will loop over the `depth` of the `dfs tree`, such that we can see the `node` by the `dp variables`.    

It also depends on how the `function` link one node to the other node. The easier problem, we can find it immediately next to the `current node`. The harder problem, we need to look up over `all the previous nodes`. In this topic, when all the previous nodes are `well-arranged`, we can `bisect` to find the value we want to find.
