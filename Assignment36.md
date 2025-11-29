# Assignment 36


## Problem Statement
Write a program, using trees, to assign the roll nos. to the students of your class as per their previous years result. i.e topper will be roll no. 1

## Theory
A tree—typically a Binary Search Tree (BST)—can be used to assign roll numbers based on students' previous year performance. The student with the highest marks is placed at the root or the extreme left/right depending on whether the BST is sorted in ascending or descending order.
When you insert each student's score into a BST, an inorder traversal yields the students in sorted order. Assigning roll numbers then becomes straightforward: the topper receives roll number 1, followed by others in increasing order of rank. This approach eliminates manual work, ensures fairness, and guarantees error-free sorting.
The BST structure allows efficient insertion and retrieval in O(log n) time for balanced trees, making it ideal for handling large classes.

## Code
```cpp
#include <iostream>
#include <cstdlib>
#include <string>
using namespace std;

struct Node
{
    int marks;
    string name;
    Node* left;
    Node* right;
};

Node* root = NULL;
int roll = 1;

Node* getNode(string name, int marks)
{
    Node* newNode = new Node();
    newNode -> name = name;
    newNode -> marks = marks;
    newNode -> left = newNode -> right = nullptr;
    return newNode;
}

Node* insertNode(Node* root, string name, int marks)
{
    if(root == nullptr)
    {
        return getNode(name, marks);
    }
    if(marks < root -> marks)
    {
        root -> left = insertNode(root -> left, name, marks);
    }
    else
    {
        root -> right = insertNode(root -> right, name, marks);
    }

    return root;
}

void assignRoll(Node* root)
{
    if(root == nullptr)
    {
        return;
    }
    assignRoll(root -> right);

    cout<<"Roll No: "<<roll
        <<" -> "<<root -> name  
        <<" (Marks: "<<root -> marks<<
        ")\n";
    roll++;

    assignRoll(root -> left);
}

void displayTree(Node* root)
{
    if(root == nullptr)
    {
        return;
    }
    displayTree(root -> left);
    cout<<root -> name<<" ("<<root -> marks<<") ";
    displayTree(root -> right);
}

int main()
{
    int ch;

    while(true)
    {
        cout<<"\n-----Menu------\n";
        cout<<"1. Insert Student\n";
        cout<<"2. Display Students\n";
        cout<<"3. Assign Roll Numbers\n";
        cout<<"4. Exit\n";
        cout<<"Enter your choice: ";
        cin>>ch;

        if(ch == 1)
        {
            string name;
            int marks;

            cout<<"Enter name: ";
            cin>>name;
            cout<<"Enter marks: ";
            cin>>marks;

            root = insertNode(root, name, marks);
        }

        else if(ch == 2)
        {
            if(root == nullptr)
            {
                cout<<"Tree is empty.\n";
            }
            else
            {
                cout<<"Students: ";
                displayTree(root);
                cout<<endl;
            }
        }

        else if(ch == 3)
        {
            if(root == nullptr)
            {
                cout<<"Tree is empty.\n";
            }
            else
            {
                roll = 1;
                cout<<"\n---Roll Number Assignment---\n";
                assignRoll(root);
            }
        }

        else if(ch == 4)
        {
            cout<<"Exiting...\n";
            exit(0);
        }
        else
        {
            cout<<"Invalid choice.\n";
        }
    }
    return 0;
}

```

## Output
-----Menu------
1. Insert Student
2. Display Students
3. Assign Roll Numbers
4. Exit
Enter your choice: 1
Enter name: Parth
Enter marks: 93

-----Menu------
1. Insert Student
2. Display Students
3. Assign Roll Numbers
4. Exit
Enter your choice: 1
Enter name: Yash
Enter marks: 94

-----Menu------
1. Insert Student
2. Display Students
3. Assign Roll Numbers
4. Exit
Enter your choice: 1
Enter name: Prasad
Enter marks: 92

-----Menu------
1. Insert Student
2. Display Students
3. Assign Roll Numbers
4. Exit
Enter your choice: 2
Students: Prasad (92) Parth (93) Yash (94)

-----Menu------
1. Insert Student
2. Display Students
3. Assign Roll Numbers
4. Exit
Enter your choice: 3

---Roll Number Assignment---
Roll No: 1 -> Yash (Marks: 94)
Roll No: 2 -> Parth (Marks: 93)
Roll No: 3 -> Prasad (Marks: 92)

## Real-Life Applications
•	Automated result processing systems in schools
•	Ranking algorithms in competitions or exams
•	Sorting students for merit lists
•	Creating ordered student databases
•	Placement-cell ranking and shortlist generation

## Conclusion
Using a tree to assign roll numbers ensures accurate ranking, minimizes human errors, and automates a typically time-consuming academic process.