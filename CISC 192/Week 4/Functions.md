# Functions and Argument Declarations

Screenshot:
Video:

```cpp
#include <iostream>
#include <string>
using namespace std;

// Function to return the sum of two integers
int sum(int a, int b) {
    return a + b;
}

// Function to return the square of an integer
int square(int num) {
    return num * num;
}

// Function to print a personalized greeting
void greet(string name) {
    cout << "Hello, " << name << "! Welcome to C++ functions." << endl;
}

int main() {
    int num1, num2;
    string name;

    // Prompt user for first number
    cout << "Enter first number: ";
    cin >> num1;

    // Prompt user for second number
    cout << "Enter second number: ";
    cin >> num2;

    // Call sum function and display result
    cout << "Sum: " << sum(num1, num2) << endl;

    // Call square function using the first input
    cout << "Square of " << num1 << ": " << square(num1) << endl;

    // Prompt user for their name
    cout << "Enter your name: ";
    cin >> name;

    // Call greet function
    greet(name);

    return 0;
}

```
