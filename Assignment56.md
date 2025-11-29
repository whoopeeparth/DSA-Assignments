# Assignment 56


## Problem Statement
WAP to simulate a faculty database as a hash table. Search a particular faculty by using 'divide' as a hash function for linear probing with chaining without replacement method of collision handling technique. Assume suitable data for faculty record.

## Theory
1.	This assignment uses a hash table to store faculty records, where each faculty member has attributes such as ID, name, department, qualification, and experience. The Divide Method (also called the Division Method) uses the formula:
2.	Hash Index = Key % Table_Size
3.	which is simple, efficient, and widely used in real-world data structures.
4.	Linear Probing With Chaining Without Replacement
5.	Here, collision handling combines concepts of:
6.	Linear probing → checks next empty slot for insertion
7.	Chaining → keeps a chain (link) for each collided entry
8.	Without replacement → the element originally occupying the hash position is never moved, even if its hash index does not match.
9.	This ensures stable structure, predictable probing, and integrity of initial placements. The method is memory-efficient and improves search stability because elements remain in their original hashed index.

## Code
```cpp
#include <iostream>
#include <string>
using namespace std;

#define SIZE 10

struct Faculty {
    int id;
    string name;
    string dept;
    bool used;
};

Faculty table[SIZE];
int linkArr[SIZE];   

int hashFunc(int id) {
    return id % SIZE; 
}

void init() {
    for (int i = 0; i < SIZE; i++) {
        table[i].used = false;
        linkArr[i] = -1;
    }
}

int findFreeSlot() {
    for (int i = 0; i < SIZE; i++) {
        if (!table[i].used) return i;
    }
    return -1;
}

void insertFaculty(int id, string name, string dept) {
    int home = hashFunc(id);

    if (!table[home].used) {
        table[home] = {id, name, dept, true};
        cout << "Inserted at home slot: " << home << endl;
        return;
    }

    int freeSlot = findFreeSlot();
    if (freeSlot == -1) {
        cout << "Table Full! Cannot insert.\n";
        return;
    }

    table[freeSlot] = {id, name, dept, true};

    int cur = home;
    while (linkArr[cur] != -1)
        cur = linkArr[cur];

    linkArr[cur] = freeSlot;

    cout << "Collision handled. Inserted at: " << freeSlot << endl;
}

void searchFaculty(int id) {
    int home = hashFunc(id);

    int cur = home;
    while (cur != -1) {
        if (table[cur].used && table[cur].id == id) {
            cout << "\nFaculty Found:\n";
            cout << "ID: " << table[cur].id << endl;
            cout << "Name: " << table[cur].name << endl;
            cout << "Dept: " << table[cur].dept << endl;
            return;
        }
        cur = linkArr[cur];
    }

    cout << "Faculty Not Found.\n";
}

void display() {
    cout << "\nIndex   ID     Name     Dept     Link\n";
    for (int i = 0; i < SIZE; i++) {
        cout << i << "\t";
        if (table[i].used)
            cout << table[i].id << "\t" << table[i].name << "\t" << table[i].dept;
        else
            cout << "---\t---\t---";

        cout << "\t" << linkArr[i] << "\n";
    }
}

int main() {
    int ch, id;
    string name, dept;

    init();

    while (true) {
        cout << "\n--- FACULTY HASH TABLE (Divide + Linear Probing + Chaining Without Replacement) ---\n";
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
                display();
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
--- FACULTY HASH TABLE (Divide + Linear Probing + Chaining Without Replacement) ---
1. Insert Faculty
2. Search Faculty
3. Display Table
4. Exit
Enter choice: 1
Enter Faculty ID: 15
Enter Name: Parth
Enter Department: CS
Inserted at home slot: 5

--- FACULTY HASH TABLE (Divide + Linear Probing + Chaining Without Replacement) ---
1. Insert Faculty
2. Search Faculty
3. Display Table
4. Exit
Enter choice: 1
Enter Faculty ID: 25
Enter Name: Yash
Enter Department: IT
Collision handled. Inserted at: 0

--- FACULTY HASH TABLE (Divide + Linear Probing + Chaining Without Replacement) ---
1. Insert Faculty
2. Search Faculty
3. Display Table
4. Exit
Enter choice: 3

Index   ID     Name     Dept     Link
0       25      Yash    IT      -1
1       ---     ---     ---     -1
2       ---     ---     ---     -1
3       ---     ---     ---     -1
4       ---     ---     ---     -1
5       15      Parth   CS      0
6       ---     ---     ---     -1
7       ---     ---     ---     -1
8       ---     ---     ---     -1
9       ---     ---     ---     -1

## Real-Life Applications
•	College faculty management systems
•	Professional organization member records
•	Clinic or hospital doctor indexing
•	Company staff lookup directories
•	Secure access control lists

## Conclusion
Divide hashing with linear probing and chaining without replacement creates a robust faculty database with fast insert and search operations. This method reduces structural disturbances and suits systems needing consistent, predictable search performance.