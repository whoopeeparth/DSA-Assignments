# Assignment 33


## Problem Statement
Write a Program to create a Binary Tree Search and Find Minimum/Maximum in BST

## Theory
In a BST, the minimum element is always found by traversing the leftmost path from the root, while the maximum is found by traversing the rightmost path. This works because of the BST’s inherent ordering property.
Finding min/max is extremely efficient—just a simple traversal, typically O(h), where h is the height of the tree. These operations are important for range queries, boundary checking, and validating the correctness of tree structure. They also serve as core steps in other BST operations, such as deletion.

## Code
```cpp
#include <iostream>
using namespace std;

struct Node {
    int data;
    Node* left;
    Node* right;
};

Node* root = NULL;

Node* getNode(int x) {
    Node* p = new Node;
    p->data = x;
    p->left = NULL;
    p->right = NULL;
    return p;
}

Node* insertNode(Node* root, int x) {
    if(root == NULL)
        return getNode(x);

    if(x < root->data)
        root->left = insertNode(root->left, x);
    else if(x > root->data)
        root->right = insertNode(root->right, x);
    else
        cout << "Duplicate value not allowed!\n";

    return root;
}

Node* searchNode(Node* root, int key) {
    if(root == NULL || root->data == key)
        return root;

    if(key < root->data)
        return searchNode(root->left, key);
    else
        return searchNode(root->right, key);
}

Node* findMin(Node* root) {
    if(root == NULL)
        return NULL;

    while(root->left != NULL)
        root = root->left;

    return root;
}

Node* findMax(Node* root) {
    if(root == NULL)
        return NULL;

    while(root->right != NULL)
        root = root->right;

    return root;
}

void inorder(Node* root) {
    if(root == NULL)
        return;
    inorder(root->left);
    cout << root->data << " ";
    inorder(root->right);
}

int main() {
    int ch, x;

    while(true) {
        cout << "\n--- BST Menu ---\n";
        cout << "1. Insert\n";
        cout << "2. Search\n";
        cout << "3. Find Minimum\n";
        cout << "4. Find Maximum\n";
        cout << "5. Display (Inorder)\n";
        cout << "6. Exit\n";
        cout << "Enter choice: ";
        cin >> ch;

        switch(ch) {
            case 1:
                cout << "Enter value to insert: ";
                cin >> x;
                root = insertNode(root, x);
                break;

            case 2:
                cout << "Enter value to search: ";
                cin >> x;
                if(searchNode(root, x))
                    cout << "Found!\n";
                else
                    cout << "Not Found!\n";
                break;

            case 3: {
                Node* m = findMin(root);
                if(m)
                    cout << "Minimum value: " << m->data << endl;
                else
                    cout << "Tree is empty.\n";
                break;
            }

            case 4: {
                Node* m = findMax(root);
                if(m)
                    cout << "Maximum value: " << m->data << endl;
                else
                    cout << "Tree is empty.\n";
                break;
            }

            case 5:
                cout << "Inorder Traversal: ";
                inorder(root);
                cout << endl;
                break;

            case 6:
                cout << "Exiting...\n";
                return 0;

            default:
                cout << "Invalid choice!\n";
        }
    }
    return 0;
}

```

## Output
--- BST Menu ---
1. Insert
2. Search
3. Find Minimum
4. Find Maximum
5. Display (Inorder)
6. Exit
Enter choice: 1
Enter value to insert: 100

--- BST Menu ---
1. Insert
2. Search
3. Find Minimum
4. Find Maximum
5. Display (Inorder)
6. Exit
Enter choice: 1
Enter value to insert: 90

--- BST Menu ---
1. Insert
2. Search
3. Find Minimum
4. Find Maximum
5. Display (Inorder)
6. Exit
Enter choice: 1
Enter value to insert: 110

--- BST Menu ---
1. Insert
2. Search
3. Find Minimum
4. Find Maximum
5. Display (Inorder)
6. Exit
Enter choice: 2
Enter value to search: 90
Found!

--- BST Menu ---
1. Insert
2. Search
3. Find Minimum
4. Find Maximum
5. Display (Inorder)
6. Exit
Enter choice: 3
Minimum value: 90

--- BST Menu ---
1. Insert
2. Search
3. Find Minimum
4. Find Maximum
5. Display (Inorder)
6. Exit
Enter choice: 4
Maximum value: 110

--- BST Menu ---
1. Insert
2. Search
3. Find Minimum
4. Find Maximum
5. Display (Inorder)
6. Exit
Enter choice: 5
Inorder Traversal: 90 100 110

## Real-Life Applications
•	Finding smallest/largest keys in databases
•	Range queries in search engines
•	Limit price detection in stock-market systems
•	Boundary filtering in computational geometry
•	Scheduling systems where earliest/latest tasks are needed

## Conclusion
Min/max operations demonstrate the power of BST ordering. Their simplicity and efficiency make BSTs ideal for systems requiring quick boundary-value lookups.