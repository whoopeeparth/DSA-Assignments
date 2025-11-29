# Assignment 13


## Problem Statement
Develop a C++ program to store and manage an appointment schedule for a single day. Appointments should be scheduled randomly using a linked list. The system must define the start time, end time, and specify the minimum and maximum duration allowed for each appointment slot.
The program should include the following operations:
a) Display the list of currently available time slots.
 b) Book a new appointment within the defined time limits.
 c) Cancel an existing appointment after validating its time, availability, and correctness.
 d) Sort the appointment list in order of appointment times.
 e) Sort the list based on appointment times using pointer manipulation (without swapping data values).

## Theory
Managing appointment schedules requires dynamic insertion and deletion based on time slots. Linked lists are ideal because they allow new appointments to be added without shifting elements. Each appointment node contains details such as start time, end time, and duration.
The system checks time constraints to avoid overlaps and maintains proper sequence of appointments. Sorting by appointment time ensures a chronological listing, and pointer manipulation sorting demonstrates advanced linked list operations. This model reflects real scheduling systems where time-bound data must be managed efficiently and accurately.

## Code
```cpp
#include <iostream>
#include <cstdlib>
#include <string>
using namespace std;

struct Appointment
{
    int startHour;
    int startMin;
    int endHour;
    int endMin;
    bool booked;
    string name;
    Appointment* next;
};

Appointment* head = NULL;

void createSchedule(int startHour, int endHour)
{
    Appointment* temp = NULL;

    for(int h = startHour; h < endHour; h++)
    {
        Appointment* newNode = new Appointment();
        newNode -> startHour = h;
        newNode -> startMin = 0;
        newNode -> endHour = h + 1;
        newNode -> endMin = 0;
        newNode -> booked = false;
        newNode -> name = "";
        newNode -> next = NULL;

        if(head == NULL)
        {
            head = newNode;
        }
        else
        {
            temp -> next = newNode;
        }
        temp = newNode;
    }
    cout<<"Appointment schedule created!\n";
}

void displayAppointments()
{
    if(head == NULL)
    {
        cout<<"No appointments scheduled.\n";
        return;
    }

    cout<<"\n-----Appointment Schedule-----\n";
    Appointment* temp = head;
    while(temp)
    {
        if(temp -> startHour < 10)
        {
            cout<<"0";
        }
        cout<<temp -> startHour<<":";
        if(temp -> startMin < 10)
        {
            cout<<"0";
        }
        cout<<temp -> startMin<<" - ";
        if(temp -> endHour < 10)
        {
            cout<<"0";
        }
        cout<<temp -> endHour<<":";
        if(temp -> endMin < 10)
        {
            cout<<"0";
        }
        cout<<temp -> endMin<<" : ";

        if(temp -> booked)
        {
            cout<<"Booked by "<<temp -> name<<endl;
        }
        else
        {
            cout<<"Available"<<endl;
        }
        temp = temp -> next;
    }
}

void bookAppointment()
{
    int hour;
    cout<<"Enter start hour to book: ";
    cin>>hour;

    Appointment* temp = head;
    while(temp)
    {
        if(temp -> startHour == hour && !temp -> booked)
        {
            cout<<"Enter your name: ";
            cin>>temp -> name;
            temp -> booked = true;
            cout<<"Appointment booked!"<<endl;
            return;
        }
        temp = temp -> next;
    }
    cout<<"Slot not available or already booked!"<<endl;
}

void cancelAppointment()
{
    int hour;
    cout<<"Enter start hour to cancel: ";
    cin>>hour;

    Appointment* temp = head;
    while(temp)
    {
        if(temp -> startHour == hour && temp -> booked)
        {
            temp -> booked = false;
            temp -> name = "";
            cout<<"Appointment cancelled!"<<endl;
            return;
        }
        temp = temp -> next;
    }
    cout<<"No booked appointment found!"<<endl;
}

void sortByPointer()
{
    if(head == NULL || head -> next == NULL)
    {
        return;
    }

    Appointment* sorted = NULL;

    while(head)
    {
        Appointment* curr = head;
        head = head -> next;
        curr -> next = NULL;

        if(sorted == NULL || curr -> startHour < sorted -> startHour)
        {
            curr -> next = sorted;
            sorted = curr;
        }
        else
        {
            Appointment* temp = sorted;
            while(temp -> next && temp -> next -> startHour <= curr -> startHour)
            {
                temp = temp -> next;
            }
            curr -> next = temp -> next;
            temp -> next = curr;
        }
    }
    head = sorted;
    cout<<"Appointments sorted by time!"<<endl;
}

int main()
{
    int ch;
    createSchedule(9, 17);

    while(true)
    {
        cout<<"\n-----Appointment Scheduler-----\n";
        cout<<"1. Display all Appointments\n";
        cout<<"2. Book Appointment\n";
        cout<<"3. Cancel Appointment\n";
        cout<<"4. Sort Appointments by Time\n";
        cout<<"5. Exit\n";
        cout<<"Enter your choice: ";
        cin>>ch;

        switch(ch)
        {
            case 1:
                displayAppointments();
                break;

            case 2:
                bookAppointment();
                break;

            case 3:
                cancelAppointment();
                break;

            case 4:
                sortByPointer();
                break;

            case 5:
                cout<<"Exiting...\n";
                exit(0);

            default:
                cout<<"Invalid choice.\n";
        }
    }
    return 0;
}

```

## Output
-----Appointment Scheduler-----
1. Display all Appointments
2. Book Appointment
3. Cancel Appointment
4. Sort Appointments by Time
5. Exit
Enter your choice: 1

-----Appointment Schedule-----
09:00 - 10:00 : Available
10:00 - 11:00 : Available
11:00 - 12:00 : Available
12:00 - 13:00 : Available
13:00 - 14:00 : Available
14:00 - 15:00 : Available
15:00 - 16:00 : Available
16:00 - 17:00 : Available

-----Appointment Scheduler-----
1. Display all Appointments
2. Book Appointment
3. Cancel Appointment
4. Sort Appointments by Time
5. Exit
Enter your choice: 2
Enter start hour to book: 10:00
Enter your name: Appointment booked!

-----Appointment Scheduler-----
1. Display all Appointments
2. Book Appointment
3. Cancel Appointment
4. Sort Appointments by Time
5. Exit
Enter your choice: 4
Appointments sorted by time!

-----Appointment Scheduler-----
1. Display all Appointments
2. Book Appointment
3. Cancel Appointment
4. Sort Appointments by Time
5. Exit
Enter your choice: 1

-----Appointment Schedule-----
09:00 - 10:00 : Available
10:00 - 11:00 : Booked by :00
11:00 - 12:00 : Available
12:00 - 13:00 : Available
13:00 - 14:00 : Available
14:00 - 15:00 : Available
15:00 - 16:00 : Available
16:00 - 17:00 : Available


## Real-Life Applications
•	Hospital appointment and scheduling systems.
•	Salon, clinic, or consultancy booking platforms.
•	Meeting room or classroom time-slot allocations.
•	Calendar and event management applications.
•	Airline/railway crew scheduling systems.

## Conclusion
Using linked lists for appointment scheduling ensures flexibility and efficient management of dynamic time slots. This assignment demonstrates how pointer manipulation and sorting can enhance real-world scheduling systems.