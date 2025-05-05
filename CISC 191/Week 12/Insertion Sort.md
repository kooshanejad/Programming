# Insertion Sort

1. Flowchart:   
![Insertion Sort](https://github.com/user-attachments/assets/26cab6e3-7dd6-45a9-accb-aad0ed82c633)
2. My main challenge in this lab was figuring out how the insertion sort algorithm worked based on the lecture and adjusting it to fit the requirements for the lab.
3. Video: https://youtube.com/shorts/F6XIa33FUR8?feature=share
4. Code:
```java
import java.util.Scanner;

public class InsertionSort {
    public static void insertionSort(int[] array) {
        int comparisons = 0;
        int swaps = 0;

        // Perform insertion sort on array
        for (int i = 1; i < array.length; ++i) {
            int j = i;
            while (j > 0) {
                comparisons++;  // Count comparisons

                if (array[j] < array[j - 1]) {
                    // Swap
                    int temp = array[j];
                    array[j] = array[j - 1];
                    array[j - 1] = temp;
                    swaps++;
                    --j;
                } else {
                    break;
                }
            }

            // Print array after each outer loop iteration
            for (int k = 0; k < array.length; k++) {
                System.out.print(array[k] + " ");
            }
            System.out.println();
        }

        System.out.println();
        System.out.println("comparisons: " + comparisons);
        System.out.println("swaps: " + swaps);
    }

    public static void main(String[] args) {
         Scanner input = new Scanner(System.in);
         int size = input.nextInt();
         int[] array = new int[size];

         // get user input for array values
         for (int i = 0; i < size; i++) {
             array[i] = input.nextInt();
         }

         // print unsorted array
         for (int i = 0; i < array.length; i++) {
             System.out.print(array[i] + " ");
         }
         System.out.println();
         System.out.println();

         insertionSort(array);
         input.close();
    }
}
``` 
