# Space Constraints

## Task 1
This algorithm's space complexity is O(N^2) because the collection array stores combinations for many pairs of elements.

## Task 2
This function's space complexity is O(N) because a brand-new array (newArray) is created that stores all N elements.

## Task 3
```cpp
void reverseArray(int array[], int size) {
    int left = 0;
    int right = size - 1;

    while (left < right) {
        int temp = array[left];
        array[left] = array[right];
        array[right] = temp;

        left++;
        right--;
    }
}
```

## Task 4
```
| Version | Time Complexity | Space Complexity |
|---------|-----------------|-------------------|
| Version #1 | O(N) | O(N) |
| Version #2 | O(N) | O(1) |
| Version #3 | O(N) | O(N) |
```
