
# EX 2E Pattern Matching using KMP Algorithm.
## DATE: 16.3.26
## AIM:
To write a Java program for the following constraints.
Longest Palindromic Substring
Given a string s, return the longest palindromic substring in s.
using Manacher's Algorithm

## Algorithm
1. Transform the string by inserting # between characters (e.g., "babad" → #b#a#b#a#d#) to handle odd/even palindromes uniformly.

2. Create an array palindromeRadii[] to store the palindrome radius at each index and initialize center = 0, radius = 0.

3. Scan each position i in the transformed string and compute its mirror index using mirror = 2 * center - i.

4. If i is within the current right boundary radius, initialize palindromeRadii[i] = min(radius - i, palindromeRadii[mirror]).

5. Expand around index i while characters match on both sides and update the radius length for that center. If the palindrome expands beyond the current boundary,
   update center and radius.

6. After scanning all positions, find the index with the maximum radius, convert it back to the corresponding start index in the original string, and return the
   substring. 

## Program:
```
import java.util.Scanner;

public class Solution {
    public String longestPalindrome(String s) {
        
        StringBuilder sPrime = new StringBuilder("#");
        for (char c : s.toCharArray()) {
            sPrime.append(c).append("#");
        }

        int n = sPrime.length();
        int[] palindromeRadii = new int[n];
        int center = 0;
        int radius = 0;

       
        for (int i = 0; i < n; i++) {
            int mirror = 2 * center - i;

            if (i < radius) {
                palindromeRadii[i] = Math.min(radius - i, palindromeRadii[mirror]);
            }

            while (
                i + 1 + palindromeRadii[i] < n &&
                i - 1 - palindromeRadii[i] >= 0 &&
                sPrime.charAt(i + 1 + palindromeRadii[i]) == sPrime.charAt(i - 1 - palindromeRadii[i])
            ) {
                palindromeRadii[i]++;
            }

            if (i + palindromeRadii[i] > radius) {
                center = i;
                radius = i + palindromeRadii[i];
            }
        }

        
        int maxLength = 0;
        int centerIndex = 0;
        for (int i = 0; i < n; i++) {
            if (palindromeRadii[i] > maxLength) {
                maxLength = palindromeRadii[i];
                centerIndex = i;
            }
        }

        int startIndex = (centerIndex - maxLength) / 2;
        return s.substring(startIndex, startIndex + maxLength);
    }

   
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        //System.out.println("Enter a string:");
        String input = scanner.nextLine();

        Solution sol = new Solution();
        String result = sol.longestPalindrome(input);

        System.out.println("Longest Palindromic Substring: " + result);
        scanner.close();
    }
}

```

## Output:

<img width="781" height="305" alt="image" src="https://github.com/user-attachments/assets/d29a698a-aabf-4009-bd76-9b2dd87ea132" />


## Result:
The program successfully implemented and the expected output is verified.
