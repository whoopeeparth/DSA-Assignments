# Assignment 18


## Problem Statement
Implement Bubble sort using Doubly Linked List

## Theory
Bubble Sort is a simple comparison-based algorithm in which adjacent elements are repeatedly compared and swapped. When implemented on a doubly linked list (DLL), the algorithm becomes more efficient for pointer manipulation because each node has links to both previous and next nodes. DLLs allow backward traversal and easier swapping without shifting elements.
Although Bubble Sort has a high time complexity (O(n²)), its simplicity and ease of implementation make it suitable for small datasets or educational purposes. With DLLs, swapping nodes is pointer-based, avoiding large data movements.

## Code
```cpp
#include <iostream>
using namespace std;

struct Node
{
    int data;
    Node* next;
    Node* prev;
};

Node* head = NULL;

Node* getNode()
{
    Node* newNode = new Node;
    cout<<"Enter data: ";
    cin>>newNode -> data;
    newNode -> next = NULL;
    newNode -> prev = NULL;
    return newNode;
}

void insertEnd()
{
    Node* newNode = getNode();
    if(head == NULL)
    {
        head = newNode;
        return;
    }
    Node* temp = head;
    while(temp -> next)
    {
        temp = temp -> next;
    }
    temp -> next = newNode;
    newNode -> prev = temp;
    temp = newNode;
}

void displayList()
{
    if(head == NULL)
    {
        cout<<"List is empty.\n";
        return;
    }
    cout<<"List elements: ";
    Node* temp = head;
    while(temp)
    {
        cout<<temp -> data<<" ";
        temp = temp -> next;
    }
    cout<<endl;
}

void bubbleSort()
{
    if(head == NULL)
    {
        cout<<"List is empty.\n";
        return;
    }
    bool swapped;
    Node* curr;
    Node* lastSorted = NULL;

    do
    {
        swapped = false;
        curr = head;
        while(curr -> next != lastSorted)
        {
            if(curr -> data > curr -> next -> data)
            {
                int temp = curr -> data;
                curr -> data = curr -> next -> data;
                curr -> next -> data = temp;
                swapped = true;
            }
            curr = curr -> next;
        }
        lastSorted = curr;
    } while (swapped);

    cout<<"List sorted.\n";
}

int main()
{
    int ch;

    while(true)
    {
        cout<<"\n-----DLL Bubble Sort-----\n";
        cout<<"1. Insert Element.\n";
        cout<<"2. Display List.\n";
        cout<<"3. Sort List using Bubble Sort.\n";
        cout<<"4. Exit.\n";
        cout<<"Enter your choice: ";
        cin>>ch;

        switch(ch)
        {
            case 1:
                insertEnd();
                break;

            case 2:
                displayList();
                break;

            case 3:
                bubbleSort();
                break;

            case 4:
                cout<<"Exiting...\n";
                exit(0);

            default:
                cout<<"Invalid choice!\n";
        }
    }
    return 0;
}

```

## Output
-----DLL Bubble Sort-----
1. Insert Element.
2. Display List.
3. Sort List using Bubble Sort.
4. Exit.
Enter your choice: 1
Enter data: 50

-----DLL Bubble Sort-----
1. Insert Element.
2. Display List.
3. Sort List using Bubble Sort.
4. Exit.
Enter your choice: 1
Enter data: 30

-----DLL Bubble Sort-----
1. Insert Element.
2. Display List.
3. Sort List using Bubble Sort.
4. Exit.
Enter your choice: 1
Enter data: 10

-----DLL Bubble Sort-----
1. Insert Element.
2. Display List.
3. Sort List using Bubble Sort.
4. Exit.
Enter your choice: 1
Enter data: 20

-----DLL Bubble Sort-----
1. Insert Element.
2. Display List.
3. Sort List using Bubble Sort.
4. Exit.
Enter your choice: 2
List elements: 50 30 10 20

-----DLL Bubble Sort-----
1. Insert Element.
2. Display List.
3. Sort List using Bubble Sort.
4. Exit.
Enter your choice: 3
List sorted.

-----DLL Bubble Sort-----
1. Insert Element.
2. Display List.
3. Sort List using Bubble Sort.
4. Exit.
Enter your choice: 2
List elements: 10 20 30 50

## Real-Life Applications
•	Sorting small datasets in embedded systems
•	Teaching tool for algorithm and pointer operations
•	User interface systems where frequent adjacent swaps occur
•	Simulation models where order changes gradually
•	Maintaining sorted playlists or small lists

## Conclusion
While not the fastest sorting technique, Bubble Sort on DLLs demonstrates effective pointer manipulation and is useful for small applications requiring simplicity over performance.