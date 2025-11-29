# Assignment 51


## Problem Statement
Implement a hash table with collision resolution using linear probing.

## Theory
1.	A hash table is a data structure that stores key–value pairs and provides extremely fast access time on average O(1). Hashing depends on a hash function that maps keys to specific array indices. However, when multiple keys map to the same index, a collision occurs.
Linear probing is an open addressing collision resolution technique where the table is searched sequentially (i+1, i+2, … mod table_size) until an empty slot is found. This method is simple, intuitive, cache-friendly, and keeps all elements in a single array.
2.	The success of linear probing relies on load factor:
3.	Lower load factor = fewer collisions
4.	Higher load factor may cause primary clustering, where consecutive filled slots increase search time
5.	Linear probing is effective for real-time systems because of its predictable memory layout and quick traversal behavior.

## Code
```cpp
#include <iostream>
using namespace std;

#define SIZE 10

int hashTable[SIZE];

void init() {
    for (int i = 0; i < SIZE; i++)
        hashTable[i] = -1;
}

int hashFunc(int key) {
    return key % SIZE;
}

void insertKey(int key) {
    int index = hashFunc(key);

    for (int i = 0; i < SIZE; i++) {
        int newIndex = (index + i) % SIZE;

        if (hashTable[newIndex] == -1) {  
            hashTable[newIndex] = key;
            cout << "Inserted at index " << newIndex << endl;
            return;
        }
    }

    cout << "Hash Table Full! Cannot insert.\n";
}

void searchKey(int key) {
    int index = hashFunc(key);

    for (int i = 0; i < SIZE; i++) {
        int newIndex = (index + i) % SIZE;

        if (hashTable[newIndex] == key) {
            cout << "Found at index " << newIndex << endl;
            return;
        }
        if (hashTable[newIndex] == -1)
            break; 
    }

    cout << "Key not found.\n";
}

void display() {
    cout << "\nHash Table:\n";
    for (int i = 0; i < SIZE; i++)
        cout << i << " : " << hashTable[i] << endl;
}

int main() {
    init();
    int ch, key;

    while (true) {
        cout << "\n--- Hash Table (Linear Probing) ---\n";
        cout << "1. Insert\n";
        cout << "2. Search\n";
        cout << "3. Display\n";
        cout << "4. Exit\n";
        cout << "Enter choice: ";
        cin >> ch;

        switch (ch) {
            case 1:
                cout << "Enter key: ";
                cin >> key;
                insertKey(key);
                break;

            case 2:
                cout << "Enter key to search: ";
                cin >> key;
                searchKey(key);
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
--- Hash Table (Linear Probing) ---
1. Insert
2. Search
3. Display
4. Exit
Enter choice: 1
Enter key: 15
Inserted at index 5

--- Hash Table (Linear Probing) ---
1. Insert
2. Search
3. Display
4. Exit
Enter choice: 1
Enter key: 25
Inserted at index 6

--- Hash Table (Linear Probing) ---
1. Insert
2. Search
3. Display
4. Exit
Enter choice: 3

Hash Table:
0 : -1
1 : -1
2 : -1
3 : -1
4 : -1
5 : 15
6 : 25
7 : -1
8 : -1
9 : -1

--- Hash Table (Linear Probing) ---
1. Insert
2. Search
3. Display
4. Exit
Enter choice: 2
Enter key to search: 25
Found at index 6

## Real-Life Applications
•	Symbol tables in compilers
•	Cache indexing in CPU architectures
•	Database indexing for small datasets
•	Game development lookups (mapping item IDs to data)
•	Routing tables in network devices

## Conclusion
Linear probing provides an easy-to-implement and fast method to handle collisions in hash tables. Its predictable memory pattern makes it efficient, though it must be used carefully to avoid clustering in high-load scenarios.