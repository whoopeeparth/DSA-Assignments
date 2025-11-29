# Assignment 37


## Problem Statement
Write a program to illustrate operations on a BST holding numeric keys.
The menu must include: • Insert • Delete • Find • Show

## Theory
A Binary Search Tree is a hierarchical structure where each node contains a numeric key, and the left subtree contains smaller values while the right subtree contains larger ones. Supporting operations such as insert, delete, find, and show (display) creates a complete dynamic data management system.
•	Insert adds new keys while maintaining BST properties.
•	Delete handles removal from three scenarios: leaf, one-child node, or two-children node.
•	Find quickly searches for a key via binary search logic.
•	Show typically uses inorder traversal to present keys in sorted order.
The BST’s efficient structure supports fast updates and searches even as the dataset grows.

## Code
```cpp
#include <iostream>
#include <cstdlib>
using namespace std;

struct Node
{
    int key;
    Node* left;
    Node* right;
};

Node* root = nullptr;

Node* getNode(int key)
{
    Node* newNode = new Node();
    newNode -> key = key;
    newNode -> left = newNode -> right = nullptr;
    return newNode;
}

Node* insertNode(Node* root, int key)
{
    if(root == nullptr)
    {
        return getNode(key);
    }

    if(key < root -> key)
    {
        root -> left = insertNode(root -> left, key);
    }
    else if(key > root -> key)
    {
        root -> right = insertNode(root -> right, key);
    }

    return root;
}

Node* minValueNode(Node* node)
{
    Node* current = node;
    while(current && current -> left != nullptr)
    {
        current = current -> left;
    }
    return current;
}

Node* deleteNode(Node* root, int key)
{
    if(root == nullptr)
    {
        return root;
    }

    if(key < root -> key)
    {
        root -> left = deleteNode(root -> left, key);
    }
    else if(key > root -> key)
    {
        root -> right = deleteNode(root -> right, key);
    }
    else
    {
        if(root -> left == nullptr && root -> right == nullptr)
        {
            delete root;
            return nullptr;
        }
        else if(root -> left == nullptr)
        {
            Node* temp = root -> right;
            delete root;
            return temp;
        }
        else if(root -> right == nullptr)
        {
            Node* temp = root -> left;
            delete root;
            return temp;
        }

        Node* temp = minValueNode(root -> right);
        root -> key = temp -> key;
        root -> right = deleteNode(root -> right, temp -> key);
    }
    return root;
}

bool searchNode(Node* root, int key)
{
    if(root == nullptr)
    {
        return false;
    }
    if(key == root -> key)
    {
        return true;
    }
    if(key < root -> key)
    {
        return searchNode(root -> left, key);
    }
    else
    {
        return searchNode(root -> right, key);
    }
}

void inOrder(Node* root)
{
    if(root == nullptr)
    {
        return;
    }
    inOrder(root -> left);
    cout<<root -> key<<" ";
    inOrder(root -> right);
}

int main()
{
    int choice, key;

    while(true)
    {
        cout<<"\n-----BST Operations-----\n";
        cout<<"1. Insert\n";
        cout<<"2. Delete\n";
        cout<<"3. Find\n";
        cout<<"4. Show(InOrder)\n";
        cout<<"5. Exit\n";
        cout<<"Enter your choice: ";
        cin>>choice;

        switch(choice)
        {
            case 1:
                cout<<"Enter key to insert: ";
                cin>>key;
                root = insertNode(root, key);
                break;

            case 2:
                cout<<"Enter key to delete: ";
                cin>>key;
                root = deleteNode(root, key);
                cout<<"Deleted\n";
                break;

            case 3:
                cout<<"Enter key to find: ";
                cin>>key;
                if(searchNode(root, key))
                {
                    cout<<key<<" found in the tree\n";
                }
                else
                {
                    cout<<key<<" not found\n";
                }
                break;

            case 4:
                cout<<"BST(InOrder): ";
                inOrder(root);
                cout<<endl;
                break;

            case 5:
                cout<<"Exiting...\n";
                exit(0);

            default:    
                cout<<"Invalid choice\n";
        }
    }
    return 0;
}

```

## Output
-----BST Operations-----
1. Insert
2. Delete
3. Find
4. Show(InOrder)
5. Exit
Enter your choice: 1
Enter key to insert: 100

-----BST Operations-----
1. Insert
2. Delete
3. Find
4. Show(InOrder)
5. Exit
Enter your choice: 1
Enter key to insert: 90

-----BST Operations-----
1. Insert
2. Delete
3. Find
4. Show(InOrder)
5. Exit
Enter your choice: 1
Enter key to insert: 110

-----BST Operations-----
1. Insert
2. Delete
3. Find
4. Show(InOrder)
5. Exit
Enter your choice: 4
BST(InOrder): 90 100 110

-----BST Operations-----
1. Insert
2. Delete
3. Find
4. Show(InOrder)
5. Exit
Enter your choice: 3
Enter key to find: 90
90 found in the tree

-----BST Operations-----
1. Insert
2. Delete
3. Find
4. Show(InOrder)
5. Exit
Enter your choice: 2
Enter key to delete: 90
Deleted

-----BST Operations-----
1. Insert
2. Delete
3. Find
4. Show(InOrder)
5. Exit
Enter your choice: 4
BST(InOrder): 100 110

## Real-Life Applications
•	•	Databases and indexing
•	Memory management inside OS
•	Auto-suggest systems
•	Routing table management
•	Search-intensive applications

## Conclusion
A BST with full CRUD operations demonstrates the core strengths of tree-based search structures. It is efficient, dynamic, and essential in various high-performance software systems.