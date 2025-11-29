# Assignment 30


## Problem Statement
In a call center, customer calls are handled on a first-come, first-served basis. Implement a queue system using Linked list where:
●	Each customer call is enqueued as it arrives.
●	Customer service agents dequeue calls to assist customers.
If there are no calls, the system waits.

## Theory
A linked-list-based queue supports dynamic memory allocation, which is crucial for systems where the number of incoming calls can vary significantly. New calls are enqueued as they arrive, and customer-service agents dequeue calls when they are ready.
Using a linked list avoids overflow problems and allows the queue to expand as needed. This design represents call-center behavior accurately, where calls cannot be dropped or held indefinitely. If no calls exist, the system simply waits, reflecting real waiting conditions. The queue operations run in O(1) time because insertion occurs at the tail and removal occurs from the head.

## Code
```cpp
#include <iostream>
using namespace std;

struct Node {
    string name;   
    Node* next;
};

Node* front = NULL;
Node* rear = NULL;

void enqueue(string n)
{
    Node* temp = new Node();
    temp->name = n;
    temp->next = NULL;

    if(front == NULL)  
    {
        front = rear = temp;
    }
    else
    {
        rear->next = temp;
        rear = temp;
    }
    cout << "Call enqueued.\n";
}

void dequeue()
{
    if(front == NULL)
    {
        cout << "No calls in queue. Waiting...\n";
        return;
    }
    Node* temp = front;
    cout << "Call handled: " << front->name << endl;
    front = front->next;

    if(front == NULL) 
        rear = NULL;

    delete temp;
}

void showFront()
{
    if(front == NULL)
    {
        cout << "No calls waiting.\n";
        return;
    }
    cout << "Next call in queue: " << front->name << endl;
}

void display()
{
    if(front == NULL)
    {
        cout << "No calls waiting.\n";
        return;
    }
    cout << "Current Call Queue: ";
    Node* t = front;
    while(t != NULL)
    {
        cout << t->name << " ";
        t = t->next;
    }
    cout << endl;
}

int main()
{
    int ch;
    string name;

    while(true)
    {
        cout << "\n--- CALL CENTER QUEUE ---\n";
        cout << "1. Add Customer Call\n";
        cout << "2. Handle Next Call\n";
        cout << "3. Show Next Call\n";
        cout << "4. Display All Calls\n";
        cout << "5. Exit\n";
        cout << "Enter choice: ";
        cin >> ch;

        switch(ch)
        {
            case 1:
                cout << "Enter customer name / call ID: ";
                cin >> name;
                enqueue(name);
                break;

            case 2:
                dequeue();
                break;

            case 3:
                showFront();
                break;

            case 4:
                display();
                break;

            case 5:
                cout << "Exiting...\n";
                return 0;

            default:
                cout << "Invalid choice!\n";
        }
    }
}

```

## Output
--- CALL CENTER QUEUE ---
1. Add Customer Call
2. Handle Next Call
3. Show Next Call
4. Display All Calls
5. Exit
Enter choice: 1
Enter customer name / call ID: Parth
Call enqueued.

--- CALL CENTER QUEUE ---
1. Add Customer Call
2. Handle Next Call
3. Show Next Call
4. Display All Calls
5. Exit
Enter choice: 1
Enter customer name / call ID: Yash
Call enqueued.

--- CALL CENTER QUEUE ---
1. Add Customer Call
2. Handle Next Call
3. Show Next Call
4. Display All Calls
5. Exit
Enter choice: 4
Current Call Queue: Parth Yash

--- CALL CENTER QUEUE ---
1. Add Customer Call
2. Handle Next Call
3. Show Next Call
4. Display All Calls
5. Exit
Enter choice: 2
Call handled: Parth

--- CALL CENTER QUEUE ---
1. Add Customer Call
2. Handle Next Call
3. Show Next Call
4. Display All Calls
5. Exit
Enter choice: 3
Next call in queue: Yash

## Real-Life Applications
•	Call centers handling customer support requests
•	Task scheduling in asynchronous systems
•	Real-time server request handling
•	Chatbot message queues
•	Emergency helpline call management

## Conclusion
A linked-list queue provides flexibility and stability for unpredictable workloads like customer calls. Efficient memory usage and dynamic scalability make it ideal for real-time customer-service environments.