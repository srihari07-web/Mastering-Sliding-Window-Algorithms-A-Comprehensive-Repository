# Longest Sub-Array with Sum K - Variable Size Sliding Window Approach

## Problem Statement

Given an array containing N integers and an integer K, find the length of the longest sub-array with the sum of the elements equal to the given value K.

## Example

**Example 1:**

```
Input:
A[] = {10, 5, 2, 7, 1, 9}
K = 15

Output:
4

Explanation:
The sub-array is {5, 2, 7, 1}.
```

**Example 2:**

```
Input:
A[] = {-1, 2, 3}
K = 6

Output:
0

Explanation:
There is no such sub-array with sum 6.
```

## Approach Explanation

1. **Variable Size Sliding Window Approach**

   - Initialize two pointers, `start` and `end`, to represent the beginning and end of the window, respectively.
   - Initialize a variable `sum` to store the sum of the elements in the current window.
   - Initialize a variable `maxi` to store the maximum length of the sub-array found so far.
   - Iterate through the array using the `end` pointer:
     a. Add the current element to the `sum`.
     b. If the `sum` is equal to `K`, update the `maxi` variable with the maximum of `maxi` and the current window size (`end - start + 1`).
     c. If the `sum` is smaller than `K`, increment the `end` pointer.
     d. If the `sum` is greater than `K`:
        - i. Subtract the element at the `start` pointer from the `sum`.
        - ii. Increment the `start` pointer.
        - iii. Repeat steps i and ii until the `sum` is smaller than or equal to `K`.
        - iv. If the `sum` is equal to `K`, update the `maxi` variable with the maximum of `maxi` and the current window size (`end - start + 1`).
        - v. Increment the `end` pointer.

2. **Return**

   - Return the `maxi` variable.

3. **Implementation**

```cpp
class Solution {
public:
    int lenOfLongSubarr(int A[], int N, int K) {

        int start = 0;
        int end = 0;
        int sum = 0;
        int maxi = INT_MIN;

        while (end < N) {

            sum = sum + A[end];

            if (sum == K) {

                maxi = max(maxi, end - start + 1);

            } else if (sum < K) {
                end++;
            } else if (sum > K) {
                while (sum > K) {
                    sum = sum - A[start];
                    start++;
                }
                if (sum == K) {
                    maxi = max(maxi, end - start + 1);
                }

                end++;
            }
        }

        return maxi;
    }
};
```

## Complexity Analysis

### Time Complexity:

The time complexity of this solution is O(N), where N is the size of the input array. The algorithm iterates through the array once.

### Space Complexity:

The space complexity is O(1), as the algorithm uses a constant amount of memory.

## Additional Resources

- [Variable Size Sliding Window | Largest Subarray of sum K | Part 1](https://youtu.be/Jv2iJ4dgX9Q?si=rBrRfjp0sWmQGYpi)
- [Largest Subarray of sum K | Part 2](https://youtu.be/TfQPoaRDeMQ?si=rBrRfjp0sWmQGYpi)
- [GeeksforGeeks Practice- Longest Sub-Array with Sum K](https://www.geeksforgeeks.org/problems/longest-sub-array-with-sum-k0809/1)