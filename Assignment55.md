# Assignment 55


## Problem Statement
WAP to simulate a faculty database as a hash table. Search a particular faculty by using MOD as a hash function for linear probing method of collision handling technique. Assume suitable data for faculty record.

## Theory
•	A faculty database can be efficiently implemented using a hash table where faculty IDs (or employee codes) are hashed to array indices. The MOD hash function:
•	index = faculty_id % table_size
•	is simple, fast, and widely used. Since collisions are inevitable, linear probing is applied to handle them by checking sequential slots.
•	This ensures:
•	Fast faculty lookup
•	Efficient insertion without restructuring
•	Minimal memory overhead
•	Faculty records may contain fields such as:
•	Name
•	Department
•	Qualification
•	Experience
•	Office number
•	Hashing makes this data instantly searchable.

## Code
```cpp
#include <iostream>
#include <string>
using namespace std;

struct Faculty {
    int id;
    string name;
    string dept;
    bool used;  
};

Faculty table[20];   

int hashFunction(int id) {
    return id % 20;     
}

void initTable() {
    for (int i = 0; i < 20; i++) {
        table[i].used = false;
    }
}

void insertFaculty(int id, string name, string dept) {
    int index = hashFunction(id);

    for (int i = 0; i < 20; i++) {
        int newIndex = (index + i) % 20;

        if (!table[newIndex].used) {
            table[newIndex].id = id;
            table[newIndex].name = name;
            table[newIndex].dept = dept;
            table[newIndex].used = true;
            cout << "Inserted at position " << newIndex << endl;
            return;
        }
    }

    cout << "Hash Table is Full! Cannot insert.\n";
}

void searchFaculty(int id) {
    int index = hashFunction(id);

    for (int i = 0; i < 20; i++) {
        int newIndex = (index + i) % 20;

        if (table[newIndex].used && table[newIndex].id == id) {
            cout << "\nFaculty Found:\n";
            cout << "ID: " << table[newIndex].id << endl;
            cout << "Name: " << table[newIndex].name << endl;
            cout << "Dept: " << table[newIndex].dept << endl;
            return;
        }
    }

    cout << "Faculty Not Found.\n";
}

void displayTable() {
    cout << "\nHash Table (Faculty Records):\n";
    for (int i = 0; i < 20; i++) {
        cout << i << ": ";
        if (table[i].used) {
            cout << "[" << table[i].id << ", " 
                 << table[i].name << ", "
                 << table[i].dept << "]";
        } else {
            cout << "EMPTY";
        }
        cout << endl;
    }
}

int main() {
    int ch, id;
    string name, dept;

    initTable();

    while (true) {
        cout << "\n--- FACULTY HASH TABLE (LINEAR PROBING) ---\n";
        cout << "1. Insert Faculty\n";
        cout << "2. Search Faculty\n";
        cout << "3. Display Table\n";
        cout << "4. Exit\n";
        cout << "Enter choice: ";
        cin >> ch;

        switch (ch) {
            case 1:
                cout << "Enter Faculty ID: ";
                cin >> id;
                cout << "Enter Name: ";
                cin >> name;
                cout << "Enter Department: ";
                cin >> dept;
                insertFaculty(id, name, dept);
                break;

            case 2:
                cout << "Enter ID to search: ";
                cin >> id;
                searchFaculty(id);
                break;

            case 3:
                displayTable();
                break;

            case 4:
                cout << "Exiting...\n";
                return 0;

            default:
                cout << "Invalid choice!\n";
        }
    }
}

```

## Output
--- FACULTY HASH TABLE (LINEAR PROBING) ---
1. Insert Faculty
2. Search Faculty
3. Display Table
4. Exit
Enter choice: 1
Enter Faculty ID: 15
Enter Name: Parth
Enter Department: CS
Inserted at position 15

--- FACULTY HASH TABLE (LINEAR PROBING) ---
1. Insert Faculty
2. Search Faculty
3. Display Table
4. Exit
Enter choice: 1
Enter Faculty ID: 25
Enter Name: Yash
Enter Department: IT
Inserted at position 5

--- FACULTY HASH TABLE (LINEAR PROBING) ---
1. Insert Faculty
2. Search Faculty
3. Display Table
4. Exit
Enter choice: 1
Enter Faculty ID: 22
Enter Name: Prasad
Enter Department: AI
Inserted at position 2

--- FACULTY HASH TABLE (LINEAR PROBING) ---
1. Insert Faculty
2. Search Faculty
3. Display Table
4. Exit
Enter choice: 3

Hash Table (Faculty Records):
0: EMPTY
1: EMPTY
2: [22, Prasad, AI]
3: EMPTY
4: EMPTY
5: [25, Yash, IT]
6: EMPTY
7: EMPTY
8: EMPTY
9: EMPTY
10: EMPTY
11: EMPTY
12: EMPTY
13: EMPTY
14: EMPTY
15: [15, Parth, CS]
16: EMPTY
17: EMPTY
18: EMPTY
19: EMPTY

## Real-Life Applications
•	College administrative software
•	Employee management systems
•	Corporate HR databases
•	Hospital/clinic staff indexing
•	Large organizations managing thousands of employee IDs

## Conclusion
Using a MOD-based hash function with linear probing is an excellent, simple solution for faculty record management. It ensures rapid search and easy maintenance, making it ideal for institutional databases where fast access is essential.