# Assignment 16


## Problem Statement
Write a C++ program to implement a Set using a Generalized Linked List (GLL).     For example:
 Let S = { p, q, {r, s, t, {}, {u, v}, w, x, {y, z}, a1, b1} }
Store this structure using a Generalized Linked List and display the elements in correct set notation format.

## Theory
A Generalized Linked List (GLL) is a flexible hierarchical data structure used to represent nested or multi-level lists. Unlike regular linked lists, which store only linear data, a GLL node can store either an atomic element or a pointer to another sublist. This allows representation of complex structures such as sets within sets, algebraic expressions, hierarchical menus, or directories.
When implementing a set using GLL, each node contains a tag: 0 for data, 1 for sublist, and the appropriate pointer. During traversal, recursive methods are typically used because nested sets can have multiple levels. Displaying the set in correct mathematical form requires careful placement of commas, braces, and recursion.

## Code
```cpp
#include <iostream>
#include <cstdlib>
using namespace std;

typedef struct GLL
{
    int flag;
    char data;
    GLL* next;
    GLL* down;
}GLL;

GLL* createNode(char data)
{
    GLL* node = new GLL;
    node -> flag = 0;
    node -> data = data;
    node -> next = NULL;
    node -> down = NULL;
    return node;
}

GLL* createSublist()
{
    GLL* node = new GLL;
    node -> flag = 1;
    node -> data = '\0';
    node -> next = NULL;
    node -> down = NULL;
    return node;
}

void displayGLL(GLL* head)
{
    cout << "{";
    while(head)
    {
        if(head -> flag == 0)
        {
            cout<< head -> data;
        }
        else
        {
            displayGLL(head -> down);
        }
        if(head -> next)
        {
            cout<< ", ";
        }
        head = head -> next;
    }
    cout<< "}";
}

void destroyGLL(GLL* head)
{
    while(head)
    {
        if(head -> flag == 1 && head -> down)
        {
            destroyGLL(head -> down);
        }
        GLL* temp = head;
        head = head -> next;
        delete temp;
    }
}

int main()
{
    GLL* s = createSublist();

    s -> down = createNode('p');

    GLL* temp = s -> down;

    temp -> next = createNode('q');

    temp = temp -> next;

    temp -> next = createSublist();

    GLL* sub = temp -> next;

    sub -> down = createNode('r');

    GLL* temp2 = sub -> down;

    temp2->next = createNode('s'); 
    temp2 = temp2->next;

    temp2->next = createNode('t'); 
    temp2 = temp2->next;

    temp2->next = createSublist(); 
    temp2 = temp2->next;

    temp2->next = createSublist(); 
    temp2 = temp2->next;

    temp2->down = createNode('u');
    temp2->down->next = createNode('v');

    temp2->next = createNode('w');
    temp2 = temp2->next;

    temp2->next = createNode('x');
    temp2 = temp2->next;

    temp2->next = createSublist();
    temp2 = temp2->next;
    temp2->down = createNode('y');
    temp2->down->next = createNode('z');

    temp2->next = createNode('a');
    temp2 = temp2->next;

    temp2->next = createNode('b');
    temp2 = temp2->next;

    cout<<"Representation of final set: ";
    displayGLL(s);
    cout<<endl;

    destroyGLL(s);

    return 0;

}

```

## Output
Representation: {{p, q, {r, s, t, {}, {u, v}, w, x, {y, z}, a, b}}}

## Real-Life Applications
•	Representation of XML/JSON hierarchical data
•	File directory systems with nested folders
•	Expression trees for compilers and interpreters
•	AI knowledge representation (nested facts or rule sets)
•	Implementation of symbolic mathematics systems

## Conclusion
GLLs provide a powerful way to model nested set structures that cannot be represented using ordinary lists. They offer flexibility, recursive traversal, and are ideal for representing complex hierarchical data efficiently.