# Arrays

Screenshot:   
Video:

```cpp
#include <iostream>
using namespace std;

// Expands an array by creating a new one with a larger size
int* expandArray(int* oldArray, int oldSize, int newSize) {
    int* newArray = new int[newSize];
    for (int i = 0; i < oldSize; ++i) {
        newArray[i] = oldArray[i];
    }
    delete[] oldArray; // Free the memory of the old array
    return newArray;
}

// Prints elements of the array
void printArray(int* arr, int size) {
    for (int i = 0; i < size; ++i) {
        cout << arr[i] << " ";
    }
    cout << endl;
}

// Returns the sum of the array elements
int sumArray(int* arr, int size) {
    int sum = 0;
    for (int i = 0; i < size; ++i) {
        sum += arr[i];
    }
    return sum;
}

int main() {
    int capacity = 5;                 // Initial capacity
    int* numbers = new int[capacity]; // Allocate dynamic array
    int count = 0;                   // Number of values entered

    cout << "Enter numbers (type -1 to stop):" << endl;

    while (true) {
        int input;
        cout << "> ";
        cin >> input;

        if (input == -1) {
            break; // Stop reading input
        }

        // Check if array is full
        if (count == capacity) {
            // Double the array size
            int newCapacity = capacity * 2;
            numbers = expandArray(numbers, capacity, newCapacity);
            capacity = newCapacity;
        }

        numbers[count] = input; // Store the input
        ++count;
    }

    cout << "\nTotal numbers entered: " << count << endl;
    cout << "You entered: ";
    printArray(numbers, count);
    cout << "Sum: " << sumArray(numbers, count) << endl;

    delete[] numbers; // Free dynamic memory
    return 0;
}
```
