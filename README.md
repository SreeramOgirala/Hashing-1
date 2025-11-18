# Hashing-1
Explain your approach in **three sentences only** at top of your code


## Problem 1:
Given an array of strings, group anagrams together.

Example:
Input: ["eat", "tea", "tan", "ate", "nat", "bat"],
Output:
[
  ["ate","eat","tea"],
  ["nat","tan"],
  ["bat"]
]

Note:
All inputs will be in lowercase.
The order of your output does not matter.

## Problem 2:
Given two strings s and t, determine if they are isomorphic.
Two strings are isomorphic if the characters in s can be replaced to get t.
All occurrences of a character must be replaced with another character while preserving the order of characters. No two characters may map to the same character but a character may map to itself.

Example 1:
Input: s = "egg", t = "add"
Output: true

Example 2:
Input: s = "foo", t = "bar"
Output: false

Example 3:
Input: s = "paper", t = "title"
Output: true
Note:
You may assume both s and t have the same length.

## Problem 3:
Given a pattern and a string str, find if str follows the same pattern.
Here follow means a full match, such that there is a bijection between a letter in pattern and a non-empty word in str.

Example 1:
Input: pattern = "abba", str = "dog cat cat dog"
Output: true

Example 2:
Input:pattern = "abba", str = "dog cat cat fish"
Output: false

Example 3:
Input: pattern = "aaaa", str = "dog cat cat dog"
Output: false

Example 4:
Input: pattern = "abba", str = "dog dog dog dog"
Output: false
Notes:
You may assume pattern contains only lowercase letters, and str contains lowercase letters that may be separated by a single space.



<!-- Problem  1: Grouping Anagrams -->
class Solution:
    def groupAnagrams(self, strs: List[str]) -> List[List[str]]:
        # The basic idea is to generate a unique hash. So the question is about generating a hash function. 

        groups = defaultdict(list)
        for s in strs:
            count = ["0"] * 26
            for c in s:
                count[ord(c) - ord('a')] = str(int(count[ord(c) - ord('a')]) + 1)

            
            key = "*".join(count)

            groups[key].append(s)
        
        return list(groups.values())

                
<!-- Problem 2: Isomorphic strings -->

class Solution:
    def isIsomorphic(self, s: str, t: str) -> bool:
        sMap = {}
        tMap = {}

        for i in range(len(s)):
            if s[i] in sMap and sMap[s[i]] != t[i]:
                return False
            elif t[i] in tMap and tMap[t[i]] != s[i]:
                return False
            else:
                sMap[s[i]] = t[i]
                tMap[t[i]] = s[i]
        
        return True