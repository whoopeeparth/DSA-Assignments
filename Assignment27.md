# Assignment 27


## Problem Statement
Pizza parlour accepting maximum n orders. Orders are served on an FCFS basis. Order once placed can’t be cancelled. Write C++ program to simulate the system using circular QUEUE.

## Theory
A circular queue is an optimized version of the linear queue in which the last position connects back to the first, forming a circle. This prevents the "false overflow" that occurs in simple queues when rear reaches the end of the array even though empty spaces exist at the front.
In a pizza parlour, only a limited number of orders can be accepted at once due to capacity constraints. Orders are taken in FCFS order and once placed cannot be canceled—making circular queues ideal. The circular queue allows efficient use of memory, constant-time operations for enqueue/dequeue, and a logical structure that mirrors real-world order processing.

## Code
```cpp
#include <iostream>
#include <cstdlib>
using namespace std;    

#define MAX 5

int orders[MAX];
int front = -1, rear = -1;

void placeOrder()
{
    if(rear == MAX - 1)
    {
        cout<<"Sorry! No more orders can be accepted.\n";
        return;
    }

    int orderId;
    cout<<"Enter Order ID: ";
    cin>>orderId;

    if(front == -1)
    {
        front = 0;
    }

    rear++;
    orders[rear] = orderId;

    cout<<"Order "<<orderId<<" placed successfully.\n";
}

void serveOrder()
{
    if(front == -1 || front > rear)
    {
        cout<<"No orders to serve.\n";
        return;
    }

    cout<<"Order "<<orders[front]<<" served.\n";
    front++;

    if(front > rear)
    {
        front = rear = -1;
    }
}

void displayOrders()
{
    if(front == -1 || front > rear)
    {
        cout<<"No pending orders.\n";
        return;
    }
    cout<<"Pending orders: ";
    for(int i = front; i <= rear; i++)
    {
        cout<<orders[i]<<" ";
    }
    cout<<endl;
}

int main()
{
    int ch;

    while(true)
    {
        cout << "\n----- Pizza Parlour Order System -----\n";
        cout << "1. Place Order\n";
        cout << "2. Serve Order\n";
        cout << "3. Display Pending Orders\n";
        cout << "4. Exit\n";
        cout << "Enter your choice: ";
        cin >> ch;

        switch(ch)
        {
            case 1:
                placeOrder();
                break;

            case 2:
                serveOrder();
                break;

            case 3:
                displayOrders();
                break;
            
            case 4:
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
----- Pizza Parlour Order System -----
1. Place Order
2. Serve Order
3. Display Pending Orders
4. Exit
Enter your choice: 1
Enter Order ID: 1
Order 1 placed successfully.

----- Pizza Parlour Order System -----
1. Place Order
2. Serve Order
3. Display Pending Orders
4. Exit
Enter your choice: 1
Enter Order ID: 2
Order 2 placed successfully.

----- Pizza Parlour Order System -----
1. Place Order
2. Serve Order
3. Display Pending Orders
4. Exit
Enter your choice: 1
Enter Order ID: 3
Order 3 placed successfully.

----- Pizza Parlour Order System -----
1. Place Order
2. Serve Order
3. Display Pending Orders
4. Exit
Enter your choice: 2
Order 1 served.

----- Pizza Parlour Order System -----
1. Place Order
2. Serve Order
3. Display Pending Orders
4. Exit
Enter your choice: 3
Pending orders: 2 3

## Real-Life Applications
•	Restaurant order management systems
•	CPU scheduling (Round Robin method)
•	Call centers with limited call queues
•	Print spoolers managing print jobs
•	Network packet buffering

## Conclusion
Circular queues maximize memory usage and maintain strict FCFS order, making them highly suitable for managing limited-capacity systems like food orders or job scheduling.