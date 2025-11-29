# Assignment 19


## Problem Statement
WAP to create a doubly linked list and perform following operations on it.A) Insert (all cases) 2. Delete (all cases).

## Theory
A Doubly Linked List contains nodes with three fields: data, a pointer to the next node, and a pointer to the previous node. This bidirectional structure makes insertion and deletion more flexible compared to singly linked lists. Operations include inserting at the beginning, end, and in-between nodes, as well as deleting from similar positions.
DLLs support efficient forward and backward traversal, making them ideal for implementing dynamic data structures where frequent modifications occur.

## Code
```cpp
#include <iostream>
#include <cstdlib>
using namespace std;

typedef struct Node
{
    int data;
    Node* next;
    Node* prev;
}Node;

Node* head = NULL;

Node* getNode()
{
    Node* newNode = new Node();
    cout<<"Enter data: ";
    cin>>newNode -> data;
    newNode -> next = NULL;
    newNode -> prev = NULL;
    return newNode;
}

void displayList()
{
    Node* temp = head;
    if(head == NULL)
    {
        cout<<"List is empty.\n";
        return;
    }
    cout<<"List elements: ";
    while(temp)
    {
        cout<<temp -> data<<" <-> ";
        temp = temp -> next;
    }
    cout<<"NULL\n";
}

void insertBeg()
{
    Node* newNode = getNode();
    if(head == NULL)
    {
        head = newNode;
    }
    newNode -> next = head;
    head -> prev = newNode;
    head = newNode;
    cout<<"Inserted node at beginning.\n";
}

void insertEnd()
{
    Node* newNode = getNode();
    if(head == NULL)
    {
        head = newNode;
        cout<<"Inserted node at end.\n";
        return;
    }
    Node* temp = head;
    while(temp -> next)
    {
        temp = temp -> next;
    }
    temp -> next = newNode;
    newNode -> prev = temp;
    cout<<"Inserted node at end.\n";
}

void insertPos()
{
    int pos, i = 1;
    cout<<"Enter pos to insert: ";
    cin>>pos;

    if(pos == 1)
    {
        insertBeg();
        return;
    }

    Node* newNode = getNode();
    Node* temp = head;
    while(i < pos - 1 && temp)
    {
        temp = temp -> next;
        i++;
    }
    
    if(temp == NULL)
    {
        cout<<"Invalid position.\n";
        delete newNode;
        return;
    }
    newNode -> next = temp -> next;
    newNode -> prev = temp;

    if(temp -> next)
    {
        temp -> next -> prev = newNode;
    }
    temp -> next = newNode;

    cout<<"Inserted node at position.\n";
}

void deleteBeg()
{
    if(head == NULL)
    {
        cout<<"List is empty.\n";
        return;
    }

    Node* temp = head;
    head = head -> next;
    head -> prev = NULL;
    delete temp;
    cout<<"Deleted node at beginning.\n";
}

void deleteEnd()
{
    if(head == NULL)
    {
        cout<<"List is empty.\n";
        return;
    }

    if(head -> next == NULL)
    {
        delete head;
        head = NULL;
        cout<<"Deleted node at end.\n";
        return;
    }

    Node* temp = head;
    while(temp -> next)
    {
        temp = temp -> next;
    }
    temp -> prev -> next = NULL;
    delete temp;
    cout<<"Deleted node at end.\n";
}

void deletePos()
{
    int pos, i = 1;
    cout<<"Enter pos to delete: ";
    cin>>pos;

    if(pos == 1)
    {
        deleteBeg();
        return;
    }

    Node* temp = head;
    while(i < pos && temp)
    {
        temp = temp -> next;
        i++;
    }

    if(temp == NULL)
    {
        cout<<"Invalid position.\n";
        return;
    }

    if(temp -> prev)
    {
        temp -> prev -> next = temp -> next;
    }
    if(temp -> next)
    {
        temp -> next -> prev = temp -> prev;
    }

    delete temp;
    cout<<"Deleted node at position.\n";
}

Node* createList()
{
    int ch = 1;
    while(ch)
    {
        insertEnd();
        cout<<"Do you want to add new node? [1: Yes | 0: No]: ";
        cin>>ch;
    }
    return head;
}

int main() {
    int ch;

    while (1) {
        printf("\n-----Doubly Linked List-----\n");
        printf("1. Create Linked List\n");
        printf("2. Display Linked List\n");
        printf("3. Insert at Beginning\n");
        printf("4. Insert at End\n");
        printf("5. Insert at Position\n");
        printf("6. Delete at Beginning\n");
        printf("7. Delete at End\n");
        printf("8. Delete at Position\n");
        printf("9. Exit\n");
        printf("Enter your choice: ");
        scanf("%d", &ch);

        switch (ch) {
            case 1: 
                createList(); 
                break;

            case 2: 
                displayList(); 
                break;

            case 3: 
                insertBeg(); 
                break;

            case 4: 
                insertEnd(); 
                break;

            case 5: 
                insertPos(); 
                break;

            case 6: 
                deleteBeg(); 
                break;

            case 7: 
                deleteEnd(); 
                break;

            case 8: 
                deletePos(); 
                break;

            case 9: 
                printf("Exiting...\n"); 
                exit(0);

            default: 
                printf("Invalid choice!\n");
        }
    }

    return 0;
}

```

## Output
-----Doubly Linked List-----
1. Create Linked List
2. Display Linked List
3. Insert at Beginning
4. Insert at End
5. Insert at Position
6. Delete at Beginning
7. Delete at End
8. Delete at Position
9. Exit
Enter your choice: 1
Enter data: 10
Inserted node at end.
Do you want to add new node? [1: Yes | 0: No]: 1
Enter data: 20
Inserted node at end.
Do you want to add new node? [1: Yes | 0: No]: 1
Enter data: 30
Inserted node at end.
Do you want to add new node? [1: Yes | 0: No]: 1
Enter data: 40
Inserted node at end.
Do you want to add new node? [1: Yes | 0: No]: 0

-----Doubly Linked List-----
1. Create Linked List
2. Display Linked List
3. Insert at Beginning
4. Insert at End
5. Insert at Position
6. Delete at Beginning
7. Delete at End
8. Delete at Position
9. Exit
Enter your choice: 2
List elements: 10 <-> 20 <-> 30 <-> 40 <-> NULL

-----Doubly Linked List-----
1. Create Linked List
2. Display Linked List
3. Insert at Beginning
4. Insert at End
5. Insert at Position
6. Delete at Beginning
7. Delete at End
8. Delete at Position
9. Exit
Enter your choice: 3
Enter data: 5
Inserted node at beginning.

-----Doubly Linked List-----
1. Create Linked List
2. Display Linked List
3. Insert at Beginning
4. Insert at End
5. Insert at Position
6. Delete at Beginning
7. Delete at End
8. Delete at Position
9. Exit
Enter your choice: 4
Enter data: 45
Inserted node at end.

-----Doubly Linked List-----
1. Create Linked List
2. Display Linked List
3. Insert at Beginning
4. Insert at End
5. Insert at Position
6. Delete at Beginning
7. Delete at End
8. Delete at Position
9. Exit
Enter your choice: 6
Deleted node at beginning.

-----Doubly Linked List-----
1. Create Linked List
2. Display Linked List
3. Insert at Beginning
4. Insert at End
5. Insert at Position
6. Delete at Beginning
7. Delete at End
8. Delete at Position
9. Exit
Enter your choice: 2
List elements: 10 <-> 20 <-> 30 <-> 40 <-> 45 <-> NULL

## Real-Life Applications
•	Navigation systems (back/forward in browsers)
•	Undo/redo functionality in editors
•	Music/video playlist management
•	Memory management in operating systems
•	Implementation of deques

## Conclusion
DLLs offer powerful features for dynamic data modification. Their two-way traversal enables efficient insertions and deletions, making them a preferred structure in many software systems requiring bidirectional movement.