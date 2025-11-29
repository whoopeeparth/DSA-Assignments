# Assignment 31


## Problem Statement
Write a program to perform Binary Search Tree (BST) operations (Create, Insert, Delete,Levelwise display )

## Theory
A Binary Search Tree (BST) is a binary tree where every node’s left child contains a value smaller than the node, and the right child contains a value larger than the node. This ordering property allows efficient searching, insertion, and deletion—usually in O(log n) time when the tree is balanced.
Creating a BST involves inserting nodes one by one while maintaining the BST property. Deletion is more complex because it depends on whether the node is a leaf, has one child, or has two children. When deleting a node with two children, the in-order successor is typically used to preserve structure. Levelwise (level-order) display uses a queue to print nodes layer by layer, representing the tree in a breadth-first manner.
BSTs are fundamental in computer science due to their structured ordering and efficient operations.

## Code
```cpp
#include <iostream>
#include <cstdlib>
using namespace std;

typedef struct Node
{
    int data;
    Node* left;
    Node* right;
}Node;

Node* createNode(int val)
{
    Node* newNode = new Node();
    newNode -> data = val;
    newNode -> left = newNode -> right = nullptr;
    return newNode;
}

Node* insertNode(Node* root, int val)
{
    if(root == nullptr)
    {
        return createNode(val);
    }

    if(val < root -> data)
    {
        root -> left = insertNode(root -> left, val);
    }
    else if(val > root -> data)
    {
        root -> right = insertNode(root -> right, val);
    }
    else
    {
        cout<<"Duplicate value not allowed!"<<endl;
    }
    return root;
}

Node* findMin(Node* root)
{
    while(root && root -> left != nullptr)
    {
        root = root -> left;
    }
    return root;
}

Node* deleteNode(Node* root, int key)
{
    if(root == nullptr)
    {
        return root;
    }
    if(key < root -> data)
    {
        root -> left = deleteNode(root -> left, key);
    }
    else if(key > root -> data)
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
        else
        {
            Node* temp = findMin(root -> right);
            root -> data = temp -> data;
            root -> right = deleteNode(root -> right, temp -> data);
        }
    }
    return root;
}

struct QNode 
{
    Node* data;
    QNode* next;
};

QNode * front = nullptr;
QNode * rear = nullptr;

void enqueue(Node* node)
{
    QNode* newNode = new QNode();
    newNode -> data = node;
    newNode -> next = NULL;

    if(front == nullptr && rear == nullptr)
    {
        front = rear = newNode;
    }
    rear -> next = newNode;
    rear = newNode;
}

Node* dequeue()
{
    if(front == nullptr)
    {
        return nullptr;
    }
    QNode* temp = front;
    Node* node = temp -> data;
    front = front -> next;
    if(front == nullptr)
    {
        rear = nullptr;
    }
    delete temp;
    return node;
}

bool isEmpty()
{
    return front == nullptr;
}
void levelOrder(Node* root)
{
    if(root == nullptr)
    {
        cout<<"Tree is empty."<<endl;
        return;
    }
    enqueue(root);
    cout<<"Level Order Traversal(BFS)";
    while(!isEmpty())
    {
        Node* curr = dequeue();
        cout<<curr -> data<<" ";

        if(curr -> left != nullptr)
        {
            enqueue(curr -> left);
        }
        if(curr -> right != nullptr)
        {
            enqueue(curr -> right);
        }
    }
    cout<<endl;
}

int main()
{
    Node* root = nullptr;
    int choice, val;

    do
    {
        cout<<endl<<"-----BST Menu-----"<<endl;
        cout<<"1. Insert Node"<<endl;
        cout<<"2. Delete Node"<<endl;
        cout<<"3. Level Order Traversal"<<endl;
        cout<<"4. Exit"<<endl;
        cout<<"Enter your choice: ";
        cin>>choice;

        switch(choice)
        {
            case 1:
                cout<<"Enter value to insert: ";
                cin>>val;
                root = insertNode(root, val);
                break;

            case 2:
                cout<<"Enter value to delete: ";
                cin>>val;
                root = deleteNode(root, val);
                break;
            
            case 3:
                levelOrder(root);
                break;

            case 4:
                cout<<"Exiting..."<<endl;
                exit(0);

            default:
                cout<<"Invalid choice."<<endl;
        }
    } while (true);
    return 0;
}

```

## Output
-----BST Menu-----
1. Insert Node
2. Delete Node
3. Level Order Traversal
4. Exit
Enter your choice: 1
Enter value to insert: 100

-----BST Menu-----
1. Insert Node
2. Delete Node
3. Level Order Traversal
4. Exit
Enter your choice: 1
Enter value to insert: 90

-----BST Menu-----
1. Insert Node
2. Delete Node
3. Level Order Traversal
4. Exit
Enter your choice: 1
Enter value to insert: 110

-----BST Menu-----
1. Insert Node
2. Delete Node
3. Level Order Traversal
4. Exit
Enter your choice: 3
Level Order Traversal(BFS)100 90 110

-----BST Menu-----
1. Insert Node
2. Delete Node
3. Level Order Traversal
4. Exit
Enter your choice: 2
Enter value to delete: 90

## Real-Life Applications
•	Database indexing (using tree-like structures)
•	File system directory organization
•	Dynamic searching in dictionaries or word suggestions
•	Memory management and garbage collection
•	Network routing tables

## Conclusion
BST operations form the core of many efficient data-access systems. Their structured organization supports fast insertion, deletion, and searching, making them essential for dynamic datasets.