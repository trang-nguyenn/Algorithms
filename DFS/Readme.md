Aug 16:

Developed from the examples from the concanated words, we can either use DP (preferably with memo) for DFS to search over the data structure, I can solve a variety of hard problems today.

Here are examples:

1. [DFS n-queens puzzle](https://leetcode.com/problems/n-queens/submissions/)   
My code is not clear and clean on this problem. If I did not spend time to polish my code writing, I will forever long-writing in code.
Also seeming that the data structure I use to loop over the problem is not optimum

2. [DP Knight Moves - Interesting Graph algo](https://leetcode.com/problems/knight-dialer/submissions/)   
The solution for this problem is interesting. Vectorization of DP to seperate numbers of the dial pad reminds me on the non-repeated subsequence problems on palindrome, coin changes,..., where we also specify the begining/end/components such that the count can never be overlap. It also reminds me how important it is to have the right data structure to loop over the problem. What is the data structure to loop over a DFS problem btw? The additional carry-on items to evaluate the next moves?

3. [DP Partition Palindrome](https://leetcode.com/problems/palindrome-partitioning-ii/)
Initially, I wrote a triagle isPal(start,end) then utilize BFS to search for optimum path.   
Turns out that I can DP for each **start** value and return DP[0] as the answer. Save the BFS if we smartly dynamic programing.   
Employing this data structure, I can solve several more medium-hard related problems.
