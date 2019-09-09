As far as we know the `next_moves` from `any given positions`, we can `dfs/bfs` to seach for the answer. Typically `dp` is the special case of `bfs` to store all the information we need in `a compressed form` (or `processed information`) for the calculation of the next depth.     
     
Think about it: (1) a contigous array problem: as we move to a new node, we have two options: attach that node to previous node or build a new data point. (2) a subsequence problem:...     
     
Think about the coin changes problem, where from one node, the `next_moves` is determined by the number of coins we have. If we do a simple dfs/bfs, the number of node we have to search is `N^depth`, which is definitely too much for the problem we faced. (It would become NP-hard if we have to do so).     
     
The `very common` technique we use to reduce the dimension of the search is `visited`. A node can be visited twice or more as we go along the search, so `visited` save us time on this search. In some problems, it becomes `DP with memo` - well, now we start to relate the 2 concepts together.     
     
The `visited` can comprise of many variables. If we choose the `right coordinates`, we can reduce the dimension of the next queue of the `bfs search`.
