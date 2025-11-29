# Assignment 39


## Problem Statement
Write a program to implement a product inventory management system for a shop using a search tree data structure. Each product must store the following information:
●	Unique Product Code
●	Product Name
●	Price
●	Quantity in Stock
●	Date Received
●	Expiration Date
Implement the following operations:
1.	Insert a product into the tree ( organized by product name).
2.	Display all items in the inventory using inorder traversal.
3.	List expired items in prefix (preorder) order of their names.

## Theory
A search tree stores product data such as code, name, price, stock quantity, date received, and expiration date. Organizing the tree by product name makes alphabetical searches efficient.
•	Insert places new products into their alphabetical position.
•	Inorder traversal displays items in sorted order by name, which is ideal for inventory listing.
•	Preorder traversal is used to list expired items in a structured, hierarchical manner. Since preorder processes the root first, it helps generate quick reports and prioritize urgent items.
Search trees allow dynamic product addition, easy searching, and structured inventory representation.

## Code
```cpp
#include <iostream>
#include <string>
using namespace std;

struct Product {
    string name;
    string code;
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
    Product* newNode = new Product();
    newNode->name = name;
    newNode->code = code;
    newNode->price = price;
    newNode->qty = qty;
    newNode->received = received;
    newNode->expiry = expiry;
    newNode->left = newNode->right = nullptr;

    return newNode;
}

Product* insertProduct(Product* root, string code, string name,
                       float price, int qty, string received, string expiry)
{
    if(root == nullptr)
    {
        return createNode(code, name, price, qty, received, expiry);
    }

    if(name < root->name)
    {
        root->left = insertProduct(root->left, code, name, price, qty, received, expiry);
    }
    else if(name > root->name)
    {
        root->right = insertProduct(root->right, code, name, price, qty, received, expiry);
    }
    else
    {
        cout << "Duplicate product name NOT allowed.\n";
    }

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

void listExpired(Product* root, string today)
{
    if(!root) 
        return;

    if(root->expiry < today)
    {
        cout << "[EXPIRED] " << root->name
             << " | Code: " << root->code
             << " | Expired: " << root->expiry << endl;
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
        cout << "\n-----PRODUCT INVENTORY (BST)-----\n";
        cout << "1. Insert Product\n";
        cout << "2. Display All (InOrder)\n";
        cout << "3. List Expired Items (Preorder)\n";
        cout << "4. Exit\n";
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
                cout << "Enter Received Date (YYYY-MM-DD): ";
                cin >> received;
                cout << "Enter Expiry Date (YYYY-MM-DD): ";
                cin >> expiry;

                root = insertProduct(root, code, name, price, qty, received, expiry);
                break;

            case 2:
                cout << "\nInventory (Sorted by name):\n";
                inOrder(root);
                break;

            case 3:
                cout << "Enter Today's Date (YYYY-MM-DD): ";
                cin >> today;
                cout << "\nExpired Products:\n";
                listExpired(root, today);
                break;

            case 4:
                cout << "Exiting...\n";
                return 0;

            default:
                cout << "Invalid choice!\n";
        }
    }
}

```

## Output
-----PRODUCT INVENTORY (BST)-----
1. Insert Product
2. Display All (InOrder)
3. List Expired Items (Preorder)
4. Exit
Enter choice: 1
Enter Product Name: Milk
Enter Product Code: 100
Enter Price: 500
Enter Quantity: 1
Enter Received Date (YYYY-MM-DD): 2025-11-27
Enter Expiry Date (YYYY-MM-DD): 2025-11-30

-----PRODUCT INVENTORY (BST)-----
1. Insert Product
2. Display All (InOrder)
3. List Expired Items (Preorder)
4. Exit
Enter choice: 1
Enter Product Name: Bread
Enter Product Code: 90
Enter Price: 70
Enter Quantity: 1
Enter Received Date (YYYY-MM-DD): 2025-11-28
Enter Expiry Date (YYYY-MM-DD): 2025-12-01

-----PRODUCT INVENTORY (BST)-----
1. Insert Product
2. Display All (InOrder)
3. List Expired Items (Preorder)
4. Exit
Enter choice: 1
Enter Product Name: Eggs
Enter Product Code: 110
Enter Price: 40
Enter Quantity: 1
Enter Received Date (YYYY-MM-DD): 2025-11-29
Enter Expiry Date (YYYY-MM-DD): 2025-12-30

-----PRODUCT INVENTORY (BST)-----
1. Insert Product
2. Display All (InOrder)
3. List Expired Items (Preorder)
4. Exit
Enter choice: 2

Inventory (Sorted by name):
Bread | Code: 90 | Price: 70 | Qty: 1 | Received: 2025-11-28 | Expiry: 2025-12-01
Eggs | Code: 110 | Price: 40 | Qty: 1 | Received: 2025-11-29 | Expiry: 2025-12-30
Milk | Code: 100 | Price: 500 | Qty: 1 | Received: 2025-11-27 | Expiry: 2025-11-30

-----PRODUCT INVENTORY (BST)-----
1. Insert Product
2. Display All (InOrder)
3. List Expired Items (Preorder)
4. Exit
Enter choice: 3
Enter Today's Date (YYYY-MM-DD): 2025-12-01

Expired Products:
[EXPIRED] Milk | Code: 100 | Expired: 2025-11-30

## Real-Life Applications
•	Retail store stock management systems
•	Warehouse inventory management
•	Pharmacy systems with expiry tracking
•	Online marketplace product catalogs
•	Supermarket inventory software

## Conclusion
A search tree provides a robust backbone for inventory systems—supporting quick insertion, sorted display, and efficient expiration-based filtering.