# Assignment 28


## Problem Statement
Write a program that maintains a queue of passengers waiting to see a ticket agent. The program user should be able to insert a new passenger at the rear of the queue, Display the passenger at the front of the Queue, or remove the passenger at the front of the queue. The program will display the number of passengers left in the queue just before it terminates.

## Theory
This system uses a simple queue to model passengers waiting for service. Passengers join the rear of the queue, and the ticket agent serves from the front. Linear queues work well when the capacity is known and deletions always happen in order.
Operations include insertion (enqueue), deletion (dequeue), and peeking at the front. Queues represent real-life waiting lines very closely and help simulate waiting times, load handling, and customer flow. Before program termination, the number of remaining passengers reflects how efficiently the system processed the queue.

## Code
```cpp
#include <iostream>
#include <string>
using namespace std;

string q[50];     
int front = -1, rear = -1;
int maxsize = 50;

void enqueue(string name)
{
    if(rear == maxsize - 1)
    {
        cout << "Queue is FULL!\n";
        return;
    }
    if(front == -1)  
        front = 0;

    q[++rear] = name;
    cout << "Passenger added.\n";
}

void dequeue()
{
    if(front == -1 || front > rear)
    {
        cout << "Queue is EMPTY!\n";
        return;
    }

    cout << "Passenger removed: " << q[front] << endl;
    front++;
}

void frontPassenger()
{
    if(front == -1 || front > rear)
    {
        cout << "Queue is EMPTY!\n";
        return;
    }
    cout << "Passenger at front: " << q[front] << endl;
}

int main()
{
    int ch;
    string name;

    while(true)
    {
        cout << "\n--- PASSENGER QUEUE ---\n";
        cout << "1. Add Passenger\n";
        cout << "2. Show Front Passenger\n";
        cout << "3. Remove Front Passenger\n";
        cout << "4. Exit\n";
        cout << "Enter choice: ";
        cin >> ch;

        switch(ch)
        {
            case 1:
                cout << "Enter passenger name: ";
                cin >> name;
                enqueue(name);
                break;

            case 2:
                frontPassenger();
                break;

            case 3:
                dequeue();
                break;

            case 4:
                cout << "\nPassengers remaining in queue: ";
                if(front == -1 || front > rear)
                    cout << 0 << endl;
                else
                    cout << (rear - front + 1) << endl;

                cout << "Exiting...\n";
                return 0;

            default:
                cout << "Invalid choice!\n";
        }
    }
}

```

## Output
--- PASSENGER QUEUE ---
1. Add Passenger
2. Show Front Passenger
3. Remove Front Passenger
4. Exit
Enter choice: 1
Enter passenger name: Parth
Passenger added.

--- PASSENGER QUEUE ---
1. Add Passenger
2. Show Front Passenger
3. Remove Front Passenger
4. Exit
Enter choice: 1
Enter passenger name: Yash
Passenger added.

--- PASSENGER QUEUE ---
1. Add Passenger
2. Show Front Passenger
3. Remove Front Passenger
4. Exit
Enter choice: 1
Enter passenger name: Prasad
Passenger added.

--- PASSENGER QUEUE ---
1. Add Passenger
2. Show Front Passenger
3. Remove Front Passenger
4. Exit
Enter choice: 2
Passenger at front: Parth

--- PASSENGER QUEUE ---
1. Add Passenger
2. Show Front Passenger
3. Remove Front Passenger
4. Exit
Enter choice: 3
Passenger removed: Parth

--- PASSENGER QUEUE ---
1. Add Passenger
2. Show Front Passenger
3. Remove Front Passenger
4. Exit
Enter choice: 2
Passenger at front: Yash

## Real-Life Applications
•	Waiting lines at bus stations or airports
•	Customer service counters
•	Drive-through food ordering
•	Ticket booking counters
•	Public service department queues (RTO, passport office)

## Conclusion
Using queues to manage passenger flow ensures systematic processing and reduces disorder. Linear queues offer simple, predictable behavior suitable for moderate-sized waiting lines.