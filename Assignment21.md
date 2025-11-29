# Assignment 21


## Problem Statement
WAP to build a simple stock price tracker that keeps a history of daily stock prices entered by the user. To allow users to go back and view or remove the most recent price, implement a stack using a linked list to store these integer prices.
Implement the following operations:
1.	record(price) – Add a new stock price (an integer) to the stack.
2.	remove() – Remove and return the most recent price (top of the stack).
3.	latest() – Return the most recent stock price without removing it.
isEmpty() – Check if there are no prices recorded.

## Theory
A stack is a Last-In-First-Out (LIFO) data structure commonly implemented using a linked list to allow dynamic memory allocation and efficient insertion/deletion from the top. Each new stock price is treated as a node pushed onto the stack, so the most recent price always stays at the top. This design reflects how stock analysis tools maintain recent data—for example, analysts often look at the most recent days first.
Using a linked list avoids overflow problems common in array-based stacks unless system memory exhausts. Operations like record(), remove(), and latest() run in constant time O(1), making the stack ideal for applications that require quick access to the most recent entry. The structure supports flexible growth, makes undo-like operations easy, and mirrors real-world tracking systems where the newest data is often accessed first.

## Code
```cpp
#include <iostream>
#include <cstdlib>
using namespace std;

typedef struct Node
{
    int price;
    struct Node* next;
}Node;

Node* top = NULL;

bool isEmpty()
{
    return top == NULL;
}

void recordPrice()
{
    Node* newNode = new Node();
    cout<<"Enter Stock Price: ";
    cin>>newNode -> price;
    newNode -> next = top;
    top = newNode;
    cout<<"Price recorded.\n";
}

void removePrice()
{
    if(isEmpty())
    {
        cout<<"No prices to remove.\n";
        return;
    }

    Node* temp = top;
    cout<<"Removed price: "<<top -> price<<endl;
    top = top -> next;
    delete temp;
}

void latestPrice()
{
    if(isEmpty())
    {
        cout<<"No prices recorded.\n";
        return;
    }

    cout<<"Latest recorded price: "<<top -> price<<endl;
}

void displayPrices()
{
    if(isEmpty())
    {
        cout<<"No prices recorded.\n";
        return;
    }

    cout<<"Stock prices: \n";
    Node* temp = top;
    while(temp)
    {
        cout<<temp -> price<<" ";
        temp = temp -> next;
    }
    cout<<endl;
}

int main()
{
    int ch;
    while(1)
    {
        cout<<"\n-----Stock Price Tracker-----\n";
        cout<<"1. Record New Price\n";
        cout<<"2. Remove Most Recent Price\n";
        cout<<"3. View Latest Price\n";
        cout<<"4. Display Prices\n";
        cout<<"5. Check if Empty\n";
        cout<<"6. Exit\n";
        cout<<"Enter your choice: ";
        cin>>ch;

        switch(ch)
        {
            case 1:
                recordPrice();
                break;

            case 2:
                removePrice();
                break;

            case 3:
                latestPrice();
                break;

            case 4:
                displayPrices();
                break;

            case 5:
                if(isEmpty())
                {
                    cout<<"No prices recorded. Stack is empty.\n";
                }
                else
                {
                    cout<<"Stack is not empty.\n";
                }
                break;

            case 6:
                cout<<"Exiting...\n";
                exit(0);

            default:
                cout<<"Invalid choice!\n";
        }
    }
    return 0;
}

```

## Output
-----Stock Price Tracker-----
1. Record New Price
2. Remove Most Recent Price
3. View Latest Price
4. Display Prices
5. Check if Empty
6. Exit
Enter your choice: 1
Enter Stock Price: 100
Price recorded.

-----Stock Price Tracker-----
1. Record New Price
2. Remove Most Recent Price
3. View Latest Price
4. Display Prices
5. Check if Empty
6. Exit
Enter your choice: 1
Enter Stock Price: 50
Price recorded.

-----Stock Price Tracker-----
1. Record New Price
2. Remove Most Recent Price
3. View Latest Price
4. Display Prices
5. Check if Empty
6. Exit
Enter your choice: 1
Enter Stock Price: 250
Price recorded.

-----Stock Price Tracker-----
1. Record New Price
2. Remove Most Recent Price
3. View Latest Price
4. Display Prices
5. Check if Empty
6. Exit
Enter your choice: 4
Stock prices:
250 50 100

-----Stock Price Tracker-----
1. Record New Price
2. Remove Most Recent Price
3. View Latest Price
4. Display Prices
5. Check if Empty
6. Exit
Enter your choice: 2
Removed price: 250

-----Stock Price Tracker-----
1. Record New Price
2. Remove Most Recent Price
3. View Latest Price
4. Display Prices
5. Check if Empty
6. Exit
Enter your choice: 4
Stock prices:
50 100

-----Stock Price Tracker-----
1. Record New Price
2. Remove Most Recent Price
3. View Latest Price
4. Display Prices
5. Check if Empty
6. Exit
Enter your choice: 3
Latest recorded price: 50

## Real-Life Applications
•	Stock market analysis tools that need quick retrieval of recent prices
•	Undo/redo systems in editors or trading dashboards
•	Browser history where the latest page is accessed first
•	Time-series applications such as sensor data monitoring
•	Stream processing where newest values are processed immediately

## Conclusion
Implementing a stock price tracker with a stack provides efficient, real-time access to the latest data while enabling easy rollback of entries. The linked list version is flexible, memory-efficient, and ideal for dynamic historical tracking.