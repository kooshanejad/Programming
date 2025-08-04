# Strings

Screenshot:   
Video:   
```cpp
#include <iostream>
#include <string>
#include <cstring> // For strcpy()

int main() {
    std::string firstName, lastName;

    // Step 1: Get user input
    std::cout << "Enter your first name: ";
    std::cin >> firstName;

    std::cout << "Enter your last name: ";
    std::cin >> lastName;

    // Step 2: Combine names
    std::string fullName = firstName + " " + lastName;
    std::cout << "\nFull name: " << fullName << std::endl;

    // Step 3: Copy to C-style string
    const int BUFFER_SIZE = 51; // Max 50 characters + null terminator
    char cString[BUFFER_SIZE];

    if (fullName.length() >= BUFFER_SIZE) {
        std::cerr << "Error: Full name is too long for the buffer." << std::endl;
        return 1;
    }

    strcpy(cString, fullName.c_str());

    // Step 4: Print each character
    std::cout << "Copied to char array:" << std::endl;
    for (int i = 0; cString[i] != '\0'; ++i) {
        std::cout << cString[i] << std::endl;
    }

    return 0;
}
```
