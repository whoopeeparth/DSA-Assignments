# Assignment 25


## Problem Statement
You are given a postfix expression (also known as Reverse Polish Notation) consisting of single-digit operands and binary operators (+, -, *, /). Your task is to evaluate the expression using stack and return its result.

## Theory
Postfix (Reverse Polish) expressions place operators after operands, making the evaluation process straightforward and unambiguous. The stack structure fits naturally into postfix evaluation because operands are pushed onto the stack, and when an operator appears, two operands are popped, the operation is applied, and the result is pushed back.
This avoids complications like operator precedence and parentheses, making postfix evaluation extremely efficient for computers. Postfix evaluation is commonly used in calculators, interpreters, compilers, and even digital circuits implementing arithmetic logic.

## Code
```cpp
#include <iostream>
using namespace std;

int stackArr[20];
int top = -1;

void push(int x)
{
    stackArr[++top] = x;
}

int pop()
{
    return stackArr[top--];
}

int main()
{
    char exp[20];
    cout<<"Enter postfix expression: ";
    cin.getline(exp, 20);

    char *e = exp;

    while(*e != '\0')
    {
        if(*e >= '0' && *e <= '9')
        {
            push(*e - '0');
        }
        else
        {
            int v2 = pop();
            int v1 = pop();
            int ans;

            switch(*e)
            {
                case '+':
                    ans = v1 + v2;
                    break;

                case '-':
                    ans = v1 - v2;
                    break;

                case '*':
                    ans = v1 * v2;
                    break;

                case '/':
                    ans = v1 / v2;
                    break;

            }
            push(ans);
        }
        e++;
    }
    cout<<"Result: "<<pop();
}

```

## Output
Enter postfix expression: 34+2*
Result: 14

## Real-Life Applications
•	Evaluators in compilers and interpreters
•	Digital circuit arithmetic units
•	RPN-based scientific calculators
•	Spreadsheet formula evaluation engines
•	Expression evaluation APIs

## Conclusion
Postfix evaluation using stacks is fast, clean, and machine-friendly. It eliminates parsing complexity and is widely used in systems that require efficient mathematical computation.