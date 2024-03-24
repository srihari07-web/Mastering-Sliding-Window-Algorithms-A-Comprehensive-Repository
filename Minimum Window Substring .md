# Minimum Window Substring - Sliding Window Approach

## Problem Statement

Given two strings `s` and `t` of lengths `m` and `n` respectively, return the minimum window substring of `s` such that every character in `t` (including duplicates) is included in the window. If there is no such substring, return the empty string `""`.

## Example

**Example 1:**

```
Input:
s = "ADOBECODEBANC"
t = "ABC"

Output:
"BANC"

Explanation:
The minimum window substring "BANC" includes 'A', 'B', and 'C' from string t.
```

**Example 2:**

```
Input:
s = "a"
t = "a"

Output:
"a"

Explanation:
The entire string s is the minimum window.
```

**Example 3:**

```
Input:
s = "a"
t = "aa"

Output:
""

Explanation:
Both 'a's from t must be included in the window.
Since the largest window of s only has one 'a', return empty string.
```

## Approach Explanation

1. **Sliding Window Approach**

   - Initialize an unordered map `mp` to store the frequency of characters in the pattern `t`.
   - Initialize two pointers, `start` and `end`, to represent the beginning and end of the window, respectively.
   - Initialize a variable `count` to store the number of unique characters in the pattern `t` that need to be found.
   - Initialize two variables, `min_length` and `min_start`, to store the minimum length and the start index of the minimum window found so far.
   - Iterate through the string `s` using the `end` pointer:
     a. If the current character is in the pattern `t`, decrement the frequency of the character in the map `mp` and decrement the `count` variable if the frequency becomes 0.
     b. If the `count` variable is 0, meaning that all unique characters from the pattern `t` have been found:
        i. Update the `min_length` and `min_start` variables if the current window size is smaller than the `min_length`.
        ii. Increment the frequency of the character at the `start` pointer in the map `mp`.
        iii. If the frequency of the character at the `start` pointer becomes 1, increment the `count` variable.
        iv. Increment the `start` pointer to slide the window.

2. **Return**

   - If the `min_length` variable is equal to `INT_MAX`, return the empty string `""`.
   - Otherwise, return the minimum window substring using the `substr` function.

3. **Implementation**

```cpp
class Solution {
public:
    string minWindow(string s, string t) {

        unordered_map<char, int> mp;
        for (auto i : t) {
            mp[i]++;
        }
        int start = 0;
        int end = 0;
        int count = t.size();
        int min_length = INT_MAX;
        int min_start = 0;

        while (end < s.size()) {
            if (mp[s[end]] > 0) {
                count--;
            }
            mp[s[end]]--;

            while (count == 0) {
                if (min_length > (end - start + 1)) {
                    min_length = end - start + 1;
                    min_start = start;
                }
                mp[s[start]]++;
                if (mp[s[start]] > 0) {
                    count++;
                }
                start++;
            }
            end++;
        }

        if (min_length == INT_MAX) {
            return "";
        }
        return s.substr(min_start, min_length);
    }
};
```

## Complexity Analysis

### Time Complexity:

The time complexity of this solution is O(N), where N is the size of the input string. The algorithm iterates through the string once.

### Space Complexity:

The space complexity is O(1) or O(26), as the frequency map `mp` has a fixed size of 26 (the number of lowercase English letters).

## Additional Resources

If you are struggling to solve the Minimum Window Substring problem on your own, I highly recommend following the tutorials provided by Aditya Verma and Prakash Shukla. Both of these resources provide clear and in-depth explanations of the problem and the sliding window approach used to solve it.

These tutorials will help you understand the problem, the sliding window approach, and the implementation details required to solve the problem efficiently. Following these resources will provide you with a solid foundation to tackle similar problems in the future.

- [Aditya Verma's Tutorial on Minimum Window Substring](https://youtu.be/iwv1llyN6mo?si=-GH40jrVkOtwNkDS)
- [Prakash Shukla's Tutorial on Minimum Window Substring](https://www.youtube.com/watch?v=nMaKzLWceFg)