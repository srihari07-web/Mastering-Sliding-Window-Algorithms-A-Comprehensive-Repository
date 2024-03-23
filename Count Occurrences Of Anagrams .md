# Count Occurrences of Anagrams - Sliding Window Approach

## Problem Statement

Given a word `pat` and a text `txt`, return the count of the occurrences of anagrams of the word in the text.

## Example

**Example 1:**

```
Input:
txt = forxxorfxdofr
pat = for

Output:
3

Explanation:
"for", "orf", and "ofr" appear in the txt, hence the answer is 3.
```

**Example 2:**

```
Input:
txt = aabaabaa
pat = aaba

Output:
4

Explanation:
"aaba" is present 4 times in txt.
```

## Approach Explanation

1. **Sliding Window Approach**

   - Initialize an unordered map `mp` to store the frequency of characters in the pattern `pat`.
   - Initialize two pointers, `start` and `ending`, to represent the beginning and end of the window, respectively.
   - Initialize a variable `count` to store the number of unique characters in the pattern `pat`.
   - Initialize a variable `ans` to store the count of anagrams found.
   - Iterate through the text using the `ending` pointer:
     a. If the current character is in the pattern `pat`, decrement the frequency of the character in the map `mp` and decrement the `count` variable if the frequency becomes 0.
     b. If the window size is smaller than the length of the pattern `pat`, increment the `ending` pointer.
     c. If the window size is equal to the length of the pattern `pat`:
        i. If the `count` variable is 0, increment the `ans` variable.
        ii. Increment the frequency of the character at the `start` pointer in the map `mp`.
        iii. If the frequency of the character at the `start` pointer becomes 1, increment the `count` variable.
        iv. Increment the `start` pointer to slide the window.

2. **Return**

   - Return the `ans` variable.

3. **Implementation**

```cpp
class Solution {
public:
    int search(string pat, string txt) {

        int start = 0;
        int ending = 0;
        int ans = 0;
        unordered_map<char, int> mp;

        for (auto i : pat) {
            mp[i]++;
        }

        int count = mp.size();

        while (ending < txt.size()) {
            if (mp.find(txt[ending]) != mp.end()) {
                mp[txt[ending]]--;

                if (mp[txt[ending]] == 0)
                    count--;
            }

            if (ending - start + 1 < pat.size())
                ending++;

            else if (ending - start + 1 == pat.size()) {
                if (count == 0) {
                    ans++;
                }

                if (mp.find(txt[start]) != mp.end()) {
                    mp[txt[start]]++;

                    if (mp[txt[start]] == 1)
                        count++;
                }

                start++;
                ending++;
            }
        }

        return ans;
    }
};
```

## Complexity Analysis

### Time Complexity:

The time complexity of this solution is O(N), where N is the size of the input text. The algorithm iterates through the text once.

### Space Complexity:

The space complexity is O(1) or O(26), as the frequency map `mp` has a fixed size of 26 (the number of lowercase English letters).

## Additional Resources

- [GeeksforGeeks - Count Occurrences of Anagrams](https://www.geeksforgeeks.org/problems/count-occurences-of-anagrams5839/1)
- [Aditya Verma's Tutorial on Count Occurrences of Anagrams Algorithm](https://youtu.be/MW4lJ8Y0xXk?si=Kk_-7zjroXUaFWm7) (Although this tutorial does not cover this specific problem, it provides a good foundation for understanding the sliding window approach.)