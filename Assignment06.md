# Assignment 6


## Problem Statement
In Computer Engg. Dept. of VIT there are S.Y., T.Y., and B.Tech. students. Assume that all these students are on ground for a function. We need to identify a student of S.Y. div. (X) whose name is "XYZ" and roll no. is "17". Apply appropriate Searching method to identify the required student.

## Theory
Linear search is a simple search algorithm that checks each element one by one.  
When using structures, you manually compare all required fields to find the matching record.

## Code
```cpp
#include <iostream>
#include <string>
using namespace std;

struct Student
{
    string name_psk;
    string div_psk;
    int rollNo_psk;
};

int main()
{
    int n_psk = 12;

    Student students[12] = {
        {"ABC", "X", 1},
        {"XYZ", "X", 17},  
        {"DEF", "Y", 5},
        {"GHI", "X", 12},
        {"JKL", "Y", 8},
        {"MNO", "Z", 3},
        {"PQR", "X", 4},
        {"STU", "Y", 15},
        {"VWX", "X", 9},
        {"YZA", "Z", 2},
        {"BCD", "X", 7},
        {"EFG", "Y", 11}
    };

    cout << "All Students:\n";
    for (int i_psk = 0; i_psk < n_psk; i_psk++)
    {
        cout << i_psk << ". Name: " << students[i_psk].name_psk
             << ", Division: " << students[i_psk].div_psk
             << ", RollNo: " << students[i_psk].rollNo_psk << endl;
    }

    bool found_psk = false;
    for (int i_psk = 0; i_psk < n_psk; i_psk++)
    {
        if (students[i_psk].name_psk == "XYZ" &&
            students[i_psk].div_psk == "X" &&
            students[i_psk].rollNo_psk == 17)
        {
            cout << "\nStudent found at index " << i_psk << endl;
            cout << "Name: " << students[i_psk].name_psk
                 << ", Division: " << students[i_psk].div_psk
                 << ", RollNo: " << students[i_psk].rollNo_psk << endl;
            found_psk = true;
            break;
        }
    }

    if (!found_psk)
    {
        cout << "No Student found!" << endl;
        return -2;
    }

    return 0;
}

```
## Output
![Program Output](Assignment6(Output).png)