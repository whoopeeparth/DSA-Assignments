# Assignment 52


## Problem Statement
Implement collision handling using separate chaining.

## Theory
Separate chaining is a collision resolution technique where every hash table index points to a linked list (or chain) of entries that hash to the same index. Instead of searching for an empty slot, all colliding values are simply appended to the linked list at that index.
This makes the hash table flexible—insertions never fail even if the load factor is high. Lookup performance remains near O(1) on average, though worst-case time becomes O(n) if all keys hash to the same index.
Separate chaining is ideal when:
•	Data set size is unpredictable
•	There are frequent insertions/deletions
•	Collisions are expected due to poor hash functions

## Code
```cpp
#include <iostream>
using namespace std;

struct Node {
    int data;
    Node* next;
};

Node* hashTable[10];   

Node* getNode(int key) {
    Node* p = new Node();
    p->data = key;
    p->next = NULL;
    return p;
}

int hashFunction(int key) {
    return key % 10;
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
    cout << "Key not found\n";
}

void display() {
    cout << "\nHash Table (Separate Chaining):\n";
    for (int i = 0; i < 10; i++) {
        cout << i << " : ";
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
        cout << "\n--- Hash Table (Separate Chaining) ---\n";
        cout << "1. Insert\n";
        cout << "2. Search\n";
        cout << "3. Display\n";
        cout << "4. Exit\n";
        cout << "Enter choice: ";
        cin >> ch;

        if (ch == 1) {
            cout << "Enter key: ";
            cin >> key;
            insertKey(key);
        }
        else if (ch == 2) {
            cout << "Enter key to search: ";
            cin >> key;
            searchKey(key);
        }
        else if (ch == 3) {
            display();
        }
        else if (ch == 4) {
            cout << "Exiting...\n";
            break;
        }
        else {
            cout << "Invalid choice!\n";
        }
    }
    return 0;
}

```

## Output
--- Hash Table (Separate Chaining) ---
1. Insert
2. Search
3. Display
4. Exit
Enter choice: 1
Enter key: 15
Inserted 15 at bucket 5

--- Hash Table (Separate Chaining) ---
1. Insert
2. Search
3. Display
4. Exit
Enter choice: 1
Enter key: 25
Inserted 25 at bucket 5

--- Hash Table (Separate Chaining) ---
1. Insert
2. Search
3. Display
4. Exit
Enter choice: 1
Enter key: 34
Inserted 34 at bucket 4

--- Hash Table (Separate Chaining) ---
1. Insert
2. Search
3. Display
4. Exit
Enter choice: 3

Hash Table (Separate Chaining):
0 : NULL
1 : NULL
2 : NULL
3 : NULL
4 : 34 -> NULL
5 : 25 -> 15 -> NULL
6 : NULL
7 : NULL
8 : NULL
9 : NULL

--- Hash Table (Separate Chaining) ---
1. Insert
2. Search
3. Display
4. Exit
Enter choice: 2
Enter key to search: 34
Key 34 found at bucket 4

## Real-Life Applications
•	•	Data retrieval systems where deletion must be efficient
•	Document indexing in search engines
•	Map/set implementations in STL, Java Collections, Python dict
•	Caching in distributed systems
•	Storing log entries based on hash keys

## Conclusion
Separate chaining is a robust collision resolution method that maintains high performance even when load factors grow. It is widely used in real-world hash table implementations due to its flexibility and ease of deletion handling.