# Assignment 58


## Problem Statement
WAP to simulate employee databases as a hash table. Search a particular faculty by using Mid square method as a hash function for linear probing method of collision handling technique. Assume suitable data for faculty record.

## Theory
The Mid-Square Method is a powerful hashing technique that works by:
1.	Squaring the key
2.	Extracting the middle digits
3.	Applying modulo with table size
This produces well-distributed hash values and significantly reduces collision probability, even for structured numeric keys like employee IDs.
Linear Probing handles collisions by searching sequentially for the next empty slot. This combination ensures:
•	Good randomness
•	Low collision rate
•	Predictable search behavior
Mid-square hashing is ideal when input keys follow patterns (e.g., sequential employee IDs), because the squaring step breaks the patterns.

## Code
```cpp
#include <iostream>
#include <string>
using namespace std;

const int SIZE = 10;

struct Employee {
    int id;
    string name;
    float salary;
    bool occupied;

    Employee() {
        id = -1;
        name = "";
        salary = 0;
        occupied = false;
    }
};

Employee table[SIZE];

int midSquareHash(int key) {
    long long sq = (long long)key * key;     
    string s = to_string(sq);

    int len = s.length();
    if (len == 1) return sq % SIZE;

    if (len % 2 == 0) {
        int mid = len / 2;
        int num = stoi(s.substr(mid - 1, 2));
        return num % SIZE;
    } else {
        int mid = len / 2;
        int num = s[mid] - '0';
        return num % SIZE;
    }
}

void insertEmployee() {
    int id;
    string name;
    float sal;

    cout << "Enter Employee ID: ";
    cin >> id;
    cout << "Enter Name: ";
    cin >> name;
    cout << "Enter Salary: ";
    cin >> sal;

    int index = midSquareHash(id);

    cout << "Initial index (Mid-square hash): " << index << endl;

    int start = index;
    while (table[index].occupied) {
        index = (index + 1) % SIZE;
        if (index == start) {
            cout << "Hash Table Full! Cannot insert.\n";
            return;
        }
    }

    table[index].id = id;
    table[index].name = name;
    table[index].salary = sal;
    table[index].occupied = true;

    cout << "Inserted at index: " << index << endl;
}

void searchEmployee() {
    int id;
    cout << "Enter Employee ID to search: ";
    cin >> id;

    int index = midSquareHash(id);

    int start = index;
    while (table[index].occupied) {
        if (table[index].id == id) {
            cout << "Employee Found at index " << index << endl;
            cout << "ID: " << table[index].id 
                 << "  Name: " << table[index].name
                 << "  Salary: " << table[index].salary << endl;
            return;
        }
        index = (index + 1) % SIZE;
        if (index == start) break;
    }

    cout << "Employee Not Found.\n";
}

void displayTable() {
    cout << "\nIndex\tID\tName\tSalary\n";
    for (int i = 0; i < SIZE; i++) {
        if (table[i].occupied)
            cout << i << "\t" << table[i].id << "\t" << table[i].name 
                 << "\t" << table[i].salary << endl;
        else
            cout << i << "\t---\t---\t---\n";
    }
}

int main() {
    int choice;
    do {
        cout << "\n--- EMPLOYEE HASH TABLE ---\n";
        cout << "1. Insert Employee\n";
        cout << "2. Search Employee\n";
        cout << "3. Display Table\n";
        cout << "4. Exit\n";
        cout << "Enter choice: ";
        cin >> choice;

        switch (choice) {
            case 1: 
                insertEmployee(); 
                break;
            case 2: 
                searchEmployee(); 
                break;
            case 3: 
                displayTable(); 
                break;
            case 4: 
                cout << "Exiting...\n"; 
                break;
            default: 
                cout << "Invalid choice!\n";
        }
    } while (choice != 4);

    return 0;
}

```

## Output
--- EMPLOYEE HASH TABLE ---
1. Insert Employee
2. Search Employee
3. Display Table
4. Exit
Enter choice: 1
Enter Employee ID: 15
Enter Name: Parth
Enter Salary: 100000
Initial index (Mid-square hash): 2
Inserted at index: 2

--- EMPLOYEE HASH TABLE ---
1. Insert Employee
2. Search Employee
3. Display Table
4. Exit
Enter choice: 1
Enter Employee ID: 25
Enter Name: Yash
Enter Salary: 120000
Initial index (Mid-square hash): 2
Inserted at index: 3

--- EMPLOYEE HASH TABLE ---
1. Insert Employee
2. Search Employee
3. Display Table
4. Exit
Enter choice: 3

Index   ID      Name    Salary
0       ---     ---     ---
1       ---     ---     ---
2       15      Parth   100000
3       25      Yash    120000
4       ---     ---     ---
5       ---     ---     ---
6       ---     ---     ---
7       ---     ---     ---
8       ---     ---     ---
9       ---     ---     ---

## Real-Life Applications
•	Employee management systems
•	Government personnel databases
•	Bank employee/branch record indexing
•	Telecom subscriber workforce management
•	Industrial HR software

## Conclusion
Mid-Square hashing provides excellent distribution even for patterned employee IDs, making it ideal for employee databases where high search performance must be maintained.