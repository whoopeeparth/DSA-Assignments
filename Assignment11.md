# Assignment 11


## Problem Statement
Implementation of Singly Linked List to Manage ‘Vertex Club’ Membership Records.
The Department of Computer Engineering has a student club named ‘Vertex Club’ for second, third, and final year students. The first member is the President and the last member is the Secretary. Write a C++ program to:
●	Add/delete members (including President/Secretary)
●	Count members
●	Display members
Concatenate two division lists
 Also implement: reverse, search by PRN, and sort by PRN operations.
 

## Theory
A Singly Linked List is a dynamic data structure where each node contains data and a pointer to the next node. It is ideal for scenarios requiring frequent insertions and deletions, especially at the beginning or end—making it suitable for managing club roles like President and Secretary.
In this assignment, the list represents student members with the first node being the President and the last being the Secretary. Operations such as adding, deleting, counting, reversing, searching, sorting, and concatenating divisions help illustrate the flexibility of linked lists. The ability to efficiently modify links without shifting elements, unlike arrays, demonstrates why linked lists are widely used in record management systems.

## Code
```cpp
#include <iostream>
#include <string>
using namespace std;

class Node
{
    public:
        int prn;
        string name;
        Node* next;

    Node(int p, string n)
    {
        prn = p;
        name = n;
        next = nullptr;
    }
};

class VortexClub
{
    Node* head;
    Node* tail;

    public:
        VortexClub()
        {
            head = tail = nullptr;
        }

        void addPresident(int prn, string name)
        {
            Node* newNode = new Node(prn, name);
            if(head == nullptr)
            {
                head = tail = newNode;
                return;
            }
            else
            {
                newNode -> next = head;
                head = newNode;
            }
        }

        void addSecretary(int prn, string name)
        {
            Node* newNode = new Node(prn, name);
            if(head == nullptr)
            {
                head = tail = newNode;
            }
            else
            {
                tail -> next = newNode;
                tail = newNode;
            }
        }

        void addMember(int prn, string name, int pos)
        {
            if(pos < 0)
            {
                addPresident(prn, name);
                return;
            }

            Node* temp = head;
            for(int i = 0; i < pos - 1; i++)
            {
                if(temp == nullptr)
                {
                    cout<<"Invalid position\n";
                    return;
                }
                temp = temp -> next;
            }

            Node* newNode = new Node(prn, name);
            newNode -> next = temp -> next;
            temp -> next = newNode;
        }

        void deletePresident()
        {
            if(head == nullptr)
            {
                cout<<"LL is empty\n";
                return;
            }

            Node* temp = head;
            head = head -> next;

            temp -> next = nullptr;

            delete temp;
        }

        void deleteSecretary()
        {
            if(head == nullptr)
            {
                cout<<"LL is empty\n";
                return;
            }

            Node* temp = head;
            while(temp -> next != tail)
            {
                temp = temp -> next;
            }

            temp -> next = nullptr;

            delete tail;
        }

        int countMembers()
        {
            int count = 0;
            Node* temp = head;
            while(temp)
            {
                count++;
                temp = temp -> next;
            }
            return count;
        }

        void searchByPRN(int prn)
        {
            Node* temp = head;
            int pos = 0;

            while(temp != nullptr)
            {
                if(temp -> prn == prn)
                {
                    cout<<"Member found at position: "<<pos<<temp -> name<<endl;
                    return;
                }

                temp = temp -> next;
                pos++;
            }

            cout<<"Member with PRN "<<prn<<" not found\n";
        }

        void reverseList()
        {
            Node* prev = nullptr;
            Node* current = head;
            Node* next = nullptr;
            tail = head;

            while(current)
            {
                next = current -> next;
                current -> next = prev;
                prev = current;
                current = next;
            }

            head = prev;
        }

        void sortByPRN()
        {
            if(!head)
            {
                return;
            }
            Node* i;
            Node* j;
            for(i = head; i != nullptr; i = i -> next)
            {
                for(j = i -> next; j != nullptr; j = j -> next)
                {
                    if(i -> prn > j -> prn)
                    {
                        swap(i -> prn, j -> prn);
                        swap(i -> name, j -> name);
                    }
                }
            }
        }

        void concatenate(VortexClub &other)
        {
            if(!other.head)
            {
                return;
            }
            if(!head)
            {
                head = other.head;
                tail = other.tail;
            }
            else
            {
                tail -> next = other.head;
                tail = other.tail;
            }
        }

        void displayMembers()
        {

            if(!head)
            {
                cout<<"Club has no members!\n";
                return;
            }
            Node* temp = head;
            while(temp != nullptr)
            {
                cout<<temp -> prn<<" - "<<temp -> name<<"->";
                temp = temp -> next;
            }

            cout<<"NULL"<<endl;
        }
};

int main()
{
    VortexClub c1, c2;
    int choice, prn, pos;
    string name;

    while(true)
    {
        cout<<"-----Vortex Club-----\n";
        cout<<"\n1. Add President\n2. Add Secretary\n3. Add Member\n4. Delete President\n5. Delete Secretary\n6. Count Members\n";
        cout<<"7. Display Members\n8. Search by PRN\n9. Reverse List\n10. Sort by PRN\n11. Concatenate other list\n12. Exit\n";
        cout<<"Enter your choice: ";
        cin>>choice;

        switch(choice)
        {
            case 1:
                cout<<"Enter PRN and Name of President: ";
                cin>>prn;
                cin.ignore();
                cin>>name;
                c1.addPresident(prn, name);
                break;

            case 2:
                cout<<"Enter PRN and Name of Secretary: ";
                cin>>prn;
                cin.ignore();
                cin>>name;
                c1.addSecretary(prn, name);
                break;

            case 3:
                cout<<"Enter PRN, Name and Position to add Member: ";
                cin>>prn;
                cin.ignore();
                cin>>name;
                cin>>pos;
                c1.addMember(prn, name, pos);
                break;

            case 4:
                c1.deletePresident();
                break;

            case 5:
                c1.deleteSecretary();
                break;

            case 6:
                cout<<"Total Members: "<<c1.countMembers()<<endl;
                break;

            case 7:
                c1.displayMembers();
                break;

            case 8:
                cout<<"Enter PRN to search: ";
                cin>>prn;
                c1.searchByPRN(prn);
                break;

            case 9:
                c1.reverseList();
                cout<<"List Reversed.\n";
                c1.displayMembers();
                break;

            case 10:
                c1.sortByPRN();
                cout<<"List sorted.\n";
                c1.sortByPRN();
                break;

            case 11:
                int n;
                cout<<"How many members to add in Second List? ";
                cin>>n;
                for(int i = 0; i < n; i++)
                {
                    cout<<"Enter PRN and Name: ";
                    cin>>prn;
                    cin.ignore();
                    cin>>name;
                    c2.addSecretary(prn, name);
                }

                c1.concatenate(c2);
                cout<<"List Concatenated.\n";
                break;

            case 12:
                exit(0);

            default:
                cout<<"Invalid Choice!\n";
        }
    }

    return 0;
}


```

## Output
-----Vortex Club-----

1. Add President
2. Add Secretary
3. Add Member
4. Delete President
5. Delete Secretary
6. Count Members
7. Display Members
8. Search by PRN
9. Reverse List
10. Sort by PRN
11. Concatenate other list
12. Exit
Enter your choice: 1
Enter PRN and Name of President: 123
Parth
-----Vortex Club-----

1. Add President
2. Add Secretary
3. Add Member
4. Delete President
5. Delete Secretary
6. Count Members
7. Display Members
8. Search by PRN
9. Reverse List
10. Sort by PRN
11. Concatenate other list
12. Exit
Enter your choice: 2
Enter PRN and Name of Secretary: 234
Yash
-----Vortex Club-----

1. Add President
2. Add Secretary
3. Add Member
4. Delete President
5. Delete Secretary
6. Count Members
7. Display Members
8. Search by PRN
9. Reverse List
10. Sort by PRN
11. Concatenate other list
12. Exit
Enter your choice: 3
Enter PRN, Name and Position to add Member: 345
Prasad
2
-----Vortex Club-----

1. Add President
2. Add Secretary
3. Add Member
4. Delete President
5. Delete Secretary
6. Count Members
7. Display Members
8. Search by PRN
9. Reverse List
10. Sort by PRN
11. Concatenate other list
12. Exit
Enter your choice: 7
123 - Parth->234 - Yash->345 - Prasad->NULL
-----Vortex Club-----

1. Add President
2. Add Secretary
3. Add Member
4. Delete President
5. Delete Secretary
6. Count Members
7. Display Members
8. Search by PRN
9. Reverse List
10. Sort by PRN
11. Concatenate other list
12. Exit
Enter your choice: 4
-----Vortex Club-----

1. Add President
2. Add Secretary
3. Add Member
4. Delete President
5. Delete Secretary
6. Count Members
7. Display Members
8. Search by PRN
9. Reverse List
10. Sort by PRN
11. Concatenate other list
12. Exit
Enter your choice: 7
234 - Yash->345 - Prasad->NULL
-----Vortex Club-----

1. Add President
2. Add Secretary
3. Add Member
4. Delete President
5. Delete Secretary
6. Count Members
7. Display Members
8. Search by PRN
9. Reverse List
10. Sort by PRN
11. Concatenate other list
12. Exit
Enter your choice: 6
Total Members: 2

## Real-Life Applications
•	Managing organizational hierarchies or club memberships.
•	Implementing undo/redo operations in software.
•	Maintaining a dynamic playlist or task list.
•	Handling queues in operating systems (schedulers, buffers).
•	Managing employee records in small-scale systems.


## Conclusion
Singly linked lists provide efficient mechanisms to manage dynamic membership records. This assignment illustrates the practicality of linked lists in handling frequent structural changes while maintaining order and accessibility.