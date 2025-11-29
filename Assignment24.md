# Assignment 24


## Problem Statement
You are given a string containing only parentheses characters: '(', ')', '{', '}', '[', and ']'. Your task is to check whether the parentheses are balanced or not.
A string is considered balanced if:
1.	Every opening bracket has a corresponding closing bracket of the same type
Brackets are closed in the correct order.

## Theory
A stack-based approach is the most natural and efficient way to validate balanced parentheses in a string. Bracket-checking problems rely heavily on matching pairs—an opening bracket must be matched with its corresponding closing bracket in the correct order.
By pushing every opening bracket onto the stack and popping when a matching closing bracket appears, the program ensures both correctness and order. If mismatches or early closing brackets appear, the string is invalid. This simple algorithm runs in O(n) time and ensures structural correctness for nested structures—a key requirement in coding languages, markup systems, compilers, and parsers.

## Code
```cpp
#include <iostream>
#include <cstdlib>
#include <string>
using namespace std;

#define MAX 100

char stack[MAX];
int top = -1;

void push(char c)
{
    if(top >= MAX - 1)
    {
        cout<<"Stack Overflow!\n";
        return;
    }

    stack[++top] = c;
}

char pop()
{
    if(top == -1)
    {
        cout<<"Stack Underflow!\n";
        return '\0';
    }

    return stack[top--];
}

bool isEmpty()
{
    return top == -1;
}

bool isBalanced(string str)
{
    for(int i = 0; i < str.length(); i++)
    {
        char ch = str[i];

        if(ch == '(' || ch == '{' || ch == '[')
        {
            push(ch);
        }

        else if(ch == ')' || ch == '}' || ch == ']')
        {
            if(isEmpty())
            {
                return false;
            }

            char open = pop();

            if((ch == ')' && open != '(') ||
               (ch == '}' && open != '{') ||
               (ch == ']' && open != '['))
               {
                return false;
               }
        }
    }

    return isEmpty();
}

int main()
{
    int choice;
    string input;

    while(true) {
        cout << "\n-----Balanced Parentheses Checker-----\n";
        cout << "1. Check an expression\n";
        cout << "2. Exit\n";
        cout << "Enter your choice: ";
        cin >> choice;

        cin.ignore(); 

        switch(choice) {
            case 1:
                cout << "Enter a string with parentheses: ";
                getline(cin, input); 
                if(isBalanced(input))
                    cout << "Balanced \n";
                else
                    cout << "Not Balanced \n";
                break;

            case 2:
                cout << "Exiting...\n";
                return 0;

            default:
                cout << "Invalid choice!\n";
        }
    }

    return 0;
}

```

## Output
-----Balanced Parentheses Checker-----
1. Check an expression
2. Exit
Enter your choice: 1
Enter a string with parentheses: {[]}
Balanced

## Real-Life Applications
•	Compilers checking syntax validity
•	HTML/XML parser validation
•	Code editor bracket highlighting
•	Expression evaluators ensuring proper nesting
•	Mathematical and logical formula validators

## Conclusion
The stack-based parentheses checker provides a robust, linear-time method to validate nested structures. Its predictable behavior makes it foundational for syntax validation in programming and markup languages.