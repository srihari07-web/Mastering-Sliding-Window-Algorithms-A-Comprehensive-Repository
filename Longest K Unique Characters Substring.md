# Longest K Unique Characters Substring - Variable Size Sliding Window Approach

## Problem Statement

Given a string, find the size of the longest possible substring that has exactly K unique characters. If there is no possible substring, return -1.

## Example

**Example 1:**

```
Input:
S = "aabacbebebe", K = 3

Output:
7

Explanation:
"cbebebe" is the longest substring with 3 distinct characters.
```

**Example 2:**

```
Input:
S = "aaaa", K = 2

Output:
-1

Explanation:
There's no substring with 2 distinct characters.
```

## Approach Explanation

1. **Variable Size Sliding Window Approach**

   - Initialize two pointers, `start` and `end`, to represent the beginning and end of the window, respectively.
   - Initialize an unordered map `charCount` to store the frequency of characters in the current window.
   - Initialize a variable `maxLength` to store the maximum length of the substring found so far.
   - Iterate through the string using the `end` pointer:
     a. Add the current character to the `charCount` map.
     b. If the size of the `charCount` map is greater than `K`:
        i. Subtract the frequency of the character at the `start` pointer from the `charCount` map.
        ii. If the frequency of the character at the `start` pointer becomes 0, remove the character from the `charCount` map.
        iii. Increment the `start` pointer.
     c. If the size of the `charCount` map is equal to `K`, update the `maxLength` variable with the maximum of `maxLength` and the current window size (`end - start + 1`).
     d. Increment the `end` pointer.

2. **Return**

   - Return the `maxLength` variable.

3. **Implementation**

```cpp
class Solution {
public:
    int longestKSubstr(string s, int k) {

        int start = 0;
        int end = 0;
        unordered_map<char, int> charCount;

        int maxLength = -1;
        int n = s.size();

        while (end < n) {
            charCount[s[end]]++;

            while (charCount.size() > k) {
                charCount[s[start]]--;

                if (charCount[s[start]] == 0)
                    charCount.erase(s[start]);

                start++;
            }

            if (charCount.size() == k) {
                maxLength = max(maxLength, end - start + 1);
            }
            end++;
        }

        return maxLength;
    }
};
```

## Complexity Analysis

### Time Complexity:

The time complexity of this solution is O(N), where N is the size of the input string. The algorithm iterates through the string once.

### Space Complexity:

The space complexity is O(1) or O(26), as the frequency map `charCount` has a fixed size of 26 (the number of lowercase English letters).

## Additional Resources

- [GeeksforGeeks Practice - Longest K Unique Characters Substring](https://www.geeksforgeeks.org/problems/longest-k-unique-characters-substring0853/1)
- [Longest Substring With K Unique Characters | Variable Size Sliding Window](https://youtu.be/Lav6St0W_pQ?si=rCZmM4qPSGrMKlYE)