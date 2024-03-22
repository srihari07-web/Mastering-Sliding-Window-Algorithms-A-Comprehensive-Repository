# Maximum of All Subarrays of Size K - Sliding Window Approach

## Problem Statement

Given an integer array `arr` of size `n` and an integer `k`, find the maximum of each subarray of size `k`.

## Example

**Example 1:**

```
Input:
n = 9
arr[] = {1, 2, 3, 1, 4, 5, 2, 3, 6}
k = 3

Output:
3 3 4 5 5 5 6

Explanation:
Maximum of each subarray of size 3:
{1, 2, 3} = 3
{2, 3, 1} = 3
{3, 1, 4} = 4
{1, 4, 5} = 5
{4, 5, 2} = 5
{5, 2, 3} = 5
{2, 3, 6} = 6
```

**Example 2:**

```
Input:
n = 4
arr[] = {8, 5, 10, 7}
k = 4

Output:
10

Explanation:
Maximum of the only subarray of size 4:
{8, 5, 10, 7} = 10
```

## Approach Explanation

1. **Sliding Window Approach**

   - Initialize a list `l` to store the indices of elements in the current window in decreasing order.
   - Initialize two pointers, `start` and `end`, to represent the beginning and end of the window, respectively.
   - Initialize a vector `ans` to store the maximum of each subarray.
   - Iterate through the array using the `end` pointer:
     a. Remove elements from the back of the list `l` that are smaller than the current element.
     b. Push the index of the current element to the back of the list `l`.
     c. If the window size is smaller than `k`, increment the `end` pointer.
     d. If the window size is equal to `k`:
        i. Push the element at the front of the list `l` to the `ans` vector.
        ii. If the element at the front of the list `l` is the element at the `start` pointer, pop the front element from the list `l`.
        iii. Increment the `start` pointer and the `end` pointer.

2. **Return**

   - Return the `ans` vector.

3. **Implementation**

```cpp
class Solution {
public:
    vector<int> max_of_subarrays(int* arr, int n, int k) {
        int end = 0;
        int start = 0;
        list<int> l;
        vector<int> ans;

        while (end < n) {

            while (l.size() > 0 && arr[l.back()] < arr[end]) {
                l.pop_back();
            }

            l.push_back(end);

            if (end - start + 1 < k) {
                end++;
            } else if (end - start + 1 == k) {
                ans.push_back(arr[l.front()]);
                if (l.front() == start) {
                    l.pop_front();
                }

                start++;
                end++;
            }
        }

        return ans;
    }
};
```

## Complexity Analysis

### Time Complexity:

The time complexity of this solution is O(N), where N is the size of the input array. The algorithm iterates through the array once.

### Space Complexity:

The space complexity is O(K), as the list `l` can store up to K indices.

## Additional Resources

- [GeeksforGeeks - Maximum of all subarrays of size k](https://www.geeksforgeeks.org/problems/maximum-of-all-subarrays-of-size-k3101/1)
- [Leetcode - Maximum of all subarrays of size k](https://leetcode.com/problems/sliding-window-maximum/description/)
- [Code with Alisha's Tutorial on Sliding Window Algorithm](https://www.youtube.com/watch?v=l_CFMVPKv2Q) (This tutorial covers this specific problem, it provides a good foundation for understanding the sliding window approach to find the Maximum of all subarrays.)

** please note that the solution is solved in geeks for geeks ,approach is same but variables may change in leetcode .