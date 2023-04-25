# Boyer-Moore Algorithm

This algorithm searches for a pattern string `p` within a larger string `t`.

### Introduction

The algorithm works by scanning the text from right to left, comparing characters with the pattern. When a mismatch occurs, the algorithm consults the "bad character" table to determine how far to shift the pattern to the right. If the mismatched character is not in the pattern, the pattern is shifted to the right by the length of the pattern. If the character is in the pattern, the pattern is shifted to the right by the difference between the index of the mismatched character in the pattern and the last occurrence of that character in the pattern. This ensures that the pattern is shifted to the right by the maximum possible amount.

When a partial match occurs, the algorithm consults the "good suffix" table to determine how far to shift the pattern to the right. If the matched suffix has a matching prefix, the pattern is shifted to the right by the difference between the length of the pattern and the index of the last occurrence of the matching prefix. If there is no matching prefix, the pattern is shifted to the right by the length of the pattern.

## Different scenarios

1. Preprocessing: Create a last occurrence dictionary of all characters in the pattern. For each character, store its last occurrence in the pattern.
2. Matching: Start matching the pattern from the end to the start. If the characters match, move on to the previous character. If the characters don't match, there are two scenarios:
   - If the character in the text is not in the pattern, shift the pattern to the next character in the text.
   - If the character in the text is in the pattern, shift the pattern to align with the last occurrence of that character in the pattern. If the last occurrence of that character is before the current position of the pattern, shift the pattern to align with the current position in the text.
3. Repeat the matching process until the end of the text is reached or a match is found.
4. Return the positions of all the matches in the text.

Remember to consider the following cases:
- The pattern is longer than the text.
- The pattern is not found in the text.
- There are characters in the text that are not in the pattern.
- There are multiple occurrences of the same character in the pattern.

I hope these notes help you understand the Boyer-Moore algorithm better and prepare for your exam. Good luck!


## Algorithm

- Initialize `last[c]` for each `c` in `p`.
	- We need to record the index of the last seen position of `c`.
- In the nested loop, compare each segment `t[i: i + len(p)]` with `p`.
- If `p` matches, record and shift by 1.
- If we find a mismatch at `t[i+j]`
	- If `j > last[t[i+j]]`, shifts by `j - last[t[i+j]]`
	- If `last[t[i+j]] > j`, shift by `1`.
		- Should not shift `p` to the left.
	- If `t[i+j]` is not in `p`, shift by `j+1`.

```Python
def boyermoore(t, p):
    # Preprocess
    last = {}  # dictionary to store the last index of each character in the pattern
    for i in range(len(p)):
        last[p[i]] = i

    poslist = []  # list to store the starting positions of all occurrences of the pattern in the text
    i = 0
    while i <= (len(t) - len(p)):
        matched, j = True, len(p) - 1
        while j >= 0 and matched:  # Compare pattern and text backwards
            if t[i+j] != p[j]:
                matched = False
            j = j - 1
        if matched:  # If pattern is found
            poslist.append(i)  # Add starting position to the list
            i = i + 1
        else:
            j = j + 1
            if t[i+j] in last.keys():  # If character in text is in the pattern
                if j > last[t[i+j]]:  # Shift pattern by j - last occurrence of the character in the pattern
                    i = i + j - last[t[i+j]]
                else:  # Shift pattern to align with the current position in the text
                    i = i + 1
            else:  # If character not in the pattern, shift pattern to align with the next character in the text
                i = i + j + 1
    return poslist

print(boyermoore('abcaaacabc','abc'))
```

```Output
[0, 7]
```

# Rabin-Karp Algorithm

### Introduction

The Rabin-Karp algorithm is a string matching algorithm that finds all occurrences of a given pattern in a text string in linear time. It is based on the idea of hashing, which is a way to convert a string of characters into a numeric value.

The algorithm works by first computing the hash value of the pattern and the first window of the text string. If the hash values match, the algorithm compares the pattern with the current window of the text string to see if they are equal. If they are not equal, the algorithm moves the window by one position and computes the hash value of the new window.

If the hash values do not match, the algorithm moves the window by one position and computes the hash value of the new window. This process is repeated until the end of the text string is reached.

Here is a high-level algorithm for the Rabin-Karp string matching algorithm:

1. Calculate the hash value of the pattern using a prime number.
2. Calculate the hash value of the first substring of the text.
3. Iterate through the text, checking for matches with the pattern.
	- If the hash value of the current substring matches the hash value of the pattern then check if the substring matches the pattern, a match is found.
4. Calculate the hash value of the next substring and repeat the process until the end of the text.

``` Python
def rabin_karp(text, pattern):
    match_found =[] # to store the starting position of matched pattern
    n = len(text)
    m = len(pattern)    
    prime = 101 # a prime number to use for the hash function
    
    # Calculate the hash value of the pattern
    pattern_hash = 0
    for i in range(m):
        pattern_hash += ord(pattern[i])
    pattern_hash = pattern_hash % prime
    
    # Calculate the hash value of the first substring of the text
    text_hash = 0
    for i in range(m):
        text_hash += ord(text[i])
    text_hash = text_hash % prime
    
    # Iterate through the text, checking for matches with the pattern
    for i in range(n - m + 1):
        # Check if the current substring matches the pattern
        if text_hash == pattern_hash and text[i:i+m] == pattern:
            match_found.append(i)
        
        # Calculate the hash value of the next substring
        if i < n - m:
            text_hash = (text_hash - ord(text[i]) + ord(text[i+m]))
            text_hash = text_hash % prime
            
    # Return the starting position of matched pattern
    return match_found
```

# 