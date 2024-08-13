# Top K Frequent Elements - LeetCode Problem #347

## Problem Statement

Given an integer array `nums` and an integer `k`, return the `k` most frequent elements. You may return the answer in any order.

## Solution 1: Bucket Sort Approach

### Explanation

- **Frequency Counting**: Use a `HashMap` to count the frequency of each element in the array.
- **Bucket Sorting**: Create a list of lists (`count`) where each index corresponds to a frequency. Populate the list such that elements with the same frequency are grouped together.
- **Collecting Results**: Iterate over the `count` list from the highest frequency to the lowest. Collect elements until the result contains `k` elements.

### Time Complexity

- **Building the Frequency Map**: \(O(n)\), where \(n\) is the number of elements in `nums`.
- **Building the Bucket List**: \(O(n)\) to initialize the list and \(O(n)\) to add elements based on their frequencies.
- **Collecting Results**: \(O(n)\) in the worst case when iterating over the bucket list.
- **Overall Time Complexity**: \(O(n)\).

### Code

```java
import java.util.*;

public class Solution {
    public int[] topKFrequent(int[] nums, int k) {
        HashMap<Integer, Integer> map = new HashMap<>();

        for (int num : nums) {
            map.put(num, map.getOrDefault(num, 0) + 1);
        }

        // Create a list of lists to bucket elements by frequency
        ArrayList<List<Integer>> count = new ArrayList<>();
        for (int i = 0; i <= nums.length; i++) {
            count.add(new ArrayList<>());
        }

        for (int key : map.keySet()) {
            int freq = map.get(key);
            count.get(freq).add(key);
        }

        List<Integer> res = new ArrayList<>();
        for (int i = count.size() - 1; i >= 0; i--) {
            if (count.get(i) != null) {
                res.addAll(count.get(i));
            }
            if (res.size() >= k) break;
        }

        int[] h = new int[k];
        for (int i = 0; i < k; i++) {
            h[i] = res.get(i);
        }

        return h;
    }
}



## Solution 2: Priority Queue Approach

### Explanation

- **Frequency Counting**: Use a `HashMap` to count the frequency of each element in the array.
- **Priority Queue**: Use a `PriorityQueue` (max-heap) to maintain the top `k` frequent elements. The heap is ordered by frequency in descending order. The `PriorityQueue` is implemented with a comparator that prioritizes higher frequencies.
- **Extracting Results**: Extract the top `k` elements from the priority queue, which will be the most frequent elements.

### Time Complexity

- **Building the Frequency Map**: \(O(n)\), where \(n\) is the number of elements in `nums`.
- **Building the Priority Queue**: \(O(n \log k)\), where \(n\) is the number of elements and \(k\) is the size of the heap.
- **Extracting Results**: \(O(k \log k)\) for extracting the `k` elements from the priority queue.
- **Overall Time Complexity**: \(O(n \log k)\).

### Code

```java
import java.util.*;

public class Solution {
    public int[] topKFrequent(int[] nums, int k) {
        HashMap<Integer, Integer> map = new HashMap<>();

        // Count the frequency of each element
        for (int num : nums) {
            map.put(num, map.getOrDefault(num, 0) + 1);
        }

        // Create a priority queue to maintain the top k frequent elements
        PriorityQueue<Map.Entry<Integer, Integer>> pq = 
            new PriorityQueue<>((a, b) -> b.getValue() - a.getValue());

        // Add all entries from the map to the priority queue
        pq.addAll(map.entrySet());

        // Extract the top k elements
        int[] res = new int[k];
        for (int i = 0; i < k; i++) {
            res[i] = pq.poll().getKey();
        }

        return res;
    }
}
