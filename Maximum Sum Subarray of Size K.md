# Maximum Sum Subarray of Size K - Sliding Window Approach

# Problem Statement

Given an integer array `Arr` of size `N` and an integer `K`, find the maximum sum of a subarray of size `K` in the given array.

## Examples

**Example 1:**

```
Input:
N = 9
K = 3
Arr = [1, 2, 3, 1, 4, 5, 2, 3, 6]

Output:
12
```

**Explanation:**
The subarray with the maximum sum of size 3 is `[4, 5, 2]`, with a sum of 12.

**Example 2:**

```
Input:
N = 5
K = 2
Arr = [1, 2, 3, 4, 5]

Output:
9
```

**Explanation:**
The subarray with the maximum sum of size 2 is `[4, 5]`, with a sum of 9.

## Approach Explanation

1. **Sliding Window Approach**

   - Initialize two pointers, `start` and `end`, to represent the beginning and end of the window, respectively.
   - Initialize a variable `max_sum` to store the maximum sum found so far and set it to the minimum possible value (e.g., `LONG_MIN`).
   - Initialize a variable `current_sum` to store the sum of the elements within the window and set it to 0.
   - Iterate through the array using the `end` pointer:
     - a. Add the current element to the `current_sum`.
     - b. If the window size is equal to `K`, update the `max_sum` with the maximum of `max_sum` and `current_sum`, and subtract the element at the `start` pointer from the `current_sum`.
     - c. Increment the `start` pointer to slide the window.

2. **Return**

   - Return the `max_sum`.

3. **Implementation**

```cpp
 class Solution{   
public:
    long maximumSumSubarray(int K, vector<int> &Arr , int N){
        // code here 
        int end = 0;
        int start = 0;
        long current_sum = 0; 
        long maxi = LONG_MIN;
        while(end < N){
            current_sum += Arr[end];
            
            if(end - start + 1 == K){
                maxi = max(maxi, current_sum);
                current_sum -= Arr[start];
                start++;
            }
            
            end++;
        }
        
        return maxi; // Returning the sum of the maximum sum subarray
    }
};


```

## Complexity Analysis

### Time Complexity:

The time complexity of this solution is O(N), where N is the size of the input array. The algorithm iterates through the array once.

### Space Complexity:

The space complexity is O(1), as the algorithm uses a constant amount of memory.

## Additional Resources

- [GeeksforGeeks Practice Here  - Max Sum Subarray of Size K](https://www.geeksforgeeks.org/problems/max-sum-subarray-of-size-k5313/1)
- [Aditya Verma's Tutorial on Maximum Sum Subarray of Size K Algorithm](https://www.youtube.com/watch?v=xFJXtB5vSmM)