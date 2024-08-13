# Encode and Decode Strings

## Problem Statement

**LeetCode Problem Number: 271**

Design an algorithm to encode a list of strings to a single string. The encoded string is then decoded back to the original list of strings.

# Encode and Decode Strings

## Problem Statement

**LeetCode Problem Number: 271**

Design an algorithm to encode a list of strings to a single string. The encoded string is then decoded back to the original list of strings.

## Explanation

The problem requires two methods:

1. **`encode(List<String> strs)`**: Encodes a list of strings into a single string. Each string is encoded by prefixing it with its length and a delimiter `#`.

2. **`decode(String s)`**: Decodes the encoded string back to a list of original strings. The method extracts each string by reading its length, then the string itself.

The encoding and decoding processes ensure that each string is uniquely identifiable by its length and delimiter.

## Time and Space Complexity

### Encoding

- **Time Complexity**: O(N), where N is the total number of characters in the list of strings. This is because each character in each string is processed exactly once.
- **Space Complexity**: O(N), where N is the total number of characters in the list of strings. This is due to the storage required for the encoded string.

### Decoding

- **Time Complexity**: O(N), where N is the total number of characters in the encoded string. This is because each character in the encoded string is processed exactly once.
- **Space Complexity**: O(N), where N is the total number of characters in the decoded strings. This is due to the storage required for the list of decoded strings.

## Java Implementation

```java
import java.util.ArrayList;
import java.util.List;

public class Codec {
    // Encoding method
    public String encode(List<String> strs) {
        StringBuilder encodedString = new StringBuilder();
        for (String s : strs) {
            // Encode length of the string and the string itself
            encodedString.append(s.length()).append('#').append(s);
        }
        return encodedString.toString();
    }

    // Decoding method
    public List<String> decode(String s) {
        List<String> decodedStrings = new ArrayList<>();
        int i = 0;
        while (i < s.length()) {
            // Find the next '#' character
            int j = s.indexOf('#', i);
            // Get the length of the string
            int length = Integer.parseInt(s.substring(i, j));
            // Move to the start of the actual string
            i = j + 1;
            // Extract the string
            String str = s.substring(i, i + length);
            decodedStrings.add(str);
            // Move to the next encoded string
            i += length;
        }
        return decodedStrings;
    }
}
