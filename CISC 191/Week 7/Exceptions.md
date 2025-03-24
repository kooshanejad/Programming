# Exceptions

1. Flowchart:   
![Exceptions](https://github.com/user-attachments/assets/51c84f3c-c86e-4893-8a28-860a930aa7ba)
2. My challenges involved going through earlier labs to remember some basics.
3. Video: https://youtu.be/YckSeiwKd5o
4. Code:
```java
public class Pedometer {
    public static double stepsToMiles(int steps) throws Exception {
        if (steps < 0) {
            throw new Exception("Exception: Negative step count entered.");
        }
        return steps / 2000.0;
    }
}

import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner input = new Scanner(System.in);

        System.out.println("Enter the number of steps walked: ");
        int steps = input.nextInt();

        try {
            double miles = Pedometer.stepsToMiles(steps);
            System.out.printf("Miles walked: %.2f", miles);
        } catch (Exception e) {
            System.out.println(e.getMessage());
        }
        input.close();
    }
}
```
