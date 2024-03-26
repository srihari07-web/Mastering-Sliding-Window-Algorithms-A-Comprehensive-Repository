# First Negative Integer in Every Window of Size K - Sliding Window Approach

## Problem Statement

Given an array `A[]` of size `N` and a positive integer `K`, find the first negative integer for each and every window (contiguous subarray) of size `K`. If a window does not contain a negative integer, return 0 for that window.

## Example

**Example 1:**

```
Input:
N = 5
A[] = {-8, 2, 3, -6, 10}
K = 2

Output:
-8 0 -6 -6

Explanation:
First negative integer for each window of size k
{-8, 2} = -8
{2, 3} = 0 (does not contain a negative integer)
{3, -6} = -6
{-6, 10} = -6
```

**Example 2:**

```
Input:
N = 8
A[] = {12, -1, -7, 8, -15, 30, 16, 28}
K = 3

Output:
-1 -1 -7 -15 -15 0
```

## Approach Explanation

1. **Sliding Window Approach**

   - Initialize a list `l` to store the negative integers in the current window.
   - Initialize two pointers, `start` and `end`, to represent the beginning and end of the window, respectively.
   - Initialize a vector `ans` to store the first negative integer in each window.
   - Iterate through the array using the `end` pointer:
     a. If the current element is negative, push it to the back of the list `l`.
     b. If the window size is smaller than `K`, increment the `end` pointer and continue to the next iteration.
     c. If the window size is equal to `K`:
        - i. If the list `l` is empty, push 0 to the `ans` vector.
        - ii. Otherwise, push the front element of the list `l` to the `ans` vector.
        - iii. If the element at the front of the list `l` is the element at the `start` pointer, pop the front element from the list `l`.
        - iv. Increment the `start` pointer.

2. **Return**

   - Return the `ans` vector.

3. **Implementation**

```cpp
vector<long long> printFirstNegativeInteger(long long int A[],
                                             long long int N, long long int K) {

    long long end = 0;
    long long start = 0;
    list<long long> l;
    vector<long long> ans;

    while (end < N) {
        if (A[end] < 0) {
            l.push_back(A[end]);
        }

        if (end - start + 1 < K) {
            end++;
            continue;
        } else if (end - start + 1 == K) {
            if (l.empty()) {
                ans.push_back(0);
            } else {
                ans.push_back(l.front());
            }

            if (A[start] == l.front()) {
                l.pop_front();
            }

            start++;
        }

        end++;
    }

    return ans;
}
```

## Complexity Analysis

### Time Complexity:

The time complexity of this solution is O(N), where N is the size of the input array. The algorithm iterates through the array once.

### Space Complexity:

The space complexity is O(K), as the list `l` can store up to K elements.

## Additional Resources

- [GeeksforGeeks - First Negative Integer in Every Window of Size K](https://www.geeksforgeeks.org/problems/first-negative-integer-in-every-window-of-size-k3345/1).
- [CodeLibrary's Tutorial on Sliding Window Algorithm](https://www.youtube.com/watch?v=Z5NHoo-KdxA).