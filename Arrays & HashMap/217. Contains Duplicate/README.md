# LeetCode Problem 217: Contains Duplicate

## Problem Statement

Given an integer array `nums`, return `true` if any value appears at least twice in the array, and return `false` if every element is distinct.

## Approach

To solve this problem efficiently, we use a `HashSet` to keep track of the elements we've encountered as we iterate through the array. The `HashSet` allows for average constant time complexity for insertion and lookup, making this approach both time and space efficient.

### Steps

1. **Initialize a HashSet**: Use this to store elements encountered so far.
2. **Iterate through the Array**: For each element:
   - If the element is already in the `HashSet`, return `true` (indicating a duplicate).
   - If not, add the element to the `HashSet`.
3. **Return False**: If no duplicates are found by the end of the loop, return `false`.

### Time and Space Complexity

- **Time Complexity**: \(O(n)\), where \(n\) is the number of elements in the array. Each insertion and lookup operation in the `HashSet` has an average time complexity of \(O(1)\).
- **Space Complexity**: \(O(n)\), where \(n\) is the number of unique elements in the array.

## Java Solution

Here is the Java implementation of the solution:

```java
import java.util.HashSet;
import java.util.Set;

public class ContainsDuplicate {
    public boolean containsDuplicate(int[] nums) {
        Set<Integer> seen = new HashSet<>();
        
        for (int num : nums) {
            if (seen.contains(num)) {
                return true;  // Found a duplicate
            }
            seen.add(num);  // Add the number to the set
        }
        
        return false;  // No duplicates found
    }
}
