# Assignment 1

## Problem Statement
Implement basic string operations such as length calculation, copy, reverse, and concatenation using character single dimensional arrays without using built-in string library functions.	

## Theory
This assignment demonstrates how to manually perform string operations using character arrays and loops in C++. The program covers:
- Finding the length of a string
- Copying one string to another
- Concatenating two strings
- Comparing two strings
- Searching for a character in a string

## Code
```cpp
#include <iostream>
using namespace std;

void getString(char str[]) {
    cout << "Enter a string: ";
    cin >> str;
}

int stringLength(char str[]) {
    int length = 0;
    while (str[length] != '\0') {
        length++;
    }
    return length;
}

void stringCopy(char str1[], char str2[]) {
    int i = 0;
    while (str1[i] != '\0') {
        str2[i] = str1[i];
        i++;
    }
    str2[i] = '\0';
}

void stringConcatenate(char str1[], char str2[]) {
    int i = 0, j = 0;
    while (str1[i] != '\0') i++;      
    while (str2[j] != '\0') {
        str1[i] = str2[j];
        i++;
        j++;
    }
    str1[i] = '\0';
}

void stringCompare(char str1[], char str2[]) {
    int i = 0;
    while (str1[i] != '\0' && str2[i] != '\0' && str1[i] == str2[i]) {
        i++;
    }
    if (str1[i] == '\0' && str2[i] == '\0') {
        cout << "Strings are the same\n";
    } else {
        cout << "Strings are not the same\n";
    }
}

void stringSearch(char str[], char c) {
    int found = 0;
    int i = 0;
    while (str[i] != '\0') {
        if (str[i] == c) {
            found = 1;
            break;
        }
        i++;
    }
    if (found) {
        cout << "Match found\n";
    } else {
        cout << "Match not found\n";
    }
}

int main() {
    int choice = 0;
    char str[100], str2[100], s;

    getString(str);

    while (choice != 7) {
        cout << "========================================\n";
        cout << "Select your choice:\n";
        cout << "1. Find String length\n";
        cout << "2. Create String Copy\n";
        cout << "3. Concatenate String\n";
        cout << "4. Compare two Strings\n";
        cout << "5. Search the String\n";
        cout << "6. Re-enter String\n";
        cout << "7. Exit\n";
        cout << "Enter your choice: ";
        cin >> choice;

        switch (choice) {
            case 1:
                cout << "The length of the string is " << stringLength(str) << endl;
                break;
            case 2:
                stringCopy(str, str2);
                cout << "String 2 is: " << str2 << endl;
                break;
            case 3:
                cout << "Enter a string to concatenate to " << str << ": ";
                cin >> str2;
                stringConcatenate(str, str2);
                cout << "String after concatenation: " << str << endl;
                break;
            case 4:
                cout << "Enter a string to compare to " << str << ": ";
                cin >> str2;
                stringCompare(str, str2);
                break;
            case 5:
                cout << "Enter a character to search in string: ";
                cin >> s;
                stringSearch(str, s);
                break;
            case 6:
                getString(str);
                break;
            case 7:
                cout << "Thank you!!\n";
                break;
            default:
                cout << "Invalid choice!!!\n";
        }
    }

    cout << "Made by Siddharth and Parth\n";
    return 0;
}

```
## Output
![Program Output](Assignment1(Output).png)
