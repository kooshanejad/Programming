# Merge Sort

1. Flowchart:

2. My main challenge in this lab was figuring out how the merge sort algorithm works using the example code from the lecture and then adjusting the code to fit the requirements for the lab.
3. Video:
4. Code:
```java
import java.util.Scanner;

public class MergeSort {
    static int comparisons = 0;
    public static void merge(int [] array, int i, int j, int k) {
        int mergedSize = k - i + 1;       // Size of merged partition
        int mergedNumbers [] = new int[mergedSize]; // Temporary array for merged numbers
        int mergePos;                     // Position to insert merged number
        int leftPos;                      // Position of elements in left partition
        int rightPos;                     // Position of elements in right partition

        mergePos = 0;
        leftPos = i;                      // Initialize left partition position
        rightPos = j + 1;                 // Initialize right partition position

        // Add smallest element from left or right partition to merged numbers
        while (leftPos <= j && rightPos <= k) {
            comparisons++;
            if (array[leftPos] < array[rightPos]) {
                mergedNumbers[mergePos] = array[leftPos];
                ++leftPos;
            }
            else {
                mergedNumbers[mergePos] = array[rightPos];
                ++rightPos;
            }
            ++mergePos;
        }

        // If left partition is not empty, add remaining elements to merged numbers
        while (leftPos <= j) {
            mergedNumbers[mergePos] = array[leftPos];
            ++leftPos;
            ++mergePos;
        }

        // If right partition is not empty, add remaining elements to merged numbers
        while (rightPos <= k) {
            mergedNumbers[mergePos] = array[rightPos];
            ++rightPos;
            ++mergePos;
        }

        // Copy merge number back to numbers
        for (mergePos = 0; mergePos < mergedSize; ++mergePos) {
            array[i + mergePos] = mergedNumbers[mergePos];
        }
    }

    public static void mergeSort(int [] array, int i, int k) {
        int j;

        if (i < k) {
            j = (i + k) / 2;  // Find the midpoint in the partition

            // Recursively sort left and right partitions
            mergeSort(array, i, j);
            mergeSort(array, j + 1, k);

            // Merge left and right partition in sorted order
            merge(array, i, j, k);
        }
    }

    public static void main(String[] args) {
        Scanner input = new Scanner(System.in);
        int size = input.nextInt();
        int[] array = new int[size];

        // Get user input for array values
        for (int i = 0; i < size; i++) {
            array[i] = input.nextInt();
        }

        // Print unsorted array
        System.out.print("unsorted: ");
        for (int i = 0; i < array.length; ++i) {
            System.out.print(array[i] + " ");
        }
        System.out.println();

        mergeSort(array, 0, array.length - 1);

        // Print sorted array
        System.out.print("\nsorted:   ");
        for (int i = 0; i < array.length; ++i) {
            System.out.print(array[i] + " ");
        }

        System.out.println("\ncomparisons: " + comparisons);

        input.close();
    }
}
```
