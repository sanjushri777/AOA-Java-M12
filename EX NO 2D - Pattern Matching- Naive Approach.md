
# EX 2D Pattern Matching using Naive Approach.
## DATE: 15.3.26
## AIM:
To write a Java program to for given constraints.
Given text string with length n and a pattern with length m, the task is to prints all occurrences of pattern in text.
Note: You may assume that n > m.

Examples: 

Input:  text = "THIS IS A TEST TEXT", pattern = "TEST"
Output: Pattern found at index 10

Input:  text =  "AABAACAADAABAABA", pattern = "AABA"
Output: Pattern found at index 0, Pattern found at index 9, Pattern found at index 12

## Algorithm
1. Read the text string and pattern string.

2. Compute lengths: n = text.length() and m = pattern.length().

3. Loop i from 0 to n − m (possible starting positions in text).

4. For each i, compare the pattern with the text starting at position i.

5. If all characters match (inner loop completes), report the match index i.

6. Continue until all positions are checked. 

## Program:
```
import java.util.Scanner;

public class NaivePatternSearch {
    static void search(String text,String pattern){
        int n=text.length();
        int m=pattern.length();
        for(int i =0;i<=n-m;i++){
            int j;
            for( j=0;j<m;j++){
                if(text.charAt(i+j) != pattern.charAt(j))
                   break;
            }
            if(j==m)
                System.out.println("Pattern found at index " +i);
}
}
 

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

       
        String text = scanner.nextLine();

        String pattern = scanner.nextLine();

       
        search(text, pattern);

        scanner.close();
    }
}

```

## Output:
<img width="716" height="361" alt="image" src="https://github.com/user-attachments/assets/18502c1c-b457-46b5-b785-46ae1679356c" />



## Result:
The program successfully implemented and the expected output is verified.
