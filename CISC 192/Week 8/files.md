# Files

Screenshot:   
Video:
```cpp
#include <iostream>
#include <fstream>
#include <string>

using namespace std;

int main() {
    string filename;

    try {
        // Step 1: Prompt user for filename
        cout << "Enter a filename to create: ";
        getline(cin, filename);

        // Step 2: Create and write to file
        ofstream outfile;
        outfile.exceptions(ios::failbit | ios::badbit); // enable exceptions

        outfile.open(filename, ios::out);
        for (int i = 1; i <= 3; ++i) {
            string line;
            cout << "Enter line " << i << ": ";
            getline(cin, line);
            outfile << line << "\n";
        }
        outfile.close();

        // Step 4: Read contents
        ifstream infile;
        infile.exceptions(ios::failbit | ios::badbit); // enable exceptions

        infile.open(filename, ios::in);
        cout << "\nReading contents:\n";
        string line;
        while (getline(infile, line)) {
            cout << line << "\n";
        }
        infile.close();

        // Step 5: Append one more line
        cout << "\nAppending to file...\n";
        outfile.open(filename, ios::app);
        cout << "Enter one more line: ";
        getline(cin, line);
        outfile << line << "\n";
        outfile.close();

        // Step 6: Read updated contents
        infile.open(filename, ios::in);
        cout << "\nUpdated contents:\n";
        while (getline(infile, line)) {
            cout << line << "\n";
        }
        infile.close();
    }
    catch (const ios_base::failure& e) {
        cerr << "File I/O error: " << e.what() << "\n";
    }

    return 0;
}

```
