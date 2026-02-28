# Adaptive Sorting Strategy Lab

cpp```
#include <iostream>
#include <vector>
#include <string>
#include <limits>

using namespace std;

static const int N = 50;
static const int THRESH_NEARLY_SORTED = 2; // Threshold used to define "nearly sorted"

// ------------------------------------------------------------
// Count adjacent inversions (required for both Part A and Part B)
// ------------------------------------------------------------
int countAdjacentInversions(const vector<int>& a) {
    int bad = 0;
    for (int i = 0; i < (int)a.size() - 1; i++) {
        if (a[i] > a[i + 1]) bad++;
    }
    return bad;
}

// ------------------------------------------------------------
// Classify case type (required for both Part A and Part B)
// ------------------------------------------------------------
string classifyCase(int adjBad, int n) {
    if (adjBad == 0) return "Best Case (already sorted)";
    if (adjBad <= THRESH_NEARLY_SORTED) return "Best Case (nearly sorted)";
    if (adjBad == n - 1) return "Worst Case (strictly descending)";
    return "Average Case";
}

// ------------------------------------------------------------
// Insertion Sort implementation (required for Part A)
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
// Selection Sort implementation (required for Part A)
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
// Shared input function (required for both Part A and Part B)
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

