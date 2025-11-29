# Assignment 60


## Problem Statement
Design and implement a smart college placement portal that uses advanced hashing techniques to efficiently manage student placement records with high performance and low collision probability, even under dynamic data growth.

## Theory
•	This assignment introduces a more advanced system:
a smart placement portal that uses hashing to store and retrieve student placement profiles.
•	The system should support:
•	Fast insertion of student records
•	Search operations by name, roll number, email, or CGPA
•	Updating and tracking placement status
•	High performance under dynamic growth
•	Minimal collisions even with large datasets
•	Advanced Hashing Techniques May Include:
•	Double hashing → secondary hashing for collision handling
•	Universal hashing → randomization to avoid patterns
•	Perfect hashing → collision-free lookup for static datasets
•	Rehashing → expanding and rebuilding hash table when load factor becomes high
•	Cuckoo hashing → two-table approach to ensure constant-time worst-case search
•	These modern hashing strategies ensure stability and performance even when thousands of student records are added each year.
•	A placement portal must handle:
•	Resume data
•	Skill tags
•	Company preferences
•	Interview tracking
•	Offers and results
•	Thus, efficient hashing is essential.

## Code
```cpp
#include <iostream>
using namespace std;

struct Student {
    int reg;         
    string name;
    string company;
    bool used;        
    bool deleted;     
};

int sizeHT = 10;      
Student* ht = new Student[sizeHT];

int hash1(int key) { return key % sizeHT; }
int hash2(int key) { return 7 - (key % 7); }  

void rehash();

void insertStudent() {
    int reg;
    string name, comp;

    cout << "Enter Registration No: ";
    cin >> reg;
    cout << "Enter Name: ";
    cin >> name;
    cout << "Enter Placed Company: ";
    cin >> comp;

    int index = hash1(reg);
    int step  = hash2(reg);

    int start = index;
    int i = 0;

    while (ht[index].used && !ht[index].deleted && ht[index].reg != reg) {
        index = (start + i * step) % sizeHT;
        i++;
        if (i >= sizeHT) { 
            cout << "Table Full! Rehashing...\n";
            rehash();
            insertStudent();
            return;
        }
    }

    ht[index].reg = reg;
    ht[index].name = name;
    ht[index].company = comp;
    ht[index].used = true;
    ht[index].deleted = false;

    cout << "Inserted at index " << index << endl;
}

void searchStudent() {
    int reg;
    cout << "Enter Registration No to Search: ";
    cin >> reg;

    int index = hash1(reg);
    int step  = hash2(reg);
    int start = index;
    int i = 0;

    while (ht[index].used) {
        if (!ht[index].deleted && ht[index].reg == reg) {
            cout << "Found at index " << index << endl;
            cout << "Name: " << ht[index].name 
                 << "  Company: " << ht[index].company << endl;
            return;
        }
        index = (start + i * step) % sizeHT;
        i++;
        if (i >= sizeHT) break;
    }

    cout << "Record NOT Found.\n";
}

void deleteStudent() {
    int reg;
    cout << "Enter Registration No to Delete: ";
    cin >> reg;

    int index = hash1(reg);
    int step  = hash2(reg);
    int start = index;
    int i = 0;

    while (ht[index].used) {
        if (!ht[index].deleted && ht[index].reg == reg) {
            ht[index].deleted = true;
            cout << "Record Deleted at index " << index << endl;
            return;
        }
        index = (start + i * step) % sizeHT;
        i++;
        if (i >= sizeHT) break;
    }
    cout << "Record Not Found.\n";
}

void display() {
    cout << "\nIndex | Reg | Name | Company\n";
    for (int i = 0; i < sizeHT; i++) {
        if (ht[i].used && !ht[i].deleted)
            cout << i << " -> " << ht[i].reg << "  " 
                 << ht[i].name << "  " << ht[i].company << endl;
        else
            cout << i << " -> ---" << endl;
    }
}

void rehash() {
    int oldSize = sizeHT;
    sizeHT = sizeHT * 2;        
    Student* oldTable = ht;

    ht = new Student[sizeHT];
    for (int i = 0; i < sizeHT; i++) {
        ht[i].used = false;
        ht[i].deleted = false;
    }

    for (int i = 0; i < oldSize; i++) {
        if (oldTable[i].used && !oldTable[i].deleted) {
            int reg = oldTable[i].reg;
            int index = hash1(reg);
            int step  = hash2(reg);
            int start = index;
            int j = 0;

            while (ht[index].used) {
                index = (start + j * step) % sizeHT;
                j++;
            }

            ht[index] = oldTable[i];
        }
    }
    delete[] oldTable;
    cout << "Rehashed to size " << sizeHT << endl;
}

int main() {
    for (int i = 0; i < sizeHT; i++) {
        ht[i].used = false;
        ht[i].deleted = false;
    }

    int ch;
    while (true) {
        cout << "\n--- Smart Placement Portal (Advanced Hashing) ---\n";
        cout << "1. Insert Student\n";
        cout << "2. Search Student\n";
        cout << "3. Delete Student\n";
        cout << "4. Display Table\n";
        cout << "5. Exit\n";
        cout << "Enter choice: ";
        cin >> ch;

        switch (ch) {
            case 1: 
                insertStudent(); 
                break;
            case 2: 
                searchStudent(); 
                break;
            case 3: 
                deleteStudent(); 
                break;
            case 4: 
                display(); 
                break;
            case 5: 
                cout << "Exiting...\n"; 
                return 0;
            default: 
                cout << "Invalid choice!\n";
        }
    }
}

```

## Output
--- Smart Placement Portal (Advanced Hashing) ---
1. Insert Student
2. Search Student
3. Delete Student
4. Display Table
5. Exit
Enter choice: 1
Enter Registration No: 15
Enter Name: Parth
Enter Placed Company: Apple
Inserted at index 5

--- Smart Placement Portal (Advanced Hashing) ---
1. Insert Student
2. Search Student
3. Delete Student
4. Display Table
5. Exit
Enter choice: 1
Enter Registration No: 25
Enter Name: Yash
Enter Placed Company: Google
Inserted at index 8

--- Smart Placement Portal (Advanced Hashing) ---
1. Insert Student
2. Search Student
3. Delete Student
4. Display Table
5. Exit
Enter choice: 1
Enter Registration No: 35
Enter Name: Prasad
Enter Placed Company: Microsoft
Inserted at index 2

--- Smart Placement Portal (Advanced Hashing) ---
1. Insert Student
2. Search Student
3. Delete Student
4. Display Table
5. Exit
Enter choice: 4

Index | Reg | Name | Company
0 -> ---
1 -> ---
2 -> 35  Prasad  Microsoft
3 -> ---
4 -> ---
5 -> 15  Parth  Apple
6 -> ---
7 -> ---
8 -> 25  Yash  Google
9 -> ---

--- Smart Placement Portal (Advanced Hashing) ---
1. Insert Student
2. Search Student
3. Delete Student
4. Display Table
5. Exit
Enter choice: 3
Enter Registration No to Delete: 25
Record Deleted at index 8

--- Smart Placement Portal (Advanced Hashing) ---
1. Insert Student
2. Search Student
3. Delete Student
4. Display Table
5. Exit
Enter choice: 4

Index | Reg | Name | Company
0 -> ---
1 -> ---
2 -> 35  Prasad  Microsoft
3 -> ---
4 -> ---
5 -> 15  Parth  Apple
6 -> ---
7 -> ---
8 -> ---
9 -> ---

## Real-Life Applications
•	College placement cell software
•	Talent acquisition platforms (LinkedIn, Naukri, Indeed)
•	Recruitment tracking systems used by HR
•	Enterprise-level applicant management systems
•	Skill-based filtering engines for job portals

## Conclusion
Building a placement portal using modern hashing ensures extremely fast search, robust collision management, and excellent scaling. This results in a high-performance system capable of handling real-time placement data and thousands of student profiles smoothly.