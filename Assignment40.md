# Assignment 40


## Problem Statement
Write a program to implement deletion operations in the product inventory system using a search tree.
 Each product must store the following information:
●	Unique Product Code
●	Product Name
●	Price
●	Quantity in Stock
●	Date Received
●	Expiration Date
Implement the following operations:
1.	Delete a product using its unique product code.

Delete all expired products based on the current date.

## Theory
Deleting from a product inventory tree involves identifying nodes either by product code (unique key) or expiration date.
•	Deleting by product code removes a single node, requiring careful handling of BST deletion rules.
•	Deleting all expired products involves traversing the entire tree, identifying expired nodes, and removing them one-by-one or rebuilding a clean tree.
Efficient deletion is crucial to maintaining the integrity of inventory systems because outdated entries affect availability, billing, and customer satisfaction. Using trees ensures that deletion operations remain structured and maintain search order even after major updates.

## Code
```cpp
#include <iostream>
#include <string>
using namespace std;

struct Product {
    string code;
    string name;
    float price;
    int qty;
    string received;
    string expiry;

    Product* left;
    Product* right;
};

Product* root = nullptr;

Product* createNode(string code, string name, float price, int qty,
                    string received, string expiry)
{
    Product* n = new Product();
    n->code = code;
    n->name = name;
    n->price = price;
    n->qty = qty;
    n->received = received;
    n->expiry = expiry;
    n->left = n->right = nullptr;
    return n;
}

Product* insertProduct(Product* root, string code, string name, float price,
                       int qty, string received, string expiry)
{
    if(root == nullptr)
        return createNode(code, name, price, qty, received, expiry);

    if(name < root->name)
        root->left = insertProduct(root->left, code, name, price, qty, received, expiry);
    else if(name > root->name)
        root->right = insertProduct(root->right, code, name, price, qty, received, expiry);
    else
        cout << "Duplicate product name not allowed!\n";

    return root;
}

void inOrder(Product* root)
{
    if(!root) return;

    inOrder(root->left);

    cout << root->name << " | Code: " << root->code
         << " | Price: " << root->price
         << " | Qty: " << root->qty
         << " | Received: " << root->received
         << " | Expiry: " << root->expiry << endl;

    inOrder(root->right);
}

Product* findMin(Product* root)
{
    while(root && root->left)
        root = root->left;
    return root;
}

bool matchCode(Product* node, string code)
{
    return node && node->code == code;
}

Product* deleteByCode(Product* root, string code)
{
    if(!root) return nullptr;

    if(matchCode(root, code))
    {
        if(!root->left && !root->right)
        {
            delete root;
            return nullptr;
        }

        if(!root->left)
        {
            Product* tmp = root->right;
            delete root;
            return tmp;
        }
        if(!root->right)
        {
            Product* tmp = root->left;
            delete root;
            return tmp;
        }

        Product* minNode = findMin(root->right);

        root->code = minNode->code;
        root->name = minNode->name;
        root->price = minNode->price;
        root->qty = minNode->qty;
        root->received = minNode->received;
        root->expiry = minNode->expiry;

        root->right = deleteByCode(root->right, minNode->code);
        return root;
    }

    root->left  = deleteByCode(root->left, code);
    root->right = deleteByCode(root->right, code);

    return root;
}

Product* deleteExpired(Product* root, string today)
{
    if(!root) return nullptr;

    root->left  = deleteExpired(root->left, today);
    root->right = deleteExpired(root->right, today);

    if(root->expiry < today)
    {
        cout << "Deleting expired product: " << root->name << endl;
        return deleteByCode(root, root->code);
    }

    return root;
}

void listExpired(Product* root, string today)
{
    if(!root) return;

    if(root->expiry < today)
    {
        cout << "[EXPIRED] " << root->name
             << " | Code: " << root->code
             << " | Expiry: " << root->expiry << endl;
    }

    listExpired(root->left, today);
    listExpired(root->right, today);
}

int main()
{
    int ch;
    string code, name, received, expiry, today;
    float price;
    int qty;

    while(true)
    {
        cout << "\n--- PRODUCT INVENTORY (BST) ---\n";
        cout << "1. Insert Product\n";
        cout << "2. Display Inventory (InOrder)\n";
        cout << "3. Delete Product by Code\n";
        cout << "4. List Expired Products\n";
        cout << "5. Delete All Expired Products\n";
        cout << "6. Exit\n";
        cout << "Enter choice: ";
        cin >> ch;

        switch(ch)
        {
            case 1:
                cout << "Enter Product Name: ";
                cin >> name;
                cout << "Enter Product Code: ";
                cin >> code;
                cout << "Enter Price: ";
                cin >> price;
                cout << "Enter Quantity: ";
                cin >> qty;
                cout << "Received Date (YYYY-MM-DD): ";
                cin >> received;
                cout << "Expiry Date (YYYY-MM-DD): ";
                cin >> expiry;

                root = insertProduct(root, code, name, price, qty, received, expiry);
                break;

            case 2:
                cout << "\nInventory (Sorted by Name):\n";
                inOrder(root);
                break;

            case 3:
                cout << "Enter Product Code to delete: ";
                cin >> code;
                root = deleteByCode(root, code);
                break;

            case 4:
                cout << "Enter today's date (YYYY-MM-DD): ";
                cin >> today;
                listExpired(root, today);
                break;

            case 5:
                cout << "Enter today's date (YYYY-MM-DD): ";
                cin >> today;
                root = deleteExpired(root, today);
                break;

            case 6:
                cout << "Exiting...\n";
                return 0;

            default:
                cout << "Invalid choice!\n";
        }
    }
}

```

## Output
--- PRODUCT INVENTORY (BST) ---
1. Insert Product
2. Display Inventory (InOrder)
3. Delete Product by Code
4. List Expired Products
5. Delete All Expired Products
6. Exit
Enter choice: 1
Enter Product Name: milk
Enter Product Code: 100
Enter Price: 67
Enter Quantity: 1
Received Date (YYYY-MM-DD): 2025-11-27
Expiry Date (YYYY-MM-DD): 2025-11-30

--- PRODUCT INVENTORY (BST) ---
1. Insert Product
2. Display Inventory (InOrder)
3. Delete Product by Code
4. List Expired Products
5. Delete All Expired Products
6. Exit
Enter choice: 1
Enter Product Name: bread
Enter Product Code: 90
Enter Price: 55
Enter Quantity: 1
Received Date (YYYY-MM-DD): 2025-11-27
Expiry Date (YYYY-MM-DD): 2025-12-01

--- PRODUCT INVENTORY (BST) ---
1. Insert Product
2. Display Inventory (InOrder)
3. Delete Product by Code
4. List Expired Products
5. Delete All Expired Products
6. Exit
Enter choice: 1
Enter Product Name: eggs
Enter Product Code: 110
Enter Price: 63
Enter Quantity: 1
Received Date (YYYY-MM-DD): 2025-11-27
Expiry Date (YYYY-MM-DD): 2025-12

--- PRODUCT INVENTORY (BST) ---
1. Insert Product
2. Display Inventory (InOrder)
3. Delete Product by Code
4. List Expired Products
5. Delete All Expired Products
6. Exit
Enter choice: 2

Inventory (Sorted by Name):
bread | Code: 90 | Price: 55 | Qty: 1 | Received: 2025-11-27 | Expiry: 2025-12-01
eggs | Code: 110 | Price: 63 | Qty: 1 | Received: 2025-11-27 | Expiry: 2025-12
milk | Code: 100 | Price: 67 | Qty: 1 | Received: 2025-11-27 | Expiry: 2025-11-30

--- PRODUCT INVENTORY (BST) ---
1. Insert Product
2. Display Inventory (InOrder)
3. Delete Product by Code
4. List Expired Products
5. Delete All Expired Products
6. Exit
Enter choice: 4
Enter today's date (YYYY-MM-DD): 2025-12-30
[EXPIRED] milk | Code: 100 | Expiry: 2025-11-30
[EXPIRED] bread | Code: 90 | Expiry: 2025-12-01
[EXPIRED] eggs | Code: 110 | Expiry: 2025-12

--- PRODUCT INVENTORY (BST) ---
1. Insert Product
2. Display Inventory (InOrder)
3. Delete Product by Code
4. List Expired Products
5. Delete All Expired Products
6. Exit
Enter choice: 3
Enter Product Code to delete: 110

--- PRODUCT INVENTORY (BST) ---
1. Insert Product
2. Display Inventory (InOrder)
3. Delete Product by Code
4. List Expired Products
5. Delete All Expired Products
6. Exit
Enter choice: 4
Enter today's date (YYYY-MM-DD): 2025-12-31
[EXPIRED] milk | Code: 100 | Expiry: 2025-11-30
[EXPIRED] bread | Code: 90 | Expiry: 2025-12-01

## Real-Life Applications
•	Pharmacy systems removing expired medicines
•	Supermarket inventory cleanup
•	Automated warehouse shelf management
•	E-commerce stock maintenance
•	Food industry systems tracking best-before dates

## Conclusion
Deletion operations in a tree-based inventory system maintain accuracy and prevent expired or invalid items from remaining in stock. Efficient management of deletions ensures reliability and real-time data correctness.