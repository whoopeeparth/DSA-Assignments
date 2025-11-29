# Assignment 53


## Problem Statement
Implement collision resolution using linked lists.

## Theory
This assignment is closely related to separate chaining. Instead of storing multiple values in the same array slot using open addressing, the hash table uses linked lists attached to each index. Each node in the linked list stores a key, value, and pointer to the next node.
The linked-list-based collision handling allows:
•	Unlimited entries at one index
•	Efficient insertion at the head or tail
•	Dynamic memory allocation
•	Independent chains for separate keys
This is especially useful for applications where records grow dynamically.

## Code
```cpp
#include <iostream>
using namespace std;

struct Node {
    int data;
    Node* next;
};

Node* hashTable[10];   

int hashFunction(int key) {
    return key % 10;
}

Node* getNode(int key) {
    Node* p = new Node();
    p->data = key;
    p->next = NULL;
    return p;
}

void insertKey(int key) {
    int index = hashFunction(key);

    Node* newNode = getNode(key);

    newNode->next = hashTable[index];
    hashTable[index] = newNode;

    cout << "Inserted " << key << " at bucket " << index << endl;
}

void searchKey(int key) {
    int index = hashFunction(key);

    Node* temp = hashTable[index];

    while (temp != NULL) {
        if (temp->data == key) {
            cout << "Key " << key << " found at bucket " << index << endl;
            return;
        }
        temp = temp->next;
    }
    cout << "Key not found!" << endl;
}

void display() {
    cout << "\nHash Table:\n";
    for (int i = 0; i < 10; i++) {
        cout << i << ": ";
        Node* temp = hashTable[i];
        while (temp != NULL) {
            cout << temp->data << " -> ";
            temp = temp->next;
        }
        cout << "NULL\n";
    }
}

int main() {
    int ch, key;

    for (int i = 0; i < 10; i++)
        hashTable[i] = NULL;

    while (true) {
        cout << "\n--- Hash Table (Linked List Collision Handling) ---\n";
        cout << "1. Insert Key\n";
        cout << "2. Search Key\n";
        cout << "3. Display Table\n";
        cout << "4. Exit\n";
        cout << "Enter your choice: ";
        cin >> ch;

        switch (ch) {

            case 1:
                cout << "Enter key to insert: ";
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
--- Hash Table (Linked List Collision Handling) ---
1. Insert Key
2. Search Key
3. Display Table
4. Exit
Enter your choice: 1
Enter key to insert: 15
Inserted 15 at bucket 5

--- Hash Table (Linked List Collision Handling) ---
1. Insert Key
2. Search Key
3. Display Table
4. Exit
Enter your choice: 1
Enter key to insert: 25
Inserted 25 at bucket 5

--- Hash Table (Linked List Collision Handling) ---
1. Insert Key
2. Search Key
3. Display Table
4. Exit
Enter your choice: 1
Enter key to insert: 23
Inserted 23 at bucket 3

--- Hash Table (Linked List Collision Handling) ---
1. Insert Key
2. Search Key
3. Display Table
4. Exit
Enter your choice: 3

Hash Table:
0: NULL
1: NULL
2: NULL
3: 23 -> NULL
4: NULL
5: 25 -> 15 -> NULL
6: NULL
7: NULL
8: NULL
9: NULL

## Real-Life Applications
•	Hash maps in languages like Java, Python, C++
•	Database indexing where records can grow dynamically
•	Dynamic network routing tables
•	Access control lists (ACL systems)
•	DNS caching and lookup tables

## Conclusion
Using linked lists to handle collisions provides a scalable, flexible hashing system that gracefully handles large data volumes and frequent insert/delete operations.