# Assignment 26


## Problem Statement
Write a program to keep track of patients as they checked into a medical clinic, assigning patients to doctors on a first-come, first-served basis.

## Theory
A queue is a First-Come, First-Served (FCFS) linear data structure in which insertion occurs at the rear and removal occurs at the front. This structure is ideal for managing situations where fairness and order are essential, such as patient check-ins at a clinic. When patients arrive, they are added to the rear of the queue; when a doctor becomes available, the next patient is taken from the front.
Using a queue ensures that no patient is skipped or treated out of order. This method minimizes disputes, maintains fairness, and ensures efficient flow. The queue may be implemented using arrays or linked lists, but linked lists are typically preferred because they allow dynamic memory allocation and prevent overflow unless system memory is exhausted.

## Code
```cpp
#include <iostream>
#include <cstdlib>
#include <string>
using namespace std;

struct Node
{
    string name;
    Node* next;
};

Node* front = NULL;
Node* rear = NULL;

void checkIn()
{
    Node* newNode = new Node;
    cout<<"Enter patient name: ";
    cin.ignore();
    getline(cin, newNode->name);
    newNode->next = NULL;

    if(front == NULL)
    {
        front = rear = newNode;
    }
    else
    {
        rear->next = newNode;
        rear = newNode;
    }
    cout<<"Patient "<<newNode->name<<" checked in successfully";
}

void assignPatient()
{
    if(front == NULL)
    {
        cout<<"No patients waiting.\n";
        return;
    }

    Node* temp = front;
    cout<<"Doctor is now seeing patient: "<<temp->name<<endl;
    front = front->next;

    if(front == NULL)
    {
        rear = NULL;
    }
    delete temp;
}

void displayQueue()
{
        if(front == NULL)
        {
            cout<<"No patients waiting.\n";
            return;
        }

        Node* temp = front;
        int count = 1;

        cout<<"Patients waiting in queue: \n";
        while(temp)
        {
            cout<<count++<<". "<<temp->name<<endl;
            temp = temp->next;
        }
}

int main()
{
    int ch;

    while(true)
    {
        cout << "\n----- Medical Clinic Queue System -----\n";
        cout << "1. Check-in Patient\n";
        cout << "2. Assign Patient to Doctor\n";
        cout << "3. Display Waiting Patients\n";
        cout << "4. Exit\n";
        cout << "Enter your choice: ";
        cin >> ch;

        switch(ch)
        {
            case 1:
                checkIn();
                break;

            case 2:
                assignPatient();
                break;

            case 3:
                displayQueue();
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
----- Medical Clinic Queue System (Linked List) -----
1. Check-in Patient
2. Assign Patient to Doctor (Next in Queue)
3. Display Waiting Patients
4. Exit
Enter your choice: 1
Enter patient name: Parth
Patient Parth checked in successfully
----- Medical Clinic Queue System (Linked List) -----
1. Check-in Patient
2. Assign Patient to Doctor (Next in Queue)
3. Display Waiting Patients
4. Exit
Enter your choice: 1
Enter patient name: Yash
Patient Yash checked in successfully
----- Medical Clinic Queue System (Linked List) -----
1. Check-in Patient
2. Assign Patient to Doctor (Next in Queue)
3. Display Waiting Patients
4. Exit
Enter your choice: 1
Enter patient name: Prasad
Patient Prasad checked in successfully
----- Medical Clinic Queue System (Linked List) -----
1. Check-in Patient
2. Assign Patient to Doctor (Next in Queue)
3. Display Waiting Patients
4. Exit
Enter your choice: 2
Doctor is now seeing patient: Parth

----- Medical Clinic Queue System (Linked List) -----
1. Check-in Patient
2. Assign Patient to Doctor (Next in Queue)
3. Display Waiting Patients
4. Exit
Enter your choice: 3
Patients waiting in queue:
1. Yash
2. Prasad

## Real-Life Applications
•	Hospital and clinic patient management systems
•	Bank or government-office line management
•	Scheduling processes in operating systems
•	Airport check-in and boarding queues
•	Customer-support priority allocation systems

## Conclusion
Implementing a patient-management system using a queue guarantees fairness and efficiency. It models real clinic behavior accurately and forms a highly reliable system for sequential task handling.