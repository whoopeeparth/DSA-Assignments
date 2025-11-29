# Assignment 14


## Problem Statement
In the Second Year Computer Engineering class, there are two groups of students based on their favorite sports:
●	Set A includes students who like Cricket.
●	Set B includes students who like Football.
Write a C++ program to represent these two sets using linked lists and perform the following operations:
a) Find and display the set of students who like both Cricket and Football.
 b) Find and display the set of students who like either Cricket or Football, but not both.
 c) Display the number of students who like neither Cricket nor Football.

## Theory
Sets represent collections of unique elements, and using linked lists to implement them allows dynamic insertion and efficient traversal. Students are categorized into two sets depending on their sports preference—Cricket (Set A) and Football (Set B).
Operations such as intersection, symmetric difference, and complement require traversing both lists and identifying relationships between elements. These operations help illustrate fundamental concepts in set theory using linked list structures, which is useful for real systems involving membership, categories, or grouping.

## Code
```cpp
#include <iostream>
#include <cstdlib>
#include <string>
using namespace std;

struct Node 
{
    string name;
    Node* next;
};

Node* cricketHead = NULL;
Node* footballHead = NULL;

Node* createList(int n, const string& sport) 
{
    Node* head = NULL;
    Node* temp = NULL;
    string student;

    for (int i = 0; i < n; i++) 
    {
        cout << "Enter name of student " << (i + 1) << " who likes " << sport << ": ";
        cin >> student;

        Node* newNode = new Node();
        newNode->name = student;
        newNode->next = NULL;

        if (head == NULL)
            head = newNode;
        else
            temp->next = newNode;

        temp = newNode;
    }

    return head;
}

bool exists(Node* head, const string& name) 
{
    Node* temp = head;
    while (temp != NULL) 
    {
        if (temp->name == name)
            return true;
        temp = temp->next;
    }
    return false;
}

void displayList(Node* head) 
{
    if (head == NULL) 
    {
        cout << "No students in this list.\n";
        return;
    }

    Node* temp = head;
    while (temp != NULL) 
    {
        cout << temp->name << " ";
        temp = temp->next;
    }
    cout << endl;
}

void intersection(Node* headA, Node* headB) 
{
    Node* temp = headA;
    Node* result = NULL;
    Node* tail = NULL;

    while (temp != NULL) 
    {
        if (exists(headB, temp->name)) 
        {
            Node* newNode = new Node();
            newNode->name = temp->name;
            newNode->next = NULL;

            if (result == NULL)
                result = newNode;
            else
                tail->next = newNode;

            tail = newNode;
        }
        temp = temp->next;
    }

    cout << "Students who like both Cricket and Football: ";
    displayList(result);
}

void symmetricDifference(Node* headA, Node* headB) 
{
    Node* result = NULL;
    Node* tail = NULL;

    Node* temp = headA;
    while (temp != NULL) 
    {
        if (!exists(headB, temp->name)) 
        {
            Node* newNode = new Node();
            newNode->name = temp->name;
            newNode->next = NULL;
            if (result == NULL)
                result = newNode;
            else
                tail->next = newNode;
            tail = newNode;
        }
        temp = temp->next;
    }

    temp = headB;
    while (temp != NULL) 
    {
        if (!exists(headA, temp->name)) 
        {
            Node* newNode = new Node();
            newNode->name = temp->name;
            newNode->next = NULL;
            if (result == NULL)
                result = newNode;
            else
                tail->next = newNode;
            tail = newNode;
        }
        temp = temp->next;
    }

    cout << "Students who like either Cricket or Football but not both: ";
    displayList(result);
}

void neitherCount(Node* headA, Node* headB, int totalStudents) 
{
    Node* temp = headA;
    int countBoth = 0;

    while (temp != NULL) {
        if (exists(headB, temp->name))
            countBoth++;
        temp = temp->next;
    }

    int uniqueStudents = 0;
    temp = headA;
    while (temp != NULL) {
        uniqueStudents++;
        temp = temp->next;
    }
    temp = headB;
    while (temp != NULL) {
        if (!exists(headA, temp->name))
            uniqueStudents++;
        temp = temp->next;
    }

    int neither = totalStudents - uniqueStudents;
    cout << "Number of students who like neither Cricket nor Football: " << neither << endl;
}

int main() 
{
    int totalStudents, nCricket, nFootball, choice;

    cout << "Enter total number of students: ";
    cin >> totalStudents;

    cout << "Enter number of students who like Cricket: ";
    cin >> nCricket;

    cricketHead = createList(nCricket, "Cricket");

    cout << "Enter number of students who like Football: ";
    cin >> nFootball;

    footballHead = createList(nFootball, "Football");

    while (true) 
    {
        cout << "\n----- Menu -----\n";
        cout << "1. Display students who like both Cricket and Football\n";
        cout << "2. Display students who like either Cricket or Football but not both\n";
        cout << "3. Display number of students who like neither\n";
        cout << "4. Exit\n";
        cout << "Enter your choice: ";
        cin >> choice;

        switch(choice) 
        {
            case 1: 
                intersection(cricketHead, footballHead); 
                break;

            case 2: 
                symmetricDifference(cricketHead, footballHead); 
                break;

            case 3: 
                neitherCount(cricketHead, footballHead, totalStudents); 
                break;

            case 4: 
                exit(0);

            default: 
                cout << "Invalid choice!\n";
        }
    }

    return 0;
}

```

## Output
Enter total number of students: 4
Enter number of students who like Cricket: 2
Enter name of student 1 who likes Cricket: Parth
Enter name of student 2 who likes Cricket: Yash
Enter number of students who like Football: 2
Enter name of student 1 who likes Football: Prasad
Enter name of student 2 who likes Football: Saee

----- Menu -----
1. Display students who like both Cricket and Football
2. Display students who like either Cricket or Football but not both
3. Display number of students who like neither
4. Exit
Enter your choice: 1
Students who like both Cricket and Football: No students in this list.

----- Menu -----
1. Display students who like both Cricket and Football
2. Display students who like either Cricket or Football but not both
3. Display number of students who like neither
4. Exit
Enter your choice: 2
Students who like either Cricket or Football but not both: Parth Yash Prasad Saee

----- Menu -----
1. Display students who like both Cricket and Football
2. Display students who like either Cricket or Football but not both
3. Display number of students who like neither
4. Exit
Enter your choice: 3
Number of students who like neither Cricket nor Football: 0

## Real-Life Applications
•	Filtering users based on interests in recommendation systems.
•	Managing categories of customers in marketing analytics.
•	Classifying students or employees based on activities.
•	Performing set operations in database queries.
•	Tag-based filtering in social media platforms.

## Conclusion
Linked lists effectively model dynamic sets and support essential operations like intersection and difference. This assignment connects set theory with practical C++ implementation for categorizing users by interests.