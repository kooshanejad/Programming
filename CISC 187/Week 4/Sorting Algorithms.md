# Sorting Algorithms Lab

1. 
```
Start:  [4, 1, 3, 2, 5]
        sorted | unsorted

i=1, key=1:
compare key(1) with 4 -> shift 4 right
        [4, 4, 3, 2, 5]
insert key at index 0
        [1, 4, 3, 2, 5]

i=2, key=3:
compare key(3) with 4 -> shift 4 right
        [1, 4, 4, 2, 5]
compare key(3) with 1 -> stop
insert key at index 1
        [1, 3, 4, 2, 5]

i=3, key=2:
compare key(2) with 4 -> shift
        [1, 3, 4, 4, 5]
compare key(2) with 3 -> shift
        [1, 3, 3, 4, 5]
compare key(2) with 1 -> stop
insert key at index 1
        [1, 2, 3, 4, 5]
```
Each "shift" fixes an inversion. For average or random outputs, the expected number of inversions is N(N-1)/4, so insertion sort performs O(N^2) operations on average.   
2. Worst case array:   
```
[5, 4, 3, 2, 1]
```
If the inspected index starts at 0 instead of 1, the first iteration does no comparisons. The remaining iterations in worst-case descending order still produce 10 comparisons and 10 shifts, totaling 20 operations.    
3. (a) The function's time complexity regarding Big O Notation is O(N), since the loop may examine every character in the string.   
(b) 
