[1000. Minimum Cost to Merge Stones](https://leetcode.com/problems/minimum-cost-to-merge-stones/)

Initially, I am thinking about priority queue, where we can lump the nearby elements and push the data into the queue (sounds like the tree solutions - check it out later) and everytime choose the smallest elements and pop it out. [Tree-based](https://leetcode.com/problems/minimum-cost-to-merge-stones/discuss/248442/(5ms)-O(n3)-Java-DP-20-lines.-Tree-based-explanation.)   


Meanwhile, people in the discussion excite about the DP techniques.I spend 15 mins to read the solution, but it is still hard for me to capture the answer.   
Something like:    
(1) DP[s][e] is the cost to merge the stone from s to e. Obviously, the number of stone left should be 0,1,2,...,K-1   
(2) When we decide to merge stone, we incur the cost of sum(stones[i:j]). This happens when (j-i)%(k-1) == 0   
(3) Let's say DP[s][s+x] = 0 with x<K-1 as we cannot merge any of them. When we hit DP[s][s+K-1], then we incur the cost sum(stones[s][s+K-1]).   
(4) Now we need to calculate DP[s][s+K]. We have 2 choices: DP[s][s+K-1] + DP[s+K-1][s+K] or DP[s][s+K-1] + DP[s+K-1][s+K] .... (to be continued)


Several layers of codes here 
