# Assignment 15


## Problem Statement
Write a C++ program to store a binary number using a doubly linked list. Implement the following functions:
a) Calculate and display the 1’s complement and 2’s complement of the stored binary number.
b) Perform addition of two binary numbers represented using doubly linked lists and display the result.

## Theory
Binary numbers can be represented more flexibly using a doubly linked list, where each node holds a single bit. The doubly linked structure allows traversal in both directions, which is useful when performing operations like 1's and 2's complement or binary addition.
1’s complement is obtained by flipping the bits, while 2’s complement is derived by adding 1 to the 1’s complement. Binary addition is performed from LSB to MSB, carrying values as needed. Linked lists allow easy bit-by-bit manipulation without relying on fixed-size data types.
This assignment demonstrates how complex numerical operations can be performed using linked data structures instead of built-in integer variables, which is useful for handling large binary numbers.

## Code
```cpp
#include <iostream>
#include <cstdlib>
using namespace std;

struct Node
{
    int bit;
    Node* next;
    Node* prev;
};

Node* head1 = NULL;
Node* head2 = NULL;

Node* createBinary()
{
    int n;
    cout<<"Enter number of bits: ";
    cin>>n;

    Node* head = NULL;
    Node* temp = NULL;

    for(int i = 0; i < n; i++)
    {
        Node* newNode = new Node();
        cout<<"Enter bit "<<i + 1<<" : ";
        cin>>newNode -> bit;
        newNode -> next = NULL;
        newNode -> prev = NULL;

        if(head == NULL)
        {
            head = newNode;
            temp = newNode;
        }
        else
        {
            temp -> next = newNode;
            newNode -> prev = temp;
            temp = newNode;
        }
    }

    return head;
}

void displayBinary(Node* head)
{
    Node* temp = head;
    while(temp)
    {
        cout<<temp -> bit;
        temp = temp -> next;
    }
    cout<<endl;
}

Node* copyList(Node* original)
{
    if(original == NULL)
    {
        return NULL;
    }
    Node* newHead = NULL;
    Node* temp = NULL;
    Node* curr = original;

    while(curr)
    {
        Node* newNode = new Node();
        newNode -> bit = curr -> bit;
        newNode -> next = NULL;
        newNode -> prev = NULL;

        if(newHead == NULL)
        {
            newHead = newNode;
            temp = newNode;
        }
        else
        {
            temp -> next = newNode;
            newNode -> prev = temp;
            temp = newNode;
        }
        curr = curr -> next;
    }
    return newHead;
}

void onesComplement(Node* head)
{
    Node* temp = head;
    while(temp)
    {
        if(temp -> bit == 0)
        {
            temp -> bit = 1;
        }
        else
        {
            temp -> bit = 0;
        }
        temp = temp -> next;
    }
}

void twosComplement(Node* head)
{
    onesComplement(head);

    Node* temp = head;
    while(temp -> next)
    {
        temp = temp -> next;
    }

    int carry = 1;
    while(temp)
    {
        int sum = temp -> bit + carry;
        if(sum == 2)
        {
            temp -> bit = 0;
            carry = 1;
        }
        else
        {
            temp -> bit = sum;
            carry = 0;
        }
        temp = temp -> prev;
    }
}

Node* addBinary(Node* h1, Node* h2)
{
    Node* t1 = h1;
    Node* t2 = h2;

    while(t1 -> next)
    {
        t1 = t1 -> next;
    }
    while(t2 -> next)
    {
        t2 = t2 -> next;
    }

    Node* result = NULL;
    int carry = 0;

    while(t1 != NULL || t2 != NULL)
    {
        int b1 = (t1 != NULL) ? t1 -> bit : 0;
        int b2 = (t2 != NULL) ? t2 -> bit : 0;
        int sum = b1 + b2 + carry;

        Node* newNode = new Node();
        newNode -> bit = sum % 2;
        newNode -> next = result;
        newNode -> prev = NULL;
        if(result != NULL)
        {
            result -> prev = newNode;
        }
        result = newNode;
        carry = sum / 2;

        if(t1)
        {
            t1 = t1 -> prev;
        }
        if(t2)
        {
            t2 = t2 -> prev;
        }
    }
    if(carry == 1)
    {
        Node* newNode = new Node();
        newNode -> bit = 1;
        newNode -> next = result;
        newNode -> prev = NULL;
        result -> prev = newNode;
        result = newNode;
    }
    return result;
}

int main() {
    int choice;

    while (true) {
        cout << "\n----- Binary Number Operations -----\n";
        cout << "1. Enter first binary number\n";
        cout << "2. Enter second binary number\n";
        cout << "3. Display binary numbers\n";
        cout << "4. 1's and 2's complement of first number\n";
        cout << "5. Add two binary numbers\n";
        cout << "6. Exit\n";
        cout << "Enter your choice: ";
        cin >> choice;

        switch (choice) {
            case 1:
                head1 = createBinary();
                break;
                
            case 2:
                head2 = createBinary();
                break;

            case 3:
                cout << "First binary number: ";
                displayBinary(head1);
                cout << "Second binary number: ";
                displayBinary(head2);
                break;

            case 4:
                if (head1 != NULL) {
                    Node* copy1 = copyList(head1);
                    Node* copy2 = copyList(head1);
                    onesComplement(copy1);
                    cout<<"1's complement: ";
                    displayBinary(copy1);
                    twosComplement(copy2);
                    cout<<"2's complement: ";
                    displayBinary(copy2);
                } else {
                    cout << "First binary number not entered.\n";
                }
                break;

            case 5:
                if (head1 != NULL && head2 != NULL) {
                    Node* sum = addBinary(head1, head2);
                    cout << "Sum of binary numbers: ";
                    displayBinary(sum);
                } else {
                    cout << "Enter both binary numbers first.\n";
                }
                break;

            case 6:
                cout << "Exiting...\n";
                exit(0);

            default:
                cout << "Invalid choice!\n";
        }
    }

    return 0;
}

```

## Output
----- Binary Number Operations -----
1. Enter first binary number
2. Enter second binary number
3. Display binary numbers
4. 1's and 2's complement of first number
5. Add two binary numbers
6. Exit
Enter your choice: 1
Enter number of bits: 4
Enter bit 1 : 1
Enter bit 2 : 1
Enter bit 3 : 0
Enter bit 4 : 1

----- Binary Number Operations -----
1. Enter first binary number
2. Enter second binary number
3. Display binary numbers
4. 1's and 2's complement of first number
5. Add two binary numbers
6. Exit
Enter your choice: 2
Enter number of bits: 4
Enter bit 1 : 1
Enter bit 2 : 0
Enter bit 3 : 1
Enter bit 4 : 1

----- Binary Number Operations -----
1. Enter first binary number
2. Enter second binary number
3. Display binary numbers
4. 1's and 2's complement of first number
5. Add two binary numbers
6. Exit
Enter your choice: 3
First binary number: 1101
Second binary number: 1011

----- Binary Number Operations -----
1. Enter first binary number
2. Enter second binary number
3. Display binary numbers
4. 1's and 2's complement of first number
5. Add two binary numbers
6. Exit
Enter your choice: 4
1's complement: 0010
2's complement: 0011

----- Binary Number Operations -----
1. Enter first binary number
2. Enter second binary number
3. Display binary numbers
4. 1's and 2's complement of first number
5. Add two binary numbers
6. Exit
Enter your choice: 5
Sum of binary numbers: 11000

## Real-Life Applications
•	Implementing arithmetic in low-level systems or simulators.
•	Binary operations in digital logic and processor design.
•	Handling extremely large numbers in cryptography.
•	Simulating registers in computer architecture.
•	Performing bit-level operations in embedded systems.

## Conclusion
Using a doubly linked list to store and manipulate binary numbers allows flexible, scalable bit-level operations. This assignment strengthens understanding of binary arithmetic and linked list-based memory representation.