# Assignment 20


## Problem Statement
Given a list, split it into two sublists — one for the front half, and one for the back half. If the number of elements is odd, the extra element should go in the front list. So FrontBackSplit() on the list {2, 3, 5, 7, 11} should yield the two lists {2, 3, 5} and {7, 11}. Getting this right for all the cases is harder than it looks. You should check your solution against a few cases (length = 2, length = 3, length=4) to make sure that the list gets split correctly near the shortlist boundary conditions. If it works right for length=4, it probably works right for length=1000. You will probably need special case code to deal with the (length <2) cases.

## Theory
The FrontBackSplit operation divides a linked list into two independent sublists. The splitting is based on the number of elements: if odd, the extra element is given to the front list. The challenge lies in correctly handling boundary conditions (lists with 0, 1, or 2 nodes).
A common method is using the fast–slow pointer technique: the slow pointer moves one step at a time, while the fast pointer moves two. When the fast pointer reaches the end, the slow pointer indicates the split point. This ensures an evenly divided list without counting nodes explicitly.

## Code
```cpp
#include <iostream>
#include <cstdlib>
using namespace std;

typedef struct Node
{
    int data;
    Node* next;
}Node;

Node* head = NULL;

Node* getNode()
{
    Node* newNode = new Node();
    cout<<"Enter data: ";
    cin>>newNode -> data;
    newNode -> next = NULL;
    return newNode;
}

void createList()
{
    int ch = 1;
    Node* tail = NULL;

    while(ch)
    {
        Node* newNode = getNode();
        if(head == NULL)
        {
            head = tail = newNode;
        }
        tail -> next = newNode;
        tail = newNode;
        cout<<"Do you want to add another node? [1: Yes | 0: No]: ";
        cin>>ch;
    }
}

void displayList(Node* h)
{
    if(h == NULL)
    {
        cout<<"List is empty.\n";
        return;
    }

    Node* temp = h;
    while(temp)
    {
        cout<<temp -> data;
        if(temp -> next)
        {
            cout<<" -> ";
        }
        temp = temp -> next;
    }
    cout<<endl;
}

void frontBackSplit(Node* source, Node*& frontRef, Node*& backRef)
{
    frontRef = NULL;
    backRef = NULL;

    if(source == NULL)
    {
        frontRef = NULL;
        backRef = NULL;
        return;
    }

    if(source -> next == NULL)
    {
        frontRef = source;
        backRef = NULL;
        return;
    }

    Node* slow = source;
    Node* fast = source -> next;

    while(fast)
    {
        fast = fast -> next;
        if(fast)
        {
            slow = slow -> next;
            fast = fast -> next;
        }
    }

    frontRef = source;
    backRef = slow -> next;
    slow -> next = NULL;
}

void freeList(Node*& h)
{
    Node* curr = h;
    while(curr)
    {
        Node* nxt = curr -> next;
        delete curr;
        curr = nxt;
    }
    h = NULL;
}

int main()
{
    int ch;

    while(true)
    {
        cout<<"\n-----Front Back Split-----\n";
        cout<<"1. Create List.\n";
        cout<<"2. Display List.\n";
        cout<<"3. Front Back split.\n";
        cout<<"4. Exit.\n";
        cout<<"Enter your choice: ";
        cin>>ch;

        switch(ch)
        {
            case 1:
                freeList(head);
                createList();
                break;

            case 2:
                cout<<"Current List: ";
                displayList(head);
                break;

            case 3:
            {
                if(head == NULL)
                {
                    cout<<"List is empty.\n";
                    break;
                }
                Node* front = NULL;
                Node* back = NULL;
                frontBackSplit(head, front, back);
                cout<<"Front List: ";
                displayList(front);
                cout<<"Back List: ";
                displayList(back);
                break;
            }

            case 4:
                cout<<"Exiting...\n";
                freeList(head);
                exit(0);

            default:
                cout<<"Invalid choice!\n";
        }
    }
    return 0;
}

```

## Output
-----Front Back Split-----
1. Create List.
2. Display List.
3. Front Back split.
4. Exit.
Enter your choice: 1
Enter data: 10
Do you want to add another node? [1: Yes | 0: No]: 1
Enter data: 20
Do you want to add another node? [1: Yes | 0: No]: 1
Enter data: 35
Do you want to add another node? [1: Yes | 0: No]: 1
Enter data: 41
Do you want to add another node? [1: Yes | 0: No]: 1
Enter data: 55
Do you want to add another node? [1: Yes | 0: No]: 0

-----Front Back Split-----
1. Create List.
2. Display List.
3. Front Back split.
4. Exit.
Enter your choice: 2
Current List: 10 -> 20 -> 35 -> 41 -> 55

-----Front Back Split-----
1. Create List.
2. Display List.
3. Front Back split.
4. Exit.
Enter your choice: 3
Front List: 10 -> 20 -> 35
Back List: 41 -> 55

## Real-Life Applications
•	Divide and conquer algorithms (Merge Sort)
•	Splitting task queues into parallel processing groups
•	Load balancing in distributed systems
•	Batching operations in simulations
•	Splitting training/test data in machine learning

## Conclusion
Front-Back Split is essential for divide-and-conquer strategies and parallelism. Using fast-slow pointers ensures efficient splitting and stable performance regardless of list size.