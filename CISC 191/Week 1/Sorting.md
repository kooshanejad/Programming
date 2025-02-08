# Sorting Activity

1)
![Sorting drawio](https://github.com/user-attachments/assets/07682c48-e6bd-42ed-8d62-1331801b8732)

2) I chose the bubble sort algorithm because it is the first one I learned in Java and the one I am most familiar with.
3) My main challenge in performing this lab was remembering the basics, as I had forgotten a lot over break and had to look back at my labs from my previous Java class.
4) https://youtu.be/LflBoNq6OHs

## This is my sorting activity code:

```java

import java.util.Scanner;

public class Sorting {

    public static void sortArray(int[] myArr, int arrSize) {
        for (int i = 0; i < arrSize - 1; i++) {
            for (int j = 0; j < arrSize - 1 - i; j++) {
                if (myArr[j] < myArr[j + 1]) {
                    int temp = myArr[j];
                    myArr[j] = myArr[j + 1];
                    myArr[j + 1] = temp;
                }
            }
        }
    }

    public static void main(String[] args) {
        // create Scanner
        Scanner input = new Scanner (System.in);

        // read number of elements
        System.out.print("Enter the number of elements: ");
        int arrSize = input.nextInt();

        // create array to store input values
        int[] myArr = new int[arrSize];

        // read elements into array
        System.out.println("Enter the elements: ");
        for (int i = 0; i < arrSize; i++) {
            myArr[i] = input.nextInt();
        }

        // call sortArray
        sortArray(myArr, arrSize);

        // output sorted array
        for (int i = 0; i < arrSize; i++) {
            System.out.print(myArr[i] + " ");
        }

        // close Scanner
        input.close();

    }
}

```
