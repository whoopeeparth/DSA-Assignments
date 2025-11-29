# Assignment 17


## Problem Statement
WAP to perform addition o f two polynomials using singly linked list.

## Theory
Polynomials can have varying degrees and sparse terms, which makes linked lists ideal for storing them because each node stores a coefficient and exponent without wasting memory on missing terms. Addition of polynomials using linked lists involves traversing both lists simultaneously, comparing exponents, and creating a new list representing the resulting polynomial.
This method supports polynomials of arbitrary length and ensures that terms remain sorted, making operations like addition, subtraction, or differentiation easier and more efficient than using arrays.

## Code
```cpp
#include <iostream>
#include <cstdlib>
using namespace std;

typedef struct PolyNode
{
    int coef;
    int exp;
    PolyNode* next;
}PolyNode;

PolyNode* createNode(int coef, int exp)
{
    PolyNode* node = new PolyNode;
    node -> coef = coef;
    node -> exp = exp;
    node -> next = NULL;
    return node;
}

void insertTerm(PolyNode* &head, int coef, int exp)
{
    PolyNode* node = createNode(coef, exp);
    if(!head)
    {
        head = node;
        return;
    }

    PolyNode* temp = head;
    while(temp -> next)
    {
        temp = temp -> next;
    }

    temp -> next = node;
}

void displayPoly(PolyNode* head)
{
    PolyNode* temp = head;
    while(temp)
    {
        cout<<temp -> coef<<"x^"<<temp -> exp;
        if(temp -> next)
        {
            cout<<" + ";
        }
        temp = temp -> next;
    }
    cout<<endl;
}

PolyNode* addPoly(PolyNode* p1, PolyNode* p2)
{
    PolyNode* result = NULL;
    PolyNode* t1 = p1;
    PolyNode* t2 = p2;

    while(t1 && t2)
    {
        if(t1 -> exp > t2 -> exp)
        {
            insertTerm(result, t1 -> coef, t1 -> exp);
            t1 = t1 -> next;
        }
        else if(t2 -> exp > t1 -> exp)
        {
            insertTerm(result, t2 -> coef, t2 -> exp);
            t2 = t2 -> next;
        }
        else
        {
            int sum = t1 -> coef + t2 -> coef;
            insertTerm(result, sum, t1 -> exp);

            t1 = t1 -> next;
            t2 = t2 -> next;
        }
    }

    while(t1)
    {
        insertTerm(result, t1 -> coef, t1 -> exp);
        t1 = t1 -> next;
    }
    while(t2)
    {
        insertTerm(result, t2 -> coef, t2 -> exp);
        t2 = t2 -> next;
    }

    return result;
}

int main()
{
    PolyNode* poly1 = NULL;
    PolyNode* poly2 = NULL;
    PolyNode* sum = NULL;

    insertTerm(poly1, 5, 3);
    insertTerm(poly1, 4, 2);
    insertTerm(poly1, 2, 0);

    insertTerm(poly2, 3, 3);
    insertTerm(poly2, 2, 1);
    insertTerm(poly2, 1, 0);

    cout<<"Polynomial 1: ";
    displayPoly(poly1);

    cout<<"Polynomial 2: ";
    displayPoly(poly2);

    sum = addPoly(poly1, poly2);

    cout<<"Sum: ";
    displayPoly(sum);

    return 0;
}

```

## Output
Polynomial 1: 5x^3 + 4x^2 + 2x^0
Polynomial 2: 3x^3 + 2x^1 + 1x^0
Sum: 8x^3 + 4x^2 + 2x^1 + 3x^0Sum: 8x^3 + 4x^2 + 2x^1 + 3x^0

## Real-Life Applications
•	Computer algebra systems (Mathematica, MATLAB, Maple)
•	Engineering calculations involving polynomial equations
•	Signal processing filters represented in polynomial form
•	Simulation models in physics (motion equations, trajectories)
•	Polynomial interpolation and curve fitting

## Conclusion
Using linked lists to store polynomials results in compact memory usage, easier manipulation of polynomial expressions, and efficient arithmetic operations, especially when terms are sparse or dynamically changing.