# Array Data Structure Lab
1. 
```cpp
int arr[100];
```
In this line of code, "int" means that the data type for the array is integers. "arr" is the name of the array, and 100 is the number of elements in the array.  
2. 
```cpp
sizeof(int)
``` 
3. For an array containing 100 elements, provide the number of steps the following operations would take:  
Reading: 1 step  
Searching for a value not contained within the array: 100 steps  
Insertion at the beginning of the array: 101 steps  
Insertion at the end of the array: 1 step  
Deletion at the beginning of the array: 99 steps  
Deletion at the end of the array: 1 step  

4. O(N) steps; even if the value appears early, you must still check all N elements to ensure every instance is counted.
5.
```cpp
int arr[100];

cout << arr << endl;
cout << &arr[0] << endl;
```
