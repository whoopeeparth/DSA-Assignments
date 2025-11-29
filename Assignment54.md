# Assignment 54


## Problem Statement
Store and retrieve student records using roll numbers.

## Theory
•	Roll numbers are unique identifiers, making them excellent hash keys. A hash table allows student records—such as name, department, marks, address—to be stored and retrieved efficiently using the roll number as the primary key.
The hash function computes the index based on the roll number (often using modulo operation). Collisions can be resolved through linear probing, quadratic probing, or separate chaining.
•	This enables O(1) average time for:
•	storing student records
•	searching a specific roll number
•	updating student information
•	Hash-based systems are highly suitable for institutional databases.

## Code
```cpp
#include <iostream>
#include <string>
using namespace std;

struct Student {
    int roll;
    string name;
    float marks;
    Student* next;
};

Student* table[10];   

int hashFunction(int roll) {
    return roll % 10;
}

Student* createStudent(int roll, string name, float marks) {
    Student* s = new Student();
    s->roll = roll;
    s->name = name;
    s->marks = marks;
    s->next = NULL;
    return s;
}

void insertRecord(int roll, string name, float marks) {
    int index = hashFunction(roll);
    Student* s = createStudent(roll, name, marks);

    s->next = table[index];   
    table[index] = s;

    cout << "Record inserted at bucket " << index << endl;
}

void searchRecord(int roll) {
    int index = hashFunction(roll);
    Student* temp = table[index];

    while (temp != NULL) {
        if (temp->roll == roll) {
            cout << "Record Found:\n";
            cout << "Roll: " << temp->roll << "\n";
            cout << "Name: " << temp->name << "\n";
            cout << "Marks: " << temp->marks << "\n";
            return;
        }
        temp = temp->next;
    }

    cout << "Record not found!\n";
}

void displayTable() {
    cout << "\nHash Table (Student Records):\n";

    for (int i = 0; i < 10; i++) {
        cout << i << ": ";
        Student* temp = table[i];

        while (temp != NULL) {
            cout << "[" << temp->roll << ", " << temp->name 
                 << ", " << temp->marks << "] -> ";
            temp = temp->next;
        }
        cout << "NULL\n";
    }
}

int main() {
    int ch, roll;
    string name;
    float marks;

    for (int i = 0; i < 10; i++)
        table[i] = NULL;

    while (true) {
        cout << "\n--- STUDENT HASH TABLE ---\n";
        cout << "1. Insert Record\n";
        cout << "2. Search Record\n";
        cout << "3. Display Hash Table\n";
        cout << "4. Exit\n";
        cout << "Enter choice: ";
        cin >> ch;

        switch (ch) {
            case 1:
                cout << "Enter Roll No: ";
                cin >> roll;
                cout << "Enter Name: ";
                cin >> name;
                cout << "Enter Marks: ";
                cin >> marks;
                insertRecord(roll, name, marks);
                break;

            case 2:
                cout << "Enter Roll No to search: ";
                cin >> roll;
                searchRecord(roll);
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
--- STUDENT HASH TABLE ---
1. Insert Record
2. Search Record
3. Display Hash Table
4. Exit
Enter choice: 1
Enter Roll No: 15
Enter Name: Parth
Enter Marks: 93
Record inserted at bucket 5

--- STUDENT HASH TABLE ---
1. Insert Record
2. Search Record
3. Display Hash Table
4. Exit
Enter choice: 1
Enter Roll No: 25
Enter Name: Yash
Enter Marks: 94
Record inserted at bucket 5

--- STUDENT HASH TABLE ---
1. Insert Record
2. Search Record
3. Display Hash Table
4. Exit
Enter choice: 1
Enter Roll No: 26
Enter Name: Prasad
Enter Marks: 95
Record inserted at bucket 6

--- STUDENT HASH TABLE ---
1. Insert Record
2. Search Record
3. Display Hash Table
4. Exit
Enter choice: 3

Hash Table (Student Records):
0: NULL
1: NULL
2: NULL
3: NULL
4: NULL
5: [25, Yash, 94] -> [15, Parth, 93] -> NULL
6: [26, Prasad, 95] -> NULL
7: NULL
8: NULL
9: NULL

--- STUDENT HASH TABLE ---
1. Insert Record
2. Search Record
3. Display Hash Table
4. Exit
Enter choice: 2
Enter Roll No to search: 26
Record Found:
Roll: 26
Name: Prasad
Marks: 95

## Real-Life Applications
•	College student management systems
•	Library systems tied to student IDs
•	Hostel attendance records
•	Exam mark sheets and quick roll number lookups
•	Fee management and receipt generation

## Conclusion
Hash tables provide a fast, reliable method for storing and retrieving student records by roll number. They ensure scalability and allow institutions to manage student databases efficiently.