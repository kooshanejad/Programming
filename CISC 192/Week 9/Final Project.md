# Final Project

```cpp
#include <iostream>
#include <iomanip>
#include <fstream>
#include <string>
#include <limits>
using namespace std;

// Data types, constants
const int MAX_STUDENTS = 50;   // maximum number of students
const int MAX_GRADES   = 5;    // maximum grades per student
const double PASS_THRESHOLD = 60.0; // minimum average to pass

// Struct to represent one student
struct Student {
    string name;                  // String to store names
    int numGrades = 0;            // number of grades entered
    double grades[MAX_GRADES]{};  // Array of grades
    double average = 0.0;         // average grade
    char letter = 'F';            // letter grade
};

// ===============================
// FUNCTIONS
// ===============================

// Function with pointer parameter
// Computes the average of a grade array
double computeAverage(const double* arr, int n) { // 5) Pointers used here
    if (n <= 0) return 0.0;
    double sum = 0.0;
    for (int i = 0; i < n; ++i) { // 3) Iteration
        sum += arr[i];            // 1) Arithmetic
    }
    return sum / n;
}

// Relational and logical operators
// Assigns letter grade based on numeric average
char letterFor(double avg) {
    if      (avg >= 90.0) return 'A';
    else if (avg >= 80.0) return 'B';
    else if (avg >= 70.0) return 'C';
    else if (avg >= 60.0) return 'D';
    else                  return 'F';
}

// Prints details about one student
void printStudent(const Student& s) {
    cout << fixed << setprecision(2); // format averages with 2 decimals
    cout << "Name: " << s.name << " | Grades: ";
    for (int i = 0; i < s.numGrades; ++i) {
        cout << s.grades[i] << (i + 1 < s.numGrades ? ", " : "");
    }
    cout << " | Avg: " << s.average
         << " | Letter: " << s.letter
         // Relational and logical operators
         << " | " << ((s.average >= PASS_THRESHOLD && s.numGrades > 0) ? "PASS" : "FAIL")
         << "\n";
}

// Adds a new student to the roster
void addStudent(Student roster[], int& count) { // Arrays, pointer decay
    if (count >= MAX_STUDENTS) {
        cout << "Roster full.\n";
        return;
    }

    Student s; // Temporary student
    cout << "Enter student name (can include spaces): ";
    getline(cin, s.name); // Use getline for full names

    cout << "How many grades (0-" << MAX_GRADES << ")? ";
    cin >> s.numGrades;
    if (s.numGrades < 0) s.numGrades = 0;
    if (s.numGrades > MAX_GRADES) s.numGrades = MAX_GRADES;

    // Enter each grade
    for (int i = 0; i < s.numGrades; ++i) {
        cout << "  Grade " << (i + 1) << ": ";
        cin >> s.grades[i];
    }
    cin.ignore(numeric_limits<streamsize>::max(), '\n'); // Clear input buffer

    // Compute average and letter grade
    s.average = computeAverage(s.grades, s.numGrades);
    s.letter  = letterFor(s.average);

    // Add student to roster array
    roster[count++] = s;
    cout << "Added.\n";
}

// Lists all students currently in the roster
void listStudents(const Student roster[], int count) {
    if (count == 0) { 
        cout << "No students yet.\n"; 
        return; 
    }

    // Example of pointer iteration
    const Student* p = roster; // Pointer to first student
    for (int i = 0; i < count; ++i, ++p) { // 3) Iteration
        cout << "[" << i << "] ";
        printStudent(*p); // Dereference pointer
    }
}

// Files — saves data to a plain text file
bool saveToFile(const Student roster[], int count, const string& path) {
    ofstream out(path);
    if (!out) return false;

    out << "Student Grade Tracker (simple format)\n";
    out << "COUNT " << count << "\n";

    for (int i = 0; i < count; ++i) {
        out << "NAME " << roster[i].name << "\n";
        out << "N " << roster[i].numGrades << "\n";
        out << "GRADES ";
        for (int g = 0; g < roster[i].numGrades; ++g) {
            out << roster[i].grades[g] << (g + 1 < roster[i].numGrades ? ' ' : '\n');
        }
        out << "AVG " << roster[i].average << "\n";
        out << "LETTER " << roster[i].letter << "\n";
        out << "---\n"; // divider between students
    }
    return true;
}

// Displays menu options
void menu() {
    cout << "\n=== Student Grade Tracker (Intro) ===\n"
         << "1) Add student\n"
         << "2) List students\n"
         << "3) Save to file\n"
         << "0) Quit\n"
         << "Choose: ";
}


int main() {
    Student roster[MAX_STUDENTS]; // Arrays
    int count = 0;                // number of students entered

    bool running = true;
    while (running) {              // Iteration (looping menu)
        menu();
        int choice;
        if (!(cin >> choice)) { // input validation
            cin.clear();
            cin.ignore(numeric_limits<streamsize>::max(), '\n');
            continue;
        }
        cin.ignore(numeric_limits<streamsize>::max(), '\n');

        // Simple menu-driven program
        switch (choice) {
            // Asks user for the student's name and grades, calculates the average, and stores the student in the
            // roster array
            case 1: addStudent(roster, count); break;
            // Prints out all students currently stored in the array
            case 2: listStudents(roster, count); break;
            // Asks user for file name, calls saveToFile(roster, count, path)
            // If saving worked, prints "Saved."; if saving failed, prints "Save failed."
            case 3: {
                string path;
                cout << "Save path (e.g., students.txt): ";
                getline(cin, path);
                if (saveToFile(roster, count, path)) 
                    cout << "Saved.\n";
                else 
                    cout << "Save failed.\n";
                break;
            }
            case 0: running = false; break;
            default: cout << "Invalid choice.\n"; break;
        }
    }

    cout << "Goodbye!\n";
    return 0;
}

```
