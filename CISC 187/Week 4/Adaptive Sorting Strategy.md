# Adaptive Sorting Strategy Lab

## Part A and B
```cpp

#include <iostream>
#include <vector>
#include <string>
#include <limits>

using namespace std;

static const int N = 50;
static const int THRESH_NEARLY_SORTED = 2; // Threshold used to define "nearly sorted"

// ------------------------------------------------------------
// Count adjacent inversions (Part A and B)
// ------------------------------------------------------------
int countAdjacentInversions(const vector<int>& a) {
    int bad = 0;
    for (int i = 0; i < (int)a.size() - 1; i++) {
        if (a[i] > a[i + 1]) bad++;
    }
    return bad;
}

// ------------------------------------------------------------
// Classify case type (Part A and B)
// ------------------------------------------------------------
string classifyCase(int adjBad, int n) {
    if (adjBad == n - 1)
        return "Worst Case";
    return "Average Case";
}

// ------------------------------------------------------------
// Insertion Sort implementation (Part A)
// ------------------------------------------------------------
void insertionSort(vector<int>& a) {
    for (int i = 1; i < (int)a.size(); i++) {
        int key = a[i];
        int j = i - 1;
        while (j >= 0 && a[j] > key) {
            a[j + 1] = a[j];
            j--;
        }
        a[j + 1] = key;
    }
}

// ------------------------------------------------------------
// Selection Sort implementation (Part A)
// ------------------------------------------------------------
void selectionSort(vector<int>& a) {
    int n = (int)a.size();
    for (int i = 0; i < n - 1; i++) {
        int minIndex = i;
        for (int j = i + 1; j < n; j++) {
            if (a[j] < a[minIndex]) {
                minIndex = j;
            }
        }
        int temp = a[i];
        a[i] = a[minIndex];
        a[minIndex] = temp;
    }
}

void printArray(const vector<int>& a) {
    cout << "[";
    for (int i = 0; i < (int)a.size(); i++) {
        cout << a[i];
        if (i != (int)a.size() - 1) cout << ", ";
    }
    cout << "]\n";
}

// ------------------------------------------------------------
// Shared input function (Part A and B)
// ------------------------------------------------------------
vector<int> read50Integers() {
    vector<int> a;
    a.reserve(N);

    cout << "Enter " << N << " integers:\n";
    for (int i = 0; i < N; i++) {
        int x;
        while (!(cin >> x)) {
            cin.clear();
            cin.ignore(numeric_limits<streamsize>::max(), '\n');
            cout << "Invalid input. Please enter an integer: ";
        }
        a.push_back(x);
    }
    return a;
}

int main() {

    cout << "Adaptive Sorting Strategy\n";
    cout << "Choose mode:\n";
    cout << "  A = Part A (analyze + choose algorithm + sort)\n";
    cout << "  B = Part B (classify only, NO sorting)\n";
    cout << "Enter A or B: ";

    char mode;
    cin >> mode;

    if (mode >= 'a' && mode <= 'z') mode = (char)(mode - 'a' + 'A');

    if (mode != 'A' && mode != 'B') {
        cout << "Invalid mode.\n";
        return 0;
    }

    vector<int> arr = read50Integers();

    // ------------------------------------------------------------
    // Shared Analysis Step (Required for both Part A and Part B)
    // ------------------------------------------------------------
    int adjBad = countAdjacentInversions(arr);
    string caseType = classifyCase(adjBad, arr.size());

    cout << "\nAnalysis:\n";
    cout << "Adjacent inversions = " << adjBad << "\n";
    cout << "Classification = " << caseType << "\n";

    // ============================================================
    // ======================= PART B =============================
    // ============================================================
    if (mode == 'B') {
        cout << "\n--- Part B: Case Classification Only ---\n";

        if (adjBad == (int)arr.size() - 1) {
            cout << "Worst Case\n";
        } else {
            cout << "Average Case\n";
        }

        cout << "(No sorting performed in Part B.)\n";
        return 0;
    }

    // ============================================================
    // ======================= PART A =============================
    // ============================================================
    cout << "\n--- Part A: Adaptive Sorting Selection ---\n";
    cout << "Original array: ";
    printArray(arr);

    // Decision logic required in Part A
    if (adjBad <= THRESH_NEARLY_SORTED) {
        cout << "Chosen algorithm: insertion sort\n";
        insertionSort(arr);
    } else if (adjBad == (int)arr.size() - 1) {
        cout << "Chosen algorithm: selection sort\n";
        selectionSort(arr);
    } else {
        cout << "Chosen algorithm: selection sort\n";
        selectionSort(arr);
    }

    cout << "Sorted array:   ";
    printArray(arr);

    return 0;
}
```

## Part C
Threshold definition: I measured how ordered the array is by counting the number of adjacent pairs where A[i] > A[i+1]. I defined adjBad as the number of adjacent inversions. I defined a threshold constant THRESH_NEARLY_SORTED = 2. For N = 50, the array is considered nearly sorted when adjBad ≤ THRESH_NEARLY_SORTED. The worst case scenario occurs when adjBad = N - 1 = 49. Any other value is classified as average case. 

Reasoning behind the assumption: Adjacent inversions are a fast O(N) way to estimate how close the array is to being sorted. If there are very few adjacent inversions, only a few elements are out of place, so insertion sort tends to perform close to its best case. If every adjacent pair is inverted, the input is strictly descending, which is insertion sort's worst case.   

Why the program selects one algorithm over the other: If the array is already sorted or nearly sorted, the program selects insertion sort because insertion sort can run in O(N) time in the best case. If the array is strictly descending (worst case), the program selects selection sort because insertion sort performs many shifts in this scenario, while selection sort's behavior is consistent regardless of input order.   

How input order affects time complexity: Selection sort performs O(N^2) comparisons in best, average, and worst cases because it always scans the remaining unsorted portion to find the next minimum. Insertion sort is adaptive: its time complexity is O(N) in the best case when the array is already sorted, but it becomes O(N^2) in the average and worst cases because elements may need to shift many positions

Video: https://youtu.be/5ku3ZBLwxuE
