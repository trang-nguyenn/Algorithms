Aug 30 2019:   
   
When I come aross the problem of palindrome pairs [palindrome-pairs](https://leetcode.com/problems/palindrome-pairs/), after completing writing code for the Trie() to store this data structure, I visit the solution without Trie where a word is divided into prefix and suffix to solve the problem.   
   
   An interesting thought that crosses over my mind is the "crazy" rule to connect two words together: if the reverse of word B is idential to the prefix or suffix of word A, while the remaining is a palindrome, then A & B are connected. Well, they are connected as similiar as the [Word_Ladder](https://leetcode.com/problems/word-ladder/) or [472. Concatenated Words](https://leetcode.com/problems/concatenated-words/), just the connected rule is more subtle.   
      
   Working on these `word searching` problems, I always find awe on the amount of in-depth we perform to search for what we want to find. So I create this sub-folder to summary the `in-depth` search on every single word.
