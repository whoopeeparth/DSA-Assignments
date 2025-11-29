# Assignment 12


## Problem Statement
The ticket reservation system for Galaxy Multiplex is to be implemented using a C++ program. The multiplex has 8 rows, with 8 seats in each row. A doubly circular linked list will be used to track the availability of seats in each row.Initially, assume that some seats are randomly booked. An array will store head pointers for each row’s linked list.The system should support the following operations:
a) Display the current list of available seats.
b) Book one or more seats as per customer request.
c) Cancel an existing booking when requested.

## Theory
A Doubly Circular Linked List supports traversal in both directions, and its circular nature eliminates NULL pointers, allowing continuous movement through nodes. This makes it ideal for applications like seat management where navigation between adjacent seats is required.
In this assignment, each row in the multiplex is represented by a doubly circular linked list, and an array stores pointers to the head nodes for all 8 rows. Booked seats are marked accordingly, and operations such as displaying available seats, booking, and canceling are performed by manipulating links. This model effectively simulates real-world ticketing systems where seats can change states dynamically.

## Code
```cpp
#include <iostream>
#include <cstdlib>
using namespace std;

#define ROWS 8
#define SEATS 8

struct Seat
{
    int seatNo;
    int status;
    Seat* next;
    Seat* prev;
};

Seat* head[ROWS] = {NULL};

void createRow(int row)
{
    Seat* temp = NULL;
    Seat* newSeat;

    for(int i = 1; i <= SEATS; i++)
    {
        newSeat = new Seat();
        newSeat -> seatNo = i;
        newSeat -> status = 1;
        newSeat -> next = newSeat -> prev = NULL;

        if(head[row] == NULL)
        {
            head[row] = newSeat;
            head[row] -> next = head[row];
            head[row] -> prev = head[row];
            temp = head[row];
        }
        else
        {
            newSeat -> prev = temp;
            newSeat -> next = head[row];
            temp -> next = newSeat;
            head[row] -> prev = newSeat;
            temp = newSeat;
        }
    }
}

void createMultiplex()
{
    for(int i = 0; i < ROWS; i++)
    {
        createRow(i);
    }

    head[0] -> status = 0;
    head[3] -> next -> next -> status = 0;
    head[5] -> next -> next -> next -> next -> status = 0;
    head[7] -> prev -> status = 0;
}

void displaySeats()
{
    cout << "\n------ Seat Availability (1 = Available, 0 = Booked) ------\n";
    for(int i = 0; i < ROWS; i++)
    {
        cout<<"Row "<<(i + 1)<<": ";
        Seat* temp = head[i];
        do
        {
            cout<<temp -> status<<" ";
            temp = temp -> next;
        } while (temp != head[i]);
        cout<<endl;
    }
}

void bookSeats()
{
    int row, seatNum, n;
    cout<<"Enter row number: ";
    cin>>row;
    row--;

    if(row < 0 || row >= ROWS)
    {
        cout<<"Invalid row number.\n";
        return;
    }

    cout<<"How many seats you want to book? ";
    cin>>n;

    for(int i = 0; i < n; i++)
    {
        cout<<"Enter seat number to book: ";
        cin>>seatNum;

        if(seatNum < 1 || seatNum > SEATS)
        {
            cout<<"Invalid seat number!\n";
            return;
        }

        Seat* temp = head[row];
        for(int j = 1; j < seatNum; j++)
        {
            temp = temp -> next;
        }

        if(temp -> status == 0)
        {
            cout<<"Seat "<<seatNum<<" already booked!\n";
            return;
        }
        else
        {
            temp -> status = 0;
            cout<<"Seat "<<seatNum<<" booked successfully.\n";
        }
    }
}

void cancelSeats()
{
    int row, seatNum, n;
    cout<<"Enter row number: ";
    cin>>row;
    row--;

    if(row < 0 || row >= ROWS)
    {
        cout<<"Invalid row number.\n";
        return;
    }

    cout<<"How many seats you want to cancel? ";
    cin>>n;

    for(int i = 0; i < n; i++)
    {
        cout<<"Enter seat number to cancel: ";
        cin>>seatNum;

        if(seatNum < 1 || seatNum > SEATS)
        {
            cout<<"Invalid seat number!\n";
            return;
        }

        Seat* temp = head[row];
        for(int j = 1; j < seatNum; j++)
        {
            temp = temp -> next;
        }

        if(temp -> status == 1)
        {
            cout<<"Seat "<<seatNum<<" is not booked!\n";
            return;
        }
        else
        {
            temp -> status = 1;
            cout<<"Seat "<<seatNum<<" booking cancelled.\n";
        }
    }
}

int main() {
    createMultiplex();

    int choice;
    while (true) {
        cout << "\n===== Galaxy Multiplex Reservation System =====\n";
        cout << "1. Display Seat Availability\n";
        cout << "2. Book Seats\n";
        cout << "3. Cancel Booking\n";
        cout << "4. Exit\n";
        cout << "Enter your choice: ";
        cin >> choice;

        switch (choice) {
            case 1:
                displaySeats();
                break;
            case 2:
                bookSeats();
                break;
            case 3:
                cancelSeats();
                break;
            case 4:
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
===== Galaxy Multiplex Reservation System =====
1. Display Seat Availability
2. Book Seats
3. Cancel Booking
4. Exit
Enter your choice: 1

------ Seat Availability (1 = Available, 0 = Booked) ------
Row 1: 0 1 1 1 1 1 1 1
Row 2: 1 1 1 1 1 1 1 1
Row 3: 1 1 1 1 1 1 1 1
Row 4: 1 1 0 1 1 1 1 1
Row 5: 1 1 1 1 1 1 1 1
Row 6: 1 1 1 1 0 1 1 1
Row 7: 1 1 1 1 1 1 1 1
Row 8: 1 1 1 1 1 1 1 0

===== Galaxy Multiplex Reservation System =====
1. Display Seat Availability
2. Book Seats
3. Cancel Booking
4. Exit
Enter your choice: 2
Enter row number: 3
How many seats you want to book? 2
Enter seat number to book: 2
Seat 2 booked successfully.
Enter seat number to book: 3
Seat 3 booked successfully.

===== Galaxy Multiplex Reservation System =====
1. Display Seat Availability
2. Book Seats
3. Cancel Booking
4. Exit
Enter your choice: 1

------ Seat Availability (1 = Available, 0 = Booked) ------
Row 1: 0 1 1 1 1 1 1 1
Row 2: 1 1 1 1 1 1 1 1
Row 3: 1 0 0 1 1 1 1 1
Row 4: 1 1 0 1 1 1 1 1
Row 5: 1 1 1 1 1 1 1 1
Row 6: 1 1 1 1 0 1 1 1
Row 7: 1 1 1 1 1 1 1 1
Row 8: 1 1 1 1 1 1 1 0
1. Display Seat Availability
2. Book Seats
3. Cancel Booking
4. Exit
Enter your choice: 1

------ Seat Availability (1 = Available, 0 = Booked) ------
Row 1: 0 1 1 1 1 1 1 1
Row 2: 1 1 1 1 1 1 1 1
Row 3: 1 1 1 1 1 1 1 1
Row 4: 1 1 0 1 1 1 1 1
Row 5: 1 1 1 1 1 1 1 1
Row 6: 1 1 1 1 0 1 1 1
Row 7: 1 1 1 1 1 1 1 1
Row 8: 1 1 1 1 1 1 1 0

===== Galaxy Multiplex Reservation System =====
1. Display Seat Availability
2. Book Seats
3. Cancel Booking
4. Exit
Enter your choice: 2
Enter row number: 3
How many seats you want to book? 2
Enter seat number to book: 2
Seat 2 booked successfully.
Enter seat number to book: 3
Seat 3 booked successfully.

===== Galaxy Multiplex Reservation System =====
1. Display Seat Availability
2. Book Seats
3. Cancel Booking
4. Exit
Enter your choice: 1

------ Seat Availability (1 = Available, 0 = Booked) ------
Row 1: 0 1 1 1 1 1 1 1
Row 2: 1 1 1 1 1 1 1 1
Row 3: 1 0 0 1 1 1 1 1
Row 4: 1 1 0 1 1 1 1 1
Row 5: 1 1 1 1 1 1 1 1
Row 6: 1 1 1 1 0 1 1 1
Row 7: 1 1 1 1 1 1 1 1
Row 8: 1 1 1 1 1 1 1 0


## Real-Life Applications
•	Cinema/theatre ticket reservation systems.
•	Circular navigation in music players or image galleries.
•	Memory allocation systems requiring circular referencing.
•	Round-robin scheduling in operating systems.
•	Reservation systems for buses, trains, and auditoriums.



## Conclusion
A doubly circular linked list offers efficient mechanisms for managing seating arrangements. This assignment shows how circular structures simplify navigation and updating seat availability in reservation systems.