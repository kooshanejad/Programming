# Collections

1. Flowchart:   
![Collections](https://github.com/user-attachments/assets/2cd11474-524d-4f8d-9b1c-696e3a3b5d22)
2. My main challenges were figuring out my plan for writing the code as well as how to use the syntax for deque and LinkedList.
3. Video: https://youtu.be/oeeM4rpZKyE
4. Code:
```java
import java.util.Deque;
import java.util.LinkedList;
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner input = new Scanner(System.in);
        String line = input.nextLine();

        if (isPalindrome(line)) {
            System.out.println("Yes, " + line + " is a palindrome.");
        } else {
            System.out.println("No, \"" + line + "\" is not a palindrome.");
        }
    }

    public static boolean isPalindrome(String text) {
        Deque<Character> deque = new LinkedList<>();

        // Add letters to the deque
        for (int i = 0; i < text.length(); i++) {
            char c = text.charAt(i);
            if (c >= 'a' && c <= 'z') {
                deque.addLast(c); // add character to back
            }
        }

        // For one-character string
        if (deque.size() == 1) {
            return true;
        }

        // Check for palindrome
        while (deque.size() > 1) {
            char front = deque.removeFirst(); // remove character from front
            char back = deque.removeLast();   // remove character from back
            if (front != back) {
                return false;
            }
        }

        return true;
    }
}
```
