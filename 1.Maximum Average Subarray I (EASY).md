# Maximum Average Subarray I (EASY)

## Problem Statement

You are given an integer array `nums` consisting of `n` elements, and an integer `k`. Find a contiguous subarray whose length is equal to `k` that has the maximum average value and return this value. Any answer with a calculation error less than `10^-5` will be accepted.

## Example 1:

**Input:** nums = [1,12,-5,-6,50,3], k = 4

**Output:** 12.75000

**Explanation:** Maximum average is (12 - 5 - 6 + 50) / 4 = 51 / 4 = 12.75

## Example 2:

**Input:** nums = [5], k = 1

**Output:** 5.00000

## Constraints

* n == nums.length
* 1 <= k <= n <= 10^5
* -10^4 <= nums[i] <= 10^4

## Solution

The solution uses a sliding window technique to find the maximum average subarray of size `k`. The window is represented by two pointers `start` and `end`. The `start` pointer represents the beginning of the current window and the `end` pointer represents the end of the current window.

The algorithm iterates through the array and calculates the sum of the first `k` elements. The maximum average is calculated as the maximum of the current average and the previous maximum average.

The algorithm then moves the `start` pointer to the right by one position and the `end` pointer to the right by one position. The sum is updated by subtracting the element at the `start` pointer and adding the element at the `end` pointer. The maximum average is updated as before.

The algorithm continues this process until the `end` pointer reaches the end of the array.

The algorithm returns the maximum average.

## Code

```cpp
class Solution {
public:
    double findMaxAverage(vector<int>& nums, int k) {
        int start = 0;
        int end = 0;
        int sum = 0;
        double maxi = INT_MIN;

        while (end < k) {
            sum += nums[end];
            end++;
        }

        maxi = max((double)sum / k, maxi);

        while (end < nums.size()) {
            sum -= nums[start];
            sum += nums[end];
            maxi = max((double)sum / k, maxi);
            start++;
            end++;
        }

        return maxi;
    }
};
```

## Complexity Analysis

* Time Complexity: O(n), where n is the length of the array `nums`.
* Space Complexity: O(1), as the algorithm uses constant space to store the `start` and `end` pointers, the sum of the current subarray, and the maximum average.

## Video Reference

The video attached in this repository is from [Youtube](https://youtu.be/56TxHMG0qhQ?si=Bh7ZN5pML6Z-sjTg) and is not owned by me. The video is used for educational purposes only, and all rights belong to their respective owners.

## Question Credits

The question used in this repository is taken from [LeetCode](https://leetcode.com/problems/maximum-average-subarray-i/description/), a popular online platform for coding practice and learning. The question is used for educational purposes only, and all rights belong to their respective owners.