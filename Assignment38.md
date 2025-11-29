# Assignment 38


## Problem Statement
Write a program to efficiently search a particular employee record by using Tree data structure. Also sort the data on emp­id in ascending order.

## Theory
Employee records stored in a BST allow fast searching based on employee ID (emp-id). Each node can hold an employee’s details such as name, ID, department, and salary. Inserting employee data into a BST ensures that searching for an employee becomes an O(log n) operation in balanced trees, opposed to O(n) sequential search.
Sorting by emp-id is naturally achieved via an inorder traversal of the BST, producing a complete list ordered in ascending order. This makes BSTs highly suitable for managing employee databases where searching and sorting are daily operations.

## Code
```cpp
#include <iostream>
#include <cstdlib>
#include <string>
using namespace std;

struct Node
{
    int eid;
    string name;
    Node* left;
    Node* right;
};

Node* root = nullptr;

Node* getNode(int id, string n)
{
    Node* newNode = new Node();
    newNode -> eid = id;
    newNode -> name = n;
    newNode -> left = nullptr;
    newNode -> right = nullptr;
    return newNode;
}

Node* insertNode(Node* root, Node* newNode)
{
    if(root == nullptr)
    {
        return newNode;
    }
    if(newNode -> eid < root -> eid)
    {
        root -> left = insertNode(root -> left, newNode);
    }
    else if(newNode -> eid > root -> eid)
    {
        root -> right = insertNode(root -> right, newNode);
    }
    else
    {
        cout<<"Duplicate Employee ID not allowed!\n";
    }
    return root;
}

Node* searchNode(Node* root, int id)
{
    if(root == nullptr || root -> eid == id)
    {
        return root;
    }
    if(id < root -> eid)
    {
        return searchNode(root -> left, id);
    }
    else
    {
        return searchNode(root -> right, id);
    }
}

void inOrder(Node* root)
{
    if(root == nullptr)
    {
        return;
    }
    inOrder(root -> left);
    cout<<"Emp ID: "<<root -> eid<<" Name: "<<root -> name<<endl;
    inOrder(root -> right);
}

int main()
{
    int ch, id;
    string name;

    while(true)
    {
        cout<<"\n-----Employee BST-----\n";
        cout<<"1. Insert Employee\n";
        cout<<"2. Search Employee by ID\n";
        cout<<"3. Display Employees\n";
        cout<<"4. Exit\n";
        cout<<"Enter your choice: ";
        cin>>ch;

        switch(ch)
        {
            case 1:
            {
                cout<<"Enter Employee ID: ";
                cin>>id;
                cout<<"Enter Name: ";
                cin>>name;
                Node* newNode = getNode(id, name);
                root = insertNode(root, newNode);
                cout<<"Employee inserted\n";
                break;
            }

            case 2:
            {
                cout<<"Enter ID to search: ";
                cin>>id;
                Node* result = searchNode(root, id);
                if(result == nullptr)
                {
                    cout<<"Employee not found.\n";
                }
                else
                {
                    cout<<"Employee found -> ID: "<<result -> eid<<", Name: "<<result -> name<<endl;
                }
                break;
            }

            case 3:
            {
                cout<<"\nEmployees sorted by ID: \n";
                inOrder(root);
                break;
            }

            case 4:
            {
                cout<<"Exiting...\n";
                exit(0);
            }

            default:
                cout<<"Invalid choice\n";
        }
    }
    return 0;
}

```

## Output
-----Employee BST-----
1. Insert Employee
2. Search Employee by ID
3. Display Employees
4. Exit
Enter your choice: 1
Enter Employee ID: 100
Enter Name: Parth
Employee inserted

-----Employee BST-----
1. Insert Employee
2. Search Employee by ID
3. Display Employees
4. Exit
Enter your choice: 1
Enter Employee ID: 90
Enter Name: Yash
Employee inserted

-----Employee BST-----
1. Insert Employee
2. Search Employee by ID
3. Display Employees
4. Exit
Enter your choice: 1
Enter Employee ID: 110
Enter Name: Prasad
Employee inserted

-----Employee BST-----
1. Insert Employee
2. Search Employee by ID
3. Display Employees
4. Exit
Enter your choice: 3

Employees sorted by ID:
Emp ID: 90 Name: Yash
Emp ID: 100 Name: Parth
Emp ID: 110 Name: Prasad

-----Employee BST-----
1. Insert Employee
2. Search Employee by ID
3. Display Employees
4. Exit
Enter your choice: 2
Enter ID to search: 110
Employee found -> ID: 110, Name: Prasad

## Real-Life Applications
•	HR management systems
•	Payroll processing
•	Government employee databases
•	Corporate directory systems
•	Large organization record maintenance

## Conclusion
Using trees to manage employee records ensures faster search and automatic sorting by employee ID. This improves efficiency and accuracy in administrative systems.