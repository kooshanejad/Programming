# Linear and Binary Search Lab

1. To perform a linear search for the number 8 in the ordered array, [2, 4, 6, 8, 10, 12, 13], it would take four steps.
2. For the previous example, binary search would take one step.
3. The maximum number of steps it would take to perform a binary search on an array of size 100,000 is 17. You get this answer by calculating log base 2 of 100,000, which gives you 16.6, and you round to 17 because the number of steps must be a whole number.
4.
```cpp
#include <iostream>
#include <vector>

using namespace std;

int linearSearch(const vector<int>& arr, int target, int& comparisons) {
    for (int i = 0; i < (int)arr.size(); i++) {
        comparisons++;
        if (arr[i] == target) {
            return i;
        }
    }
    return -1;
}

int binarySearch(const vector<int>& arr, int target, int& comparisons) {
    int left = 0;
    int right = (int)arr.size() - 1;

    while (left <= right) {
        int mid = (left + right) / 2;
        comparisons++;

        if (arr[mid] == target) {
            return mid;
        } else if (arr[mid] < target) {
            left = mid + 1;
        } else {
            right = mid - 1;
        }
    }
    return -1;
}

int main() {
    vector<int> arr(100000);
    for (int i = 0; i < 100000; i++) {
        arr[i] = i;  // sorted array
    }

    int target = 99999;
    int linearComparisons = 0;
    int binaryComparisons = 0;

    int linearIndex = linearSearch(arr, target, linearComparisons);
    int binaryIndex = binarySearch(arr, target, binaryComparisons);

    cout << "Linear search index: " << linearIndex
         << ", comparisons: " << linearComparisons << endl;

    cout << "Binary search index: " << binaryIndex
         << ", comparisons: " << binaryComparisons << endl;

    return 0;
}
```

The observed behavior matches the theoretical Big-O time complexities of the algorithms. Linear search exhibits O(N) complexity because, in the worst-case scenario, the algorithm must examine every element in the array before finding the target (or determining it is not present). As the array size increases, the number of comparisons increases proportionally. For example, in an array of 100,000 elements, linear search required 100,000 comparisons in the worst case. Therefore, its time complexity grows linearly in relation to N. Binary search, on the other hand, exhibits O(log N) complexity; instead of checking each element sequentially, binary search repeatedly divides the search space in half. With each iteration, half of the remaining elements are eliminated from the search. Since the array is sorted, this halving process significantly reduces the number of comparisons needed. In an array of 100,000 elements, binary search required only 17 comparisons in the worst case. Seeing as the number of steps increases logarithmically as N grows, the time complexity of binary search is O(log N).

5.
