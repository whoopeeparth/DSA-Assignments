# Assignment 35


## Problem Statement
Write a Program to create a Binary Tree and perform the following Recursive operations on it. a. Inorder Traversal b. Preorder Traversal c. Display Number of Leaf Nodes d. Mirror Image

## Theory
Recursive traversal is the most natural way to process binary trees because the tree structure itself is recursive.
•	Inorder visits nodes in sorted order for BSTs.
•	Preorder visits roots before exploring subtrees.
Counting leaf nodes recursively checks each node’s children and accumulates the count.
Mirroring with recursion simply swaps subtrees at each node during the recursive descent.
Recursion simplifies implementation and closely matches the conceptual definition of trees. It is readable, maintainable, and ideal for most environments unless the tree is extremely deep.

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

Node* createNode(int x) {
    Node* n = new Node();
    n->data = x;
    n->left = n->right = NULL;
    return n;
}

Node* insert(Node* root, int x) {
    if(root == NULL)
        return createNode(x);

    if(x < root->data)
        root->left = insert(root->left, x);
    else
        root->right = insert(root->right, x);

    return root;
}

void inorder(Node* root) {
    if(root == NULL) return;
    inorder(root->left);
    cout << root->data << " ";
    inorder(root->right);
}

void preorder(Node* root) {
    if(root == NULL) return;
    cout << root->data << " ";
    preorder(root->left);
    preorder(root->right);
}

int countLeaf(Node* root) {
    if(root == NULL) return 0;

    if(root->left == NULL && root->right == NULL)
        return 1;

    return countLeaf(root->left) + countLeaf(root->right);
}

void mirror(Node* root) {
    if(root == NULL) return;

    Node* temp = root->left;
    root->left = root->right;
    root->right = temp;

    mirror(root->left);
    mirror(root->right);
}

int main() {
    int ch, x;

    while(true) {
        cout << "\n--- BINARY TREE (RECURSIVE) ---\n";
        cout << "1. Insert\n";
        cout << "2. Inorder Traversal\n";
        cout << "3. Preorder Traversal\n";
        cout << "4. Count Leaf Nodes\n";
        cout << "5. Mirror Image\n";
        cout << "6. Exit\n";
        cout << "Enter choice: ";
        cin >> ch;

        switch(ch) {
            case 1:
                cout << "Enter value: ";
                cin >> x;
                root = insert(root, x);
                break;

            case 2:
                cout << "Inorder: ";
                inorder(root);
                cout << endl;
                break;

            case 3:
                cout << "Preorder: ";
                preorder(root);
                cout << endl;
                break;

            case 4:
                cout << "Leaf Nodes = " << countLeaf(root) << endl;
                break;

            case 5:
                mirror(root);
                cout << "Mirror created.\n";
                break;

            case 6:
                return 0;

            default:
                cout << "Invalid choice!\n";
        }
    }
}

```

## Output
--- BINARY TREE (RECURSIVE) ---
1. Insert
2. Inorder Traversal
3. Preorder Traversal
4. Count Leaf Nodes
5. Mirror Image
6. Exit
Enter choice: 1
Enter value: 100

--- BINARY TREE (RECURSIVE) ---
1. Insert
2. Inorder Traversal
3. Preorder Traversal
4. Count Leaf Nodes
5. Mirror Image
6. Exit
Enter choice: 1
Enter value: 90

--- BINARY TREE (RECURSIVE) ---
1. Insert
2. Inorder Traversal
3. Preorder Traversal
4. Count Leaf Nodes
5. Mirror Image
6. Exit
Enter choice: 1
Enter value: 110

--- BINARY TREE (RECURSIVE) ---
1. Insert
2. Inorder Traversal
3. Preorder Traversal
4. Count Leaf Nodes
5. Mirror Image
6. Exit
Enter choice: 2
Inorder: 90 100 110

--- BINARY TREE (RECURSIVE) ---
1. Insert
2. Inorder Traversal
3. Preorder Traversal
4. Count Leaf Nodes
5. Mirror Image
6. Exit
Enter choice: 3
Preorder: 100 90 110

--- BINARY TREE (RECURSIVE) ---
1. Insert
2. Inorder Traversal
3. Preorder Traversal
4. Count Leaf Nodes
5. Mirror Image
6. Exit
Enter choice: 4
Leaf Nodes = 2

--- BINARY TREE (RECURSIVE) ---
1. Insert
2. Inorder Traversal
3. Preorder Traversal
4. Count Leaf Nodes
5. Mirror Image
6. Exit
Enter choice: 5
Mirror created.

--- BINARY TREE (RECURSIVE) ---
1. Insert
2. Inorder Traversal
3. Preorder Traversal
4. Count Leaf Nodes
5. Mirror Image
6. Exit
Enter choice: 2
Inorder: 110 100 90

## Real-Life Applications
•	Recursive parsing algorithms in compilers
•	Algorithms for decision and game trees
•	Directory traversal utilities
•	Expression evaluation and syntax trees
•	Recursive search algorithms in AI

## Conclusion
Recursive binary-tree processing leverages the natural hierarchical structure of trees. It simplifies implementation and is widely used in algorithms involving expressions, file systems, and search structures.