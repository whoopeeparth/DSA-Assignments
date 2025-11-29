# Assignment 34


## Problem Statement
Write a Program to create a Binary Tree and perform following Nonrecursive operations on it. a. Inorder Traversal b. Preorder Traversal c. Display Number of Leaf Nodes d. Mirror Image

## Theory
Non-recursive traversals use explicit stacks to simulate recursion.
•	Inorder Traversal (Left, Root, Right) sorts the BST when applied to BSTs.
•	Preorder Traversal (Root, Left, Right) processes parent nodes before children, useful for copying trees.
Counting leaf nodes involves checking which nodes have no children. The mirror operation swaps left/right children iteratively.
Non-recursive methods are extremely important for environments where recursion depth may cause stack overflow or where explicit control of traversal is needed. Using stacks, programmers mimic the internal call stack behavior manually.

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
    if(root == NULL) {
        return createNode(x);
    }
    if(x < root->data)
        root->left = insert(root->left, x);
    else
        root->right = insert(root->right, x);

    return root;
}

void inorder() {
    Node* stack[50];
    int top = -1;
    Node* curr = root;

    cout << "Inorder: ";

    while(curr != NULL || top != -1) {
        while(curr != NULL) {
            stack[++top] = curr;
            curr = curr->left;
        }

        curr = stack[top--];
        cout << curr->data << " ";
        curr = curr->right;
    }
    cout << endl;
}

void preorder() {
    if(root == NULL) return;

    Node* stack[50];
    int top = -1;

    stack[++top] = root;

    cout << "Preorder: ";

    while(top != -1) {
        Node* temp = stack[top--];
        cout << temp->data << " ";

        if(temp->right)
            stack[++top] = temp->right;
        if(temp->left)
            stack[++top] = temp->left;
    }
    cout << endl;
}

int countLeaf(Node* root) {
    if(root == NULL) return 0;

    int count = 0;
    Node* stack[50];
    int top = -1;

    stack[++top] = root;

    while(top != -1) {
        Node* temp = stack[top--];

        if(temp->left == NULL && temp->right == NULL)
            count++;

        if(temp->right) stack[++top] = temp->right;
        if(temp->left)  stack[++top] = temp->left;
    }
    return count;
}

void mirror(Node* node) {
    if(node == NULL) return;

    Node* stack[50];
    int top = -1;

    stack[++top] = node;

    while(top != -1) {
        Node* temp = stack[top--];

        Node* s = temp->left;
        temp->left = temp->right;
        temp->right = s;

        if(temp->left)  stack[++top] = temp->left;
        if(temp->right) stack[++top] = temp->right;
    }
}

int main() {
    int ch, x;

    while(true) {
        cout << "\n--- BINARY TREE MENU ---\n";
        cout << "1. Insert\n";
        cout << "2. Inorder (Non-recursive)\n";
        cout << "3. Preorder (Non-recursive)\n";
        cout << "4. Count Leaf Nodes\n";
        cout << "5. Mirror Tree\n";
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
                inorder();
                break;

            case 3:
                preorder();
                break;

            case 4:
                cout << "Leaf nodes = " << countLeaf(root) << endl;
                break;

            case 5:
                mirror(root);
                cout << "Mirror image created.\n";
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
--- BINARY TREE MENU ---
1. Insert
2. Inorder (Non-recursive)
3. Preorder (Non-recursive)
4. Count Leaf Nodes
5. Mirror Tree
6. Exit
Enter choice: 1
Enter value: 100

--- BINARY TREE MENU ---
1. Insert
2. Inorder (Non-recursive)
3. Preorder (Non-recursive)
4. Count Leaf Nodes
5. Mirror Tree
6. Exit
Enter choice: 1
Enter value: 90

--- BINARY TREE MENU ---
1. Insert
2. Inorder (Non-recursive)
3. Preorder (Non-recursive)
4. Count Leaf Nodes
5. Mirror Tree
6. Exit
Enter choice: 1
Enter value: 110

--- BINARY TREE MENU ---
1. Insert
2. Inorder (Non-recursive)
3. Preorder (Non-recursive)
4. Count Leaf Nodes
5. Mirror Tree
6. Exit
Enter choice: 2
Inorder: 90 100 110

--- BINARY TREE MENU ---
1. Insert
2. Inorder (Non-recursive)
3. Preorder (Non-recursive)
4. Count Leaf Nodes
5. Mirror Tree
6. Exit
Enter choice: 3
Preorder: 100 90 110

--- BINARY TREE MENU ---
1. Insert
2. Inorder (Non-recursive)
3. Preorder (Non-recursive)
4. Count Leaf Nodes
5. Mirror Tree
6. Exit
Enter choice: 4
Leaf nodes = 2

--- BINARY TREE MENU ---
1. Insert
2. Inorder (Non-recursive)
3. Preorder (Non-recursive)
4. Count Leaf Nodes
5. Mirror Tree
6. Exit
Enter choice: 5
Mirror image created.

--- BINARY TREE MENU ---
1. Insert
2. Inorder (Non-recursive)
3. Preorder (Non-recursive)
4. Count Leaf Nodes
5. Mirror Tree
6. Exit
Enter choice: 2
Inorder: 110 100 90

## Real-Life Applications
•	Iterative tree algorithms used in compilers
•	File-system traversal without recursion
•	Tree serialization/deserialization in memory-restricted environments
•	Iterative evaluation of expression trees
•	AI search trees requiring controlled traversal strategies

## Conclusion
Non-recursive tree operations enhance control, stability, and safety in tree algorithms. They are essential for real-time systems and low-memory devices where recursion is not feasible.