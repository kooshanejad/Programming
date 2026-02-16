# Linear and Binary Search Lab

1. To perform a linear search for the number 8 in the ordered array, [2, 4, 6, 8, 10, 12, 13], it would take four steps.
2. For the previous example, binary search would take one step.
3. The maximum number of steps it would take to perform a binary search on an array of size 100,000 is 17. You get this answer by calculating log base 2 of 100,000, which gives you 16.6, and you round to 17 because the number of steps must be a whole number.
4.
```cpp
#include <iostream>
#include <vector>

using namespace std;

// Linear Search Function
// Searches each element sequentially until the target is found
// Time complexity: O(N) in the worst case
int linearSearch(const vector<int>& arr, int target, int& comparisons) {
    // Iterate through entire array
    for (int i = 0; i < (int)arr.size(); i++) {
        comparisons++;  // Count each comparison made

        // If current element matches target, return index
        if (arr[i] == target) {
            return i;
        }
    }

    // Return -1 if target is not found
    return -1;
}

// Binary Search Function
// Requires sorted array
// Repeatedly divides the search space in half
// Time complexity: O(log N) in the worst case
int binarySearch(const vector<int>& arr, int target, int& comparisons) {
    int left = 0;                          // Starting index
    int right = (int)arr.size() - 1;       // Ending index

    // Continue searching while valid range exists
    while (left <= right) {
        int mid = (left + right) / 2;      // Find middle index
        comparisons++;                     // Count comparison

        // If middle element matches target, return index
        if (arr[mid] == target) {
            return mid;
        }
        // If target is greater, search right half
        else if (arr[mid] < target) {
            left = mid + 1;
        }
        // If target is smaller, search left half
        else {
            right = mid - 1;
        }
    }

    // Return -1 if target is not found
    return -1;
}

int main() {

    // Create sorted dataset of 100,000 distinct elements
    vector<int> arr(100000);
    for (int i = 0; i < 100000; i++) {
        arr[i] = i;  // Fill with values 0 to 99999
    }

    int target = 99999;  // Choose worst-case for linear search

    int linearComparisons = 0;   // Tracks comparisons for linear search
    int binaryComparisons = 0;   // Tracks comparisons for binary search

    // Perform linear search
    int linearIndex = linearSearch(arr, target, linearComparisons);

    // Perform binary search
    int binaryIndex = binarySearch(arr, target, binaryComparisons);

    // Output results
    cout << "Linear search index: " << linearIndex
         << ", comparisons: " << linearComparisons << endl;

    cout << "Binary search index: " << binaryIndex
         << ", comparisons: " << binaryComparisons << endl;

    return 0;  // End program
}
```

The observed behavior matches the theoretical Big-O time complexities of the algorithms. Linear search exhibits O(N) complexity because, in the worst-case scenario, the algorithm must examine every element in the array before finding the target (or determining it is not present). As the array size increases, the number of comparisons increases proportionally. For example, in an array of 100,000 elements, linear search required 100,000 comparisons in the worst case. Therefore, its time complexity grows linearly in relation to N. Binary search, on the other hand, exhibits O(log N) complexity; instead of checking each element sequentially, binary search repeatedly divides the search space in half. With each iteration, half of the remaining elements are eliminated from the search. Since the array is sorted, this halving process significantly reduces the number of comparisons needed. In an array of 100,000 elements, binary search required only 17 comparisons in the worst case. Seeing as the number of steps increases logarithmically as N grows, the time complexity of binary search is O(log N).

5. Pseudocode:
randomized_search(A, target):
    N = length(A)

    // build index list
    idx = [0, 1, 2, ..., N-1]

    // shuffle idx (Fisher–Yates)
    for i from N-1 down to 1:
        j = random integer in [0, i]
        swap idx[i] and idx[j]

    comparisons = 0
    for k from 0 to N-1:
        comparisons = comparisons + 1
        if A[idx[k]] == target:
            return (idx[k], comparisons)

    return (-1, comparisons)

Best case: O(1)
The best case happens when the first randomly selected index contains the target, so only one comparison is needed.

Average case: O(N)
On average, the target will be found after examining about half the elements (~N/2 comparisons). Big-O notation ignores constant factors, so this is O(N).

Worst case: O(N)
The worst case happens when the target is the last element checked (or not present). Since indices are chosen without repetition and each element is examined once at most, the algorithm may need to examine all N elements, so its time complexity is O(N).

```cpp
#include <iostream>
#include <vector>
#include <random>

using namespace std;

// Linear Search Function
// Searches each element sequentially until the target is found
// Time complexity: O(N) in the worst case
int linearSearch(const vector<int>& arr, int target, int& comparisons) {
    // Iterate through entire array
    for (int i = 0; i < (int)arr.size(); i++) {
        comparisons++;  // Count each comparison made

        // If current element matches target, return index
        if (arr[i] == target) {
            return i;
        }
    }

    // Return -1 if target is not found
    return -1;
}

// Binary Search Function
// Requires sorted array
// Repeatedly divides the search space in half
// Time complexity: O(log N) in the worst case
int binarySearch(const vector<int>& arr, int target, int& comparisons) {
    int left = 0;                          // Starting index
    int right = (int)arr.size() - 1;       // Ending index

    // Continue searching while valid range exists
    while (left <= right) {
        int mid = (left + right) / 2;      // Find middle index
        comparisons++;                     // Count comparison

        // If middle element matches target, return index
        if (arr[mid] == target) {
            return mid;
        }
        // If target is greater, search right half
        else if (arr[mid] < target) {
            left = mid + 1;
        }
        // If target is smaller, search left half
        else {
            right = mid - 1;
        }
    }

// Randomized search without repetition:
// 1) Build an index list [0..N-1]
// 2) Shuffle the indices (Fisher-Yates) so the order is random with no repeats
// 3) Check data in that random index order, counting comparisons
int randomizedSearch(const vector<int>& data, int target, int& comparisons) {
    int n = (int)data.size();

    // Create index list: 0, 1, 2, ..., n-1
    vector<int> idx(n);
    for (int i = 0; i < n; i++) {
        idx[i] = i;
    }

    // Set up random engine
    random_device rd;
    mt19937 gen(rd());

    // Fisher-Yates shuffle (no <algorithm> allowed)
    for (int i = n - 1; i > 0; i--) {
        uniform_int_distribution<int> dist(0, i);
        int j = dist(gen);

        // Manual swap to avoid including <algorithm>
        int temp = idx[i];
        idx[i] = idx[j];
        idx[j] = temp;
    }

    // Search in randomized order (each element examined at most once)
    comparisons = 0;
    for (int k = 0; k < n; k++) {
        comparisons++; // Count the comparison with the target
        if (data[idx[k]] == target) {
            return idx[k]; // Return the index in the original data vector
        }
    }

    return -1; // Target not found
}


    // Return -1 if target is not found
    return -1;
}

int main() {

    // Create sorted dataset of 100,000 distinct elements
    vector<int> arr(100000);
    for (int i = 0; i < 100000; i++) {
        arr[i] = i;  // Fill with values 0 to 99999
    }

    int target = 99999;  // Choose worst-case for linear search

    int linearComparisons = 0;   // Tracks comparisons for linear search
    int binaryComparisons = 0;   // Tracks comparisons for binary search

    // Perform linear search
    int linearIndex = linearSearch(arr, target, linearComparisons);

    // Perform binary search
    int binaryIndex = binarySearch(arr, target, binaryComparisons);

    // Output results
    cout << "Linear search index: " << linearIndex
         << ", comparisons: " << linearComparisons << endl;

    cout << "Binary search index: " << binaryIndex
         << ", comparisons: " << binaryComparisons << endl;

// Track the # of comparisons made by the randomized search
int randomComparisons = 0;

// Perform randomized search on the same dataset and target
int randomIndex = randomizedSearch(arr, target, randomComparisons);

// Output the results of the randomized search
cout << "Randomized search index: " << randomIndex
     << ", comparisons: " << randomComparisons << endl;

    return 0;  
}
```
