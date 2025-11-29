# Assignment 59


## Problem Statement
WAP to simulate student databases as a hash table. a student database management system using hashing techniques to allow efficient insertion, search, and deletion of student records.

## Theory
•	A student database requires:
•	Fast insertions
•	Quick lookup based on roll number
•	Efficient deletion
•	Dynamic record updates
•	Hashing is the best approach because it provides O(1) average-case performance for all operations.
A hash table can store complete student information:
•	Roll number (key)
•	Name
•	Year/class
•	Marks
•	Contact details
•	The system must handle collisions using methods like:
•	Linear probing
•	Quadratic probing
•	Double hashing
•	Chaining (linked list)
•	Hash tables ensure stable performance even when thousands of student records are involved.

## Code
```cpp
#include <iostream>
using namespace std;

struct Student {
    int roll;
    string name;
    int marks;
    bool occupied;   
};

Student ht[20];      
int sizeHT = 20;     

int hashFunction(int key) {
    return key % sizeHT;
}

void insertStudent() {
    Student s;
    cout << "Enter Roll No: ";
    cin >> s.roll;
    cout << "Enter Name: ";
    cin >> s.name;
    cout << "Enter Marks: ";
    cin >> s.marks;
    s.occupied = true;

    int index = hashFunction(s.roll);
    int start = index;

    while (ht[index].occupied && ht[index].roll != -1) {
        index = (index + 1) % sizeHT;
        if (index == start) {
            cout << "Hash Table Full!\n";
            return;
        }
    }

    ht[index] = s;
    cout << "Inserted at index " << index << endl;
}

void searchStudent() {
    int roll;
    cout << "Enter Roll No to Search: ";
    cin >> roll;

    int index = hashFunction(roll);
    int start = index;

    while (ht[index].occupied) {
        if (ht[index].roll == roll) {
            cout << "Student Found at index " << index << endl;
            cout << "Roll: " << ht[index].roll
                 << "  Name: " << ht[index].name
                 << "  Marks: " << ht[index].marks << endl;
            return;
        }
        index = (index + 1) % sizeHT;
        if (index == start)
            break;
    }

    cout << "Student Not Found.\n";
}

void deleteStudent() {
    int roll;
    cout << "Enter Roll No to Delete: ";
    cin >> roll;

    int index = hashFunction(roll);
    int start = index;

    while (ht[index].occupied) {
        if (ht[index].roll == roll) {
            cout << "Student Deleted from index " << index << endl;
            ht[index].roll = -1;   
            ht[index].name = "";
            ht[index].marks = 0;
            return;
        }
        index = (index + 1) % sizeHT;
        if (index == start)
            break;
    }

    cout << "Student Not Found.\n";
}

void display() {
    cout << "\nIndex   Roll    Name      Marks\n";
    for (int i = 0; i < sizeHT; i++) {
        if (ht[i].occupied && ht[i].roll != -1) {
            cout << i << "       " << ht[i].roll << "     "
                 << ht[i].name << "      " << ht[i].marks << endl;
        } else {
            cout << i << "       ---     ---       ---\n";
        }
    }
}

int main() {

    for (int i = 0; i < sizeHT; i++) {
        ht[i].occupied = false;
        ht[i].roll = -1;
    }

    int ch;

    while (true) {
        cout << "\n--- Student Hash Table ---\n";
        cout << "1. Insert Student\n";
        cout << "2. Search Student\n";
        cout << "3. Delete Student\n";
        cout << "4. Display Hash Table\n";
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
                cout << "Invalid Choice!\n";
        }
    }
}

```

## Output
--- Student Hash Table ---
1. Insert Student
2. Search Student
3. Delete Student
4. Display Hash Table
5. Exit
Enter choice: 1
Enter Roll No: 15
Enter Name: Parth
Enter Marks: 93
Inserted at index 15

--- Student Hash Table ---
1. Insert Student
2. Search Student
3. Delete Student
4. Display Hash Table
5. Exit
Enter choice: 1
Enter Roll No: 25
Enter Name: Yash
Enter Marks: 94
Inserted at index 5

--- Student Hash Table ---
1. Insert Student
2. Search Student
3. Delete Student
4. Display Hash Table
5. Exit
Enter choice:
1
Enter Roll No: 26
Enter Name: Prasad
Enter Marks: 95
Inserted at index 6

--- Student Hash Table ---
1. Insert Student
2. Search Student
3. Delete Student
4. Display Hash Table
5. Exit
Enter choice: 4

Index   Roll    Name      Marks
0       ---     ---       ---
1       ---     ---       ---
2       ---     ---       ---
3       ---     ---       ---
4       ---     ---       ---
5       25     Yash      94
6       26     Prasad      95
7       ---     ---       ---
8       ---     ---       ---
9       ---     ---       ---
10       ---     ---       ---
11       ---     ---       ---
12       ---     ---       ---
13       ---     ---       ---
14       ---     ---       ---
15       15     Parth      93
16       ---     ---       ---
17       ---     ---       ---
18       ---     ---       ---
19       ---     ---       ---

## Real-Life Applications
•	University student registration systems
•	Library ID–based lookup
•	Exam record management
•	Hostel/student accommodation management
•	Online learning platforms (student profile management)

## Conclusion
Hashing-based student databases provide instant access to records and scale well as the number of students grows. They simplify management tasks and ensure smooth functioning of academic systems.