# Products of Array Except Self

## Problem Statement

**LeetCode Problem Number: 238**

Given an integer array `nums`, return an array `result` such that `result[i]` is equal to the product of all the elements of `nums` except `nums[i]`.

You must solve it without using division and in O(n) time complexity.

## Explanation

To solve this problem, we need to construct the result array such that each element at index `i` is the product of all elements in the input array except the one at index `i`. We can achieve this by using two auxiliary arrays (or variables), one to keep track of the product of all elements to the left of the current index and another for the product of all elements to the right of the current index.

### Steps to Solve

1. **Initialize Two Arrays**: 
   - `left_products`: This will store the product of all elements to the left of each index.
   - `right_products`: This will store the product of all elements to the right of each index.

2. **Populate Left Products**: 
   Traverse the array from left to right, and for each index, store the product of all elements to its left in the `left_products` array.

3. **Populate Right Products**: 
   Traverse the array from right to left, and for each index, multiply the product of all elements to its right (stored in `right_products`) with the corresponding element in `left_products`.

4. **Compute Final Results**: 
   The final result for each index is the product of the corresponding elements from the `left_products` and `right_products` arrays.

## Time and Space Complexity

- **Time Complexity**: O(n), where n is the length of the input array. The algorithm makes a constant number of passes over the array.
- **Space Complexity**: O(n), where n is the length of the input array. This is due to the additional space required for the `left_products` and `right_products` arrays.

## Java Implementation

```java
public class Solution {
    public int[] productExceptSelf(int[] nums) {
        int n = nums.length;
        int[] result = new int[n];

        // Initialize the result array with 1s
        // for the purpose of left and right product accumulation
        int[] left_products = new int[n];
        int[] right_products = new int[n];

        // Compute left products
        left_products[0] = 1;
        for (int i = 1; i < n; i++) {
            left_products[i] = left_products[i - 1] * nums[i - 1];
        }

        // Compute right products
        right_products[n - 1] = 1;
        for (int i = n - 2; i >= 0; i--) {
            right_products[i] = right_products[i + 1] * nums[i + 1];
        }

        // Compute result by multiplying left and right products
        for (int i = 0; i < n; i++) {
            result[i] = left_products[i] * right_products[i];
        }

        return result;
    }
}
