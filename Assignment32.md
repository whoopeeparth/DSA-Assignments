# Assignment 32


## Problem Statement
Write a program to perform Binary Search Tree (BST) operations (Count the total number of nodes, Compute the height of the BST, Mirror Image ).

## Theory
Counting the total number of nodes in a BST is a recursive process that sums all nodes from left and right subtrees plus one for the root. The height of a BST is the length of the longest path from the root to any leaf node. Height helps determine the efficiency of operations—a smaller height means faster operations.
The mirror image of a BST swaps the left and right children recursively for every node. It visually reverses the tree’s structure and is useful for checking symmetry-related properties. These operations rely heavily on recursive traversal and are critical in understanding structural behavior of the tree.

## Code
```cpp
#include <iostream>
#include <cstdlib>
using namespace std;

struct Node
{
    int data;
    Node* left;
    Node* right;
};

Node* root = NULL;

Node* createNode(int val)
{
    Node* newNode = new Node();
    newNode -> data = val;
    newNode -> left = newNode -> right = nullptr;
    return newNode;
}

void insert(Node* temp, int val)
{
    if(root == nullptr)
    {
        root = createNode(val);
        cout<<"Root crrated with value"<<val<<endl;
        return;
    }

    if(val < temp -> data)
    {
        if(temp -> left == nullptr)
        {
            temp -> left = createNode(val);
        }
        else
        {
            insert(temp -> left, val);
        }
    }
    else if(val > temp -> data)
    {
        if(temp -> right == nullptr)
        {
            temp -> right = createNode(val);
        }
        else
        {
            insert(temp -> right, val);
        }
    }
    else
    {
        cout<<endl;
    }
}

int countNodes(Node* temp)
{
    if(temp == nullptr)
    {
        return 0;
    }
    return 1 + countNodes(temp -> left) + countNodes(temp -> right);
}

int height(Node* temp)
{
    if(temp == nullptr)
    {
        return 0;
    }
    int leftH = height(temp -> left);
    int rightH = height(temp -> right);
    return max(leftH, rightH) + 1;
}

void mirror(Node* temp)
{
    if(temp == nullptr)
    {
        return;
    }
    mirror(temp -> left);
    mirror(temp -> right);
    Node* t = temp -> left;
    temp -> left = temp -> right;
    temp -> right = t;
}

void inorder(Node* temp)
{
    if(temp == nullptr)
    {
        return;
    }
    inorder(temp -> left);
    cout<<temp -> data<<" ";
    inorder(temp -> right);
}

int main()
{
    int choice, val;

    do
    {
        cout<<endl<<"-----BST Menu-----"<<endl;
        cout<<"1. Insert Node"<<endl;
        cout<<"2. Count Nodes"<<endl;
        cout<<"3. Compute Height"<<endl;
        cout<<"4. Mirror BST"<<endl;
        cout<<"5. Display (InOrder)"<<endl;
        cout<<"Enter your choice: ";
        cin>>choice;

        switch(choice)
        {
            case 1:
                cout<<"Enter value to insert: ";
                cin>>val;
                insert(root, val);
                break;

            case 2:
                cout<<"Total number of nodes: "<<countNodes(root)<<endl;
                break;

            case 3:
                cout<<"Height of the BST: "<<height(root)<<endl;
                break;

            case 4:
                mirror(root);
                cout<<"Mirror image created of BST"<<endl;
                break;

            case 5:
                cout<<"Inorder traversal: ";
                inorder(root);
                cout<<endl;
                break;

            case 6:
                cout<<"Exiting..."<<endl;
                exit(0);

            default:
                cout<<"Invalid choice!"<<endl;
        }
    } while (choice != 6);
    return 0;
}

```

## Output
-----BST Menu-----
1. Insert Node
2. Count Nodes
3. Compute Height
4. Mirror BST
5. Display (InOrder)
Enter your choice: 1
Enter value to insert: 100
Root crrated with value100

-----BST Menu-----
1. Insert Node
2. Count Nodes
3. Compute Height
4. Mirror BST
5. Display (InOrder)
Enter your choice: 1
Enter value to insert: 90

-----BST Menu-----
1. Insert Node
2. Count Nodes
3. Compute Height
4. Mirror BST
5. Display (InOrder)
Enter your choice: 1
Enter value to insert: 110

-----BST Menu-----
1. Insert Node
2. Count Nodes
3. Compute Height
4. Mirror BST
5. Display (InOrder)
Enter your choice: 2
Total number of nodes: 3

-----BST Menu-----
1. Insert Node
2. Count Nodes
3. Compute Height
4. Mirror BST
5. Display (InOrder)
Enter your choice: 3
Height of the BST: 2

-----BST Menu-----
1. Insert Node
2. Count Nodes
3. Compute Height
4. Mirror BST
5. Display (InOrder)
Enter your choice: 5
Inorder traversal: 90 100 110

-----BST Menu-----
1. Insert Node
2. Count Nodes
3. Compute Height
4. Mirror BST
5. Display (InOrder)
Enter your choice: 4
Mirror image created of BST

-----BST Menu-----
1. Insert Node
2. Count Nodes
3. Compute Height
4. Mirror BST
5. Display (InOrder)
Enter your choice: 5
Inorder traversal: 110 100 90

## Real-Life Applications
•	•	Analyzing performance of decision trees
•	Checking symmetry in image processing
•	Evaluating network tree depth for routing optimization
•	Constructing reverse-mapped structures
•	AI game-tree evaluations

## Conclusion
Node counting, height calculation, and mirroring help in analyzing and transforming a BST. These operations provide valuable structural insights and are used widely in performance optimization and tree manipulation.