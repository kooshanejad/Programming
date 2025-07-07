# Iteration Structures

Screenshot:   

Code:   
#include <iostream>
using namespace std;

int main() {
    // start at i=5, increment by 5, end at i=100
    for (int i = 5; i <= 100; i+= 5) {
        cout << i << " ";
    }
    // newline
    cout << endl;

    // variables for number and sum
    int number = 0;
    int sum = 0;

    // while number is non-negative, prompt user to
    // enter another number and assign input to
    // number variable
    while (number >= 0) {
        cout << "Enter a number: ";
        cin >> number;

        // if number is non-negative, add to sum
        if (number >= 0) {
            sum += number;
        }
    }

    // print sum
    cout << "Total sum: " << sum << endl;

    int choice;

    do {
        cout << "1. Say Hello" << endl;
        cout << "2. Exit" << endl;
        cout << "Enter your choice: ";
        cin >> choice;

        if (choice == 1) {
            cout << "Hello!" << endl;
        }
        else if (choice == 2) {
            cout << "Goodbye!" << endl;
        }
    } while (choice == 1);

    // exit program
    return 0;
}
