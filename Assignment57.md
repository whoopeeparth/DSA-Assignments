# Assignment 57


## Problem Statement
WAP to simulate a faculty database as a hash table. Search a particular faculty by using MOD as a hash function for linear probing with chaining with replacement method of collision handling technique. Assume suitable data for faculty record.

## Theory
•	This version uses MOD hashing, a direct and popular hashing technique:
•	index = key % tableSize
•	Collisions are handled through linear probing with replacement, which differs from the previous method.
•	Linear Probing With Replacement
•	If a collision occurs at index h(key)
•	And the occupant of that index does not belong to that hash position
•	Then that occupant is replaced (shifted) and the new element is placed at its rightful hash location.
•	This technique drastically increases search efficiency because elements are placed closer to their correct hash positions.
•	It improves search time, reduces clustering, and enhances average-case performance for large datasets.

## Code
```cpp
#include <iostream>
#include <string>
using namespace std;

#define SIZE 10

struct Faculty
{
    int id;
    string name;
    string dept;
    bool empty;
};

Faculty table[SIZE];
int linkArr[SIZE];

void init()
{
    for (int i = 0; i < SIZE; i++)
    {
        table[i].empty = true;
        linkArr[i] = -1;
    }
}

int hashFunc(int id)
{
    return id % SIZE;
}

void insertFaculty()
{
    int id;
    string name, dept;

    cout << "Enter Faculty ID: ";
    cin >> id;
    cout << "Enter Name: ";
    cin >> name;
    cout << "Enter Department: ";
    cin >> dept;

    int home = hashFunc(id);

    if (table[home].empty)
    {
        table[home] = {id, name, dept, false};
        cout << "Inserted at home slot: " << home << endl;
        return;
    }

    int existingHome = hashFunc(table[home].id);

    if (existingHome != home)
    {
        int pos = (home + 1) % SIZE;
        while (!table[pos].empty)
            pos = (pos + 1) % SIZE;

        table[pos] = table[home];
        table[home] = {id, name, dept, false};

        linkArr[pos] = linkArr[home];
        linkArr[home] = -1;

        cout << "Inserted with replacement at home slot: " << home << endl;
        return;
    }

    int pos = (home + 1) % SIZE;
    while (!table[pos].empty)
        pos = (pos + 1) % SIZE;

    table[pos] = {id, name, dept, false};

    int t = home;
    while (linkArr[t] != -1)
        t = linkArr[t];
    linkArr[t] = pos;

    cout << "Inserted using linear probing at: " << pos << endl;
}

void searchFaculty()
{
    int id;
    cout << "Enter ID to search: ";
    cin >> id;

    int home = hashFunc(id);

    int t = home;
    while (t != -1)
    {
        if (!table[t].empty && table[t].id == id)
        {
            cout << "Faculty Found:\n";
            cout << "ID: " << table[t].id << "  Name: " << table[t].name
                 << "  Dept: " << table[t].dept << endl;
            return;
        }
        t = linkArr[t];
    }

    cout << "Faculty Not Found.\n";
}

void display()
{
    cout << "\nIndex\tID\tName\tDept\tLink\n";
    for (int i = 0; i < SIZE; i++)
    {
        if (!table[i].empty)
            cout << i << "\t" << table[i].id << "\t" << table[i].name
                 << "\t" << table[i].dept << "\t" << linkArr[i] << endl;
        else
            cout << i << "\t---\t---\t---\t" << linkArr[i] << endl;
    }
}

int main()
{
    int ch;
    init();

    while (true)
    {
        cout << "\n--- FACULTY HASH TABLE (LP + REPLACEMENT + CHAINING) ---\n";
        cout << "1. Insert Faculty\n";
        cout << "2. Search Faculty\n";
        cout << "3. Display Table\n";
        cout << "4. Exit\n";
        cout << "Enter choice: ";
        cin >> ch;

        if (ch == 1)
            insertFaculty();
        else if (ch == 2)
            searchFaculty();
        else if (ch == 3)
            display();
        else if (ch == 4)
        {
            cout << "Exiting...\n";
            break;
        }
        else
            cout << "Invalid choice!\n";
    }

    return 0;
}

```

## Output
--- FACULTY HASH TABLE (LP + REPLACEMENT + CHAINING) ---
1. Insert Faculty
2. Search Faculty
3. Display Table
4. Exit
Enter choice: 1
Enter Faculty ID: 15
Enter Name: Parth
Enter Department: CS
Inserted at home slot: 5

--- FACULTY HASH TABLE (LP + REPLACEMENT + CHAINING) ---
1. Insert Faculty
2. Search Faculty
3. Display Table
4. Exit
Enter choice: 1
Enter Faculty ID: 25
Enter Name: IT
Enter Department: AI
Inserted using linear probing at: 6

--- FACULTY HASH TABLE (LP + REPLACEMENT + CHAINING) ---
1. Insert Faculty
2. Search Faculty
3. Display Table
4. Exit
Enter choice: 3

Index   ID      Name    Dept    Link
0       ---     ---     ---     -1
1       ---     ---     ---     -1
2       ---     ---     ---     -1
3       ---     ---     ---     -1
4       ---     ---     ---     -1
5       15      Parth   CS      6
6       25      IT      AI      -1
7       ---     ---     ---     -1
8       ---     ---     ---     -1
9       ---     ---     ---     -1

## Real-Life Applications
•	University faculty indexing for attendance systems
•	Employee record management in corporate sectors
•	Digital ID systems
•	IoT device registry mapping
•	Classroom or lab management databases

## Conclusion
Using MOD hashing with “replacement” probing achieves tighter clustering around true hash positions, greatly improving lookup efficiency in faculty databases.