# Group Anagrams - LeetCode Problem #49

## Problem Statement

Given a list of strings, group the anagrams together. You can return the answer in any order.

## Solution 1: Sorting Approach

### Explanation

- **Sorting Each String**: Convert each string to a character array, sort the array, and convert it back to a string. This sorted string serves as the key to group anagrams.
- **HashMap Usage**: Use a `HashMap` where the key is the sorted string, and the value is a list of strings that are anagrams of that key.
- **Building the Result**: Iterate over the values of the `HashMap` to collect the grouped anagrams into a final list.

### Time Complexity

- **Sorting Each String**: The time complexity to sort each string is \(O(k \log k)\), where \(k\) is the length of the string.
- **Overall Time Complexity**: Assuming \(n\) is the number of strings and \(k\) is the average length of strings, the total complexity is \(O(n \cdot k \log k)\).

### Code

```java
import java.util.*;

public class Solution {
    public List<List<String>> groupAnagrams(String[] strs) {
        HashMap<String, List<String>> map = new HashMap<>();
        
        for (String str : strs) {
            // Sort each string
            char[] chars = str.toCharArray();
            Arrays.sort(chars);
            String key = new String(chars);
            
            if (map.containsKey(key)) {
                map.get(key).add(str);
            } else {
                List<String> list = new ArrayList<>();
                list.add(str);
                map.put(key, list);
            }
        }
        
        List<List<String>> res = new ArrayList<>();
        for (List<String> l : map.values()) {
            res.add(l);
        }
        
        return res;
    }
}


## Solution 2: Character Array Approach

This solution groups anagrams using character counting and a `HashMap`. Each unique group of anagrams is identified by a key derived from the character counts of the strings.

### Explanation

- **Character Counting**: For each string, initialize an integer array of size 26 to count occurrences of each character. The index in the array corresponds to the position of the character in the alphabet (`a` = 0, `b` = 1, ..., `z` = 25).
- **Generating the Key**: Convert the integer array into a `String` using `Arrays.toString(count)`. This string serves as the key to group anagrams.
- **HashMap Usage**: Use a `HashMap` where the key is the character count array (as a `String`), and the value is a list of strings that are anagrams of that key.
- **Building the Result**: Iterate over the values of the `HashMap` to collect the grouped anagrams into a final list.

### Time Complexity

- **Character Counting**: Counting characters in each string takes \(O(k)\) time, where \(k\) is the length of the string.
- **Generating the Key**: Converting the integer array to a `String` using `Arrays.toString(count)` involves a constant-time operation since the array size is fixed at 26. Thus, this step is \(O(1)\).
- **Overall Time Complexity**: Assuming \(n\) is the number of strings and \(k\) is the average length of strings, the total complexity is \(O(n \cdot k)\).

### Code

```java
import java.util.*;

public class Solution {
    public List<List<String>> groupAnagrams(String[] strs) {
        // Create a HashMap to store lists of anagrams
        Map<String, List<String>> map = new HashMap<>();
        
        // Process each string in the input array
        for (String str : strs) {
            // Initialize an array to count the occurrences of each character
            int[] count = new int[26];
            
            // Count characters in the current string
            for (int i = 0; i < str.length(); i++) {
                count[str.charAt(i) - 'a']++;
            }
            
            // Convert the count array to a String key for HashMap
            String key = Arrays.toString(count);
            
            // Add the string to the corresponding list in the map
            if (map.containsKey(key)) {
                map.get(key).add(str);
            } else {
                List<String> list = new ArrayList<>();
                list.add(str);
                map.put(key, list);
            }
        }
        
        // Build the result list from the map's values
        List<List<String>> res = new ArrayList<>();
        for (List<String> list : map.values()) {
            res.add(list);
        }
        
        return res;
    }
}
