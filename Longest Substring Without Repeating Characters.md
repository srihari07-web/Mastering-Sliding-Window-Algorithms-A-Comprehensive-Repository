# Longest Substring Without Repeating Characters - Variable Size Sliding Window Approach

## Problem Statement

Given a string `s`, find the length of the longest substring without repeating characters.

## Example

**Example 1:**

```
Input:
s = "abcabcbb"

Output:
3

Explanation:
The answer is "abc", with the length of 3.
```

**Example 2:**

```
Input:
s = "bbbbb"

Output:
1

Explanation:
The answer is "b", with the length of 1.
```

**Example 3:**

```
Input:
s = "pwwkew"

Output:
3

Explanation:
The answer is "wke", with the length of 3.
```

## Approach Explanation

1. **Variable Size Sliding Window Approach**

   - Initialize two pointers, `start` and `end`, to represent the beginning and end of the window, respectively.
   - Initialize an unordered map `mp` to store the frequency of characters in the current window.
   - Initialize a variable `maxi` to store the maximum length of the substring found so far.
   - Iterate through the string using the `end` pointer:
     - a. Add the current character to the `mp` map.
     - b. If the frequency of the current character in the `mp` map is greater than 1:
        i. Subtract the frequency of the character at the `start` pointer from the `mp` map.
        ii. If the frequency of the character at the `start` pointer becomes 0, remove the character from the `mp` map.
        iii. Increment the `start` pointer.
     - c. Update the `maxi` variable with the maximum of `maxi` and the current window size (`end - start + 1`).
     - d. Increment the `end` pointer.

2. **Return**

   - Return the `maxi` variable.

3. **Implementation**

```cpp
class Solution {
public:
    int lengthOfLongestSubstring(string s) {

        int start = 0;
        int end = 0;
        unordered_map<char, int> mp;
        int maxi = 0;

        while (end < s.size()) {
            mp[s[end]]++;

            while (mp[s[end]] > 1) {
                mp[s[start]]--;
                if (mp[s[start]] == 0) {
                    mp.erase(s[start]);
                }
                start++;
            }

            maxi = max(maxi, end - start + 1);
            end++;
        }

        return maxi;
    }
};
```

## Complexity Analysis

### Time Complexity:

The time complexity of this solution is O(N), where N is the size of the input string. The algorithm iterates through the string once.

### Space Complexity:

The space complexity is O(1) or O(26), as the frequency map `mp` has a fixed size of 26 (the number of lowercase English letters).

## Additional Resources

- [LeetCode - Longest Substring Without Repeating Characters](https://leetcode.com/problems/longest-substring-without-repeating-characters/)
- [Aditya Verma's Tutorial on Longest Substring With Without Repeating Characters](https://youtu.be/L6cffskouPQ?si=Ri3gztTpxDWzPAvu)

