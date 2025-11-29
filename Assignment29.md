# Assignment 29


## Problem Statement
Write a program to implement multiple queues i.e. two queues using array and perform following operations on it. A. Add Queue, B. Delete from Queue, C. Display Queue

## Theory
Multiple queues allow the simultaneous management of separate groups of items using one shared memory space. Two queues can be implemented within one array by dividing the array into two segments or by managing two pointers that grow toward each other.
This structure is especially useful in scenarios where different categories must be processed independently but share memory resources. Operations such as enqueue, dequeue, and display must ensure that queues do not collide and remain within boundaries. The challenge is efficient partitioning and preventing overflow in one queue when the other still has free space.

## Code
```cpp
#include <iostream>
using namespace std;

int q[10];
int front1 = -1, rear1 = -1;
int front2 = -1, rear2 = -1;

void enqueue1(int x)
{
    if(rear1 == 4)  
    {
        cout << "Queue 1 is FULL!\n";
        return;
    }
    if(front1 == -1) front1 = 0;

    q[++rear1] = x;
    cout << "Inserted in Queue 1\n";
}

void enqueue2(int x)
{
    if(rear2 == 9)   
    {
        cout << "Queue 2 is FULL!\n";
        return;
    }
    if(front2 == -1) front2 = 5;

    if(rear2 == -1) rear2 = 4;  

    q[++rear2] = x;
    cout << "Inserted in Queue 2\n";
}

void dequeue1()
{
    if(front1 == -1 || front1 > rear1)
    {
        cout << "Queue 1 is EMPTY!\n";
        return;
    }
    cout << "Deleted from Queue 1: " << q[front1++] << endl;
}

void dequeue2()
{
    if(front2 == -1 || front2 > rear2)
    {
        cout << "Queue 2 is EMPTY!\n";
        return;
    }
    cout << "Deleted from Queue 2: " << q[front2++] << endl;
}

void display1()
{
    if(front1 == -1 || front1 > rear1)
    {
        cout << "Queue 1 is EMPTY!\n";
        return;
    }
    cout << "Queue 1: ";
    for(int i = front1; i <= rear1; i++)
        cout << q[i] << " ";
    cout << endl;
}

void display2()
{
    if(front2 == -1 || front2 > rear2)
    {
        cout << "Queue 2 is EMPTY!\n";
        return;
    }
    cout << "Queue 2: ";
    for(int i = front2; i <= rear2; i++)
        cout << q[i] << " ";
    cout << endl;
}

int main()
{
    int ch, qn, x;

    while(true)
    {
        cout << "\n--- MULTIPLE QUEUES (2 Queues in One Array) ---\n";
        cout << "1. Add to Queue\n";
        cout << "2. Delete from Queue\n";
        cout << "3. Display Queue\n";
        cout << "4. Exit\n";
        cout << "Enter choice: ";
        cin >> ch;

        switch(ch)
        {
            case 1:
                cout << "Enter Queue number (1 or 2): ";
                cin >> qn;
                cout << "Enter value: ";
                cin >> x;

                if(qn == 1) enqueue1(x);
                else if(qn == 2) enqueue2(x);
                else cout << "Invalid Queue number!\n";
                break;

            case 2:
                cout << "Enter Queue number (1 or 2): ";
                cin >> qn;

                if(qn == 1) dequeue1();
                else if(qn == 2) dequeue2();
                else cout << "Invalid Queue number!\n";
                break;

            case 3:
                cout << "Enter Queue number (1 or 2): ";
                cin >> qn;

                if(qn == 1) display1();
                else if(qn == 2) display2();
                else cout << "Invalid Queue number!\n";
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
--- MULTIPLE QUEUES (2 Queues in One Array) ---
1. Add to Queue
2. Delete from Queue
3. Display Queue
4. Exit
Enter choice: 1
Enter Queue number (1 or 2): 1
Enter value: 10
Inserted in Queue 1

--- MULTIPLE QUEUES (2 Queues in One Array) ---
1. Add to Queue
2. Delete from Queue
3. Display Queue
4. Exit
Enter choice: 1
Enter Queue number (1 or 2): 1
Enter value: 20
Inserted in Queue 1

--- MULTIPLE QUEUES (2 Queues in One Array) ---
1. Add to Queue
2. Delete from Queue
3. Display Queue
4. Exit
Enter choice: 1
Enter Queue number (1 or 2): 1
Enter value: 30
Inserted in Queue 1

--- MULTIPLE QUEUES (2 Queues in One Array) ---
1. Add to Queue
2. Delete from Queue
3. Display Queue
4. Exit
Enter choice: 1
Enter Queue number (1 or 2): 2
Enter value: 40
Inserted in Queue 2

--- MULTIPLE QUEUES (2 Queues in One Array) ---
1. Add to Queue
2. Delete from Queue
3. Display Queue
4. Exit
Enter choice: 1
Enter Queue number (1 or 2): 2
Enter value: 50
Inserted in Queue 2

--- MULTIPLE QUEUES (2 Queues in One Array) ---
1. Add to Queue
2. Delete from Queue
3. Display Queue
4. Exit
Enter choice: 3
Enter Queue number (1 or 2): 1
Queue 1: 10 20 30

--- MULTIPLE QUEUES (2 Queues in One Array) ---
1. Add to Queue
2. Delete from Queue
3. Display Queue
4. Exit
Enter choice: 3
Enter Queue number (1 or 2): 2
Queue 2: 40 50

--- MULTIPLE QUEUES (2 Queues in One Array) ---
1. Add to Queue
2. Delete from Queue
3. Display Queue
4. Exit
Enter choice: 2
Enter Queue number (1 or 2): 1
Deleted from Queue 1: 10

## Real-Life Applications
•	Managing multiple service counters (e.g., Billing Queue & Inquiry Queue)
•	Multilevel priority scheduling in operating systems
•	Simultaneous input streams (e.g., sensor queues)
•	Message buffering in communication systems
•	Multi-lane toll booth simulation

## Conclusion
Multiple queues implemented using a single array allow efficient parallel management of data streams without extra memory overhead. This is especially valuable in constrained or embedded environments.