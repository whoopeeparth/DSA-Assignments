# Assignment 22


## Problem Statement
Convert given infix expression Eg. a-b*c-d/e+f into postfix form using stack and show the operations step by step.

## Theory
Infix expressions (e.g., a-b*c) are how humans write arithmetic, but they are difficult for machines to evaluate directly because operator precedence and parentheses must be handled carefully. Postfix notation (Reverse Polish Notation) eliminates the need for parentheses and directly expresses the order of operations, making it ideal for computation.
Stacks are the standard method for converting infix to postfix because they allow temporary storage of operators and symbols while maintaining correct precedence and associativity. When scanning the infix expression, operands are added to the output immediately, while operators are pushed to the stack and popped according to precedence rules. This makes the process well-structured and deterministic.

## Code
```cpp
#include <iostream>
using namespace std;

char stack[20];
int top = -1;

void push(char x)
{
    stack[++top] = x;
}

char pop()
{
    if(top == -1)
    {
        return -1;
    }
    else
    {
        return stack[top--];
    }
}

int priority(char x)
{
    if(x == '(')
    {
        return 0;
    }
    if(x == '+' || x == '-')
    {
        return 1;
    }
    if(x == '*' || x == '/')
    {
        return 2;
    }
    return -1;
}

int main()
{
    char exp[20];
    char *e, x;
    cout<<"Enter the expression: ";
    cin.getline(exp, 20);
    e = exp;
    while(*e != '\0')
    {
        if(isalnum(*e))
        {
            cout<<*e;
        }
        else if(*e == '(')
        {
            push(*e);
        }
        else if(*e == ')')
        {
            while((x = pop()) != '(')
            {
                cout<<x;
            }
        }
        else
        {
            while(top != -1 && priority(stack[top]) >= priority(*e))
            {
                cout<<pop();
            }
            push(*e);
        }
        e++;
    }
    while(top != -1)
    {
        cout<<pop();
    }
}

```

## Output
Enter the expression: a*b+a*c/d+c
ab*ac*d/+c+

## Real-Life Applications
•	Compiler design for parsing mathematical expressions
•	Scientific calculators that internally use postfix evaluation
•	Expression evaluation engines in programming languages
•	Symbolic mathematics software
•	Embedded systems that require minimal memory expression parsing

## Conclusion
Converting infix to postfix using a stack creates an unambiguous and machine-friendly expression format. It simplifies the evaluation process and forms the foundation for expression parsing in numerous computational systems.