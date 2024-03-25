# Permutation in String

## Problem Statement

Given two strings `s1` and `s2`, return `true` if `s2` contains a permutation of `s1`, or `false` otherwise.

In other words, return `true` if one of `s1`'s permutations is the substring of `s2`.

## Constraints

* `1 <= s1.length, s2.length <= 10^4`
* `s1` and `s2` consist of lowercase English letters.

## Examples

**Example 1:**

**Input:** s1 = "ab", s2 = "eidbaooo"

**Output:** true

**Explanation:** s2 contains one permutation of s1 ("ba").

**Example 2:**

**Input:** s1 = "ab", s2 = "eidboaoo"

**Output:** false

## Acceptance Rate

44.3%

## Topics

* Hash Table
* Two Pointers
* String
* Sliding Window

## Solution

The solution uses a sliding window technique to check if `s2` contains a permutation of `s1`. It uses an unordered map to store the character counts of `s1` and a variable `count` to keep track of the remaining characters to be matched.

The sliding window is moved using two pointers `start` and `end`. When a character in `s2` matches a character in `s1`, the corresponding character count in the unordered map is decremented and `count` is decremented if the count becomes non-negative.

When the window size equals the length of `s1`, the function checks if `count` is zero. If it is, then a permutation of `s1` has been found in `s2` and the function returns `true`. Otherwise, the character at the start of the window is removed from the unordered map and `count` is incremented if the count becomes positive.

The function returns `false` if no permutation of `s1` is found in `s2`.

## Code

```cpp
class Solution {
public:
    bool checkInclusion(string s1, string s2) {
         int start = 0;
        int end = 0;
        unordered_map<char, int> mp;
        int count = s1.size();

        if (s1.size() > s2.size()) {
            return false;
        }

        for (auto i : s1) {
            mp[i]++;
        }

        while (end < s2.size()) {
            if (mp.find(s2[end]) != mp.end()) {
                mp[s2[end]]--;
                if (mp[s2[end]] >= 0) {
                    count--;
                }
            }

            if (end - start + 1 == s1.size()) {
                if (count == 0) {
                    return true;
                }

                if (mp.find(s2[start]) != mp.end()) {
                    mp[s2[start]]++;
                    if (mp[s2[start]] > 0) {
                        count++;
                    }
                }

                start++;
            }

            end++;
        }

        return false;
    }
};
```

## Complexity Analysis

* Time Complexity: O(n), where n is the length of `s2`.
* Space Complexity: O(1), as the unordered map has a fixed size of 26 (the number of lowercase English letters).

- [LeetCode Practice - Permutation in String](https://leetcode.com/problems/permutation-in-string/description/)